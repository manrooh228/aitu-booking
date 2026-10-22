# UX Designs and Key User Scenarios

**Purpose:** Present the interface designs of AITU Booking and the key user scenarios they support. Each scenario is linked to requirements in [06-requirements.md](06-requirements.md) and use cases in the [Use Case diagram](diagrams/export/use-case.png).

## 1. Where the designs are

| Design | Content | Link |
|---|---|---|
| Mobile app — dark design v2 (current) | 10 screens: sign-up, verification, floor maps C1.1 / C1.2 / C1.3, room booking, confirmation, conflict, consultations, profile | Figma, page **«Тёмный дизайн v2»** in [AITU Booking — Pre-defense prototype](https://www.figma.com/design/VDu3NBrZE9RSqq8gShbb71/AITU-Booking-%E2%80%94-Pre-defense-prototype) |
| Admin web panel | Key issue and return, unreturned keys, schedule import and preview | Figma, page **«Page 1»**, frames `keys`, `overdue`, `returned`, `import`, `preview` |
| Mobile app — first iteration (v1, light) | Wireframe-level screens used to agree on the flows | Figma, page **«Page 1»** |
| Scenario map | Key scenarios step by step with screens and requirement IDs | Figma, page **«UX — ключевые сценарии»** |

> All screens use demonstration data (capacities, equipment, lecturers, statuses). The interface language is Russian.

## 2. Design decisions

### 2.1 Navigation

The mobile app has three sections in a bottom navigation bar, so every main task is one tap away:

| Tab | Purpose | Requirements |
|---|---|---|
| **Бронирование** | Find a room on the floor map and book it | FR-04 – FR-14 |
| **Консультации** | Find a lecturer and book a consultation slot (Stage 2) | FR-36 – FR-39 |
| **Профиль** | My bookings and consultations, key status, settings, sign-out | FR-03, FR-13, FR-14 |

### 2.2 Map-first booking

- The booking tab opens on the **floor plan of the main building**: building switch (Главный корпус / Korkem), floor 1–3, block C1.1 / C1.2 / C1.3.
- The plan follows the real AITU floor plan of **floor 2** for all three blocks, with every room number (proportions simplified to fit a phone screen). Floors 1 and 3 show a "plan not loaded yet" state until their plans are added.
- Each room is a tappable area. Status is shown by **fill and border style, not colour alone**: free (solid blue), busy (dark, dashed border), my booking (outlined), common space (green, not bookable — e.g. Актовый зал). A legend is always visible (NFR-09).
- Tapping a room opens a **bottom sheet** with the room details, date chips and hourly slots, so the user never types a room number (FR-06, FR-09).

### 2.3 Booking rules shown before the error

Unavailable slots are disabled in the picker and labelled with the reason, instead of failing after submit:

| Slot label | Meaning | Rule |
|---|---|---|
| `< 1 ч` | Starts less than 1 hour from now | BR-01 |
| `> 72 ч` | Starts more than 72 hours from now | BR-01 |
| `пара` | Class or exam in the schedule | BR-02 |
| `занято` | Booked by someone else | BR-02 |
| `ваша` | Already booked by this user | BR-02 |

The sheet also states the key rule before booking: the key is issued at the reception against the university ID card (BR-05).

### 2.4 Visual system

| Token | Value | Use |
|---|---|---|
| Background | `#0B1424` | Screen background |
| Surface | `#121D33` | Cards, sheets, inputs |
| Line | `#25344F` | Borders |
| Text | `#E6EAF2` | Primary text |
| Muted text | `#9AA6BC` | Secondary text (≥ 4.5:1 contrast) |
| Accent | `#A9B4FF` | Primary buttons, selection, active tab |
| Free room | `#24477A` / border `#4A7BC4` | Map |
| Warning | `#F5C48A` on `#3A2A16` | Conflict, "key not issued" |

Typeface: **Inter** (Regular, Medium, Semi Bold, Bold). Touch targets are at least 44 px; cards and buttons use 12–16 px radii.

## 3. Screen inventory

### 3.1 Mobile app (dark design v2, 390 × 844)

| # | Screen (Figma frame) | Content | Requirements |
|---|---|---|---|
| 1 | `1 · Регистрация` | University email and password; "Получить код"; link to sign-in | FR-01 |
| 2 | `2 · Код из письма` | 6-digit code sent to the university email; resend | FR-01, NFR-04 |
| 3 | `3 · Карта — C1.1` | Building, floor and block switches; search; floor plan with room statuses; legend | FR-04, FR-05, FR-07 |
| 3b | `3b · Карта — C1.2` | Same, block C1.2 | FR-04, FR-05 |
| 3c | `3c · Карта — C1.3` | Same, block C1.3 | FR-04, FR-05 |
| 4 | `4 · Аудитория и время` | Room sheet: capacity, equipment, date chips, hourly slots with reasons, rules, "Забронировать" | FR-06, FR-09 – FR-11 |
| 5 | `5 · Бронь подтверждена` | Confirmation; key not issued yet; how to cancel | FR-09, FR-13, BR-05 |
| 6 | `6 · Время уже заняли` | Another student booked the slot first; choose another time | FR-12, NFR-03 |
| 7 | `7 · Консультации` | Lecturers with free slots (Stage 2) | FR-36, FR-37 |
| 8 | `8 · Профиль` | My bookings with cancel, key status, consultations, settings, sign-out | FR-03, FR-13, FR-14 |

### 3.2 Admin web panel

| Screen (Figma frame, «Page 1») | Content | Requirements |
|---|---|---|
| [`keys`](https://www.figma.com/design/VDu3NBrZE9RSqq8gShbb71/?node-id=5-131) | Find a student and the active booking; issue the key against the ID card | FR-31 |
| [`overdue`](https://www.figma.com/design/VDu3NBrZE9RSqq8gShbb71/?node-id=5-143) | Unreturned keys at the end of the day | FR-33, FR-34 |
| [`returned`](https://www.figma.com/design/VDu3NBrZE9RSqq8gShbb71/?node-id=5-153) | Return recorded; saved in the log | FR-32, NFR-13 |
| [`import`](https://www.figma.com/design/VDu3NBrZE9RSqq8gShbb71/?node-id=5-163) | Schedule type (weeks 1–10 / exams 11–12), validity period, PDF | FR-21, FR-25 |
| [`preview`](https://www.figma.com/design/VDu3NBrZE9RSqq8gShbb71/?node-id=5-177) | Extracted entries; a conflict blocks publication | FR-22 – FR-24, FR-27 |

## 4. Key user scenarios

### S1. Sign up with a university email

| Step | User action | System response | Screen |
|---|---|---|---|
| 1 | Enters the university email and a password, taps **Получить код** | Code sent to the university email | 1 → 2 |
| 2 | Enters the 6-digit code, taps **Подтвердить** | Account confirmed; the booking tab opens on the floor map | 2 → 3 |

**Requirements:** FR-01, NFR-04 · **Use case:** UC-01

### S2. Find a free room on the map and book it *(main scenario)*

| Step | User action | System response | Screen |
|---|---|---|---|
| 1 | Opens **Бронирование**; selects floor 2 and block (C1.1, C1.2 or C1.3) | Floor plan with room statuses for the current time | 3 / 3b / 3c |
| 2 | Taps a free room (e.g. 224P) | Bottom sheet: room details, date chips, hourly slots; unavailable slots labelled with the reason | 4 |
| 3 | Picks a date and a free slot, taps **Забронировать 14:00–15:00** | Booking confirmed; the room turns busy on the maps of other users | 5 |

**Result:** a room is booked in a few taps without typing its number, and the student knows the next step (bring the ID card for the key).
**Requirements:** FR-04 – FR-11, FR-13, FR-17, BR-01, BR-02, BR-05 · **Use cases:** UC-02 – UC-04

### S3. Two students book the same slot

| Step | What happens | Screen |
|---|---|---|
| 1 | Two students pick the same room and time | 4 |
| 2 | The server confirms one booking; the other request gets 409 Conflict | — |
| 3 | The second student sees "Это время только что заняли"; the slot is now marked `занято` | 6 |
| 4 | Taps **Выбрать другое время** and books another slot | 4 → 5 |

**Requirements:** FR-11, FR-12, NFR-03 · **Use case:** UC-04 · see the [booking sequence diagram](diagrams/export/booking-sequence.png)

### S4. Cancel a booking

| Step | User action | System response | Screen |
|---|---|---|---|
| 1 | Opens **Профиль → Мои бронирования** | List of bookings with key status | 8 |
| 2 | Taps **Отменить бронь** | Booking cancelled; a message confirms that the time is available again; the map updates for everyone | 8 |

**Requirements:** FR-13, FR-14, FR-17, BR-03 · **Use case:** UC-05

### S5. Administrator issues and receives a key *(admin panel)*

Find the student and the active booking → take the ID card, record the signature → key appears in the unreturned list at the end of the day (the end of the booking does not close it) → mark the key and ID card as returned.
**Screens:** `keys` → `overdue` → `returned` · **Requirements:** FR-31 – FR-34, BR-05, BR-08 · **Use cases:** UC-11, UC-12

### S6. Administrator imports a schedule *(admin panel)*

Choose the schedule type (weeks 1–10 or exams 11–12), the validity period and the PDF → review the extracted entries → a conflict with an existing booking blocks publication until it is fixed.
**Screens:** `import` → `preview` · **Requirements:** FR-21 – FR-27 · **Use case:** UC-08

### S7. Book a consultation *(Stage 2)*

| Step | User action | System response | Screen |
|---|---|---|---|
| 1 | Opens **Консультации**, finds a lecturer | Lecturer cards with free slots | 7 |
| 2 | Taps a slot, optionally enters a topic, taps **Записаться** | "Вы записаны"; the booking appears in the profile; cancellation allowed until 1 hour before the start | 7 → 8 |

**Requirements:** FR-36 – FR-39, BR-04 · **Use case:** UC-14

## 5. Traceability

| Scenario | Screens | Requirements | Use case |
|---|---|---|---|
| S1 | 1, 2 | FR-01 | UC-01 |
| S2 | 3, 3b, 3c, 4, 5 | FR-04 – FR-11, FR-13 | UC-02 – UC-04 |
| S3 | 4, 6 | FR-11, FR-12 | UC-04 |
| S4 | 8 | FR-13, FR-14 | UC-05 |
| S5 | keys, overdue, returned | FR-31 – FR-34 | UC-11, UC-12 |
| S6 | import, preview | FR-21 – FR-27 | UC-08 |
| S7 | 7, 8 | FR-36 – FR-39 | UC-14 |

## 6. Not yet designed

| Item | Planned for |
|---|---|
| Plans for floors 1 and 3, and the Korkem building | After the plans are prepared from the AITU floor plans |
| "No confirmed schedule for these dates" state in the dark design (exists in v1 as `no_schedule`) | Next design iteration |
| Admin: room management, manual schedule editing, cancelling a booking as admin | Next design iteration |
| Admin panel in the dark visual system | Next design iteration |
| Lecturer: publishing consultation slots | Stage 2 |

## 7. Usability evaluation (planned)

The team plans to compare how long students need to find and book a free room using the PDF schedule versus the prototype (S2), and to observe S3 and S4. Results have not been measured yet; the method is described in the [evaluation plan](09-evaluation-plan.md).
