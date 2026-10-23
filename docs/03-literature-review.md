# Literature Review — AITU Booking

## 1. Introduction

This literature review examines existing research and technical solutions related to room booking, university timetable management, resource allocation, and real-time system updates. Its purpose is to identify approaches relevant to the AITU Booking project and determine which requirements are not fully addressed by existing solutions.

The review includes eight academic publications and four technical or practical sources covering room booking, timetable optimization, database functionality, real-time communication, PDF data extraction, and room scheduling services.

## 2. Analysis of Existing Research

Maulana et al. (2024) describe the development of the Paramadina Roomhub room booking application. This research demonstrates how a digital system can support room reservations. However, the available information does not establish whether it addresses all AITU Booking requirements, particularly real-time availability and concurrent booking requests.

Several studies focus on university course timetabling and optimization. Bashab et al. (2023) review optimization techniques, constraints, and open challenges. Müller et al. (2025) examine a real-world university timetabling problem, while Rappos et al. (2022) apply mixed-integer programming to timetable generation. Other studies explore hybrid teaching, individual study plans, and multi-criteria scheduling. These approaches help identify scheduling constraints, but AITU Booking uses an approved timetable as input rather than generating a new university timetable.

Technical documentation provides solutions for specific implementation challenges. PostgreSQL range types can represent time intervals and support the detection of overlapping bookings. FastAPI WebSockets enable real-time communication, but additional database and application-level controls are needed to prevent conflicting reservations. The pypdf library can extract text from PDF files, although imported timetable data requires validation because PDF layouts may vary. LibCal provides a practical example of an existing room and resource scheduling service.

Overall, the reviewed sources provide useful methods and technologies, but they do not establish that a single solution satisfies all AITU Booking requirements.

## 3. Comparison of Existing Solutions

| Source | Approach | Main Contribution | Limitations | Application to AITU Booking |
|---|---|---|---|---|
| Maulana et al. (2024) | Room booking application | Demonstrates digital room reservations | Coverage of AITU-specific requirements is not established | Reference for booking functionality |
| Bashab et al. (2023) | Timetabling optimization review | Summarizes constraints and optimization methods | Focuses on timetable optimization | Identifying scheduling constraints |
| Müller et al. (2025) | University timetabling | Examines real-world scheduling problems | Does not focus on consultation bookings | Understanding university scheduling |
| Rappos et al. (2022) | Mixed-integer programming | Models and solves timetable problems | Primarily addresses timetable generation | Understanding scheduling constraints |
| Davison et al. (2025) | Hybrid teaching timetabling | Considers different teaching formats | Does not cover the complete booking workflow | Supporting different room-use requirements |
| Steiner et al. (2025) | Curriculum-based timetabling | Considers individual study plans | Focuses on curriculum scheduling | Additional scheduling context |
| Dunke and Nickel (2023) | Multi-level, multi-criteria timetabling | Addresses complex scheduling objectives | Does not directly address real-time booking | Understanding multiple constraints |
| Chen et al. (2021) | Timetabling survey | Reviews research trends and opportunities | Provides a broad overview | Research background |
| PostgreSQL Documentation | Database range operations | Represents time intervals | Does not implement complete booking logic | Detecting overlapping reservations |
| FastAPI Documentation | WebSockets | Enables real-time communication | Does not guarantee booking consistency | Updating room availability |
| pypdf Documentation | PDF text extraction | Extracts text from timetable documents | Complex layouts require validation | Importing timetable data |
| LibCal | Room scheduling service | Provides an existing scheduling solution | Suitability for all AITU workflows requires evaluation | Practical comparison |

## 4. Research Gap

The reviewed sources address individual aspects of room booking and university scheduling, but they do not confirm that one solution covers all AITU Booking requirements.

The project must combine:

- Importing an approved timetable from a PDF in the university's "10+2 weeks" format.
- Displaying room availability.
- Preventing overlapping reservations, including simultaneous booking requests.
- Scheduling staff consultations.
- Providing real-time availability updates.
- Supporting classroom key management through ID cards.

The reviewed sources do not provide sufficient evidence that the classroom key workflow is covered by the examined approaches. This requirement must therefore be validated with the university.

Reliable booking management also requires database-level protection and application-level validation. Imported timetable data must be checked for correctness before being used by the system.

## 5. Conclusion

Existing research and technologies provide a foundation for developing AITU Booking. Timetabling studies help identify scheduling constraints, while PostgreSQL, FastAPI WebSockets, and pypdf provide tools for managing time intervals, delivering updates, and importing timetable data.

The main challenge is integrating these capabilities into one system that meets the university's specific requirements. AITU Booking will focus on approved timetable integration, room reservations, staff consultations, conflict prevention, real-time availability updates, and classroom key management through ID cards.

## References

1. Maulana et al. (2024). *Development of Paramadina Roomhub Application As Room Booking System Using Waterfall Method.*
2. Bashab et al. (2023). *Optimization Techniques in University Timetabling Problem: Constraints, Methodologies, Benchmarks, and Open Issues.*
3. Müller, Rudová, and Müllerová (2025). *Real-world university course timetabling at the International Timetabling Competition 2019.*
4. Rappos et al. (2022). *A mixed-integer programming approach for solving university course timetabling problems.*
5. Davison, Kheiri, and Zografos (2025). *Modelling and solving the university course timetabling problem with hybrid teaching considerations.*
6. Steiner, Pferschy, and Schaerf (2025). *Curriculum-based university course timetabling considering individual course of studies.*
7. Dunke and Nickel (2023). *A matheuristic for customized multi-level multi-criteria university timetabling.*
8. Chen et al. (2021). *A Survey of University Course Timetabling Problem: Perspectives, Trends and Opportunities.*
9. PostgreSQL Documentation. *Range Types.*
10. FastAPI Documentation. *WebSockets.*
11. pypdf Documentation. *Extract Text from a PDF.*
12. LibCal. *Room and Resource Scheduling Service.*