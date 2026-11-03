---
module: "patients"
doc: "PRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Patients: Product Requirements Document


## 1. Overview

The patients module covers the records of the people a doctor treats: creating a patient (named or anonymous), editing and viewing one, listing and searching patients, deleting a patient, listing a patient's previous visits and symptom history, deleting a visit report, and saving fees and next-appointment details for a visit. (`Ashoka-World-Backend:routes/api.php:1114-1146`, `Ashoka-World-Backend:routes/api.php:926-935`)

The backend exposes 32 route entries for the module (`getAllCountries` appears as GET and POST entries on one route), the web app has 22 module routes, and the module has 5 mobile screens and 6 web views. (`Ashoka-World-Backend:routes/api.php:766`, `Nadi-Tarangini-Frontend:routes/web.php:402-444`, `atreya-docs/_map/_modules/patients/facts.md`)

14 backend routes have no caller in the three repos of this workspace; they are listed in section 6 and asked about in section 13. (`atreya-docs/_map/_modules/patients/facts.md`)

## 2. Users, roles & permissions

- All 32 patient routes listed here, except `getAllCountries` and `getLanguage` carry the `auth.token` middleware; `getAllCountries` and `getLanguage` carry only `api` (public). (`Ashoka-World-Backend:routes/api.php:766`, `Ashoka-World-Backend:routes/api.php:1423`, `Ashoka-World-Backend:routes/api.php:926-935`, `Ashoka-World-Backend:routes/api.php:1114-1146`)
- `v2/patient/patientPreviousVisit` lists only `auth.token`. Several of the same controller methods are also registered under a `reception-api` group with `reception.authentication` (see section 13). (`Ashoka-World-Backend:routes/api.php:1647`)
- All 22 web routes of the module run behind `check_auth_token`, `fetch_notifications`, `ensure_normal_dashboard_mode`. (`Nadi-Tarangini-Frontend:routes/web.php:402-473`)
- Deleting a patient updates only a `user_personal_info` row whose `role_id` is '2'; an earlier lookup requires the patient's `doctor_id` to be in the caller's allowed doctor ids and the patient to be active and not already deleted by the doctor. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4770-4785`)
- The doctor/receptionist/admin/patient role names that map to these routes are not stated in the fact pack; see section 13.

## 3. User journeys

**Web: add a patient.** Patient list (`patient.patientlist`) goes to Add member (`patient.add-member`); saving calls `patient/addClient` (or `patient/addAnonymousClient` for an anonymous patient), then reloads the list with `infinitePatientList`; the view then goes back to the patient list. (`atreya-docs/_map/_modules/patients/facts.md`, `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:150`, `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:200`, `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:336`)

**Web: edit / view / delete.** Patient list opens View member (`patient.view_member`, loads `patient/getClientDetails`), which goes to `/edit-member/` (`patient.edit_member`); saving calls `patient/updateClient` then `infinitePatientList`. Delete calls `patient/deletePatient` then `infinitePatientList`. (`Nadi-Tarangini-Frontend:app/Http/Controllers/ViewMemberController.php:21`, `Nadi-Tarangini-Frontend:app/Http/Controllers/EditMemberController.php:23`, `Nadi-Tarangini-Frontend:app/Http/Controllers/EditMemberController.php:121`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:366`)

**Web: previous visits.** `previousVisits/{id}` loads `infinitePatientList`, `appointment/dateWiseAppointment` and `v2/patient/patientPreviousVisit`; a visit report can be deleted via `deleteReport/{medicalId}/{patientId}`; `resumeVisit` calls `v2/report/getCurrentVisitInfo`. (`Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:35`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:53`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:83`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:160`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:231`)

**Mobile: patient list.** PatientScreen (`/patientScreen`) goes to AddPatientScreen, EditPatientScreen, ViewPatientScreen, `/assessmentScreen`, `/fillPrakrutiScreen` and `/reportScreen`. AddPatientScreen goes to `/addAppointmentScreen`, `/dashboardScreen`, `/patientScreen`. AddPatientFromAppointmentScreen goes to `/addAppointmentScreen`. (`atreya-docs/_map/_modules/patients/facts.md`, `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/patient_list/patient_screen.dart`)

## 4. Functional requirements

### PATIENTS-R01: Add a patient
The backend creates a patient through `patient/addClient`. It requires first name and last name (letters and spaces only), gender (M, F, D or N), and three consent flags (`nadi_consent`, `report_consent`, `share_report_consent`, each 0 or 1). Middle name is optional (letters and spaces). Profile picture, if sent, must be an image (jpeg, png, jpg). Date of birth or age is required, and the date of birth may not be in the future. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:83-91`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:397`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:134`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:227`)
**Acceptance criteria**
- Given a missing first name, last name, gender or consent flag, when addClient is called, then validation fails. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:83-89`)
- Given a date of birth in the future, when addClient is called, then the response message is "Date of birth cannot be a future date". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:134`)
- Given a date of birth that is not between 1 and 100 years old, then 400 "Date of birth must be between 1 and 100 years old". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:206`)
- Given an age that is not valid, then 400 "Invalid age"; given neither date of birth nor age, then 400 "Date of birth or age is required". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:218`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:227`)
- Given a phone number that does not match its country code, then the message is "The provided country code is not valid for the given phone number"; given a malformed number, then 400 "Invalid phone number format". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:104`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:182`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:83-227`, `Ashoka-World-Backend:routes/api.php:1145`
**Screens**: AddPatientScreen, AddPatientFromAppointmentScreen, EditPatientScreen (App); patient.add-member (Web) · **API**: POST patient/addClient

### PATIENTS-R02: Add an anonymous patient
`patient/addAnonymousClient` requires a user id, a client code and a gender, the three consent flags (0 or 1), and either date of birth (not in the future) or age. Anonymous patients cannot later be edited. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:658-673`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:754`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1054`)
**Acceptance criteria**
- Given no user id, then 400 "User id is not provided"; no client code, then 400 "Client code is required"; no gender, then 400 "Gender is required". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:658`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:661`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:664`)
- Given a date of birth that is invalid or outside 1 to 100 years, or an invalid age, or neither, then the 400 messages "Invalid date of birth", "Date of birth must be between 1 and 100 years old", "Invalid age", "Date of birth or age is required" respectively. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:740`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:743`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:750`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:754`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:658-754`, `Ashoka-World-Backend:routes/api.php:1122`
**Screens**: AddPatientScreen (App); patient.add-member (Web) · **API**: POST patient/addAnonymousClient

### PATIENTS-R03: Edit a patient
`patient/updateClient` requires a client id and applies the same name, gender, date-of-birth and picture rules as add. An anonymous patient cannot be edited. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1030-1063`)
**Acceptance criteria**
- Given no client id, then 400 "Client id is required"; invalid, then 400 "Invalid client id"; unknown, then 404 "Client not found". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1030`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1034`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1046`)
- Given an anonymous patient, then 404 "Anonymous patient cannot be edited". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1054`)
- Given a phone number problem, then the messages "Phone number is required", "Invalid phone number format" or the country-code message are returned. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1077`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1103`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1149`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1030-1149`, `Ashoka-World-Backend:routes/api.php:1123`
**Screens**: EditPatientScreen, AddPatientScreen, AddPatientFromAppointmentScreen (App); patient.edit_member (Web) · **API**: POST patient/updateClient

### PATIENTS-R04: View patient details
`patient/getClientDetails` returns one patient's details for a user id and client id. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:896-1017`)
**Acceptance criteria**
- Given no user id, then 400 "User id is not provided"; no client id, then 400 "Client id is required"; invalid client id, then 400 "Invalid client id". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:896`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:899`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:902`)
- Given an unknown client, then 404 "Client not found"; given no details, then 404 "Details not found". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:924`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1009`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:896-1017`, `Ashoka-World-Backend:routes/api.php:1126`
**Screens**: PatientScreen, ViewPatientScreen, EditPatientScreen (App); patient.view_member, patient.edit_member (Web) · **API**: POST patient/getClientDetails

### PATIENTS-R05: List patients
`infinitePatientList` returns the patient list (paged "infinite" list) and is used by the patient list, add/edit/delete refresh and many web flows; `getLimitedActivePatients` returns a limited list for the doctor dashboard. Both require a user id. `patientList` is an older list route with no caller. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3725`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4019`, `Ashoka-World-Backend:routes/api.php:926-928`)
**Acceptance criteria**
- Given no user id, then 400 "User id is not provided." for `infinitePatientList`, `getLimitedActivePatients` and `patientList`. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3725`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4019`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3496`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3496-4300`, `Ashoka-World-Backend:routes/api.php:927-928`
**Screens**: PatientScreen, VisitReportListScreen, DashboardScreen (App); patient.patientlist, doctor_dashboard.dashboard (Web) · **API**: POST infinitePatientList, POST getLimitedActivePatients

### PATIENTS-R06: Search patients by name
`searchPatientUsingName` searches the doctor's patients by name. (`Ashoka-World-Backend:routes/api.php:929`)
**Acceptance criteria**
- Given no user id, then 400 "User id is not provided.". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4311`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4311-4603`, `Ashoka-World-Backend:routes/api.php:929`
**Screens**: PatientScreen (App); patient.patientlist, admin.user_patient_list, auth.nt-lite.nt_lite_dashboard (Web) · **API**: POST searchPatientUsingName

### PATIENTS-R07: Delete a patient
`patient/deletePatient` requires a numeric `patient_id`. It marks the patient `delete_by_doctor = 1` (it does not remove the row) for a patient whose doctor id is among the caller's allowed doctor ids. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4744`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4770-4789`)
**Acceptance criteria**
- Given an unknown or not-permitted patient, then 404 "Invalid patient id". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4778`)
- Given success, then 200 "Patient deleted successfully"; given no row updated, then 404 "Patient not found or not deleted". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4789`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4792`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4744-4798`, `Ashoka-World-Backend:routes/api.php:1120`
**Screens**: PatientScreen (App); patient.patientlist, patient.view_member (Web) · **API**: POST patient/deletePatient

### PATIENTS-R08: Previous visits and symptom history
`v2/patient/patientPreviousVisit` returns a patient's visit list (requires `patient_id`); `patient/previousVisitsDetails` returns symptom history (requires numeric `patient_id`). (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1758`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5021`)
**Acceptance criteria**
- Given an unknown patient, then 404 "Invalid patient id" on both. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1792`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5056`)
- Given no visits, then 404 "Visit list not found" on both; given visits, then 200 "Get visit list" (v2) or "Success" (details). (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1999`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2001`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5144`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5146`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1758-2006`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5021-5152`, `Ashoka-World-Backend:routes/api.php:1116`, `Ashoka-World-Backend:routes/api.php:1647`
**Screens**: PatientScreen, VisitReportListScreen (App); patient.previousVisits, admin.user_previous_visits, auth.nt-lite.nt_lite_previous_visits (Web) · **API**: POST v2/patient/patientPreviousVisit, POST patient/previousVisitsDetails

### PATIENTS-R09: Delete a visit report
`patient/deleteReport` requires a patient id and a medical id and soft-deletes that visit report: it sets `delete_by_doctor` = 1 and `last_modified_on` on `medical_report` for the caller's own `doctor_id`; no row is removed. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4966-5007`)
**Acceptance criteria**
- Given no patient id, then 400 "Patient id is required"; no medical id, then 400 "Medical id is required"; invalid ids, then 400 "Invalid patient id" / "Invalid medical id". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4966`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4969`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4973`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4977`)
- Given no matching patient or medical id, then 404 "Invalid patient id" / "Enter valid medical id"; given success, then 200 "Report deleted successfully". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4987`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4998`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5007`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4966-5013`, `Ashoka-World-Backend:routes/api.php:1118`
**Screens**: ReportScreen (App, caller deleteReportForDoctor); web route DELETE `deleteReport/{medicalId}/{patientId}` · **API**: POST patient/deleteReport

### PATIENTS-R10: Save fees, doctor remarks and next appointment
`patient/saveFees` stores fee charged, fee paid, consultation and therapy fees (integers), doctor remarks (required), yoga and panchakarma recommendations, shared report ids (1,2,3,4,7,8,9), an uploaded file with description, and an optional next appointment date, start time and end time. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2475-2489`)
**Acceptance criteria**
- Given no medical id or client id, then 400 "Medical id is required" / "Client id is required"; invalid ids, then 400 "Invalid medical id" / "Invalid client id". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2459`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2462`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2466`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2469`)
- Given a next appointment date earlier than tomorrow, then validation fails. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2487`)
- Given a start or end time but no next appointment date, then 400 "Next appointment date is mandatory". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2543`)
- Given an end time that is not after the start time or not in H:i format, then validation fails or "Invalid end time format". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2489`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2508`)
- Given an unknown medical id, then 404 "Enter valid medical id"; unknown client, 404 "Invalid client id". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2527`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2532`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2459-2543`, `Ashoka-World-Backend:routes/api.php:1131`
**Screens**: MainAssessmentScreen (App, caller saveFeesDetails); live_nadi.medical_assessment (Web, via DietController and FeeDetailsController) · **API**: POST patient/saveFees

### PATIENTS-R11: Patient pick-lists for appointments
`fetchPatientNames` and `accessUserWisePatientList` supply patient names to the add-appointment screens. `accessUserWisePatientList` returns 400 "Invalid user id" for a bad user id. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4638`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4662`)
**Acceptance criteria**
- Given an invalid user id, then 400 "Invalid user id" for `accessUserWisePatientList`. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4662`)
- Given success, then the message is "Success". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4638`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4693`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4638-4702`, `Ashoka-World-Backend:routes/api.php:931`, `Ashoka-World-Backend:routes/api.php:933`
**Screens**: AddAppointmentScreen (App); appointment.add-appointment (Web) · **API**: POST fetchPatientNames, POST accessUserWisePatientList

### PATIENTS-R12: Country list
`getAllCountries` is one route (GET and POST entries) without `auth.token` and returns countries for phone-number pick-lists in patient, clinic, sign-up, receptionist and admin forms. On failure it returns 500 "Internal server error". (`Ashoka-World-Backend:routes/api.php:766`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:627`)
**Acceptance criteria**
- Given a failure, then 500 "Internal server error". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:627`)
**Source**: `Ashoka-World-Backend:routes/api.php:766`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:627`
**Screens**: AddPatientScreen, AddPatientFromAppointmentScreen, AddClinicScreen, EditClinicScreen (App); patient.add-member, patient.edit_member and 13 other web controllers (20 caller methods) (Web) · **API**: GET/POST getAllCountries

### PATIENTS-R13: Dashboard counts and banners
`getAssociationsCount` returns a count for the doctor dashboard (401 "Unauthorized" otherwise) and `patient/getBannerList` returns the banner and referral list (404 "Banner and referal list not found" when empty). (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5166`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3436`)
**Acceptance criteria**
- Given an unauthorized caller, then getAssociationsCount returns 401 "Unauthorized". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5166`)
- Given no banners, then getBannerList returns 404 "Banner and referal list not found". (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3436`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5166-5219`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3436-3454`, `Ashoka-World-Backend:routes/api.php:935`, `Ashoka-World-Backend:routes/api.php:1143`
**Screens**: DashboardScreen (App, getBannerList); doctor_dashboard.dashboard (Web) · **API**: POST getAssociationsCount, POST patient/getBannerList

### PATIENTS-R14: Web patient-list helpers
The web app adds routes under the patient list: `getPatient`, `callPatientList`, `scheduledAppointments`, `getMedicalId`, `getMedicalIdntlite`, `getLastVisitInformation`, `getLastVisitQuestions`, `getLastVisitMandatoryQuesitons`, `storePatient`, `setCurrentVisitSession`. Their upstream calls are `appointment/dateWiseAppointment`, `appointment/dateWisePatientAppointment`, `report/getNewMedicalId`, `v2/report/getNewMedicalId`, `v2/report/getLastVisitInformation`, `v2/report/getLastVisitMandatoryQuesitons`. (`Nadi-Tarangini-Frontend:routes/web.php:403-473`, `Nadi-Tarangini-Frontend:routes/web.php:639`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:166`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:220`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:442`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:626`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:661`)
**Acceptance criteria**
- Given a signed-out web user, then these routes sit behind `check_auth_token`. (`Nadi-Tarangini-Frontend:routes/web.php:403`)
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:403-473`
**Screens**: patient.patientlist (Web) · **API**: see section 6 (called backend endpoints belong to other modules)

## 5. Screens (web / mobile)

| Screen | Platform | File | Route / path | Purpose (provable) |
|---|---|---|---|---|
| AddPatientFromAppointmentScreen | App | `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/add_patient/add_patient_from_appointment_screen.dart` | none listed; goes to /addAppointmentScreen | Calls addClient / updateClient and country list (fact pack) |
| AddPatientScreen | App | `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/add_patient/add_patient_screen.dart` | /addPatientScreen | Calls addClient, addAnonymousClient, updateClient, getAllCountries |
| EditPatientScreen | App | `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/edit_patient/edit_patient_screen.dart` | /editPatientScreen | Calls getClientDetails, addClient, updateClient |
| PatientScreen | App | `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/patient_list/patient_screen.dart` | /patientScreen | Calls infinitePatientList, searchPatientUsingName, deletePatient, getClientDetails, v2 patientPreviousVisit |
| ViewPatientScreen | App | `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/view_patient/view_patient_screen.dart` | /viewPatientScreen | Calls getClientDetails |
| errors.410 | Web | `Nadi-Tarangini-Frontend:resources/views/errors/410.blade.php` | GET add-member | Rendered by AddMemberController@index |
| patient.add-member | Web | `Nadi-Tarangini-Frontend:resources/views/patient/add-member.blade.php` | GET add-member | Add member; goes to GET patientlist |
| patient.edit_member | Web | `Nadi-Tarangini-Frontend:resources/views/patient/edit_member.blade.php` | GET edit-member/{id} | Edit member; goes to GET patientlist |
| patient.patientlist | Web | `Nadi-Tarangini-Frontend:resources/views/patient/patientlist.blade.php` | GET patientlist | Patient list; goes to GET add-member |
| patient.previousVisits | Web | `Nadi-Tarangini-Frontend:resources/views/patient/previousVisits.blade.php` | GET previousVisits/{id} | Previous visits; goes to GET patientlist |
| patient.view_member | Web | `Nadi-Tarangini-Frontend:resources/views/patient/view_member.blade.php` | GET view-member/{id} | View member; goes to /edit-member/ and GET patientlist |

Sources for each row: `atreya-docs/_map/_modules/patients/facts.md` "Screens (11)" and the API-calls table.

## 6. APIs

All on `Ashoka-World-Backend`, routes in `Ashoka-World-Backend:routes/api.php` (line shown). "Called by" is from the fact pack call table; "none" means no caller in this workspace.

| Method | Endpoint | Controller | Auth | Called by |
|---|---|---|---|---|
| POST | accessUserWisePatientList (:933) | PatientDetailsController@accessUserWisePatientList | auth.token | App AddAppointmentScreen; Web appointment.add-appointment |
| GET | checkpatientcode (:996) | CheckUserExistOrNotController@checkPatientCode | auth.token | none |
| POST | fetchPatientNames (:931) | PatientDetailsController@fetchPatientNames | auth.token | App AddAppointmentScreen; Web appointment.add-appointment |
| GET, POST | getAllCountries (:766) | PatientDetailsController@getAllCountries | none (api only) | App (GET), Web (POST) many screens |
| POST | getAssociationsCount (:935) | PatientDetailsController@getAssociationsCount | auth.token | Web doctor_dashboard.dashboard |
| POST | getLanguage (:1423) | PatientDetailsController@fetchLanguageCode | none (api only) | none |
| POST | getLimitedActivePatients (:928) | PatientDetailsController@getLimitedActivePatients | auth.token | App DashboardScreen; Web doctor_dashboard.dashboard |
| POST | infinitePatientList (:927) | PatientDetailsController@infinitePatientList | auth.token | App PatientScreen, VisitReportListScreen; Web many |
| POST | patient/add-new-symptom (:1134) | PatientDetailsController@addNewSymptom | auth.token | none |
| POST | patient/addAnonymousClient (:1122) | PatientDetailsController@addAnonymousClient | auth.token | App AddPatientScreen; Web patient.add-member |
| POST | patient/addClient (:1145) | PatientDetailsController@addNewClient | auth.token | App add/edit patient screens; Web patient.add-member |
| POST | patient/clinicDetails (:1136) | PatientDetailsController@loadClinic | auth.token | none |
| POST | patient/deletePatient (:1120) | PatientDetailsController@deletePatient | auth.token | App PatientScreen; Web patient.patientlist |
| POST | patient/deletePatientQuery (:1140) | PatientDetailsController@deletePatientQuery | auth.token | none |
| POST | patient/deleteReport (:1118) | PatientDetailsController@deleteVisitReport | auth.token | App ReportScreen; Web PreviousVisitsController@deleteReport |
| POST | patient/getBannerList (:1143) | PatientDetailsController@getBannerList | auth.token | App getBannerList; Web doctor_dashboard.dashboard |
| POST | patient/getClientDetails (:1126) | PatientDetailsController@getClientDetails | auth.token | App PatientScreen, ViewPatientScreen, EditPatientScreen; Web view/edit member |
| POST | patient/getTopicsList (:1144) | PatientDetailsController@getTopicsList | auth.token | none |
| POST | patient/patientAppointmentInfo (:1142) | PatientDetailsController@patientAppointmentInfo | auth.token | none |
| POST | patient/patientPreviousVisit (:1114) | PatientDetailsController@patientPreviousVisit | auth.token | none |
| POST | patient/patientPreviousVisit-2 (:1128) | PatientDetailsController@patientPreviousVisit2 | auth.token | none |
| POST | patient/patientProgress (:1146) | PatientDetailsController@patientProgress | auth.token | none |
| POST | patient/previousVisitsDetails (:1116) | PatientDetailsController@previousVisitsDetails | auth.token | App fetchSymptomHistory; Web VikrutiController@getSymptomHistory |
| POST | patient/remainingFees (:1130) | PatientDetailsController@remainingFees | auth.token | none |
| POST | patient/saveFees (:1131) | PatientDetailsController@saveFees | auth.token | App MainAssessmentScreen; Web Diet/FeeDetails controllers |
| POST | patient/showPatientQueries (:1137) | PatientDetailsController@showPatientQueries | auth.token | none |
| POST | patient/updateClient (:1123) | PatientDetailsController@updateClient | auth.token | App add/edit patient screens; Web patient.edit_member |
| POST | patient/updatePatientQueries (:1138) | PatientDetailsController@updateQueries | auth.token | none |
| POST | patientList (:926) | PatientDetailsController@getPatientList | auth.token | none |
| POST | searchPatientUsingName (:929) | PatientDetailsController@searchPatientUsingName | auth.token | App PatientScreen; Web patient.patientlist and others |
| POST | v2/patient/patientPreviousVisit (:1647) | PatientDetailsController@patientPreviousVisitV2 | auth.token | App PatientScreen, VisitReportListScreen; Web patient.previousVisits and others |

Web routes (all `Nadi-Tarangini-Frontend:routes/web.php`, middleware `check_auth_token`, `fetch_notifications`, `ensure_normal_dashboard_mode`): GET add-member (:434), POST callPatientList (:403), DELETE deletePatient/{id} (:430), DELETE deleteReport/{medicalId}/{patientId} (:432), GET edit-member/{id} (:440), POST getLastVisitInformation (:473), POST getLastVisitMandatoryQuesitons (:472), POST getLastVisitQuestions (:471), POST getMedicalId (:460), POST getMedicalIdntlite (:462), GET getPatient (:419), GET patientlist (:402), GET previousVisits/{id} (:425), POST resumeVisit (:426), POST saveAnonymousData (:438), POST saveMemberData (:436), POST scheduledAppointments (:639), GET search-patients (:404), POST setCurrentVisitSession (:427), POST storePatient (:407), POST updatetMemberData (:442), GET view-member/{id} (:444).

## 7. Data model

Tables reported by the fact pack for this module, with the columns it found in migrations. Source: `atreya-docs/_map/_modules/patients/facts.md` "Tables (16)".

| Table (model) | Key fields from migrations |
|---|---|
| banners_data (BannersData) | accessibility, mobile_url |
| calendar_events (CalendarEvent) | clinic_id, consultation_type, reception_id |
| doctor_form_details (DoctorFormDetail) | columns not in migrations |
| languages (Languages) | columns not in migrations |
| locality_info (LocalityInfo) | is_default, timezone |
| medical_report (MedicalReport) | city, country, external_visit_id, field_id_1, ip_address, mark_on_image_url, panchakarma_recom, reception_id, recommendations, state, try_count, user_nadi_capture_type, yoga_recom |
| medical_report_diet (MedicalReportDiet) | create_date, diet, doctor_id, id, is_active, last_modified_on, medical_id, patient_id, vikruti_type |
| medical_report_file_upload (MedicalReportFileUpload) | columns not in migrations |
| medical_report_prescription (MedicalReportPrescription) | is_active, other_details, total_quantity |
| medical_report_symptom_details_1 (MedicalReportSymptomDetail) | symptom_value |
| nadi_report (NadiReport) | columns not in migrations |
| notification_topics (NotificationTopic) | columns not in migrations |
| other_report_data (OtherReportData) | create_date, id, is_active, last_modified_on, medical_id, report_data, sub_title, title |
| patient_question_answer (PatientQuestionAnswer) | delete_by_doctor, delete_by_patient, is_active |
| symptoms (Symptoms) | is_active |
| user_personal_info (UserPersonalInfo) | allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken |

Patient delete writes `delete_by_doctor` and `last_modified_on` on `user_personal_info` where `role_id` is '2'. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4781-4785`) Tables with "columns not in migrations" are asked about in section 13.

## 8. Validations & error handling

| API | Field / case | Rule or message | HTTP | Source |
|---|---|---|---|---|
| patient/addClient | firstname, lastname | required, letters and spaces only | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:83`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:85` |
| patient/addClient | middlename | nullable, letters and spaces only | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:84` |
| patient/addClient | gender | required, one of M,F,D,N | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:86` |
| patient/addClient | nadi_consent, report_consent, share_report_consent | required, 0 or 1 | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:87-89` |
| patient/addClient | dateofbirth | nullable, Y-m-d, not after today | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:90` |
| patient/addClient | profile_picture | image jpeg,png,jpg | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:397` |
| patient/addClient | country code vs phone | "The provided country code is not valid for the given phone number" | not stated | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:104` |
| patient/addClient | future date of birth | "Date of birth cannot be a future date" | not stated | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:134` |
| patient/addClient | phone format | "Invalid phone number format" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:182` |
| patient/addClient, addAnonymousClient | date of birth | "Invalid date of birth" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:198`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:740` |
| patient/addClient, addAnonymousClient | date of birth range | "Date of birth must be between 1 and 100 years old" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:206`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:743` |
| patient/addClient, addAnonymousClient | age | "Invalid age" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:218`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:750` |
| patient/addClient, addAnonymousClient | neither dob nor age | "Date of birth or age is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:227`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:754` |
| patient/addAnonymousClient | user id, client code, gender | "User id is not provided" / "Client code is required" / "Gender is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:658`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:661`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:664` |
| patient/addAnonymousClient | consent flags | required, integer, 0 or 1 | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:671-673` |
| patient/addAnonymousClient | email | "Invalid email format" | not stated | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:723` |
| patient/updateClient | client id | "Client id is required" / "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1030`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1034` |
| patient/updateClient | unknown client | "Client not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1046` |
| patient/updateClient | anonymous patient | "Anonymous patient cannot be edited" | 404 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1054` |
| patient/updateClient | phone | "Phone number is required" / "Invalid phone number format" | not stated | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1103`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1149` |
| patient/getClientDetails | user id, client id | "User id is not provided" / "Client id is required" / "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:896`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:899`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:902` |
| patient/getClientDetails | not found | "Client not found" / "Details not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:924`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1009` |
| patient/deletePatient | patient_id | required, numeric | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4744` |
| patient/deletePatient | unknown patient | "Invalid patient id" / "Patient not found or not deleted" | 404 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4778`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4792` |
| patient/deleteReport | ids | "Patient id is required" / "Invalid patient id" / "Medical id is required" / "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4966-4977` |
| patient/deleteReport | not found | "Invalid patient id" / "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4987`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4998` |
| patient/saveFees | fee fields | fee_charged, fee_paid, consultation_fees, therapy_fees nullable integer | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2475-2478` |
| patient/saveFees | doctor_remarks | required | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2479` |
| patient/saveFees | share_report_ids.* | one of 1,2,3,4,7,8,9 | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2484` |
| patient/saveFees | next_appointment_date | Y-m-d, on or after tomorrow | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2487` |
| patient/saveFees | starttime / endtime | H:i; endtime after starttime | validation | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2488-2489` |
| patient/saveFees | date missing | "Next appointment date is mandatory" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2543` |
| patient/saveFees | ids | "Medical id is required" / "Client id is required" / "Invalid medical id" / "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2459-2469` |
| patient/saveFees | not found | "Enter valid medical id" / "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2527`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2532` |
| infinitePatientList, getLimitedActivePatients, searchPatientUsingName, patientList | user id | "User id is not provided." | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3725`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4019`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4311`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3496` |
| accessUserWisePatientList | user id | "Invalid user id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4662` |
| getAssociationsCount | auth | "Unauthorized" | 401 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5166` |
| v2/patient/patientPreviousVisit | not found | "Invalid patient id" / "Visit list not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1792`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1999` |
| patient/previousVisitsDetails | not found | "Invalid patient id" / "Visit list not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5056`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5144` |
| checkpatientcode | patient_code, doctor_id | required string; required integer | validation | `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:88-89` |
| all listed routes | server error | "Internal server error" | 500 (where stated) | `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:627`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4007`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4300`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4603`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4647`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4702`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4798`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5013`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5152`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5219`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2006` |

## 9. Non-functional

- **Security.** Patient routes use `auth.token` except `getAllCountries` and `getLanguage`; web routes use `check_auth_token`. (`Ashoka-World-Backend:routes/api.php:766`, `Ashoka-World-Backend:routes/api.php:1423`, `Nadi-Tarangini-Frontend:routes/web.php:402`)
- **Languages.** Required: English, Marathi, Hindi, Czech, German, Spanish, Italian (`references/qa-scope-rules.md`). Language files found in code: `Nadi-Tarangini-Frontend:resources/lang/en/auth.php`, `en/pagination.php`, `en/passwords.php`, `en/validation.php`, `Nadi-Tarangini-Frontend:resources/lang/en_patient.json`; only English was found. A `languages` table and a `getLanguage` route exist. (`atreya-docs/_map/_modules/patients/facts.md`)
- **Performance.** `infinitePatientList` and `getLimitedActivePatients` are named as infinite-scroll and limited lists; no timeouts or limits were checked. Not otherwise stated.

## 10. Environment matrix

Copied verbatim from `atreya-docs/environments.md` (status TO FILL).

### Ashoka-World-Backend

| Env | Ref | Host | Feature flags | Integration mode |
|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL |

### Nadi-Tarangini-Frontend

| Env | Ref | Host | Feature flags | Integration mode |
|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL |

### Nadi-Tarangini-App

| Env | Ref | Build flavor | Host | Feature flags | Integration mode |
|---|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |

## 11. Staging delta

See [staging-delta.md](staging-delta.md). Status: not computed; all three repos are skipped, "waiting for environments.md" (staging and production refs are TO FILL). (`atreya-docs/nt/patients/staging-delta.md`)

## 12. External integrations

- **Firebase** is used from PatientDetailsController at lines 576, 838 and 3011. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:576`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:838`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3011`)
- **S3** is used from PatientDetailsController at lines 381, 412 and 422. (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:381`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:412`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:422`)
What each is used for is in section 13.

## 13. Open questions

1. (Dev) What do Firebase (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:576`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:838`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3011`) and S3 (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:381`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:412`, `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:422`) do in the patient flows (for example profile picture storage, notifications)?
2. (PO) Which roles (doctor, receptionist, admin, patient) may use each patient route? The fact pack shows only `auth.token`, not role checks, apart from `role_id` '2' on delete (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4783`).
3. (PO) The 14 backend routes with no caller (`checkpatientcode`, `getLanguage`, `patient/add-new-symptom`, `patient/clinicDetails`, `patient/deletePatientQuery`, `patient/getTopicsList`, `patient/patientAppointmentInfo`, `patient/patientPreviousVisit`, `patient/patientPreviousVisit-2`, `patient/patientProgress`, `patient/remainingFees`, `patient/showPatientQueries`, `patient/updatePatientQueries`, `patientList`): are they in use by any other client (for example patient app) or retired?
4. (Dev) Why are the tables `doctor_form_details`, `languages`, `medical_report_file_upload`, `nadi_report` and `notification_topics` reported "columns not in migrations"? Where is their schema defined?
5. (PO) Which languages must the patient forms and messages support? Only English language files were found for this module.
6. (Dev) The response HTTP status is not shown (fact pack "?") for several messages, for example "Invalid email format" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:723`), "Date of birth cannot be a future date" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:134`) and the country-code message (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:104`). What status do they return?
7. (PO) What is the intended behaviour of delete patient for the patient's visit history and reports: is a soft-deleted patient still shown in reports or lists of other users?
8. (PO) Is the rule "date of birth between 1 and 100 years old" intended to exclude infants under 1 year?
9. (PO) Environments (hosts, refs, feature flags) are TO FILL in `environments.md`; who will fill them so the staging delta can be computed?
10. (Dev) Which web and mobile flows apply `getAssociationsCount` (what is counted)? The fact pack lists only the dashboard as caller.

11. (Dev) The same controller methods (`patientList`, `infinitePatientList`, `getLimitedActivePatients`, `searchPatientUsingName`, `patient/addClient`, `addAnonymousClient`, `updateClient`, `getClientDetails`, `fetchPatientNames`) are also registered under `reception-api` with `reception.authentication`. Should the receptionist routes be part of this module's scope and PRD?
12. (Dev) `patient/addClient` also requires `mobile_no` and `country_code` (required with `mobile_no`) (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:95-101`); confirm the full phone rules, which this PRD only partly describes.

13. (Dev) The paging behaviour of `infinitePatientList`, what `saveFees` stores for uploaded files and yoga/panchakarma recommendations, and what `getAssociationsCount` counts are described only by route name or validation rules; please confirm or point to the logic. Mobile screen purposes come from the fact pack and were not checked in the Dart files.

## 14. Diagrams

None yet: run /atreya:diagram patients.

## 15. Document control

| Field | Value |
|---|---|
| Status | Draft |
| Date | 2026-11-03 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend 8dfbb37db7d71a400b3656bd50fbed6173908a24; Nadi-Tarangini-Frontend e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d; Nadi-Tarangini-App 0b7deec6de2b0b8b4f05eab4be8c8430523829bf |
