# Project Plan: Milestones, Responsibilities, Dependencies, and Risks

**Project:** AITU Booking  
**Team:** Adilbek Arman, Maksat Sugirov, Aizat Kydyrkhan  
**Supervisor:** Islam Amanzholuly Omirzak  
**Status:** Planning document for the first pre-defense

This document describes planned work. A milestone is marked as completed only when its deliverables are available in the repository and its acceptance criteria have been met.

## 1. Milestones

| Milestone | Target | Expected deliverables | Completion criteria |
|---|---|---|---|
| M1 — First pre-defense | 24 October 2026 | Project proposal, evidence of relevance, literature review, system and technology comparisons, requirements, architecture diagrams, UX designs, evaluation plan, and project plan | Documents and editable diagrams are accessible from the repository; YouTrack tasks identify owners and remaining work; the submitted version is tagged `pre-defense-1` |
| M2 — Requirements validation | Date to be agreed with the supervisor | Findings from user discussions, confirmed room and key procedures, revised requirements | Confirmed findings are distinguished from assumptions; changes to requirements are recorded |
| M3 — Backend and data model | Date to be agreed with the supervisor | FastAPI endpoints, PostgreSQL schema and migrations, timetable import prototype | Core API operations can be run and tested; conflicting bookings are rejected |
| M4 — Client applications | Date to be agreed with the supervisor | iOS booking flow, administrator web panel, and an initial Android implementation | Key scenarios work with the backend; changes in availability reach connected clients |
| M5 — Integration and evaluation | Date to be agreed with the supervisor | Integrated system, automated tests, concurrency results, usability findings, and measured evaluation | Results are compared with the targets and baselines in the evaluation plan; limitations are documented |
| M6 — Final submission | Date set by the university | Final code, documentation, demonstration, and repository tag | The submitted version is reproducible and approved for submission |

The first pre-defense does not require a complete application. Its purpose is to demonstrate completed analysis, design, planning, and traceable team contributions.

## 2. Responsibilities

| Team member | Primary responsibility | Deliverables |
|---|---|---|
| Adilbek Arman | Mobile development, interactive room map, mobile UI/UX | iOS application, Android application, mobile designs, map interaction, and mobile scenario checks |
| Maksat Sugirov | Backend and database | FastAPI application, PostgreSQL schema, booking rules, timetable processing, API tests, and concurrency checks |
| Aizat Kydyrkhan | Administrator web panel and UI/UX | Web panel, timetable review interface, key-management screens, and administrator scenario checks |
| All team members | Analysis, integration, reviews, and presentation | Contributions linked to YouTrack tasks, commits, pull requests, and reviewed documentation |

Each team member uses an individual Git account. The author of a pull request requests a review from another team member before it is merged.

## 3. Work Tracking and Review

Meaningful work is tracked in YouTrack. Each task must have an owner, expected outcome, acceptance criteria, priority, and deadline. The task ID is included in its branch name and commit or pull request description.

The team workflow is:

1. Create a task branch from the current `dev` branch.
2. Complete and commit the work in the task branch.
3. Open a pull request from the task branch into `dev`.
4. Have another team member review the changes and address comments.
5. Merge the reviewed change into `dev`.
6. Prepare and review a pull request from `dev` into `main` for a submission milestone.
7. Tag the exact commit submitted for pre-defense.

## 4. Dependencies

| Work item | Depends on | Why it matters |
|---|---|---|
| Final room-booking requirements | Discussions with students and responsible university staff | Booking permissions, key procedures, and working hours need confirmation |
| Room map and room catalog | Verified floor plans and room identifiers | Users must select the correct physical room |
| Availability calculation | Room catalog, booking rules, and timetable data | A room is available only when no class or active booking blocks the requested interval |
| PDF timetable import | Representative teaching and exam-session PDF files | Extraction rules must be checked against the actual document formats |
| Mobile and web integration | Agreed API contracts and test data | Client teams need stable request, response, and event formats |
| Concurrent booking tests | PostgreSQL schema and booking transactions | Conflicts must be prevented under simultaneous requests |
| Production email verification | Access to an approved email delivery method | University email codes cannot be verified without a working delivery process |
| Final evaluation | Integrated implementation and test environment | Metrics require a working system and recorded measurement conditions |

## 5. Risks

| Risk | Likelihood | Impact | Response | Owner |
|---|---|---|---|---|
| PDF layouts vary or text cannot be extracted reliably | Medium | High | Test representative PDFs early; show an import preview; allow manual corrections and reject uncertain entries | Maksat, Aizat |
| Room plans or room numbers are incomplete | Medium | High | Verify room identifiers against university material; label unverified map data; start with a confirmed area | Adilbek |
| Two users book the same room at the same time | Medium | High | Enforce conflict rules in PostgreSQL transactions and run concurrent-request tests | Maksat |
| Actual room and key procedures differ from project assumptions | High | High | Discuss the process with responsible staff and revise requirements before treating the workflow as final | All team members |
| Clients display outdated availability after a disconnect | Medium | Medium | Reload current availability after reconnection; treat the server response as authoritative | Adilbek, Maksat, Aizat |
| iOS, Android, backend, and web work exceed the available time | High | High | Prioritize the iOS and administrator scenarios; implement Android in stages; record unfinished scope honestly | All team members |
| Work cannot be traced to individual contributors | Medium | High | Use individual accounts, task branches, descriptive commits, pull requests, and YouTrack links | All team members |
| Supervisor comments arrive close to submission | Medium | Medium | Share draft deliverables in advance, record comments, and prioritize corrections affecting requirements and architecture | All team members |

## 6. Submission Check

Before the first pre-defense, the team will verify that:

- The README links to the available documentation, diagrams, UX designs, YouTrack project, and Figma project.
- Diagram source files and readable exports are present.
- Contributions from each team member can be traced from a YouTrack task to a commit or pull request.
- Supervisor feedback is recorded only if it has actually been received.
- The repository link, `pre-defense-1` tag, completed work, known limitations, and outstanding tasks are ready to present.