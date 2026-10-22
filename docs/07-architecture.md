# Architecture Description

**Purpose:** Describe how AITU Booking is structured, how its parts communicate, and the decisions that ensure the main requirements are met — especially no double bookings ([NFR-03](06-requirements.md)) and real-time availability ([NFR-02](06-requirements.md)).

Diagrams: [System Context](diagrams/export/system-context.png) · [Use Case](diagrams/export/use-case.png) · [Component](diagrams/export/component.png) · [Booking sequence](diagrams/export/booking-sequence.png). Sources are in [`diagrams/`](diagrams/).

## 1. Architectural style

AITU Booking is a **client–server system with a modular monolith backend**.

- **Clients:** iOS app (Swift, SwiftUI), the admin web panel (React), and later an Android app (Kotlin, Jetpack Compose).
- **Backend:** one FastAPI application divided into modules with clear boundaries (auth, rooms, reservations, schedule, consultations, keys, realtime, notifications).
- **Database:** one PostgreSQL instance.

**Why a modular monolith and not microservices.** The team has three people, one backend developer, and a single deployment target. Microservices would add service-to-service communication, distributed transactions, and more infrastructure without a real benefit at university scale (a few thousand users). Booking correctness depends on one database transaction, which is simplest inside one application. Module boundaries keep the code organised so a module could be extracted later if needed.

## 2. System context

![System Context](diagrams/export/system-context.png)

| External system | Role | Interface |
|---|---|---|
| University email (SMTP) | One-time verification codes and email reminders to `@astanait.edu.kz` addresses | SMTP |
| APNs (FCM for Android later) | Push notifications | HTTPS |
| Official schedule (PDF) | Source of class and exam schedule; uploaded by the administrator | File upload |

> Only university email addresses can register. Ownership of the address is confirmed with a one-time code (see the `login` and `verify` screens in the prototype). Single sign-on with university Microsoft accounts can be considered later if university IT provides access.

## 3. Components

![Component](diagrams/export/component.png)

| Component | Responsibility | Main requirements |
|---|---|---|
| API Router | REST endpoints under `/api/v1`, input validation (Pydantic), uniform error format | all |
| Auth module | Registration with university email, one-time verification codes, password hashing, short-lived JWT access tokens and refresh tokens, role checks on every endpoint | FR-01 – FR-03, NFR-04, NFR-05 |
| Rooms module | Buildings, floors, rooms, map areas (room ↔ polygon on the floor plan), temporary blocks | FR-04 – FR-08, FR-28 – FR-30 |
| Reservations module | Booking window 1–72 h by server time, overlap checks (room and user), closed periods without a confirmed schedule, create / cancel | FR-09 – FR-16 |
| Schedule module | PDF parsing (pypdf), preview, conflict detection that blocks publication, validity period, weeks 1–10 vs 11–12, manual edits | FR-21 – FR-27 |
| Consultations module | Lecturer slots, student bookings, 1 h cancellation rule (Stage 2) | FR-36 – FR-41 |
| Keys module | Key issue / return, ID-card deposit, signature in the log, unreturned keys at the end of the day (reservation end ≠ key return) | FR-31 – FR-35 |
| Realtime hub | WebSocket connections grouped by building; broadcasts availability events | FR-17, FR-18, NFR-02 |
| Notifications | Background worker for reminders and cancellation notices | FR-19, FR-20 |
| Audit log | Records user, action, timestamp for booking, schedule, and key operations | NFR-13 |

### Planned backend structure

```text
backend/
  app/
    main.py
    core/            config, security, db session
    auth/            router.py, service.py, schemas.py
    rooms/
    reservations/
    schedule/        parser.py (PDF), router.py, service.py
    consultations/
    keys/
    realtime/        ws.py, events.py
    notifications/
    audit/
  migrations/        Alembic
  tests/
  docker-compose.yml
```

## 4. Data model (main entities)

| Entity | Key fields |
|---|---|
| `users` | id, email (unique, university domain), password_hash, email_verified_at, full_name, role (student / lecturer / admin) |
| `email_codes` | id, user_id, code_hash, expires_at, used_at |
| `buildings`, `floors` | id, name; floor plan image and SVG layer |
| `rooms` | id, floor_id, name, capacity, equipment, is_bookable, map_polygon |
| `schedule_entries` | id, room_id, weekday, start_time, end_time, course, group, week_from, week_to, type (class / exam), import_id |
| `schedule_imports` | id, file_name, type (regular / exam), valid_from, valid_to, uploaded_by, status (preview / blocked / confirmed / discarded), created_at |
| `room_blocks` | id, room_id, period (tstzrange), reason |
| `reservations` | id, room_id, user_id, period (tstzrange), status (confirmed / cancelled), cancel_reason |
| `consultation_slots` | id, lecturer_id, period, location, status |
| `consultation_bookings` | id, slot_id (unique for active bookings), student_id, topic, status |
| `key_records` | id, room_id, student_id, issued_at, returned_at, id_card_number, signature_ref, issued_by |
| `audit_log` | id, user_id, action, entity, entity_id, created_at |

## 5. Key architectural decisions

### AD-1. Double bookings are prevented by the database

The application checks availability first, but the final guarantee is a PostgreSQL **exclusion constraint**:

```sql
CREATE EXTENSION IF NOT EXISTS btree_gist;

ALTER TABLE reservations
  ADD CONSTRAINT no_overlapping_reservations
  EXCLUDE USING gist (room_id WITH =, period WITH &&)
  WHERE (status = 'confirmed');
```

If two requests for the same room and overlapping time are processed at the same moment, the second `INSERT` fails with `exclusion_violation`, and the API returns **409 Conflict**. An application-only check (`SELECT` then `INSERT`) is not enough because both requests could pass the `SELECT` before either inserts. The same idea is used for consultations: a partial unique index on `slot_id` for active bookings.

![Booking sequence](diagrams/export/booking-sequence.png)

### AD-2. Real-time updates through WebSocket

Clients open one WebSocket connection (`/ws?building=<id>`) after sign-in. When a reservation is created or cancelled, the reservations module publishes an event **after the transaction commits**, so clients never see a booking that was rolled back:

```json
{ "type": "room.updated", "room_id": 412, "date": "2026-11-05",
  "interval": ["14:00", "15:30"], "status": "busy" }
```

If the connection drops, the app reconnects and re-loads availability through REST, so no event loss leads to wrong data. For the first release one backend instance is enough and Redis is not required; if more instances are needed, events will go through PostgreSQL `LISTEN/NOTIFY` or Redis pub/sub.

### AD-3. Schedule import with preview

PDF parsing is error-prone, and the real AITU PDF format still has to be verified, so import has two steps: (1) upload with type and validity period → the backend extracts entries into a `schedule_imports` record with status `preview`; (2) the administrator reviews the entries. If an entry conflicts with an existing reservation, publication is blocked until the conflict is resolved. Only confirmed entries affect availability. Regular (weeks 1–10) and exam (weeks 11–12) schedules are stored separately; the exam period does not inherit the regular schedule, and a period with no confirmed schedule is closed for booking.

### AD-4. Time stored in UTC

All timestamps are `timestamptz` in UTC. Clients convert to Astana time (UTC+5). The 1–72 h rule is checked on the server with server time, not client time.

### AD-5. Stateless API with tokens

The API keeps no session state. Short-lived access tokens (15 min) and refresh tokens allow horizontal scaling and simple mobile clients.

## 6. Main flow: booking a room

1. Student opens the map; the app loads room statuses for the selected floor and date (`GET /rooms?floor=..&date=..`) and subscribes to the building channel.
2. Student taps a room → the room card shows free intervals (`GET /rooms/{id}/availability?date=..`).
3. Student selects a slot and confirms → `POST /reservations`.
4. Backend checks role, 1–72 h window (server time), that the period has a confirmed schedule, classes / exams / blocks, and the user's own overlapping bookings, then inserts inside a transaction. The exclusion constraint resolves races.
5. On success: 201 + reservation; event broadcast; reminder scheduled. On conflict: 409 and the app refreshes the card.

## 7. Deployment

| Element | Plan |
|---|---|
| Backend + worker | Docker containers (FastAPI with Uvicorn) |
| Database | PostgreSQL 16 container with a persistent volume, daily backup |
| Admin panel | React static build served by Nginx, which also proxies `/api` and `/ws` |
| TLS | HTTPS / WSS through Nginx with a certificate (Let's Encrypt) |
| Environments | `dev` (local, `docker compose up`) and `staging` (university or cloud VM for demo) |
| CI | GitHub Actions: lint, tests, coverage report on every pull request |

## 8. Security

- Role-based access control checked on every endpoint; administrators only through the web panel.
- Passwords are stored only as salted hashes (Argon2 or bcrypt); verification codes are hashed, single-use, and expire.
- ID-card numbers and signatures are visible only to administrators; signatures are stored as files with restricted access.
- Input validation with Pydantic; SQL through SQLAlchemy (parameterised queries).
- Rate limiting on booking endpoints to prevent spam reservations.

## 9. Risks and mitigations

| Risk | Mitigation |
|---|---|
| PDF schedule format changes or is hard to parse | Preview step, manual editing, parser covered by tests with real schedule files |
| Real AITU floor plan not yet received | Prototype uses a schematic floor map; the list view works without the map |
| Key-handling rules not yet confirmed with staff | Interviews with the key-issuing staff before implementation |
| WebSocket connections lost on mobile networks | Auto-reconnect and REST reload on reconnect |
| Students book rooms and do not show up | Per-user limit; future option: check-in or automatic release |
