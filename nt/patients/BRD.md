---
module: "patients"
doc: "BRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Patients: Business Requirements Document

Evidence is in the Source columns only. PRD IDs refer to `atreya-docs/nt/patients/PRD.md`.

## 1. Purpose & overview

The Patients part of Nadi Tarangini lets a doctor keep a record of the people they treat. They can add a patient (named or anonymous), correct a patient's details, look a patient up, search by name, remove a patient from their list, see a patient's earlier visits and symptoms, delete a visit report, and record fees, remarks and the next appointment for a visit. It is available on the website and in the mobile app. (PRD-1; `Nadi-Tarangini-Frontend:routes/web.php:402-444`; `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/patient_list/patient_screen.dart`)

## 2. Business objectives

The code does not state why this module exists or what it should achieve. See section 12 (question 1) and section 11.

## 3. Stakeholders & user roles

| Role | How the code shows them | Source |
|---|---|---|
| Doctor | Patient actions run for a signed-in user; deletion is limited to patients of the caller's allowed doctor ids | PRD-R07; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4770-4785` |
| Admin | An admin web view lists a user's patients and visits | PRD-R05; `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:358` |
| NT Lite user | A lite dashboard lists and searches patients | PRD-R05; `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteDashboardController.php:43` |
| Receptionist | Same patient functions are also registered for a reception login | PRD section 13 item 11; `Ashoka-World-Backend:routes/api.php:1684-1695` |

Which roles exactly may do what is not stated in code; see question 2.

## 4. Scope

### In scope
- Add a patient, add an anonymous patient, edit, view (PRD-R01 to R04).
- List and search patients (PRD-R05, PRD-R06).
- Remove a patient from the doctor's list (PRD-R07).
- Previous visits, symptom history, delete a visit report (PRD-R08, PRD-R09).
- Fees, doctor remarks and next appointment (PRD-R10).
- Patient pick-lists for booking appointments, country list, dashboard counts and banners (PRD-R11 to R13).
- Web helper steps around the patient list (PRD-R14).

### Out of scope
- Appointments, reports and medical assessment themselves; the patient module only calls them. (PRD-R14; `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:324`)
- 14 backend functions with no screen calling them (patient queries, patient progress, remaining fees, clinic details, topics list, new symptom and others) are not presented as live features; see question 3. (PRD section 6)

## 5. Current business process (as-is)

1. The doctor opens the patient list. (`Nadi-Tarangini-Frontend:routes/web.php:402`)
2. To add a patient, the doctor opens Add member, fills in name, gender, date of birth or age, phone and consents, and saves; the list then refreshes. (PRD-R01; `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:150`)
3. To record a patient without identity, the doctor adds an anonymous patient. (PRD-R02)
4. The doctor can open a patient to view details, edit them, or delete the patient. (PRD-R03, R04, R07)
5. The doctor can open the previous visits of a patient, see symptom history, resume a visit, or delete a visit report. (PRD-R08, R09; `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:231`)
6. After a consultation, the fee, doctor remarks and optional next appointment are saved. (PRD-R10)
7. On mobile the same steps start from the patient list screen (per the fact pack, Dart files not read). (`atreya-docs/_map/_modules/patients/facts.md`; `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/patient_list/patient_screen.dart`)

## 6. Business rules

| # | Rule | Source |
|---|---|---|
| 1 | A patient needs a first name and a last name, using letters and spaces only; the middle name is optional. | PRD-R01; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:83-85` |
| 2 | Gender must be one of four codes (M, F, D, N). | PRD-R01; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:86` |
| 3 | Three consents (nadi, report, share report) must each be recorded as yes or no. | PRD-R01; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:87-89` |
| 4 | Either date of birth or age is needed; a date of birth cannot be in the future and the person must be between 1 and 100 years old. | PRD-R01; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:134`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:206`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:227` |
| 5 | A profile picture must be a JPEG or PNG image. | PRD-R01; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:397` |
| 6 | The phone number must match the chosen country code. | PRD-R01; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:104` |
| 7 | An anonymous patient needs a client code and gender, and cannot be edited later. | PRD-R02, R03; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:661`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1054` |
| 8 | Deleting a patient hides the patient from the doctor; the record is marked, not erased. | PRD-R07; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4785` |
| 9 | Deleting a visit report marks it deleted by the doctor; it is not erased. | PRD-R09; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4980-5007` |
| 10 | Doctor remarks are required when saving fees; fee amounts are whole numbers. | PRD-R10; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2475-2479` |
| 11 | A next appointment date must be tomorrow or later, and is required if a start or end time is given; the end time must be after the start time. | PRD-R10; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2487-2489`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2543` |
| 12 | Only the listed report types (1,2,3,4,7,8,9) can be marked to share. | PRD-R10; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2484` |

## 7. Business requirements

| ID | Requirement | Source |
|---|---|---|
| BR-01 | A doctor can add a patient with name, gender, date of birth or age, phone number, and three consents. | PATIENTS-R01; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:83-227` |
| BR-02 | A doctor can add an anonymous patient without full identity details. | PATIENTS-R02; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:658-754` |
| BR-03 | A doctor can correct a patient's details, except for anonymous patients. | PATIENTS-R03; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1030-1149` |
| BR-04 | A doctor can view a patient's details. | PATIENTS-R04; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:896-1017` |
| BR-05 | A doctor can see a list of their patients on web and mobile and on the dashboard. | PATIENTS-R05; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3725`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4019` |
| BR-06 | A doctor can search patients by name. | PATIENTS-R06; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4311` |
| BR-07 | A doctor can remove a patient from their list. | PATIENTS-R07; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4744-4798` |
| BR-08 | A doctor can see a patient's earlier visits and symptom history. | PATIENTS-R08; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1758-2006`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5021-5152` |
| BR-09 | A doctor can delete a visit report. | PATIENTS-R09; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4966-5013` |
| BR-10 | A doctor can record fees, remarks, recommendations, shared reports and the next appointment for a visit. | PATIENTS-R10; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2459-2543` |
| BR-11 | When booking an appointment, a doctor can pick from their patients. | PATIENTS-R11; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4638-4702` |
| BR-12 | Phone-number forms offer a list of countries. | PATIENTS-R12; `Ashoka-World-Backend:routes/api.php:766` |
| BR-13 | The doctor dashboard shows an association count and a banner/referral list. | PATIENTS-R13; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5166`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3436` |
| BR-14 | On the web, the patient list also supports start-of-visit helpers (new medical id, last-visit information, scheduled appointments). | PATIENTS-R14; `Nadi-Tarangini-Frontend:routes/web.php:403-473` |

## 8. Availability by environment

Taken from `atreya-docs/environments.md` (status TO FILL). All environments for all three repositories are TO FILL, so availability per environment is not known.

| Repository | dev | staging | production |
|---|---|---|---|
| Ashoka-World-Backend | TO FILL | TO FILL | TO FILL |
| Nadi-Tarangini-Frontend | TO FILL | TO FILL | TO FILL |
| Nadi-Tarangini-App | TO FILL | TO FILL | TO FILL |

The comparison of staging against production has not been computed (`atreya-docs/nt/patients/staging-delta.md`).

## 9. Dependencies & external systems

| Dependency | Use | Source |
|---|---|---|
| Push-notification service (Firebase) | Used in the patient code; purpose not stated | PRD section 12; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:576` |
| Cloud file storage (S3) | Used in the patient code; probably profile pictures, not stated | PRD section 12; `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:381` |
| Appointments and reports parts of the product | Patient list calls them for appointments and medical ids | PRD-R14; `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:166` |

## 10. Assumptions & constraints

- Patients are shown to doctors by user id; most functions need a signed-in user. (PRD section 2)
- Age must be between 1 and 100 years. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:235`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:757`)
- Only English language files were found for this module while seven languages are required. (PRD section 9; required list from the plugin's `references/qa-scope-rules.md`, language files from `atreya-docs/_map/_modules/patients/facts.md`)

## 11. Success measures (TO CONFIRM)

- TO CONFIRM (product owner): what counts as success for the Patients part (for example patients added per doctor, time to find a patient)?
- TO CONFIRM (product owner): is there a target for duplicates or incomplete patient records?

## 12. Needs confirmation

1. (Product owner) What are the business goals of the Patients part, and who is it mainly for?
2. (Product owner) Which roles (doctor, receptionist, admin, patient) may add, edit, delete and view patients?
3. (Product owner) The 14 backend functions with no screen calling them: are they retired or used by another app?
4. (Product owner) When a patient or a visit report is deleted, should the data be kept or removed for good, and who may see it afterwards?
5. (Product owner) Why must a patient be between 1 and 100 years old; how should infants be recorded?
6. (Product owner) Which languages must the patient forms and messages support?
7. (Developer) What are Firebase and cloud storage used for in the patient flows?
8. (Product owner) Should receptionist logins be covered by the same requirements?
9. (Product owner) Who will fill in environments.md so availability per environment can be stated?
10. (Developer) What does the association count on the dashboard measure?

## 13. Document control

| Field | Value |
|---|---|
| Status | Draft |
| Date | 2026-11-03 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend 8dfbb37db7d71a400b3656bd50fbed6173908a24; Nadi-Tarangini-Frontend e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d; Nadi-Tarangini-App 0b7deec6de2b0b8b4f05eab4be8c8430523829bf |
