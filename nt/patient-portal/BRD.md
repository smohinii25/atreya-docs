---
module: "patient-portal"
doc: "BRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Patient portal (client login, reports, questions, consent): Business Requirements Document

## 1. Purpose & overview

The patient portal lets a signed-in patient use the product on the website and in the mobile app. Patients can see their dashboard, update their profile, look at past visits and reports, manage their data consent, change their password in the app, and delete their account. A "ask a question" feature exists in the system but is not reachable from any screen in the web code checked; the app was not verified (see section 12). Source: PRD patient-portal Overview; `Nadi-Tarangini-Frontend:routes/web.php:780`.

## 2. Business objectives

Not stated in code. See section 11 and 12 (TO CONFIRM by the product owner).

## 3. Stakeholders & user roles

| Role | How they use it | Source |
|---|---|---|
| Patient (client) | Signs in and uses the capabilities in this module | `Ashoka-World-Backend:routes/api.php:1446`; PATIENT-PORTAL-R01 |
| Corporate patient | Has a separate corporate dashboard that shows visits and details | `Nadi-Tarangini-Frontend:app/Http/Controllers/Corporate/PatientDashboardManagementController.php:38`; PATIENT-PORTAL-R13 |
| Doctor / clinic staff | Answer patient questions (inferred from a field "delete by doctor" in the question table; to confirm) | PATIENT-PORTAL-R11 |

## 4. Scope

### In scope
- Finding the patient's details at sign-in (PATIENT-PORTAL-R01)
- Patient dashboard (R02)
- Viewing and editing the profile (R03)
- Changing the password, app only (R04)
- Visit history and remaining fees (R05)
- Viewing reports of a visit (R06) and deleting a report (R07)
- Viewing and changing data consent (R08)
- Deleting the account (R09)
- Daily diet and lifestyle view (R10)
- Corporate patient dashboard (R13)

### Out of scope
- Ask-a-question feature: the four server functions have no caller in the web or app per the fact pack, and the web page calls services that do not exist on the server (`Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:320`, `:357`; `Ashoka-World-Backend:routes/api.php:1451-1452`). Treated as a question, not a live feature (PATIENT-PORTAL-R11; section 12).
- Appointment request page: only the page exists; the fact pack shows no data service for it (R12, `Nadi-Tarangini-Frontend:routes/web.php:783`).
- Doctor-side report functions and the diet/lifestyle data service, which belong to other modules.

## 5. Current business process (as-is)

1. The patient signs in; the system looks up the patient's details (R01).
2. The patient lands on a dashboard showing details, Nadi parameters, banners and help videos (R02).
3. From the visit list the patient opens the reports of a visit, and can delete a report (R05, R06, R07).
4. The patient may edit the profile, including a picture and phone number (R03).
5. The patient may review and change three consents (R08).
6. The patient may delete the account (R09).
Source: PRD §3 User journeys.

## 6. Business rules

| Rule | Source |
|---|---|
| A new password must contain at least one digit and must differ from the old one. | `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:294`, `:321` |
| To change the password, the current password must be entered and be correct. | `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:286`, `:328` |
| When a patient changes their phone number, it cannot be one already used by another patient of the same doctor. | `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:68-79` |
| The phone number length and country code must be valid. | `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:140`, `:143` |
| A profile picture cannot be larger than 1 MB. | `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:93` (see PRD check) |
| Three consents (Nadi, report, share report) must each be answered yes or no. | `Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:52` |
| Opening or deleting a report needs a valid visit (medical) identifier. | `Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:139`, `:176` |
| An answered question can no longer be edited. | `Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:130` |
| A question cannot be empty. | `Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:33` |

## 7. Business requirements

| ID | Requirement | Source |
|---|---|---|
| BR-01 | The system finds a patient's details when they sign in on web or app, and refuses an unknown client identifier (the unknown-username refusal is in PATIENT-PORTAL-R01). | PATIENT-PORTAL-R01; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:713` |
| BR-02 | A patient sees a dashboard with their details, Nadi parameters and banners. | PATIENT-PORTAL-R02; `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:29` |
| BR-03 | A patient can view and edit their profile, including picture and phone number, under the rules in section 6. | PATIENT-PORTAL-R03; `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:34` |
| BR-04 | A patient can change their password in the app. | PATIENT-PORTAL-R04; `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:286` |
| BR-05 | A patient can see past visits that were shared with them (web and app) and, on the web, the fees remaining. | PATIENT-PORTAL-R05; `Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:20-84` |
| BR-06 | A patient can open the reports of a visit (visit report, prescription, Swasthya Darshika). | PATIENT-PORTAL-R06; `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:581` |
| BR-07 | A patient can delete a report from their visit list. | PATIENT-PORTAL-R07; `Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:159` |
| BR-08 | A patient can view and change their data consents. | PATIENT-PORTAL-R08; `Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:86` |
| BR-09 | A patient can delete their own account. | PATIENT-PORTAL-R09; `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:45` |
| BR-10 | A patient can view daily diet and lifestyle guidance. | PATIENT-PORTAL-R10; `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:642` |
| BR-11 | A corporate patient sees a corporate dashboard with visits and details. | PATIENT-PORTAL-R13; `Nadi-Tarangini-Frontend:app/Http/Controllers/Corporate/PatientDashboardManagementController.php:22` |

Ask-a-question (R11) and appointment request (R12) have no BR until confirmed (section 12).

## 8. Availability by environment

All environment details are TO FILL in `environments.md` for the backend, web and app (dev, staging, production). Staging versus production differences have not been computed. Source: `atreya-docs/environments.md`; PRD §10, §11.

## 9. Dependencies & external systems

- Cloud file storage (S3) holds profile pictures. Source: `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:84`.
- Shared services used by the web patient pages: help videos, country list, diet data, and report generation. Source: `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:126`, `:154`, `:642`, `:613`.

## 10. Assumptions & constraints

- Only English language files were found in the web code, while seven languages are required. Source: `references/qa-scope-rules.md`; `Nadi-Tarangini-Frontend:resources/lang/en_patient.json`.
- Password change exists only in the app. Source: `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2601`.

## 11. Success measures (TO CONFIRM)

- How will the product owner judge that patients use the portal successfully (for example logins, report views, consents given)?
- Is there a target for consent completion or report access?

## 12. Needs confirmation

1. (Product owner) What are the business objectives and success measures of the patient portal?
2. (Product owner) Is the ask-a-question feature live, planned or retired? Its server functions have no screen, and the web page calls missing services.
3. (Product owner) Is the appointment request page meant to do anything beyond showing a page?
4. (Product owner) What do the "Coming soon" and "Contact" app screens show?
5. (Product owner) Is the corporate patient dashboard part of this module?
6. (Product owner) Should patients be able to change their password on the web too?
7. (Product owner) What happens to a patient's data and reports after account deletion?
8. (Product owner) How are the seven required languages to be delivered for the patient pages?
9. (Ops) Please fill in `environments.md` so availability and staging differences can be stated.
10. (Product owner) Which clinic staff answer patient questions?

## 13. Document control

- Status: Draft
- Date: 2026-11-03
- Reviewer: TBD
- Commits: Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`; Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`; Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d`
