---
module: "patient-portal"
doc: "PRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Patient portal (client login, reports, questions, consent): Product Requirements Document

## 1. Overview

The patient portal is the set of client-facing (patient) capabilities served by the `client/*` API group in the backend (17 routes in this module, all behind the `client.authentication` middleware) (`Ashoka-World-Backend:routes/api.php:1447`). The web side exposes 15 `patient/*` routes protected by `check_client_auth_token` (`Nadi-Tarangini-Frontend:routes/web.php:780`). The mobile app has patient screens under `lib/patient_module/view/` (10 files; 7 are listed in the fact pack, see §13) (`Nadi-Tarangini-App:lib/patient_module/view/report_screen.dart`). Capabilities covered: patient login lookup, dashboard, profile edit, password change, visit history and reports, data consent, account deletion, diet/lifestyle view, and a question ("ask queries") feature (`Nadi-Tarangini-Frontend:routes/web.php:784`).

## 2. Users, roles & permissions

- Patient / client: every `client/*` route in this module except `v2/client/getClientDetails` carries middleware `api, client.authentication` (`Ashoka-World-Backend:routes/api.php:1451`). `GET v2/client/getClientDetails` carries only `client.authentication` (`Ashoka-World-Backend:routes/api.php:1674`).
- Web: all 15 `patient/*` routes carry `check_client_auth_token` (`Nadi-Tarangini-Frontend:routes/web.php:780`).
- The fact pack lists a corporate patient dashboard (`corporate-patient-module.dashboard`) calling `client/clientDetails` and `client/getPreviousVisits` (`Nadi-Tarangini-Frontend:app/Http/Controllers/Corporate/PatientDashboardManagementController.php:38`). Its web route is `GET corporate/patientDashboard` with middleware `corporate_patient_check_auth` inside the `check_client_auth_token` group (`Nadi-Tarangini-Frontend:routes/web.php:804`).
- Role data (`verified_role_id`, `corp_role_id`) exists in tables `user_personal_info` and `corporate_info` (see §7); how roles gate behaviour is not shown in the fact pack (see §13).

## 3. User journeys

**Web**
1. Patient logs in; the login controller calls `GET v2/client/getClientDetails` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:94`).
2. `GET patient/dashboard` loads client details, Nadi parameters, banners and help videos (`Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:29`, `:54`, `:103`, `:126`).
3. `GET patient/visits` loads previous visits, client details and remaining fees (`Nadi-Tarangini-Frontend:app/Http/Controllers/PatientVisitController.php:21`, `:37`, `:63`).
4. From visits, the patient opens reports through `POST patient/report/viewAllReports`, `viewVisitReport` or `viewSwasthyaDarshika`; these views go back to `GET patient/visits` (`Nadi-Tarangini-Frontend:routes/web.php:798`).
5. `GET patient/edit` then `POST patient/updateProfileData` edits the profile (`Nadi-Tarangini-Frontend:routes/web.php:787`).
6. `GET patient/data-consent` then `POST patient/updateConsentData` changes consents (`Nadi-Tarangini-Frontend:routes/web.php:790`).
7. `POST patient/delete-account` deletes the account (`Nadi-Tarangini-Frontend:routes/web.php:793`).

**Mobile app**
1. Login screen calls `getPatientData` (`GET /v2/client/getClientDetails`) (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:376`).
2. Dashboard/drawer call `client/clientDetails` and `client/getNadiParametersData` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2548`, `:2558`).
3. ReportScreen lists previous visits; AllReportScreen lists a visit's reports (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2622`, `:2671`).
4. EditPatientProfileScreen goes to `/drawerMenuPatient` (`Nadi-Tarangini-App:lib/patient_module/view/edit_patient_profile_screen.dart`); UpdateDataConsentScreen goes to `/drawerMenuPatient` (`Nadi-Tarangini-App:lib/patient_module/view/update_data_consent_screen.dart`); DietScreen goes to `/patientDashboard` (`Nadi-Tarangini-App:lib/patient_module/view/diet_screen.dart`).

## 4. Functional requirements

### PATIENT-PORTAL-R01: Look up client details at login
`GET v2/client/getClientDetails` returns 400 "Invalid client id", 401 "Invalid username" or 500 "Internal server error" on failure (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:713`, `:757`, `:789`). The web login (`loginController@checkLoginCredentials`) and the app login screen (`LoginWithUsernameScreen`) call it.
**Acceptance criteria**
- Given an invalid client id when the API is called then it returns 400 "Invalid client id".
- Given an invalid username then it returns 401 "Invalid username".
**Source**: `Ashoka-World-Backend:routes/api.php:1674`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:713`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:94`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:376`
**Screens**: LoginWithUsernameScreen (App), auth.login (Web) · **API**: GET v2/client/getClientDetails

### PATIENT-PORTAL-R02: Patient dashboard
The web dashboard loads client details, Nadi parameters, banners and help videos; the app dashboard loads client details and Nadi parameters. `getNadiParametersData` returns 200 "Success" or 500 "Internal server error"; `getBannerList` returns "Success" or 500.
**Acceptance criteria**
- Given a signed-in patient when `GET patient/dashboard` is opened then the controller calls `client/clientDetails`, `client/getNadiParametersData`, `client/getBannerList` and `getNtHelpVideos`.
**Source**: `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:29`, `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:227`, `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:268`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2558`
**Screens**: patient-module.patient_dashboard (Web), PatientDashboard (App) · **API**: POST client/clientDetails, POST client/getNadiParametersData, POST client/getBannerList

### PATIENT-PORTAL-R03: View and edit profile
`client/clientEditProfile` validates and updates the profile. Error cases: 400 "Invalid client id", 400 "Phone number already exists", 400 "Image shouldn't be greater than 1 MB", 500 "An error occurred while uploading the file", 400 "Invalid phone number length1", 400 "The provided country code is not valid for the given phone number2"; success is 200 "Client profile updated successfully"; otherwise 400 "Client profile not updated". Profile image upload uses S3.
**Acceptance criteria**
- Given a phone number already used when the profile is saved then 400 "Phone number already exists".
- Given a phone number whose length or country code is invalid then 400 with the messages above.
- Given a successful update then 200 "Client profile updated successfully".
**Source**: `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:34`, `:78`, `:93`, `:107`, `:140`, `:143`, `:174`, `:177`; S3 use at `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:84`
**Screens**: patient-module.edit_profile (Web), EditPatientProfileScreen (App) · **API**: POST client/clientEditProfile, POST client/clientDetails, POST getAllCountries (Web)

### PATIENT-PORTAL-R04: Change password (app)
`client/changePassword` requires `current_password`; the new password must contain at least one digit and differ from the old one; wrong current password returns 400 "Incorrect current password".
**Acceptance criteria**
- Given a missing `current_password` then validation fails (rule: required).
- Given a new password without a digit then message "New password must contain at least one digit" (validation failures return 400, `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:303`).
- Given a new password equal to the old one then 400 "New password must be different from the old password.".
- Given a correct change then 200 "Password updated successfully".
**Source**: `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:286`, `:294`, `:317`, `:321`, `:326`, `:328`; called by `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2601`
**Screens**: ChangePasswordPatient (App) · **API**: POST client/changePassword

### PATIENT-PORTAL-R05: Visit history and remaining fees
`client/getPreviousVisits` returns 200 "Success" or 500; `client/clientRemainingFees` returns 404 "Client not found" or 500. The web visit page calls both plus `clientDetails`.
**Acceptance criteria**
- Given an unknown client when `clientRemainingFees` is called then 404 "Client not found".
**Source**: `Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:82`, `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:263`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientVisitController.php:21`
**Screens**: patient-module.visit_history (Web), ReportScreen (App) · **API**: POST client/getPreviousVisits, POST client/clientRemainingFees

### PATIENT-PORTAL-R06: View reports of a visit
`client/visitWiseReports` requires a medical id: 400 "Medical id is required", 400 "Invalid medical id", 404 "Enter valid medical id". Web view routes then fetch `medicalVisitReportV2`, `prescriptionReport` and `swasthyaDarshikaReport`.
**Acceptance criteria**
- Given no medical id then 400 "Medical id is required".
- Given an invalid medical id then 400 "Invalid medical id"; given one with no match then 404 "Enter valid medical id".
**Source**: `Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:176`, `:180`, `:188`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:581`, `:613`, `:526`, `:545`
**Screens**: patient-module.patientAllReportsView, patientVisitReportView, patientSwasthyaDarshikaView, patientArogyaDarshikaView (Web), AllReportScreen (App) · **API**: POST client/visitWiseReports

### PATIENT-PORTAL-R07: Delete a report
`client/deleteReport` requires a medical id and returns 200 "Report deleted successfully".
**Acceptance criteria**
- Given no medical id then 400 "Medical id is required"; invalid then 400 "Invalid medical id"; no match then 404 "Enter valid medical id".
**Source**: `Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:139`, `:143`, `:151`, `:159`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientVisitController.php:120`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2656`
**Screens**: ReportScreen (App), Web route `DELETE patient/deletePatientReport/{id}` · **API**: POST client/deleteReport

### PATIENT-PORTAL-R08: View and update data consent
`client/updateDataConsent` requires `nadi_consent`, `report_consent`, `share_report_consent`, each matching `^[01]$`. Responses: 404 "User not found", 200 "Data updated successfully".
**Acceptance criteria**
- Given any of the three fields missing or not 0/1 then validation fails.
- Given an unknown user then 404 "User not found".
- Given success then 200 "Data updated successfully".
**Source**: `Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:52`, `:53`, `:54`, `:77`, `:86`; `getDataConsent`: `Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:25`
**Screens**: patient-module.data_consent (Web), UpdateDataConsentScreen (App) · **API**: POST client/getDataConsent, POST client/updateDataConsent

### PATIENT-PORTAL-R09: Delete patient account
`client/deleteClientAccount` returns 401 "Unauthorized", 200 "Success" or 500.
**Acceptance criteria**
- Given an unauthorized caller then 401 "Unauthorized".
- Given success then 200 "Success".
**Source**: `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:34`, `:45`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2591`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:479`
**Screens**: DrawerMenuPatient (App), my_account.myaccount, patient-module.daily_diet_lifestyle, data_consent, edit_profile (Web) · **API**: POST client/deleteClientAccount

### PATIENT-PORTAL-R10: Daily diet and lifestyle
The web page `patient/daily-diet-lifestyle/{parameterName}` and the app call `POST client/turyaa/homeData`. That endpoint matched a route outside this module's route list.
**Acceptance criteria**
- Given the page is opened then the controller calls `client/turyaa/homeData`.
**Source**: `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:642`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2574`
**Screens**: patient-module.daily_diet_lifestyle (Web), DietScreen (App) · **API**: POST client/turyaa/homeData

### PATIENT-PORTAL-R11: Ask queries (questions to the doctor)
Backend has `askQuery`, `fetchAskedQueriesList`, `updateQuery`, `deleteQuery`; no screen calls them. The web `askQueries` and `SaveQueries` instead call `/client/askQuestionList` and `/client/askQuestion`, for which no backend route was found. Backend rules: "Query is required"; "This query is already answered" blocks update.
**Acceptance criteria**
- Given `askQuery` without query then 400 "Query is required".
- Given `updateQuery` on an answered query then 400 "This query is already answered".
- Given `deleteQuery` without id then 400 "Query id is required".
**Source**: `Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:33`, `:109`, `:130`, `:161`, `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:320`, `:357`
**Screens**: patient-module.ask_queries (Web) · **API**: POST client/askQuery, fetchAskedQueriesList, updateQuery, deleteQuery (no screen calls)

### PATIENT-PORTAL-R12: Request appointment page
`GET patient/request-appointment` renders `patient-module.request_appointment` via `RequestAppointmentController@requestAppointment`. The fact pack shows no API call for it.
**Acceptance criteria**
- Given a signed-in patient when the route is opened then the view is rendered.
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:783`, `Nadi-Tarangini-Frontend:resources/views/patient-module/request_appointment.blade.php`
**Screens**: patient-module.request_appointment (Web) · **API**: none found

### PATIENT-PORTAL-R13: Corporate patient dashboard
The controller `PatientDashboardManagementController@corporatePatientDashboard` calls `client/getPreviousVisits` and `client/clientDetails`.
**Acceptance criteria**
- Given the corporate dashboard is opened then both APIs are called.
**Source**: `Nadi-Tarangini-Frontend:app/Http/Controllers/Corporate/PatientDashboardManagementController.php:22`, `:38`
**Screens**: corporate-patient-module.dashboard (Web) · **API**: POST client/getPreviousVisits, POST client/clientDetails

## 5. Screens (web / mobile)

| Screen | Platform | File | Route / path | Purpose (provable) |
|---|---|---|---|---|
| AllReportScreen | App | `Nadi-Tarangini-App:lib/patient_module/view/all_report_screen.dart` | - | Calls visitWiseReports (R06) |
| ComingSoonPage | App | `Nadi-Tarangini-App:lib/patient_module/view/comming_soon_page.dart` | - | Not provable (see §13) |
| ContactScreen | App | `Nadi-Tarangini-App:lib/patient_module/view/contact_screen.dart` | - | Not provable (see §13) |
| DietScreen | App | `Nadi-Tarangini-App:lib/patient_module/view/diet_screen.dart` | /dietScreen, goes to /patientDashboard | Diet (R10) |
| EditPatientProfileScreen | App | `Nadi-Tarangini-App:lib/patient_module/view/edit_patient_profile_screen.dart` | /editPatientProfile, goes to /drawerMenuPatient | Edit profile (R03) |
| ReportScreen | App | `Nadi-Tarangini-App:lib/patient_module/view/report_screen.dart` | /reportScreenPatient | Visits, delete report (R05, R07) |
| UpdateDataConsentScreen | App | `Nadi-Tarangini-App:lib/patient_module/view/update_data_consent_screen.dart` | /updateDataConsentScreen, goes to /drawerMenuPatient | Consent (R08) |
| patient-module.ask_queries | Web | `Nadi-Tarangini-Frontend:resources/views/patient-module/ask_queries.blade.php` | GET patient/ask-queries | Ask queries (R11) |
| patient-module.daily_diet_lifestyle | Web | `Nadi-Tarangini-Frontend:resources/views/patient-module/daily_diet_lifestyle.blade.php` | GET patient/daily-diet-lifestyle/{parameterName} | R10 |
| patient-module.data_consent | Web | `Nadi-Tarangini-Frontend:resources/views/patient-module/data_consent.blade.php` | GET patient/data-consent | R08 |
| patient-module.edit_profile | Web | `Nadi-Tarangini-Frontend:resources/views/patient-module/edit_profile.blade.php` | GET patient/edit | R03 |
| patient-module.patientAllReportsView | Web | `Nadi-Tarangini-Frontend:resources/views/patient-module/patientAllReportsView.blade.php` | POST patient/report/viewAllReports, goes to GET patient/visits | R06 |
| patient-module.patientArogyaDarshikaView | Web | `Nadi-Tarangini-Frontend:resources/views/patient-module/patientArogyaDarshikaView.blade.php` | no route in fact pack; rendered by PatientDashboardController@patientViewArogyaDarshika | R06 (see §13) |
| patient-module.patientSwasthyaDarshikaView | Web | `Nadi-Tarangini-Frontend:resources/views/patient-module/patientSwasthyaDarshikaView.blade.php` | POST patient/report/viewSwasthyaDarshika | R06 |
| patient-module.patientVisitReportView | Web | `Nadi-Tarangini-Frontend:resources/views/patient-module/patientVisitReportView.blade.php` | POST patient/report/viewVisitReport | R06 |
| patient-module.patient_dashboard | Web | `Nadi-Tarangini-Frontend:resources/views/patient-module/patient_dashboard.blade.php` | GET patient/dashboard | R02 |
| patient-module.request_appointment | Web | `Nadi-Tarangini-Frontend:resources/views/patient-module/request_appointment.blade.php` | GET patient/request-appointment | R12 |
| patient-module.visit_history | Web | `Nadi-Tarangini-Frontend:resources/views/patient-module/visit_history.blade.php` | GET patient/visits | R05 |

## 6. APIs

| Method | Endpoint | Controller | Auth (middleware) | Called by |
|---|---|---|---|---|
| POST | client/askQuery | AskQuestionController@askQuestion | api, client.authentication | no screen |
| POST | client/changePassword | AccountManagementController@changePassword | api, client.authentication | App updatePasswordPatient |
| POST | client/clientDetails | EditProfileController@clientDetails | api, client.authentication | App; Web dashboard, edit, visits, corporate |
| POST | client/clientEditProfile | EditProfileController@clientEditProfile | api, client.authentication | App; Web updateProfileData |
| POST | client/clientRemainingFees | EditProfileController@clientRemainingFees | api, client.authentication | Web visitHistory |
| POST | client/deleteClientAccount | AccountManagementController@deleteClientAccount | api, client.authentication | App; Web |
| POST | client/deleteQuery | AskQuestionController@deleteQuestion | api, client.authentication | no screen |
| POST | client/deleteReport | VisitManagementController@deleteReport | api, client.authentication | App; Web |
| POST | client/fetchAskedQueriesList | AskQuestionController@askQuestionList | api, client.authentication | no screen |
| POST | client/getBannerList | AccountManagementController@getBannerList | api, client.authentication | Web dashboard (app use not proven, see §13) |
| POST | client/getDataConsent | DataConsentController@getDataConsent | api, client.authentication | App; Web |
| POST | client/getNadiParametersData | AccountManagementController@getNadiParametersData | api, client.authentication | App; Web dashboard |
| POST | client/getPreviousVisits | VisitManagementController@getPreviousVisits | api, client.authentication | App; Web visits, corporate |
| POST | client/updateDataConsent | DataConsentController@updateDataConsent | api, client.authentication | App; Web |
| POST | client/updateQuery | AskQuestionController@updateQuestion | api, client.authentication | no screen |
| POST | client/visitWiseReports | VisitManagementController@visitWiseReports | api, client.authentication | App; Web |
| GET | v2/client/getClientDetails | AuthController@getClientDetails | client.authentication | App login; Web login |

Source: `Ashoka-World-Backend:routes/api.php:1447` to `:1472` and `:1674`. Web routes (all `check_client_auth_token`) are listed in §3 and §5 (`Nadi-Tarangini-Frontend:routes/web.php:780`).

## 7. Data model

Key fields from migrations, per the fact pack (module-facts tables list):

| Table | Model | Fields from migrations |
|---|---|---|
| `arogya_darshika_saved_data` | ArogyaDarshikaSavedData | lang_prakriti, lang_swasthya |
| `banners_data` | BannersData | accessibility, mobile_url |
| `corporate_info` | CorporateInfo | add_patient_url, city, corp_role_id, corporate_id, corporate_type, country, doctors_info, pincode, profile_image, state |
| `medical_report` | MedicalReport | city, country, external_visit_id, field_id_1, ip_address, mark_on_image_url, panchakarma_recom, reception_id, recommendations, state, try_count, user_nadi_capture_type, yoga_recom |
| `medical_report_diet` | MedicalReportDiet | create_date, diet, doctor_id, id, is_active, last_modified_on, medical_id, patient_id, vikruti_type |
| `medical_report_prescription` | MedicalReportPrescription | is_active, other_details, total_quantity |
| `medical_report_symptom_details_1` | MedicalReportSymptomDetail | symptom_value |
| `nadi_report` | NadiReport | columns not in migrations (see §13) |
| `patient_question_answer` | PatientQuestionAnswer | delete_by_doctor, delete_by_patient, is_active |
| `resource_name_master` | ResourceNameMaster | endpoint, is_default, no_of_pages, order_by, title |
| `user_personal_info` | UserPersonalInfo | allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken |
| `user_report` | UserReport | symptom_prediction |

Source: `atreya-docs/_map/_modules/patient-portal/facts.md` (Tables section, derived from backend migrations/models).

## 8. Validations & error handling

| API | Field / case | Rule or message | HTTP | Source |
|---|---|---|---|---|
| client/askQuery | query | "Query is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:33` |
| client/askQuery | save failure | "Query not added" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:42` |
| client/changePassword | current_password | required | - | `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:286` |
| client/changePassword | new password | "New password must contain at least one digit" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:303` |
| client/changePassword | client | "Client not found" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:317` |
| client/changePassword | same password | "New password must be different from the old password." | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:321` |
| client/changePassword | wrong current | "Incorrect current password" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:328` |
| client/clientEditProfile | client id | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:34` |
| client/clientEditProfile | phone | "Phone number already exists" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:78` |
| client/clientEditProfile | image | "Image shouldn't be greater than 1 MB" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:93` |
| client/clientEditProfile | upload | "An error occurred while uploading the file" | 500 | `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:107` |
| client/clientEditProfile | phone length | "Invalid phone number length1" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:140` |
| client/clientEditProfile | country code | "The provided country code is not valid for the given phone number2" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:143` |
| client/clientRemainingFees | client | "Client not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:263` |
| client/deleteClientAccount | auth | "Unauthorized" | 401 | `Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:34` |
| client/deleteQuery | id | "Query id is required" / "Enter valid query id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:161` |
| client/deleteReport | medical id | "Medical id is required" / "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:139` |
| client/deleteReport | no match | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:151` |
| client/fetchAskedQueriesList | empty | "Question list not found" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:84` |
| client/getDataConsent | client id | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:25` |
| client/updateDataConsent | nadi_consent, report_consent, share_report_consent | required, regex `^[01]$` | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:52` |
| client/updateDataConsent | share report | "Invalid share report consent" | 400 (validation failure branch) | `Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:62` |
| client/updateDataConsent | user | "User not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:77` |
| client/updateQuery | id / query | "Query id is required", "Enter valid query id", "Query is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:109` |
| client/updateQuery | answered | "This query is already answered" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:130` |
| client/visitWiseReports | medical id | "Medical id is required" / "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:176` |
| client/visitWiseReports | no match | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:188` |
| v2/client/getClientDetails | client id | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:713` |
| v2/client/getClientDetails | username | "Invalid username" | 401 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:757` |
| all client/* routes above with a catch block | unexpected error | "Internal server error" | 500 | e.g. `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:248` |

## 9. Non-functional

- Security: backend routes use `client.authentication`; web routes use `check_client_auth_token` (`Ashoka-World-Backend:routes/api.php:1451`, `Nadi-Tarangini-Frontend:routes/web.php:780`). Change-password rules are in R04. No OTP is shown in this module's facts.
- Languages: required are English, Marathi, Hindi, Czech, German, Spanish, Italian (`references/qa-scope-rules.md`). Language files found in code: `Nadi-Tarangini-Frontend:resources/lang/en/auth.php`, `en/pagination.php`, `en/passwords.php`, `en/validation.php` and `Nadi-Tarangini-Frontend:resources/lang/en_patient.json`. Only English files were found; other languages are a gap (§13).
- Performance: no timeouts or limits shown in the fact pack.

## 10. Environment matrix

From `environments.md` (verbatim; all still "TO FILL").

**Ashoka-World-Backend**

| Env | Ref | Host | Feature flags | Integration mode |
|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL |

**Nadi-Tarangini-App**

| Env | Ref | Build flavor | Host | Feature flags | Integration mode |
|---|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |

**Nadi-Tarangini-Frontend**

| Env | Ref | Host | Feature flags | Integration mode |
|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL |

## 11. Staging delta

See [staging-delta.md](staging-delta.md). Status: skipped for all three repos, waiting for `environments.md` (`atreya-docs/nt/patient-portal/staging-delta.md`). No delta was computed.

## 12. External integrations

- S3: profile image upload in `clientEditProfile` (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:84`, `:98`).
- Shared endpoints called by the web side and matched to routes outside this module's list: `getNtHelpVideos`, `getAllCountries`, `client/turyaa/homeData`, `medicalVisitReportV2`, `prescriptionReport`, `swasthyaDarshikaReport` (`Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:126`, `:154`, `:642`, `:613`).

## 13. Open questions

1. (PO/dev) The four question APIs (`askQuery`, `fetchAskedQueriesList`, `updateQuery`, `deleteQuery`) are called by no screen. Are they live, planned or dead?
2. (dev) The web `ask-queries` page calls `/client/askQuestion` and `/client/askQuestionList`, for which no backend route was found. Is the feature broken or served by a different route?
3. (dev) `getBannerList` has a defined app URL (`Nadi-Tarangini-App:lib/common_files/constants/strings_const.dart:94`); does the app dashboard call it, and what is `/patient/getBannerList` (`:144`)? Also, `getBannerList` and `visitWiseReports` success statuses were not captured.
4. (dev) Which web route serves `patientViewArogyaDarshika` (view `patientArogyaDarshikaView`)? No route is in the fact pack.
5. (PO) What do ComingSoonPage and ContactScreen show? Their purpose is not provable from the fact pack.
6. (dev) The corporate patient dashboard (`corporate/patientDashboard`) is outside this module's route list. Is it part of this module or a corporate module?
7. (dev) Is there a web password-change feature? Only the app calls `client/changePassword`.
8. (dev) `nadi_report` columns are not in migrations. Where is its schema defined?
9. (PO/QA) Required languages other than English have no language files in the web code. Where are Marathi, Hindi, Czech, German, Spanish and Italian handled?
10. (PO) How do roles (`verified_role_id`, `corp_role_id`) restrict patient features, and what does "client" versus "patient" mean here (glossary)?
11. (dev) The app screens `patient_dashboard.dart`, `drawer_menu_patient.dart`, `change_password_patient.dart` exist in `lib/patient_module/view/` but are not in the fact pack screen list. Should they be listed here?
12. (Ops) Please fill `environments.md` so the staging delta can run.

## 14. Diagrams

None yet: run /atreya:diagram patient-portal.

## 15. Document control

- Status: Draft
- Date: 2026-11-03
- Reviewer: TBD
- Commits: Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`; Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`; Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d`
