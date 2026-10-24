# Project Description
Title: Development of a Real-Time Mobile Application for Booking Consultations and Study Rooms at a University
Team: Adilbek Arman, Maksat Sugirov, Aizat Kydyrkhan.
Supervisor: Islam Amanzholuly Omirzak.
## Problem Statement
Students may find it difficult to quickly determine which study room is available at a suitable time. Class schedules show when rooms are occupied by lessons, but availability outside scheduled classes often has to be checked separately. Consultations with lecturers may also be arranged through personal messages or verbal agreements. These processes take time and can lead to scheduling conflicts.
## Project Aim
To develop a system that allows users to find a room on an interactive university map, view available times, and book it without overlapping reservations. The system will also support consultation bookings and provide administrators with tools to manage schedules, rooms, and keys.
## Target Users
Students select rooms on the map, book available times, view and cancel reservations, and register for consultations.
Lecturers set consultation availability and view bookings.
Administrators upload and edit schedules, manage rooms, record key collection and return, and monitor unreturned keys.
## Main User Scenario
A user selects a building and floor, finds a room directly on the map, and taps it. A room card opens with date and time options. If the selected time slot is available, the system confirms the booking and updates its status. Users do not need to enter a room number manually.
A reservation may start no earlier than one hour and no later than 72 hours from the time of booking. A room reservation may be cancelled before it begins. A consultation booking may be cancelled at least one hour before its start.
## Project Objectives
Study the current room-use and consultation-booking processes and gather user requirements.
Prepare interactive building and floor maps with selectable rooms.
Design a database for rooms, schedules, consultations, reservations, and key-handling records.
Implement schedule import from a file, with an administrator preview and confirmation step. Support a separate examination schedule for weeks 11–12 and manual corrections.
Develop a server API that checks time-slot availability and prevents double bookings during simultaneous requests.
Build a mobile application and a web administration panel.
Implement booking-status updates and reminders.
Evaluate the system through functional, integration, and concurrency testing.
## Project Scope
The first version focuses on room booking through the interactive map, schedule import, and administrative key tracking. Mobile development will begin with iOS using Swift/SwiftUI. An Android application using Kotlin and the complete consultation-booking workflow are planned for later stages of the diploma project.
The proposed technology stack includes FastAPI for the backend, PostgreSQL for the main database, and a web application for the administration panel. These choices will be justified in the technology comparison.
The planned key-handling process records the student’s signature and university ID card as a deposit when a key is issued. When the key is returned, the administrator records the return of the ID card.
## Expected Outcomes
The expected outcome is a working prototype consisting of a mobile interface, an interactive room map, a server API, and a web administration panel. During the demonstration, the team will show room selection, reservation creation and cancellation, schedule import, key tracking, and the system’s response when two users attempt to book the same time slot simultaneously.
