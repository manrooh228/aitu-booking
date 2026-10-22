# Functional and Non-Functional Requirements

**Purpose:** Define what AITU Booking must do and the quality constraints it must meet. Every requirement has an ID so it can be traced to diagrams, UX scenarios, YouTrack tasks, and tests.

**Priority (MoSCoW):** **M** — Must have for the first release, **S** — Should have, **C** — Could have, **W** — Won't have in this diploma stage.
**Stage:** **1** — first development stage (room booking, iOS, schedule, admin panel), **2** — later stage (consultations, Android).

## 1. Actors

| Actor | Description |
|---|---|
| Student | Finds and books study rooms, books consultations, picks up and returns keys. |
| Lecturer | Publishes consultation slots and views student bookings. |
| Administrator | Manages rooms, schedules, and the key log through the web panel. |
| Email service (external) | Delivers verification codes to the university email and booking reminders. |
| Push service — APNs (external) | Delivers reminders and status notifications to the iOS app. |

## 2. Functional Requirements

### 2.1 Authentication and roles

| ID | Requirement | Actor | Priority | Stage |
|---|---|---|---|---|
| FR-01 | The system shall let users register and sign in only with a university email address (`@astanait.edu.kz`), confirmed by a one-time code sent to that address. | All | M | 1 |
| FR-02 | The system shall assign one of three roles — Student, Lecturer, Administrator — and restrict functions by role. | All | M | 1 |
| FR-03 | The system shall let a user sign out and shall expire sessions after a period of inactivity. | All | M | 1 |

### 2.2 Interactive map and room search

| ID | Requirement | Actor | Priority | Stage |
|---|---|---|---|---|
| FR-04 | The mobile app shall let the user select a building and a floor. | Student | M | 1 |
| FR-05 | The app shall display the floor plan with rooms as selectable areas, colour-coded by status for the selected interval (free / busy / no data). | Student | M | 1 |
| FR-06 | Tapping a room shall open a room card with its name, capacity, equipment, and today's timeline. | Student | M | 1 |
| FR-07 | The user shall be able to filter rooms by date, time, and minimum capacity. | Student | S | 1 |
| FR-08 | The app shall offer a list view of rooms as an alternative to the map (accessibility fallback). | Student | S | 1 |

### 2.3 Room reservations

| ID | Requirement | Actor | Priority | Stage |
|---|---|---|---|---|
| FR-09 | The user shall be able to book a free time slot from the room card without typing the room number. | Student | M | 1 |
| FR-10 | A reservation shall start no earlier than **1 hour** and no later than **72 hours** after the moment of the request. | System | M | 1 |
| FR-11 | The system shall reject a reservation that overlaps a class, an exam, or another confirmed reservation for the same room, and a reservation that overlaps another active booking of the same user. | System | M | 1 |
| FR-11a | Booking shall be closed for any period that has no confirmed schedule; the app shall explain this to the user. | System | M | 1 |
| FR-12 | When two requests for the same room and overlapping interval arrive simultaneously, exactly one shall be confirmed and the other shall receive a conflict response. | System | M | 1 |
| FR-13 | The user shall be able to view a list of their upcoming and past reservations. | Student | M | 1 |
| FR-14 | The user shall be able to cancel a room reservation at any time before it starts. | Student | M | 1 |
| FR-15 | The system should limit the number of active reservations per student (proposed default: 2, configurable; to be confirmed with the supervisor). | System | C | 1 |
| FR-16 | The administrator shall be able to cancel any reservation and give a reason, which is shown to the student. | Administrator | S | 1 |

### 2.4 Real-time updates and notifications

| ID | Requirement | Actor | Priority | Stage |
|---|---|---|---|---|
| FR-17 | When a reservation is created or cancelled, the system shall push an availability event to all connected clients viewing that building. | System | M | 1 |
| FR-18 | The app shall refresh room status on the map without manual reload after receiving the event. | Student | M | 1 |
| FR-19 | The system shall send a reminder notification before a reservation or consultation starts (default: 30 minutes). | System | S | 1 |
| FR-20 | The system shall notify a student when an administrator cancels their reservation. | System | S | 1 |

### 2.5 Schedule management

| ID | Requirement | Actor | Priority | Stage |
|---|---|---|---|---|
| FR-21 | The administrator shall be able to upload the class schedule as a PDF file. | Administrator | M | 1 |
| FR-22 | The system shall extract schedule entries (room, day, time, course, group, week range) and show a preview before saving. | System | M | 1 |
| FR-23 | The preview shall highlight entries that could not be parsed or that reference unknown rooms. | System | M | 1 |
| FR-24 | The administrator shall confirm or discard the import; nothing is saved without confirmation. | Administrator | M | 1 |
| FR-25 | The system shall support a regular schedule for weeks 1–10 and a separate examination schedule for weeks 11–12; the examination period does not inherit the regular schedule. The administrator sets the validity period of each import. | System | M | 1 |
| FR-26 | The administrator shall be able to add, edit, and delete schedule entries manually. | Administrator | M | 1 |
| FR-27 | If imported entries conflict with existing reservations, the preview shall list the conflicts and block publication until each conflict is resolved (entry corrected or reservation cancelled with notification). | Administrator | M | 1 |

### 2.6 Room management

| ID | Requirement | Actor | Priority | Stage |
|---|---|---|---|---|
| FR-28 | The administrator shall be able to create, edit, and deactivate rooms (name, building, floor, capacity, equipment, bookable flag). | Administrator | M | 1 |
| FR-29 | The administrator shall be able to link a room to its area on the floor map. | Administrator | S | 1 |
| FR-30 | The administrator shall be able to block a room for a period (e.g., maintenance, event). | Administrator | S | 1 |

### 2.7 Key tracking

| ID | Requirement | Actor | Priority | Stage |
|---|---|---|---|---|
| FR-31 | The administrator shall record key issue: room, student, time, the student's signature, and the university ID card taken as deposit. | Administrator | M | 1 |
| FR-32 | The administrator shall record key return, which also records the return of the ID card. | Administrator | M | 1 |
| FR-33 | The panel shall display all keys not yet returned, with the student and the time issued. | Administrator | M | 1 |
| FR-34 | The end of a reservation shall not mark the key as returned; keys not returned by the end of the working day shall appear in the unreturned list. | System | M | 1 |
| FR-35 | The administrator shall be able to view and export the key log for a chosen period. | Administrator | C | 1 |

### 2.8 Consultations

| ID | Requirement | Actor | Priority | Stage |
|---|---|---|---|---|
| FR-36 | The lecturer shall be able to publish consultation slots (date, time, location or online link, capacity of one). | Lecturer | M | 2 |
| FR-37 | The student shall be able to view a lecturer's free slots and book one. | Student | M | 2 |
| FR-38 | The system shall prevent two students from booking the same consultation slot. | System | M | 2 |
| FR-39 | The student shall be able to cancel a consultation booking at least **1 hour** before it starts. | Student | M | 2 |
| FR-40 | The lecturer shall see the list of booked slots with student names and the topic entered by the student. | Lecturer | M | 2 |
| FR-41 | The lecturer shall be able to cancel a slot; booked students are notified. | Lecturer | S | 2 |

### 2.9 Out of scope for this diploma stage

| ID | Item | Priority |
|---|---|---|
| W-01 | Online payment or paid room rental. | W |
| W-02 | Integration with the university LMS or the official schedule system through an API (PDF import is used instead). | W |
| W-03 | Indoor navigation or turn-by-turn directions to a room. | W |

## 3. Non-Functional Requirements

| ID | Category | Requirement | How it will be verified |
|---|---|---|---|
| NFR-01 | Performance | Proposed target: p95 API response time ≤ **500 ms** with 50 concurrent clients. | Load test (Locust) on staging; actual results recorded in the test report. |
| NFR-02 | Real-time | An availability change reaches connected clients within **2 seconds** of the booking being confirmed. | Integration test with two WebSocket clients measuring the delay. |
| NFR-03 | Consistency | Overlapping reservations for one room are impossible, even under concurrent requests; enforced at database level (PostgreSQL exclusion constraint on room and time range). | Concurrency test: 100 parallel requests for the same interval → exactly 1 confirmed reservation. |
| NFR-03a | Correctness | The 1–72 h rule is checked against server time at its boundaries. | Boundary tests: 59:59 vs 60:00 minutes; 72 h vs 72 h + 1 s. |
| NFR-04 | Security | All traffic uses HTTPS / WSS. Passwords are stored only as salted hashes (Argon2 / bcrypt); verification codes expire and are single-use; the API uses signed access tokens. | Configuration review; security checklist. |
| NFR-05 | Security | Every API endpoint checks the caller's role (role-based access control). | Automated authorization tests per endpoint. |
| NFR-06 | Privacy | Only data needed for booking and key tracking is stored. ID-card data is limited to the card number and the deposit status; signatures are stored only for the key log and are accessible only to administrators. | Data-model review against this requirement. |
| NFR-07 | Availability | Target uptime of 99% during the academic semester (excluding planned maintenance). | Uptime monitoring during the pilot. |
| NFR-08 | Usability | Target: a first-time user finds and books a free room faster in the app than by using the PDF schedule (proposed target: under 60 seconds). | Comparison of task time, PDF vs app, with students; results not yet measured. |
| NFR-09 | Usability | The mobile app supports Light and Dark mode and Dynamic Type; status is never shown by colour alone (icon or label is also used). | UI review; accessibility inspector. |
| NFR-10 | Localization | The interface is in Russian for the first release; Kazakh and English are planned. | UI review. |
| NFR-11 | Compatibility | iOS app targets iOS 17+; the admin panel (React) works in the last two versions of Chrome, Safari, Edge, and Firefox. | Manual test matrix. |
| NFR-12 | Maintainability | Backend code is covered by automated tests of at least **70%** for booking, schedule, and key modules; CI runs tests on every pull request. | Coverage report in CI. |
| NFR-13 | Auditability | Creation, cancellation, schedule import, and key operations are logged with user, timestamp, and action. | Inspection of the audit log after test scenarios. |
| NFR-14 | Time handling | All times are stored in UTC and shown in the Astana time zone (UTC+5). | Unit tests on time conversion and the 1–72 h rule. |
| NFR-15 | Portability | The backend and database run in Docker containers and can be started with one command for development. | Fresh-clone setup check. |

## 4. Business Rules

| ID | Rule | Related requirements |
|---|---|---|
| BR-01 | Booking window: start time ≥ now + 1 h and ≤ now + 72 h. | FR-10 |
| BR-02 | A room cannot be booked during a class, an exam, an administrator block, or another confirmed reservation. A user cannot hold two overlapping bookings. | FR-11, FR-25, FR-30 |
| BR-07 | A period without a confirmed schedule is closed for booking. | FR-11a |
| BR-08 | The end of a reservation does not mean the key was returned; return is recorded only by the administrator. | FR-34 |
| BR-03 | Room reservations may be cancelled any time before the start. | FR-14 |
| BR-04 | Consultation bookings may be cancelled no later than 1 h before the start. | FR-39 |
| BR-05 | A key is issued only against a signature and a university ID card deposit; the ID card is returned with the key. | FR-31, FR-32 |
| BR-06 | Weeks 1–10 use the regular schedule, weeks 11–12 use the examination schedule. | FR-25 |

## 5. Traceability

| Requirement group | Diagram / document | UX scenario | Owner |
|---|---|---|---|
| FR-01 – FR-03 | Use Case UC-01; Component: Auth module | S1 | Maksat (backend), Adilbek (iOS) |
| FR-04 – FR-18 | Use Cases UC-02 – UC-05, UC-07; Component: Rooms, Reservations, Realtime | S2 – S4 | Adilbek (iOS), Maksat (backend) |
| FR-19 – FR-20 | Use Case UC-06; Component: Notifications | — | Maksat |
| FR-21 – FR-30 | Use Cases UC-08 – UC-10; Component: Schedule, Rooms | S6 | Aizat (admin), Maksat |
| FR-31 – FR-35 | Use Case UC-11 – UC-12; Component: Keys | S5 | Aizat (admin), Maksat |
| FR-36 – FR-41 | Use Cases UC-13 – UC-16; Component: Consultations | S7 | Stage 2 |
| NFR-01 – NFR-15 | [Evaluation plan](09-evaluation-plan.md) | — | Team |
