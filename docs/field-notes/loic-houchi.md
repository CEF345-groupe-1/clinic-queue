# Field notes – Loic Houchi

**Place visited:** Regional Hospital of Bafoussam (public hospital; our project targets a small private clinic, so the scale is larger)

## What I observed
- Patient registration is done by hand, on paper.
- Each patient carries a personal health booklet (carnet).
- Most patients come without an appointment.
- At busy times there are many patients, and each one has to wait for their turn.
- A separate block is reserved for emergencies.
- Payment is made at the cash desk after the consultation.

## Problems I noticed
- Everything is on paper, so there is no quick way to know how many patients are waiting or how long they have waited.
- Patients with no appointment wait without knowing their position in the queue.
- Payment happens after the consultation, so a separate step is needed at the end of the visit.

## What this means for Clinic Queue
- The system must handle walk-in patients as the main case, not as an exception, and add them to the doctor's queue in order of arrival.
- Emergencies need their own handling, separate from the normal queue.
- The queue position should be visible to the patient, for example on the waiting-room display.
- Patient records should replace the paper registers, and could point to the patient's booklet.