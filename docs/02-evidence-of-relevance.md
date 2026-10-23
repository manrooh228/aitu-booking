# Evidence of Relevance and User Research

**Purpose:** Check whether the problems AITU Booking is meant to solve actually exist, using answers from students and teachers, and record what this changes in the requirements.

**Sources:**

| Code | Method | Participants | Date | Collected by |
|---|---|---|---|---|
| SURVEY | Google Forms questionnaire with role-based branching | 11 responses: 10 students, 1 teacher | 21–23 October 2026 | Team |
| TI-1, TI-2 | Short written interviews with teachers ([teacher-interviews.md](interviews/teacher-interviews.md)) | 2 teachers | 23 October 2026 | Adilbek |

Raw survey answers are kept in the team's Google Sheet "AITU Booking — ответы на опрос". Names are removed in this document; respondents are referred to by code (S01–S10 for students, T-F for the teacher who filled in the form). The anonymised answers are in the [appendix](#appendix-anonymised-survey-answers).

**Limitations.** This is a small convenience sample, mostly from our own groups, so percentages below describe these respondents, not AITU students in general. One student response is empty and one has only the first question answered. Nobody responsible for rooms and keys has answered yet, so every hypothesis about the key process is still unchecked. The teacher who filled in the form may be one of the two interviewed teachers; we cannot tell, because the form was anonymous.

## 1. Hypotheses and results

| ID | Hypothesis | Result | Evidence |
|---|---|---|---|
| H1 | Students have trouble finding a free room. | **Partly confirmed** | Most students who answered find rooms by walking along corridors, asking teachers or using a Telegram bot that gives only approximate results (S02, S03, S04, S06, S08). Search time ranged from under 5 to over 30 minutes. Two students said finding a room is quick because rooms have glass walls or the search takes under 5 minutes (S07, S10). |
| H2 | Students find a room occupied after agreeing to use it. | **Weak** | 2 of 8 said yes (S03 "a couple of times", S07 "often"); 6 said never. Most students do not reserve rooms at all, so there is little to "agree" on; the more common problem is finding a room busy or locked on arrival (S06). |
| H3 | A locked room and the key process stop students from using free rooms. | **Signal only, not confirmed** | S06: if the room is locked and a key is needed, "we just give up". S05 asked by email to reserve a room and got no reply. No staff response yet. |
| H4 | A booking window of 1–72 hours suits students. | **Not confirmed** | Only 1 of 8 said the window is convenient. 4 of 8 want to book closer to the start time, 1 wants to book more than 72 hours ahead, 2 are unsure. |
| H5 | Consultation sign-up is informal and could be improved with time slots. | **Confirmed** | Both interviewed teachers announce consultations through group representatives in Teams (TI-1, TI-2). Students mostly walk in during office hours or write in messengers (3 of 8 each). TI-1 reports that too many students sometimes arrive at once; TI-2 does not have this problem. |
| H6 | Teachers would accept automatic booking without manual confirmation. | **Confirmed (1 teacher)** | T-F: automatic booking is enough, consultation times are set by the teacher, cancelling 1 hour before is enough. |
| H7 | Teachers also need to find free rooms. | **Confirmed (1 teacher)** | TI-2 has to contact the academic department to find a room and would like the app to show and book free rooms in coordination with the department. |
| H8 | The timetable is published as PDF; weeks 1–10 regular, 11–12 exams. | **Not checked in this round** | Not covered by the survey. Still needs a sample file and confirmation from the academic department. |
| H9 | An ID card deposit for the key is acceptable. | **Not checked** | Requires the staff interview (INT-05). |

## 2. Student survey summary

Base: 8 students who answered the closed questions (S01–S03, S05–S08, S10). S04 answered only the first question; S09 is empty. S01 has never looked for a free room, so S01 is excluded from the search-time question.

### How students look for a free room now

| Method mentioned | Respondents |
|---|---|
| Walk from room to room and look inside | S02, S04, S06 |
| Telegram bot that lists free rooms (approximate) | S03, S06 |
| Ask a teacher / the room is free or a teacher allowed it | S02, S08 |
| Glass walls make it visible whether a room is free | S10 |
| Email request to reserve a room (no answer received) | S05 |
| Heard from friends | S05 |

### Time spent finding a room and getting a key (n = 7)

| Answer | Count |
|---|---|
| Under 5 minutes | 2 |
| 5–15 minutes (incl. S06 "10–20 minutes") | 3 |
| Over 30 minutes | 1 |
| Don't remember | 1 |

### What matters in a room (n = 8, multiple choice)

| Feature | Count |
|---|---|
| Power sockets | 7 |
| Quiet | 6 |
| Capacity | 4 |
| Projector or screen | 2 |
| Location (building, floor) | 2 |
| Whiteboard | 1 |

### Booking window 1–72 hours (n = 8)

| Answer | Count |
|---|---|
| Want to book closer to the start time | 4 |
| Convenient as is | 1 |
| Want to book more than 72 hours ahead | 1 |
| Don't know | 2 |

### How students sign up for consultations (n = 8, multiple choice)

| Answer | Count |
|---|---|
| Don't sign up, come during office hours | 3 |
| Approach the teacher in person | 3 |
| Write in a messenger | 3 |
| Email | 2 |
| LMS / Moodle | 1 |

### Free-text comments

- S05: the current process is "inconvenient and slow".
- S06: there is no way to book a free room except for consultations; students want to sit somewhere with their group, walk to a distant free room and find it taken, and end up in the canteen.

## 3. Teacher findings

| Topic | TI-1 | TI-2 | T-F (form) |
|---|---|---|---|
| How students learn about consultations | Through the group representative in Teams | Through group representatives in Teams | — |
| Too many students arrive at once | Yes | No | — |
| Who sets consultation times | — | — | The teacher |
| Manual confirmation of each booking | — | — | Not needed |
| Cancelling 1 hour before | — | — | Enough |
| Finding a free room | — | Has to contact the academic department | — |
| Conditions for using the app | Integration with the existing LMS | Room booking coordinated with the academic department | — |
| Biggest frustration | — | — | Students who skip classes |

## 4. Conclusions

1. **The room problem is real but not universal.** Several students spend 5–30+ minutes walking around or rely on an approximate Telegram bot; others find rooms quickly. The strongest pain is not the search itself but arriving at a room that is busy or locked. This supports live availability on the map (FR-05, FR-17, FR-18) more than anything else.
2. **There is an informal alternative we had not listed.** Students already use a Telegram bot that shows free rooms. It should be added to the [comparison of existing systems](04-existing-systems.md): what it shows, how accurate it is, and why it is not enough (no booking, no key process).
3. **Sockets and quiet matter more than equipment.** Power sockets (7 of 8) and quiet (6 of 8) were chosen far more often than projector or whiteboard. The room card and filters should show these (FR-06, FR-07, FR-28).
4. **The 1-hour minimum lead time does not match how students behave.** Half of the respondents want to book closer to the start. This is a direct conflict with FR-10 / BR-01 and should be discussed with the supervisor and the staff member responsible for keys, since the 1-hour minimum may exist to give time for key issue.
5. **Consultation slots are wanted, with two conditions.** Teachers already set their own times and accept automatic booking and a 1-hour cancellation rule (FR-36–FR-39 match). Teachers asked for LMS integration and coordination with the academic department; both are currently out of scope (W-02).
6. **Teachers are also room users.** TI-2 looks for rooms through the academic department. The Lecturer role currently has no room-booking requirement.
7. **The key process has no evidence yet.** One student gives up when a key is needed, but the rules (who may book, ID deposit, working hours, unreturned keys) are still assumptions until INT-05 is done.

## 5. Impact on requirements

| Finding | Affected requirement | Proposed action | Status |
|---|---|---|---|
| Students want to book closer to start | FR-10, BR-01, NFR-03a | Discuss lowering the minimum lead time (e.g. 15 minutes or "now") with the supervisor and key staff | To discuss |
| Sockets and quiet are most important | FR-06, FR-07, FR-28 | Add "power sockets" to room equipment; consider a "quiet room" attribute and filter | Proposed |
| Arriving at a busy or locked room | FR-05, FR-17, FR-18, NFR-02 | Keep as Must; show in the room card whether a key must be collected | Keep / proposed |
| Students book for group work, not only consultations | FR-15 | Keep the per-student limit configurable; check it does not block group bookings | Keep |
| Telegram bot already used | [04-existing-systems](04-existing-systems.md) | Add as an existing alternative | To do |
| Teachers announce consultations via Teams | FR-36, FR-37, FR-19 | Keep slot publishing and reminders; consider a shareable link to a teacher's slots | Proposed |
| Teacher accepts automatic booking and 1 h cancellation | FR-38, FR-39, BR-04 | No change | Confirmed |
| Teachers asked for LMS integration | W-02 | Keep out of scope for this stage; note as future work | No change |
| Teachers look for rooms too | FR-02, FR-09 | Decide whether lecturers can book rooms in stage 1 | To discuss |

## 6. Next steps

| Step | Owner | Needed for |
|---|---|---|
| Interview the staff member responsible for rooms and keys (INT-05) using the staff questions from the survey | Aizat | H3, H9, FR-31–FR-35, BR-05 |
| Get a sample timetable PDF and confirm weeks 1–10 / 11–12 | Maksat | H8, FR-21–FR-25 |
| Collect 5–10 more student responses outside our own groups | Adilbek | H1, H4 |
| Look at the Telegram bot and add it to the comparison | Team | Section 4 |
| Measure search time with the prototype vs. the current way | Team | NFR-08 |

## Appendix: anonymised survey answers

### Students

| Code | Last time looking for a room | How they knew it was free | Time | Room was taken after agreeing | Important in a room | 1–72 h window | Consultation sign-up |
|---|---|---|---|---|---|---|---|
| S01 | Never looked | — | Never looked | No | Sockets, quiet | Want closer to start | Come during office hours |
| S02 | Every day, walked in and checked each room | Room empty or teacher allowed it | 5–15 min | No | Capacity, sockets, quiet | Convenient | In person, messenger, email |
| S03 | Used a Telegram bot | The bot said so | 5–15 min | A couple of times | Capacity, sockets | Want closer to start | Messenger |
| S04 | Walked around rooms, sometimes found one, sometimes not | — | — | — | — | — | — |
| S05 | A week ago; told to email for a booking, nobody replied | From friends | Don't remember | No | Capacity, sockets, projector, quiet, location | Want closer to start | In person, messenger, email |
| S06 | Bot lists approximate free rooms, then check in person; locked rooms need a key | Go and check | 10–20 min; give up if a key is needed | No | Sockets, quiet, location | Want closer to start | Come during office hours |
| S07 | — | — | Under 5 min | Often | Projector | Don't know | Come during office hours |
| S08 | — | Through teachers | Over 30 min | No | Capacity, sockets, whiteboard, quiet | Want more than 72 h ahead | In person, LMS |
| S09 | (empty response) | | | | | | |
| S10 | Rooms have glass walls, could see it was free | Saw nobody inside | Under 5 min | No | Sockets, quiet | Don't know | — |

### Teacher (form)

| Code | Who sets times | Manual confirmation | Cancellations / no-shows | 1 h cancellation | Data needed | Comment |
|---|---|---|---|---|---|---|
| T-F | The teacher | Not needed, automatic is enough | "There will be none" | Enough | "Office hours" | Students who don't study and skip classes |
