## 3. Functional requirements

| ID | Requirement | Priority | Problem |
|----|-------------|----------|---------|
| FR-01 | The system shall let a user log in with a username and a password. | Must | |
| FR-02 | The system shall let the owner add a doctor with a name and working days and hours. | Must | 5 |
| FR-03 | The system shall let the receptionist register a patient with a name and a phone number. | Must | 3 |
| FR-04 | The system shall let the receptionist book an appointment for a patient with a doctor at a given date and time. | Must | 5 |
| FR-05 | The system shall reject an appointment if the doctor already has an appointment at that date and time, and show the free times of that doctor. | Must | 5 |
| FR-06 | The system shall let the receptionist cancel an appointment up to [2 hours] before its time. | Should | 5 |
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