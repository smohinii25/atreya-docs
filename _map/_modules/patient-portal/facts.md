# Fact pack: patient-portal (Patient portal (client login, reports, questions, consent))

Generated 2026-11-03 by scripts/module-facts.sh. Product nt, critical false. Every line below is from code or a human-owned doc; cite the source given.

Commits: Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`, Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`, Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d`

## Backend routes (17)

### POST client/askQuery
- controller: AskQuestionController@askQuestion (found) · route: `Ashoka-World-Backend:routes/api.php:1451` · middleware: api, client.authentication
- called by: no screen in this workspace
- errors: 400 "Query is required" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:33`); 400 "Query not added" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:42`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:58`); 400 "Query not added" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:61`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:67`)

### POST client/changePassword
- controller: AccountManagementController@changePassword (found) · route: `Ashoka-World-Backend:routes/api.php:1465` · middleware: api, client.authentication
- called by: Nadi-Tarangini-App updatePasswordPatient (ChangePasswordPatient)
- validation: `current_password`: required (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:286`)
- errors: ? "New password must contain at least one digit" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:294`); 400 "Client not found" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:317`); 400 "New password must be different from the old password." (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:321`); 200 "Password updated successfully" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:326`); 400 "Incorrect current password" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:328`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:334`)

### POST client/clientDetails
- controller: EditProfileController@clientDetails (found) · route: `Ashoka-World-Backend:routes/api.php:1462` · middleware: api, client.authentication
- called by: Nadi-Tarangini-App fetchClientDetails (DrawerMenuPatient, EditPatientProfileScreen, PatientDashboard, ReportScreen); Nadi-Tarangini-Frontend PatientDashboardController@editProfile (patient-module.edit_profile); Nadi-Tarangini-Frontend PatientDashboardController@index (patient-module.patient_dashboard); Nadi-Tarangini-Frontend PatientDashboardManagementController@corporatePatientDashboard (corporate-patient-module.dashboard); Nadi-Tarangini-Frontend PatientVisitController@visitHistory (patient-module.visit_history)
- errors: 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:248`)

### POST client/clientEditProfile
- controller: EditProfileController@clientEditProfile (found) · route: `Ashoka-World-Backend:routes/api.php:1450` · middleware: api, client.authentication
- called by: Nadi-Tarangini-App editPatientPrifile (EditPatientProfileScreen); Nadi-Tarangini-Frontend PatientDashboardController@updateProfileData (patient-module.edit_profile)
- errors: 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:34`); 400 "Phone number already exists" (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:78`); 400 "Image shouldn" (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:93`); 500 "An error occurred while uploading the file" (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:107`); 400 "Invalid phone number length1" (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:140`); 400 "The provided country code is not valid for the given phone number2" (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:143`); 200 "Client profile updated successfully" (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:174`); 400 "Client profile not updated" (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:177`)

### POST client/clientRemainingFees
- controller: EditProfileController@clientRemainingFees (found) · route: `Ashoka-World-Backend:routes/api.php:1463` · middleware: api, client.authentication
- called by: Nadi-Tarangini-Frontend PatientVisitController@visitHistory (patient-module.visit_history)
- errors: 404 "Client not found" (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:263`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:294`)

### POST client/deleteClientAccount
- controller: AccountManagementController@deleteClientAccount (found) · route: `Ashoka-World-Backend:routes/api.php:1468` · middleware: api, client.authentication
- called by: Nadi-Tarangini-App deletePatientAccount (DrawerMenuPatient); Nadi-Tarangini-Frontend PatientDashboardController@deleteClientAccount (my_account.myaccount, patient-module.daily_diet_lifestyle, patient-module.data_consent, patient-module.edit_profile)
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:34`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:45`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:51`)

### POST client/deleteQuery
- controller: AskQuestionController@deleteQuestion (found) · route: `Ashoka-World-Backend:routes/api.php:1458` · middleware: api, client.authentication
- called by: no screen in this workspace
- errors: 400 "Query id is required" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:161`); 400 "Enter valid query id" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:165`); 400 "Enter valid query id" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:175`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:181`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:187`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:194`)

### POST client/deleteReport
- controller: VisitManagementController@deleteReport (found) · route: `Ashoka-World-Backend:routes/api.php:1469` · middleware: api, client.authentication
- called by: Nadi-Tarangini-App deletePatientReport (ReportScreen); Nadi-Tarangini-Frontend PatientVisitController@deletePatientReport
- errors: 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:139`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:143`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:151`); 200 "Report deleted successfully" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:159`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:165`)

### POST client/fetchAskedQueriesList
- controller: AskQuestionController@askQuestionList (found) · route: `Ashoka-World-Backend:routes/api.php:1452` · middleware: api, client.authentication
- called by: no screen in this workspace
- errors: 400 "Question list not found" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:84`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:95`)

### POST client/getBannerList
- controller: AccountManagementController@getBannerList (found) · route: `Ashoka-World-Backend:routes/api.php:1464` · middleware: api, client.authentication
- called by: Nadi-Tarangini-Frontend PatientDashboardController@index (patient-module.patient_dashboard)
- errors: ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:268`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:276`)

### POST client/getDataConsent
- controller: DataConsentController@getDataConsent (found) · route: `Ashoka-World-Backend:routes/api.php:1448` · middleware: api, client.authentication
- called by: Nadi-Tarangini-App getDataConsent (UpdateDataConsentScreen); Nadi-Tarangini-Frontend PatientDashboardController@dataConsent (patient-module.data_consent)
- errors: 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:25`); 200 "Get consent data" (`Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:33`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:38`)

### POST client/getNadiParametersData
- controller: AccountManagementController@getNadiParametersData (found) · route: `Ashoka-World-Backend:routes/api.php:1472` · middleware: api, client.authentication
- called by: Nadi-Tarangini-App getNadiParametersData (PatientDashboard); Nadi-Tarangini-Frontend PatientDashboardController@index (patient-module.patient_dashboard)
- errors: 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:227`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/AccountManagementController.php:234`)

### POST client/getPreviousVisits
- controller: VisitManagementController@getPreviousVisits (found) · route: `Ashoka-World-Backend:routes/api.php:1447` · middleware: api, client.authentication
- called by: Nadi-Tarangini-App getPreviousVisitsforPatient (ReportScreen); Nadi-Tarangini-Frontend PatientDashboardManagementController@corporatePatientDashboard (corporate-patient-module.dashboard); Nadi-Tarangini-Frontend PatientVisitController@visitHistory (patient-module.visit_history)
- errors: 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:82`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:89`)

### POST client/updateDataConsent
- controller: DataConsentController@updateDataConsent (found) · route: `Ashoka-World-Backend:routes/api.php:1449` · middleware: api, client.authentication
- called by: Nadi-Tarangini-App updateDataConsent (UpdateDataConsentScreen); Nadi-Tarangini-Frontend PatientDashboardController@updateConsentData (patient-module.data_consent)
- validation: `nadi_consent`: required|regex:/^[01]$/ (`Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:52`); `report_consent`: required|regex:/^[01]$/ (`Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:53`); `share_report_consent`: required|regex:/^[01]$/ (`Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:54`)
- errors: ? "Invalid share report consent" (`Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:62`); 404 "User not found" (`Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:77`); 200 "Data updated successfully" (`Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:86`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/DataConsentController.php:92`)

### POST client/updateQuery
- controller: AskQuestionController@updateQuestion (found) · route: `Ashoka-World-Backend:routes/api.php:1457` · middleware: api, client.authentication
- called by: no screen in this workspace
- errors: 400 "Query id is required" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:109`); 400 "Enter valid query id" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:113`); 400 "Query is required" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:116`); 400 "Enter valid query id" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:126`); 400 "This query is already answered" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:130`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:136`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:142`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/AskQuestionController.php:149`)

### POST client/visitWiseReports
- controller: VisitManagementController@visitWiseReports (found) · route: `Ashoka-World-Backend:routes/api.php:1460` · middleware: api, client.authentication
- called by: Nadi-Tarangini-App visitWiseReportsPatientDashboard (AllReportScreen); Nadi-Tarangini-Frontend PatientDashboardController@patientViewAllReports (patient-module.patientAllReportsView, patient-module.visit_history)
- errors: 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:176`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:180`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:188`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:229`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/Client/VisitManagementController.php:240`)

### GET v2/client/getClientDetails
- controller: AuthController@getClientDetails (found) · route: `Ashoka-World-Backend:routes/api.php:1674` · middleware: client.authentication
- called by: Nadi-Tarangini-App getPatientData (LoginWithUsernameScreen); Nadi-Tarangini-Frontend loginController@checkLoginCredentials (auth.login)
- errors: 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:713`); 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:757`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:789`)

## Backend routes no screen calls

`POST client/askQuery`, `POST client/deleteQuery`, `POST client/fetchAskedQueriesList`, `POST client/updateQuery`

## Web routes (15)

- Nadi-Tarangini-Frontend `GET patient/ask-queries` → PatientDashboardController@askQueries · `Nadi-Tarangini-Frontend:routes/web.php:784` · check_client_auth_token
- Nadi-Tarangini-Frontend `GET patient/daily-diet-lifestyle/{parameterName}` → PatientDashboardController@dailyDietLifestyle · `Nadi-Tarangini-Frontend:routes/web.php:794` · check_client_auth_token
- Nadi-Tarangini-Frontend `GET patient/dashboard` → PatientDashboardController@index · `Nadi-Tarangini-Frontend:routes/web.php:780` · check_client_auth_token
- Nadi-Tarangini-Frontend `GET patient/data-consent` → PatientDashboardController@dataConsent · `Nadi-Tarangini-Frontend:routes/web.php:790` · check_client_auth_token
- Nadi-Tarangini-Frontend `POST patient/delete-account` → PatientDashboardController@deleteClientAccount · `Nadi-Tarangini-Frontend:routes/web.php:793` · check_client_auth_token
- Nadi-Tarangini-Frontend `DELETE patient/deletePatientReport/{id}` → PatientVisitController@deletePatientReport · `Nadi-Tarangini-Frontend:routes/web.php:782` · check_client_auth_token
- Nadi-Tarangini-Frontend `GET patient/edit` → PatientDashboardController@editProfile · `Nadi-Tarangini-Frontend:routes/web.php:787` · check_client_auth_token
- Nadi-Tarangini-Frontend `POST patient/report/viewAllReports` → PatientDashboardController@patientViewAllReports · `Nadi-Tarangini-Frontend:routes/web.php:800` · check_client_auth_token
- Nadi-Tarangini-Frontend `POST patient/report/viewSwasthyaDarshika` → PatientDashboardController@patientViewSwasthyaDarshika · `Nadi-Tarangini-Frontend:routes/web.php:798` · check_client_auth_token
- Nadi-Tarangini-Frontend `POST patient/report/viewVisitReport` → PatientDashboardController@patientViewVisitReport · `Nadi-Tarangini-Frontend:routes/web.php:799` · check_client_auth_token
- Nadi-Tarangini-Frontend `GET patient/request-appointment` → RequestAppointmentController@requestAppointment · `Nadi-Tarangini-Frontend:routes/web.php:783` · check_client_auth_token
- Nadi-Tarangini-Frontend `POST patient/saveQueries` → PatientDashboardController@saveQueries · `Nadi-Tarangini-Frontend:routes/web.php:785` · check_client_auth_token
- Nadi-Tarangini-Frontend `POST patient/updateConsentData` → PatientDashboardController@updateConsentData · `Nadi-Tarangini-Frontend:routes/web.php:791` · check_client_auth_token
- Nadi-Tarangini-Frontend `POST patient/updateProfileData` → PatientDashboardController@updateProfileData · `Nadi-Tarangini-Frontend:routes/web.php:788` · check_client_auth_token
- Nadi-Tarangini-Frontend `GET patient/visits` → PatientVisitController@visitHistory · `Nadi-Tarangini-Frontend:routes/web.php:781` · check_client_auth_token

## Screens (18)

- Nadi-Tarangini-App **AllReportScreen** `Nadi-Tarangini-App:lib/patient_module/view/all_report_screen.dart`
- Nadi-Tarangini-App **ComingSoonPage** `Nadi-Tarangini-App:lib/patient_module/view/comming_soon_page.dart`
- Nadi-Tarangini-App **ContactScreen** `Nadi-Tarangini-App:lib/patient_module/view/contact_screen.dart`
- Nadi-Tarangini-App **DietScreen** `Nadi-Tarangini-App:lib/patient_module/view/diet_screen.dart` · route /dietScreen · goes to /patientDashboard
- Nadi-Tarangini-App **EditPatientProfileScreen** `Nadi-Tarangini-App:lib/patient_module/view/edit_patient_profile_screen.dart` · route /editPatientProfile · goes to /drawerMenuPatient
- Nadi-Tarangini-App **ReportScreen** `Nadi-Tarangini-App:lib/patient_module/view/report_screen.dart` · route /reportScreenPatient
- Nadi-Tarangini-App **UpdateDataConsentScreen** `Nadi-Tarangini-App:lib/patient_module/view/update_data_consent_screen.dart` · route /updateDataConsentScreen · goes to /drawerMenuPatient
- Nadi-Tarangini-Frontend **patient-module.ask_queries** `Nadi-Tarangini-Frontend:resources/views/patient-module/ask_queries.blade.php` · route GET patient/ask-queries · rendered by PatientDashboardController@askQueries
- Nadi-Tarangini-Frontend **patient-module.daily_diet_lifestyle** `Nadi-Tarangini-Frontend:resources/views/patient-module/daily_diet_lifestyle.blade.php` · route GET patient/daily-diet-lifestyle/{parameterName} · rendered by PatientDashboardController@dailyDietLifestyle
- Nadi-Tarangini-Frontend **patient-module.data_consent** `Nadi-Tarangini-Frontend:resources/views/patient-module/data_consent.blade.php` · route GET patient/data-consent · rendered by PatientDashboardController@dataConsent
- Nadi-Tarangini-Frontend **patient-module.edit_profile** `Nadi-Tarangini-Frontend:resources/views/patient-module/edit_profile.blade.php` · route GET patient/edit · rendered by PatientDashboardController@editProfile
- Nadi-Tarangini-Frontend **patient-module.patientAllReportsView** `Nadi-Tarangini-Frontend:resources/views/patient-module/patientAllReportsView.blade.php` · route POST patient/report/viewAllReports · rendered by PatientDashboardController@patientViewAllReports · goes to GET patient/visits
- Nadi-Tarangini-Frontend **patient-module.patientArogyaDarshikaView** `Nadi-Tarangini-Frontend:resources/views/patient-module/patientArogyaDarshikaView.blade.php` · rendered by PatientDashboardController@patientViewArogyaDarshika · goes to GET patient/visits
- Nadi-Tarangini-Frontend **patient-module.patientSwasthyaDarshikaView** `Nadi-Tarangini-Frontend:resources/views/patient-module/patientSwasthyaDarshikaView.blade.php` · route POST patient/report/viewSwasthyaDarshika · rendered by PatientDashboardController@patientViewSwasthyaDarshika · goes to GET patient/visits
- Nadi-Tarangini-Frontend **patient-module.patientVisitReportView** `Nadi-Tarangini-Frontend:resources/views/patient-module/patientVisitReportView.blade.php` · route POST patient/report/viewVisitReport · rendered by PatientDashboardController@patientViewVisitReport · goes to GET patient/visits
- Nadi-Tarangini-Frontend **patient-module.patient_dashboard** `Nadi-Tarangini-Frontend:resources/views/patient-module/patient_dashboard.blade.php` · route GET patient/dashboard · rendered by PatientDashboardController@index
- Nadi-Tarangini-Frontend **patient-module.request_appointment** `Nadi-Tarangini-Frontend:resources/views/patient-module/request_appointment.blade.php` · route GET patient/request-appointment · rendered by RequestAppointmentController@requestAppointment
- Nadi-Tarangini-Frontend **patient-module.visit_history** `Nadi-Tarangini-Frontend:resources/views/patient-module/visit_history.blade.php` · route GET patient/visits · rendered by PatientVisitController@visitHistory

## API calls (45)

| Client | Caller | Call | Route | Status | Source |
|---|---|---|---|---|---|
| Nadi-Tarangini-App | deletePatientAccount | POST `/client/deleteClientAccount` | POST client/deleteClientAccount | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2591` |
| Nadi-Tarangini-App | deletePatientReport | POST `/client/deleteReport` | POST client/deleteReport | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2656` |
| Nadi-Tarangini-App | deleteReportForDoctor | POST `/patient/deleteReport` | POST patient/deleteReport | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1893` |
| Nadi-Tarangini-App | deleteReportForDoctor | POST `/report/visitWiseAllowedReports` | POST report/visitWiseAllowedReports | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1907` |
| Nadi-Tarangini-App | dietAndLifeStyleForPatient | POST `/client/turyaa/homeData` | POST client/turyaa/homeData | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2574` |
| Nadi-Tarangini-App | editPatientPrifile | POST `/client/clientEditProfile` | POST client/clientEditProfile | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2643` |
| Nadi-Tarangini-App | fetchClientDetails | POST `/client/clientDetails` | POST client/clientDetails | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2548` |
| Nadi-Tarangini-App | getDataConsent | POST `/client/getDataConsent` | POST client/getDataConsent | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2612` |
| Nadi-Tarangini-App | getNadiParametersData | POST `/client/getNadiParametersData` | POST client/getNadiParametersData | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2558` |
| Nadi-Tarangini-App | getPatientData | GET `/v2/client/getClientDetails` | GET v2/client/getClientDetails | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:376` |
| Nadi-Tarangini-App | getPreviousVisitsforPatient | POST `/client/getPreviousVisits` | POST client/getPreviousVisits | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2622` |
| Nadi-Tarangini-App | updateDataConsent | POST `/client/updateDataConsent` | POST client/updateDataConsent | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2632` |
| Nadi-Tarangini-App | updatePasswordPatient | POST `/client/changePassword` | POST client/changePassword | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2601` |
| Nadi-Tarangini-App | visitWiseReportsPatientDashboard | POST `/client/visitWiseReports` | POST client/visitWiseReports | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2671` |
| Nadi-Tarangini-Frontend | PatientDashboardController@SaveQueries | POST `/client/askQuestion` | - | no-route | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:357` |
| Nadi-Tarangini-Frontend | PatientDashboardController@askQueries | POST `/client/askQuestionList` | - | no-route | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:320` |
| Nadi-Tarangini-Frontend | PatientDashboardController@dailyDietLifestyle | POST `/client/turyaa/homeData` | POST client/turyaa/homeData | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:642` |
| Nadi-Tarangini-Frontend | PatientDashboardController@dataConsent | POST `/client/getDataConsent` | POST client/getDataConsent | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:390` |
| Nadi-Tarangini-Frontend | PatientDashboardController@dataConsent | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:408` |
| Nadi-Tarangini-Frontend | PatientDashboardController@deleteClientAccount | POST `/client/deleteClientAccount` | POST client/deleteClientAccount | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:479` |
| Nadi-Tarangini-Frontend | PatientDashboardController@editProfile | POST `/client/clientDetails` | POST client/clientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:172` |
| Nadi-Tarangini-Frontend | PatientDashboardController@editProfile | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:154` |
| Nadi-Tarangini-Frontend | PatientDashboardController@editProfile | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:200` |
| Nadi-Tarangini-Frontend | PatientDashboardController@index | POST `/client/clientDetails` | POST client/clientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:29` |
| Nadi-Tarangini-Frontend | PatientDashboardController@index | POST `/client/getBannerList` | POST client/getBannerList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:103` |
| Nadi-Tarangini-Frontend | PatientDashboardController@index | POST `/client/getNadiParametersData` | POST client/getNadiParametersData | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:54` |
| Nadi-Tarangini-Frontend | PatientDashboardController@index | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:126` |
| Nadi-Tarangini-Frontend | PatientDashboardController@patientViewAllReports | POST `/client/visitWiseReports` | POST client/visitWiseReports | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:581` |
| Nadi-Tarangini-Frontend | PatientDashboardController@patientViewAllReports | ? `/medicalVisitReportV2` | GET medicalVisitReportV2 | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:613` |
| Nadi-Tarangini-Frontend | PatientDashboardController@patientViewAllReports | ? `/prescriptionReport` | GET prescriptionReport | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:614` |
| Nadi-Tarangini-Frontend | PatientDashboardController@patientViewAllReports | ? `/swasthyaDarshikaReport` | GET swasthyaDarshikaReport | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:615` |
| Nadi-Tarangini-Frontend | PatientDashboardController@patientViewSwasthyaDarshika | ? `/swasthyaDarshikaReport` | GET swasthyaDarshikaReport | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:526` |
| Nadi-Tarangini-Frontend | PatientDashboardController@patientViewVisitReport | ? `/medicalVisitReportV2` | GET medicalVisitReportV2 | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:545` |
| Nadi-Tarangini-Frontend | PatientDashboardController@patientViewVisitReport | ? `/prescriptionReport` | GET prescriptionReport | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:546` |
| Nadi-Tarangini-Frontend | PatientDashboardController@updateConsentData | POST `/client/updateDataConsent` | POST client/updateDataConsent | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:440` |
| Nadi-Tarangini-Frontend | PatientDashboardController@updateProfileData | POST `/client/clientEditProfile` | POST client/clientEditProfile | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:245` |
| Nadi-Tarangini-Frontend | PatientDashboardManagementController@corporatePatientDashboard | POST `/client/clientDetails` | POST client/clientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/Corporate/PatientDashboardManagementController.php:38` |
| Nadi-Tarangini-Frontend | PatientDashboardManagementController@corporatePatientDashboard | POST `/client/getPreviousVisits` | POST client/getPreviousVisits | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/Corporate/PatientDashboardManagementController.php:22` |
| Nadi-Tarangini-Frontend | PatientVisitController@deletePatientReport | POST `/client/deleteReport` | POST client/deleteReport | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientVisitController.php:120` |
| Nadi-Tarangini-Frontend | PatientVisitController@visitHistory | POST `/client/clientDetails` | POST client/clientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientVisitController.php:37` |
| Nadi-Tarangini-Frontend | PatientVisitController@visitHistory | POST `/client/clientRemainingFees` | POST client/clientRemainingFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientVisitController.php:63` |
| Nadi-Tarangini-Frontend | PatientVisitController@visitHistory | POST `/client/getPreviousVisits` | POST client/getPreviousVisits | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientVisitController.php:21` |
| Nadi-Tarangini-Frontend | PatientVisitController@visitHistory | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientVisitController.php:90` |
| Nadi-Tarangini-Frontend | loginController@checkLoginCredentials | GET `/v2/client/getClientDetails` | GET v2/client/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:94` |

## Tables (12)

- `arogya_darshika_saved_data` (models: ArogyaDarshikaSavedData): lang_prakriti, lang_swasthya
- `banners_data` (models: BannersData): accessibility, mobile_url
- `corporate_info` (models: CorporateInfo): add_patient_url, city, corp_role_id, corporate_id, corporate_type, country, doctors_info, pincode, profile_image, state
- `medical_report` (models: MedicalReport): city, country, external_visit_id, field_id_1, ip_address, mark_on_image_url, panchakarma_recom, reception_id, recommendations, state, try_count, user_nadi_capture_type, yoga_recom
- `medical_report_diet` (models: MedicalReportDiet): create_date, diet, doctor_id, id, is_active, last_modified_on, medical_id, patient_id, vikruti_type
- `medical_report_prescription` (models: MedicalReportPrescription): is_active, other_details, total_quantity
- `medical_report_symptom_details_1` (models: MedicalReportSymptomDetail): symptom_value
- `nadi_report` (models: NadiReport): columns not in migrations
- `patient_question_answer` (models: PatientQuestionAnswer): delete_by_doctor, delete_by_patient, is_active
- `resource_name_master` (models: ResourceNameMaster): endpoint, is_default, no_of_pages, order_by, title
- `user_personal_info` (models: UserPersonalInfo): allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken
- `user_report` (models: UserReport): symptom_prediction

## External systems

- S3 (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:84,98`

## Environment matrix (verbatim from atreya-docs/environments.md)

### Ashoka-World-Backend

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

### Nadi-Tarangini-Frontend

| Env | Ref | Host | Feature flags | Integration mode |
|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL |

## Languages

Required: English, Marathi, Hindi, Czech, German, Spanish, Italian (source: references/qa-scope-rules.md).
Language files in code: Nadi-Tarangini-Frontend:resources/lang/en/auth.php, Nadi-Tarangini-Frontend:resources/lang/en/pagination.php, Nadi-Tarangini-Frontend:resources/lang/en/passwords.php, Nadi-Tarangini-Frontend:resources/lang/en/validation.php, Nadi-Tarangini-Frontend:resources/lang/en_patient.json
