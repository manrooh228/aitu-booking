# Verification and Evaluation Plan

## 1. Purpose

The purpose of testing is to verify that AITU Booking supports room and consultation booking, prevents scheduling conflicts, and maintains up-to-date availability across mobile applications and the administrator panel.

The criteria below are proposed acceptance targets. Actual results will be recorded during development.

## 2. Functional Testing

| ID | Area | Test Scenario | Acceptance Criteria |
|---|---|---|---|
| FT-01 | Registration | Register using a university email address | Production registration accepts only verified `@astanait.edu.kz` addresses. The development verification bypass is disabled in production. |
| FT-02 | Access control | Perform actions using different user roles | Students cannot access administrative operations. Teachers manage their own consultation slots. Key operations require an authorized staff account. |
| FT-03 | Room map | Select a building, floor, and room | The correct floor plan is displayed. Selecting a room opens its details and booking options. |
| FT-04 | Booking window | Test start times immediately below, at, and above the 1-hour and 72-hour boundaries | Bookings starting between 1 and 72 hours ahead, inclusive, are accepted when available. Requests outside this range are rejected. |
| FT-05 | Room booking | Reserve an available room | One confirmed booking is saved and appears in the user's booking list. |
| FT-06 | Booking conflicts | Request a room during an existing booking or scheduled class | The request is rejected with a clear conflict message. No conflicting booking is saved. |
| FT-07 | Adjacent bookings | Create a booking that starts exactly when another ends | The booking is accepted if no other restrictions apply. |
| FT-08 | Room cancellation | Cancel before, at, and after the booking start time | Cancellation is allowed before the start. At or after the start, cancellation is rejected. |
| FT-09 | Consultations | Book an available consultation slot and attempt to book it again | The first booking succeeds. A booking exceeding the slot's defined capacity is rejected. |
| FT-10 | Consultation cancellation | Cancel 61, 60, and 59 minutes before the consultation | Cancellation succeeds at least 60 minutes before the start and is rejected less than 60 minutes before it. |
| FT-11 | Timetable import | Upload a teaching timetable PDF and a separate exam-session PDF | Teaching weeks 1–10 and exam-session weeks 11–12 are handled separately. The administrator can review and correct extracted data before publication. |
| FT-12 | Import errors | Upload an unsupported or unreadable PDF | The system reports the problem and does not automatically publish incomplete or incorrect data. |
| FT-13 | Schedule conflicts | Publish timetable changes that overlap existing bookings | Conflicts are identified. Publication does not silently create overlapping occupancy. |
| FT-14 | Key tracking | Record key issue, ID-card deposit, and return | Each action is linked to the correct booking and responsible staff member. Returned keys no longer appear as outstanding. |
| FT-15 | Outstanding keys | Check the panel at the configured end of the working day | All issued but unreturned keys are listed correctly. |
| FT-16 | Availability updates | Create or cancel a booking while another device is connected | The other device updates room availability without manual refresh. |
| FT-17 | Reconnection | Disconnect a device, change a booking, and reconnect | The application reloads the current state and does not continue displaying outdated availability. |

Time-boundary tests will use a controlled server clock. Booking intervals will include the start time and exclude the end time.

## 3. Testing Methods

| Method | Scope |
|---|---|
| Unit testing | Booking-window rules, interval overlap detection, cancellation rules, and timetable parsing |
| Integration testing | API operations with PostgreSQL, access control, timetable publication, and key records |
| End-to-end testing | Complete user journeys through the mobile application and administrator panel |
| Concurrency testing | Simultaneous attempts to book the same room or consultation slot |
| Performance testing | API response times, notification delay, and behavior under load |
| Usability testing | Whether users can complete key tasks without assistance |

Integration and concurrency tests will use PostgreSQL, matching the planned production database.

## 4. Metrics and Acceptance Targets

| Metric | Measurement | Proposed Target |
|---|---|---|
| Functional correctness | Percentage of mandatory acceptance tests passed | 100% before final acceptance |
| Conflicting bookings | Number of overlapping active bookings after concurrent requests | 0 |
| Same-slot booking outcome | Send 50 simultaneous requests for one available room and time interval | Exactly one booking succeeds; all other requests receive a controlled conflict response |
| API response time | 95th percentile of availability-query and booking-request duration | No more than 1 second under the defined test load |
| Availability update delay | Time from database commit to the updated state being displayed on another device | 95th percentile of no more than 2 seconds while connected |
| Unexpected server errors | Percentage of requests returning unexpected HTTP 5xx responses | Less than 1% under the defined test load |
| Timetable extraction accuracy | Percentage of fully correct extracted entries in a manually checked reference sample | At least 95% for the agreed PDF format |
| Published timetable correctness | Compare reviewed and published entries with the reference timetable | 100% for the test dataset |
| Usability task completion | Percentage of tasks completed without assistance | At least 90% |
| Reconnection recovery | Time from restored connection to current availability being displayed | No more than 5 seconds under the test conditions |

The 95th percentile means that 95% of measured requests or updates complete within the stated time.

Expected rejections, such as attempts to book an occupied room, will be counted separately from unexpected server errors.

Targets will be reviewed with the supervisor. Reasons for any changes will be documented.

## 5. Measurement Conditions

Testing will use synthetic accounts and booking records. The dataset will include at least:

- 100 rooms;
- 500 user accounts;
- 5,000 booking records;
- a representative teaching timetable;
- a separate exam-session timetable;
- records of issued, returned, and outstanding keys.

Each report will record the hardware specifications, operating system, software versions, application commit, database configuration, network conditions, and test dataset.

The initial load test will use one FastAPI backend process and 50 concurrent virtual users. Approximately 80% of requests will query availability, while 20% will create or cancel bookings.

Each run will include a one-minute warm-up followed by five minutes of measurement. The test will be repeated three times. A separate burst test will send simultaneous requests for the same slot.

The mobile application will be tested on at least one physical iPhone and in the iOS simulator. Android testing will be added when the Android client is available. Administrator workflows will be tested in Chrome and Safari.

## 6. Baseline Comparison

| Evaluation Area | Baseline | Proposed Solution | Comparison |
|---|---|---|---|
| Availability updates | REST polling every 5 seconds | WebSocket notifications | Update delay, number of HTTP requests, server resource usage, and recovery after interruption |
| Finding a room | A simple list containing building, floor, and room details | An interactive building and floor map | Task completion time, success rate, and incorrect selections |
| Timetable entry | Manual entry of a selected timetable sample | PDF import followed by administrator review | Total time required to publish correct data and number of errors requiring correction |

Both alternatives will use the same data and equivalent tasks. Task order will be varied to reduce the effect of participants remembering previous answers.

Any conclusion about improvement will be based on measured results.

## 7. Usability Evaluation

A small study will involve 5–8 representative users, including students and teachers. Key-management and timetable-import scenarios will additionally be reviewed with a staff member familiar with these processes.

Participants will be asked to:

1. Find an available room in a specified building and floor.
2. Book the room for a valid time.
3. Find and cancel their booking.
4. Book a consultation.
5. Complete relevant administrative tasks where applicable to their role.

For each task, the team will record completion, time taken, errors, requests for help, and participant comments.

This small sample will be used to improve the interface. Its findings will not be treated as representative of all university users.

## 8. Test Evidence and Responsibilities

| Team Member | Main Responsibility |
|---|---|
| Adilbek Arman | Mobile workflows, map interaction, device testing, and mobile usability |
| Maksat Sugirov | API, database integrity, concurrency, and backend performance |
| Aizat Kydyrkhan | Administrator workflows, timetable review, and the key-management interface |
| All team members | Integration testing, defect review, and evaluation of results |

Each test record will contain:

- test ID;
- expected result;
- actual result;
- pass/fail status;
- tested commit;
- supporting evidence.

Defects will be recorded in YouTrack with reproduction steps and links to the relevant fixes.

Automated tests and supporting materials will be stored in the repository. The final report will present achieved targets and remaining limitations.