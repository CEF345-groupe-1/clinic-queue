# Software Requirements Specification: Clinic Queue

**Course:** CEF 345, Group 1
**Project:** clinic-queue (clinic appointments and queue)
**Written by:** Analysis team (Nyietalem, Ticha)

## 1. Introduction

### 1.1 Purpose
This document says what the Clinic Queue system must do. It is written for
the development team, the testers and the lecturer, so that a developer who
has never visited the clinic can build the right system and a tester can
check it.

### 1.2 Scope
Clinic Queue is a web application for a small private clinic in Buea. It lets
the receptionist book appointments and manage the waiting queue of each
doctor. It lets the doctors follow their patients and the owner follow the
day. It answers the problems of the problem statement
(docs/problem-statement.md): long and unpredictable waits, queue jumping, no
record of the day, patients leaving without being seen, and no appointment
times.

### 1.3 Definitions

| Term | Meaning |
|------|---------|
| Appointment | A time booked in advance for a patient with a doctor |
| Walk-in | A patient who arrives without an appointment |
| Queue | The ordered list of patients waiting for one doctor |
| Position | A patient's number in the queue, given in order of arrival |
| No-show | A patient who booked an appointment and did not come |

## 2. Overall description

### 2.1 Stakeholders

| Stakeholder | Interest in Clinic Queue |
|-------------|--------------------------|
| Patients | Know their turn, wait fairly and are not forgotten |
| Receptionist | Less manual work and fewer conflicts at the desk |
| Doctors and nurses | A clear order of patients, no time lost calling absent people |
| Clinic owner | Reliable records and statistics to run the clinic |
| Development team | Finish a tested and documented system by February |

### 2.2 Users

| User | Use of the system |
|------|-------------------|
| Receptionist | Registers patients, books appointments, manages queues |
| Doctor | Views his or her queue, calls patients |
| Owner | Manages doctors and users, reads the daily report |

### 2.3 Operating environment
The system is a web application used in a phone or computer browser. It runs
on Node.js with Express and a SQLite database, the tools of the course.

### 2.4 Constraints
- The system is built with the course toolchain: JavaScript, Node.js, Express, SQLite, Git and GitHub.
- It must be finished and tested by February by a team of part-time students.
- Every change is made through a reviewed pull request.

### 2.5 Assumptions
- The clinic has a device at reception and one for each doctor.
- Patients give a phone number when they register.
- The clinic has an internet connection of at least 3G during opening hours.
- Three kinds of users exist: receptionist, doctor and owner.

## 3. Functional requirements

| ID | Requirement | Priority | Problem |
|----|-------------|----------|---------|
| FR-01 | The system shall let a user log in with a username and a password. | Must | |
| FR-02 | The system shall let the owner add a doctor with a name and working days and hours. | Must | 5 |
| FR-03 | The system shall let the receptionist register a patient with a name and a phone number. | Must | 3 |
| FR-04 | The system shall let the receptionist book an appointment for a patient with a doctor at a given date and time. | Must | 5 |
| FR-05 | The system shall reject an appointment if the doctor already has an appointment at that date and time, and show the free times of that doctor. | Must | 5 |
| FR-06 | The system shall let the receptionist cancel an appointment up to 2 hours before its time. | Should | 5 |
| FR-07 | The system shall let the receptionist mark an appointment as attended or as a no-show. | Should | 3, 4 |
| FR-08 | The system shall let the receptionist add a patient without an appointment (walk-in) to the waiting queue of a doctor. | Must | 1, 2 |
| FR-09 | The system shall give each patient in a queue a position number in order of check-in, and shall not change it except when a patient is removed from the queue. | Must | 2 |
| FR-10 | The system shall show each doctor's queue with the position of every patient. | Must | 1 |
| FR-11 | The system shall let the doctor call the next patient and mark the consultation as started and finished. | Must | 1 |
| FR-12 | The system shall let the receptionist remove a patient who left from the queue and record the reason "left without being seen". | Should | 4 |
| FR-13 | The system shall show a waiting-room screen with the position numbers currently called and the next ones. | Could | 1 |
| FR-14 | The system shall record for each patient the arrival time, the start time and the end time of the consultation. | Must | 3 |
| FR-15 | The system shall show the owner a daily report with the number of patients seen per doctor, the average waiting time, the number of cancellations and the number of no-shows. | Should | 3 |
| FR-16 | The system shall record which user made each change to an appointment or a queue, and when. | Should | 2 |

The Problem column refers to the numbered problems of the problem statement.

## 4. Non-functional requirements

| ID | Requirement | Type |
|----|-------------|------|
| NFR-01 | Adding a walk-in patient to the queue shall take no more than 30 seconds for a trained receptionist. | Usability |
| NFR-02 | Every page shall load in under 3 seconds on a 3G connection. | Performance |
| NFR-03 | The interface shall work in a phone browser 360 px wide. | Compatibility |
| NFR-04 | Only the owner shall be able to add or remove doctors and users. | Security |
| NFR-05 | Passwords shall not be stored in plain text. | Security |
| NFR-06 | All appointments and queue entries shall still be present after the server restarts. | Reliability |
| NFR-07 | Times shall be shown in the 24-hour format, for example 14:30. | Constraint |

## 5. Use case diagram and use case descriptions

![Use case diagram](diagrams/usecases.drawio.svg)

### UC-01 Book an appointment

| Field | Description |
|-------|-------------|
| ID | UC-01 |
| Actors | Receptionist |
| Preconditions | The receptionist is logged in. The doctor exists with working days and hours. |
| Main flow | 1. The receptionist opens "New appointment". 2. She selects the patient, or registers a new one. 3. She selects the doctor. 4. She picks a date and a time. 5. The system checks that the doctor is free at that time. 6. She confirms. 7. The system saves the appointment and shows it in the doctor's agenda. |
| Alternative flow 2a | The patient is not found: the receptionist registers the patient (name and phone number), then continues at step 3. |
| Alternative flow 4a | The date is in the past: the system refuses with "Date must be in the future" and stays at step 4. |
| Alternative flow 5a | The doctor already has an appointment at that time: the system refuses with "Dr. X is already booked at HH:MM", lists the free times of the doctor and stays at step 4. |
| Postconditions | The appointment is saved with patient, doctor, date, time and the user who booked it. |
| Requirements covered | FR-02, FR-03, FR-04, FR-05, FR-16 |

### UC-02 Add a walk-in patient to the queue

| Field | Description |
|-------|-------------|
| ID | UC-02 |
| Actors | Receptionist |
| Preconditions | The receptionist is logged in. The doctor exists. |
| Main flow | 1. The receptionist opens "Walk-in". 2. She searches the patient by name. 3. She selects the doctor. 4. She confirms. 5. The system adds the patient at the end of the doctor's queue, records the arrival time and shows the position number. |
| Alternative flow 2a | The patient is not found: the receptionist registers the patient, then continues at step 3. |
| Alternative flow 4a | The patient is already in that queue: the system shows the current position and adds nothing. |
| Postconditions | The patient is in the queue with a fixed position and an arrival time. The other positions are unchanged. |
| Requirements covered | FR-03, FR-08, FR-09, FR-14 |

### UC-03 Call the next patient

| Field | Description |
|-------|-------------|
| ID | UC-03 |
| Actors | Doctor |
| Preconditions | The doctor is logged in and at least one patient waits in his or her queue. |
| Main flow | 1. The doctor opens his or her queue. 2. He or she clicks "Call next". 3. The system marks the patient at position 1 as "in consultation", records the start time and moves the other patients up by one position. 4. After the consultation, the doctor clicks "Finish". 5. The system records the end time and sets the status to "done". |
| Alternative flow 1a | The queue is empty: the system shows "No patient waiting". |
| Alternative flow 2a | The patient called has left: the receptionist removes the patient with the reason "left without being seen", and the doctor calls the next one. |
| Postconditions | Start and end times are saved. The queue shows the remaining patients in order. |
| Requirements covered | FR-09, FR-10, FR-11, FR-12, FR-14 |

## 6. Priorities (MoSCoW)

| Priority | Requirements |
|----------|--------------|
| **Must have** | FR-01, FR-02, FR-03, FR-04, FR-05, FR-08, FR-09, FR-10, FR-11, FR-14 |
| **Should have** | FR-06, FR-07, FR-12, FR-15, FR-16 |
| **Could have** | FR-13 |
| **Won't have this time** | Online payment and Mobile Money, online consultation (telemedicine), pharmacy stock management, full electronic medical records |

## 7. Out of scope

- Online payment and Mobile Money.
- Online doctor consultation (telemedicine).
- Pharmacy stock management.
- Full electronic medical records.
- Lab and pharmacy queues: only the doctors' queues are covered.

The system covers the queue and the patient flow inside the clinic only.