---
module: "nt-admin"
doc: "PRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# NT admin panel (users, access, data management, customise by user): Product Requirements Document

## 1. Overview

This module covers the admin panel of Nadi Tarangini: 44 web routes under `admin/*` listed in the fact pack (the middleware group in web.php also holds a few more admin routes, e.g. `switchToAdminToDoctor`) (`Nadi-Tarangini-Frontend:routes/web.php:111-164`), 18 admin and customise screens, and 23 backend API routes, most under the `nt-admin/*` prefix (`Ashoka-World-Backend:routes/api.php:1356-1386`). The panel lets an admin create and edit users, activate or deactivate them, set per-user feature permissions and data access, view a user's patients and visits, customise report pages and questionnaires per user, and manage plans and invoices (`Nadi-Tarangini-Frontend:routes/web.php:111-164`). Three backend routes are also called by the mobile App and by non-admin Frontend screens (see §6). The fact pack lists no mobile admin screen, only Frontend screens (`atreya-docs/_map/_modules/nt-admin/facts.md`).

## 2. Users, roles & permissions

- All routes in the admin group (the 44 in the fact pack and the few others in that group) use the `nt_admin_authentication` middleware (`Nadi-Tarangini-Frontend:routes/web.php:111-164`). It lets a request through only if the session holds `user_id`, `auth_token` and `role_id`, and `role_id` equals 7; any other case redirects to the login route (`Nadi-Tarangini-Frontend:app/Http/Middleware/NTAdminAuthentication.php:23-34`). For role 7 it also runs a geo-IP check and redirects to `regionRestricted` when not allowed (`Nadi-Tarangini-Frontend:app/Http/Middleware/NTAdminAuthentication.php:25-27`).
- 22 of the 23 backend routes use `api, auth.token`; `GET public/allRoles` uses `api` only, so it needs no token (`Ashoka-World-Backend:routes/api.php:903`, `Ashoka-World-Backend:routes/api.php:1356-1386`).
- The backend identifies the caller from the `user-id` request header; when it is missing the endpoints return 401 "Unauthorized" (e.g. `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:46`).
- A user created by the admin cannot be given role ids 2, 3, 4 or 7 (`Ashoka-World-Backend:app/Http/Requests/NTAdmin/UserManagement/AddUserRequest.php:40`).
- What each role id means (names of roles 2, 3, 4, 7 and others) is not stated in the cited code: see §13 Q1.

## 3. User journeys

**Web (admin, role 7)**
1. Admin opens `admin/dashboard`; the page loads current user details, child roles and help videos (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:24`, `:41`, `:64`). Users by role and consultation-type counts load through `admin/get-users-by-role` and `admin/consultation-type-counts` (`Nadi-Tarangini-Frontend:routes/web.php:112-113`).
2. Admin opens `admin/user-and-teams` and from it goes to create user, edit profile, update password, permissions, data management, patient list, customise report (user-wise) and customise questionnaire (user-wise) (screen navigation in `atreya-docs/_map/_modules/nt-admin/facts.md`, screen `admin.user_and_teams`).
3. Create user: admin fills `admin/create-user`, which posts to `admin/saveUser`, which calls `nt-admin/access-management/addUser` (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1290`).
4. Permissions: `admin/permissions/{id}` loads features via `nt-admin/access-management/features` and saves via `updateFeatures` (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1397`, `:1485`).
5. Data management: `admin/data-management/{id}` loads and saves per-user data access (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1079`, `:1176`).
6. Patient list: `admin/patient-list/{id}` lists a user's patients, with search, last-visit info, previous visits and report views (`Nadi-Tarangini-Frontend:routes/web.php:118-125`).
7. Plans: `admin/getPlanDetails` leads to apply-coupon, create-order and verify-transaction (screen `admin.plan_details` navigation, `atreya-docs/_map/_modules/nt-admin/facts.md`).

**Mobile App**: the fact pack lists no admin journey. It lists these App calls: `public/allRoles` from LoginWithOtpScreen, `currentUserAccessibleUsersWithLocations` from AddAppointmentScreen and AddPatientScreen, and `report/getTypeWiseFeatureDetails` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:63`, `:2396`, `:2038`).

## 4. Functional requirements

### NT-ADMIN-R01: Restrict the admin panel to the admin role
All `admin/*` web routes require an active session with `user_id`, `auth_token` and `role_id`, and only `role_id` 7 proceeds; others are redirected to login. Role 7 requests are also subject to a geo-IP check.
**Acceptance criteria**
- Given no session `user_id`/`auth_token`/`role_id` when any `admin/*` route is requested then the user is redirected to the login route.
- Given `role_id` is not 7 when an `admin/*` route is requested then the user is redirected to the login route.
- Given `role_id` is 7 and the geo-IP check fails then the user is redirected to `regionRestricted`.
**Source**: `Nadi-Tarangini-Frontend:app/Http/Middleware/NTAdminAuthentication.php:23-34`, `Nadi-Tarangini-Frontend:app/Http/Kernel.php:73`
**Screens**: all admin.* and customize.* screens · **API**: n/a

### NT-ADMIN-R02: Admin dashboard (user counts and consultation counts)
The dashboard shows data for the current user and child roles, lists users by role (optionally by date range) and fetches consultation-type counts for a list of user ids.
**Acceptance criteria**
- Given `getUsersByRole` is called without a `user-id` header then it returns 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:513`).
- Given `consultationTypeCounts` receives invalid input then it returns 400 "Validation failed" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:565`); `user_ids` must be an array of 1 to 500 distinct positive integers, and `from_date`/`to_date` must be `Y-m-d`, given together, with `to_date` on or after `from_date` (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:556-559`).
**Source**: `Ashoka-World-Backend:routes/api.php:1366`, `:1372`, `:1378`, `:1380`; `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:24`, `:41`, `:114`, `:147`, `:186`
**Screens**: admin.admin_dashboard (Web) · **API**: GET getCurrentUserDetails, GET getChildRole, POST getUsersByRole, POST consultationTypeCounts

### NT-ADMIN-R03: View users and teams
The users-and-teams page loads active users, all roles, child roles and feature details, and links to the per-user actions.
**Acceptance criteria**
- Given a missing `user-id` header then `getActiveUserDetails` and `getChildRole` return 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:99`, `:226`).
- Given success then they return 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:108`, `:243`).
**Source**: `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:207`, `:218`, `:258`, `:269`; `Ashoka-World-Backend:routes/api.php:1360`, `:1367`, `:1371`, `:1372`
**Screens**: admin.user_and_teams (Web) · **API**: GET getActiveUserDetails, GET getAllFeatureDetails, GET getAllRoles, GET getChildRole

### NT-ADMIN-R04: Create a user
Admin creates a user under themselves. On success the backend returns 200 "User signup successfully", and tries to add an "Account Created" Firebase notification for the new user; a notification failure is logged and does not fail the request. The create-user page also loads countries, profession types, salutation types, active users, roles and clinic details of a user.
**Acceptance criteria**
- Given no `user-id` header then 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:46`).
- Given invalid input then the request fails validation per §8 with messages in `NT_xxxx|text` form (`Ashoka-World-Backend:app/Http/Requests/NTAdmin/UserManagement/AddUserRequest.php:68-107`).
- Given the service returns an error then 400 with the service's status code and message (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:58-64`).
- Given success then 200 "User signup successfully" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:84`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:38-90`; `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1200-1290`
**Screens**: admin.create_user (Web) · **API**: POST addUser, POST getUserWiseActiveClinicDetails, GET getActiveUserDetails, GET getAllRoles

### NT-ADMIN-R05: Activate or deactivate a user
Admin changes a user's status from the users-and-teams page. The backend returns 200 "Success" or 500 "Internal server error".
**Acceptance criteria**
- Given a status change then `updateUserStatus` returns 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:139`) or 500 on exception (`:146`).
**Source**: `Ashoka-World-Backend:routes/api.php:1365`; `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1515`
**Screens**: admin.user_and_teams (Web, caller `activeInactiveUser` is not tied to a view in the fact pack) · **API**: POST updateUserStatus

### NT-ADMIN-R06: Edit own profile or another user's profile
`admin/updateProfile` calls `editProfile` and `editUserProfile`. `editUserProfile` returns 401 "User id is required" when the target user id is missing.
**Acceptance criteria**
- Given `editUserProfile` without `user-id` header then 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:471`).
- Given a missing target user id then 401 "User id is required" (`:481`).
- Given success then 200 "User details update successfully" (`:498`); `editProfile` returns 200 "Success" (`:314`).
**Source**: `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1002`, `:1037`; `Ashoka-World-Backend:routes/api.php:1374`, `:1376`
**Screens**: admin.edit_profile (Web) · **API**: POST editProfile, POST editUserProfile, POST getUserDetails, GET getCurrentUserDetails

### NT-ADMIN-R07: Update a user's password
Admin sets a new password for a user. Backend returns 401 "Unauthorized" without `user-id`, else 200 "Password updated successfully".
**Acceptance criteria**
- Given no `user-id` header then 401 (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:339`).
- Given success then 200 "Password updated successfully" (`:359`).
**Source**: `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1348`, `:1371`; `Ashoka-World-Backend:routes/api.php:1375`
**Screens**: admin.update_password (Web) · **API**: POST updateUserPassword, POST getUserDetails

### NT-ADMIN-R08: Set per-user feature permissions
Admin loads the features available to a user and saves the updated selection.
**Acceptance criteria**
- Given the permissions page then `features` returns 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:32`) or 500 (`:40`).
- Given a save then `updateFeatures` returns 200 "Success" (`:66`) or 500 (`:73`).
**Source**: `Ashoka-World-Backend:routes/api.php:1361-1362`; `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1397`, `:1485`
**Screens**: admin.user_permissions (Web) · **API**: POST features, POST updateFeatures

### NT-ADMIN-R09: Manage per-user data access
Admin views and updates which data a user can access. A separate endpoint returns the users (with clinic locations) the current user can access.
**Acceptance criteria**
- Given the data-management page then `userWiseDataAccess` returns 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:27`) or 500 (`:36`).
- Given a save then `updateUserWiseDataAccess` returns 200 "Success" (`:63`) or 500 (`:69`).
- Given `currentUserAccessibleUsersWithLocations` without `user-id` then 401 (`:117`), success 200 (`:126`), error 500 (`:133`). It is called by the App (AddAppointmentScreen, AddPatientScreen) and by `AppointmentController` in the Frontend (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2396`, `Nadi-Tarangini-Frontend:app/Http/Controllers/AppointmentController.php:133`).
**Source**: `Ashoka-World-Backend:routes/api.php:1043`, `:1384`, `:1386`; `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1079`, `:1176`
**Screens**: admin.data_management (Web), AddAppointmentScreen, AddPatientScreen (App) · **API**: POST userWiseDataAccess, POST updateUserWiseDataAccess, GET currentUserAccessibleUsersWithLocations

### NT-ADMIN-R10: View a user's patients, visits and reports
Admin opens a user's patient list (paged fetch, name search, last-visit info), a patient's previous visits, and the all-reports and visit-report views.
**Acceptance criteria**
- Given the patient list then the Frontend calls `infinitePatientList`, `searchPatientUsingName` and `v2/report/getLastVisitInformation` (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:476`, `:519`, `:855`).
- Given previous visits then it calls `v2/patient/patientPreviousVisit` (`:600`); all-reports calls `report/visitWiseAllowedReports` (`:710`).
- Given a visit report then the controller references `medicalVisitReport`, `medicalVisitReportV2`, `prescriptionReport`, `dietReport`, `careServicesReport` (`:797-804`); their HTTP method is shown as unresolved in the fact pack.
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:118-125`
**Screens**: admin.user_patient_list, admin.user_previous_visits, admin.all_report_view, admin.visit_report_view (Web) · **API**: Not owned by this module's backend (calls to other modules' endpoints)

### NT-ADMIN-R11: Customise report pages (all users and per user)
Admin views report page counts, edits report pages globally (`updateReportPages`) and for one user (`updateUserWiseRportPages`).
**Acceptance criteria**
- Given the global page then it calls `reportManagement/getReportWiseNoOfPages`, `reportManagement/getReportPages` and `reportManagement/customizeReportPages` (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:75`, `:275`, `:170`).
- Given the user-wise page then it calls `reportManagement/fetchSingleUserWiseReportPages` and `reportManagement/customizeSingleUserReportPages` (`:384`, `:502`).
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:140-150`
**Screens**: customize.customize_report, customize.user_wise_customize_report (Web) · **API**: calls other modules' `reportManagement/*` endpoints

### NT-ADMIN-R12: Customise questionnaire (all users and per user)
Admin adds questions, updates category-wise questions globally and for one user.
**Acceptance criteria**
- Given add-question then it calls `getAnswerTypes`, `medicalForm/getFormCategories` and `addnewDetails` (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:304`, `:315`, `:351`).
- Given updates then it calls `medicalForm/updateCateogoryWiseQuestions` and `medicalForm/updateCateogoryWiseQuestionsForSingleUser` (`:234`, `:647`); per-user load uses `medicalForm/getCateogoryWiseQuestionsForSingleUser` (`:621`).
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:138-154`
**Screens**: customize.add_question, customize.add_question_v2, customize.user_wise_customize_questionnaire (Web) · **API**: calls other modules' `medicalForm/*` endpoints

### NT-ADMIN-R13: Plans, coupon, order, payment verification and invoices
Admin views plan details and plan status, applies a coupon, creates an order, verifies a transaction and lists payment invoices.
**Acceptance criteria**
- Given plan details then `subscriptions/getReportWisePlans` is called (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1619`); plan status calls `planStatus` (`:1774`).
- Given a coupon then `calculatePlanPrice` is called (`:1650`); order creation calls `createNtOrder` (`:1699`); verification calls `verifyTransaction` (`:1727`); invoices call `payment-invoices` (`:1808`).
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:158-164`
**Screens**: admin.plan_details, admin.payment_invoices (Web) · **API**: calls other modules' subscription/payment endpoints

### NT-ADMIN-R14: Add self as admin and switch to doctor
A logged-in user can call `add-self-admin` (from `DashboardController@saveSelfAdminData`). It returns 401 "Unauthorized" without `user-id`, else 200 "Success". The Frontend's `switchToDoctor` loads feature details.
**Acceptance criteria**
- Given no `user-id` then 401 (`Ashoka-World-Backend:app/Http/Controllers/NTUser/AdminManagementController.php:27`); success 200 "Success" (`:47`); service error or exception 400 (`:36-57`).
**Source**: `Ashoka-World-Backend:routes/api.php:1356`; `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1326`, `:1499`
**Screens**: Not stated in the fact pack (caller `saveSelfAdminData`; view not listed) · **API**: POST add-self-admin, GET getAllFeatureDetails

### NT-ADMIN-R15: Roles and feature details at login
Login screens fetch all roles from the public endpoint and feature details after authentication.
**Acceptance criteria**
- Given `GET public/allRoles` (no token) then 200 "success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:201`) or 500 (`:209`).
- Given `getAllFeatureDetails` then 401 without `user-id` (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:88`), 200 (`:97`), 500 (`:105`).
**Source**: `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:209`, `:589`, `:728`; `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:63`
**Screens**: auth.login (Web), LoginWithOtpScreen (App) · **API**: GET public/allRoles, GET getAllFeatureDetails

### NT-ADMIN-R16: Type-wise feature details for a medical assessment
`report/getTypeWiseFeatureDetails` validates type, patient and medical ids and returns feature details. It is called from the live Nadi V3 medical assessment page and the App.
**Acceptance criteria**
- The medical id is optional: it is validated only when supplied (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:164-192`).
- Given missing type then 400 "Type is required"; missing patient id then 400 "Patient id is required"; invalid patient id then 400 "Invalid patient id"; invalid medical id then 400 "Invalid medical id"; invalid medical report then 400 "Invalid medical report"; unknown type then 404 "Invalid type" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:122-202`).
**Source**: `Ashoka-World-Backend:routes/api.php:1208`; `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1261`; `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2038`
**Screens**: medical_assessment.medical_assesment (Web), errors.expiredMedicalIdV3 (Web) · **API**: POST report/getTypeWiseFeatureDetails

### NT-ADMIN-R17: GET currentUserAccessibleUsers (no screen calls it)
The route exists and returns 401/200/500, but no screen in this workspace calls it (`Ashoka-World-Backend:routes/api.php:1041`, `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:84`). Whether it is live is asked in §13 Q6.
**Acceptance criteria**
- Given no `user-id` then 401 (`:84`); success 200 (`:93`); error 500 (`:102`).
**Source**: `Ashoka-World-Backend:routes/api.php:1041`
**Screens**: none · **API**: GET currentUserAccessibleUsers

## 5. Screens (web / mobile)

| Screen | Platform | File | Route / path | Purpose (provable) |
|---|---|---|---|---|
| admin.admin_dashboard | Web | `Nadi-Tarangini-Frontend:resources/views/admin/admin_dashboard.blade.php` | GET admin/dashboard | Rendered by AdminDashboardController@index |
| admin.all_report_view | Web | `Nadi-Tarangini-Frontend:resources/views/admin/all_report_view.blade.php` | POST admin/report/viewAllReport | All-reports view; links to previous visits and user-and-teams |
| admin.create_user | Web | `Nadi-Tarangini-Frontend:resources/views/admin/create_user.blade.php` | GET admin/create-user | Create user form |
| admin.data_management | Web | `Nadi-Tarangini-Frontend:resources/views/admin/data_management.blade.php` | GET admin/data-management/{id} | Per-user data access |
| admin.edit_profile | Web | `Nadi-Tarangini-Frontend:resources/views/admin/edit_profile.blade.php` | GET admin/edit-profile/{id} | Edit profile |
| admin.payment_invoices | Web | `Nadi-Tarangini-Frontend:resources/views/admin/payment_invoices.blade.php` | GET admin/payment-invoices | Invoices; links to plan details |
| admin.plan_details | Web | `Nadi-Tarangini-Frontend:resources/views/admin/plan_details.blade.php` | GET admin/getPlanDetails | Plan details; links to coupon, order, verify |
| admin.update_password | Web | `Nadi-Tarangini-Frontend:resources/views/admin/update_password.blade.php` | GET admin/update-password/{id} | Update password |
| admin.user_and_teams | Web | `Nadi-Tarangini-Frontend:resources/views/admin/user_and_teams.blade.php` | GET admin/user-and-teams | Hub linking to per-user pages |
| admin.user_patient_list | Web | `Nadi-Tarangini-Frontend:resources/views/admin/user_patient_list.blade.php` | GET admin/patient-list/{id} | User's patient list |
| admin.user_permissions | Web | `Nadi-Tarangini-Frontend:resources/views/admin/user_permissions.blade.php` | GET admin/permissions/{id} | Feature permissions |
| admin.user_previous_visits | Web | `Nadi-Tarangini-Frontend:resources/views/admin/user_previous_visits.blade.php` | GET admin/patient-list/{id}/previous-visits/{patientId} | Previous visits |
| admin.visit_report_view | Web | `Nadi-Tarangini-Frontend:resources/views/admin/visit_report_view.blade.php` | POST admin/report/viewVisitReport | Visit report view |
| customize.add_question | Web | `Nadi-Tarangini-Frontend:resources/views/customize/add_question.blade.php` | GET admin/add-question | Add question; rendered by AdminCustomizeController@index and CustomizeController@index |
| customize.add_question_v2 | Web | `Nadi-Tarangini-Frontend:resources/views/customize/add_question_v2.blade.php` | GET admin/customize-question | Customise question |
| customize.customize_report | Web | `Nadi-Tarangini-Frontend:resources/views/customize/customize_report.blade.php` | GET admin/customize-report | Customise report |
| customize.user_wise_customize_questionnaire | Web | `Nadi-Tarangini-Frontend:resources/views/customize/user_wise_customize_questionnaire.blade.php` | GET admin/get-user-wise-customize-question/{id} | User-wise questionnaire |
| customize.user_wise_customize_report | Web | `Nadi-Tarangini-Frontend:resources/views/customize/user_wise_customize_report.blade.php` | GET admin/customize-report-user-wise/{id} | User-wise report |

Source for every row: `atreya-docs/_map/_modules/nt-admin/facts.md` (Screens). App screens that use this module's APIs: LoginWithOtpScreen, AddAppointmentScreen, AddPatientScreen (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:63`, `:2396`).

## 6. APIs

All in `Ashoka-World-Backend`; line numbers are in `routes/api.php`.

| Method | Endpoint | Controller | Auth (middleware) | Called by |
|---|---|---|---|---|
| POST | add-self-admin (:1356) | AdminManagementController@addSelfAdmin | api, auth.token | Frontend DashboardController@saveSelfAdminData |
| GET | currentUserAccessibleUsers (:1041) | DataManagementController@getCurrentUserDataAccess | api, auth.token | none in workspace |
| GET | currentUserAccessibleUsersWithLocations (:1043) | DataManagementController@getCurrentAccessibleUsersWithClinics | api, auth.token | App AddAppointmentScreen, AddPatientScreen; Frontend AppointmentController |
| POST | nt-admin/access-management/addUser (:1364) | UserManagementController@addUser | api, auth.token | AdminDashboardController@saveUser |
| POST | nt-admin/access-management/consultationTypeCounts (:1380) | UserManagementController@getConsultationTypeCounts | api, auth.token | AdminDashboardController@getConsultationTypeCounts |
| POST | nt-admin/access-management/editProfile (:1374) | UserManagementController@editProfile | api, auth.token | AdminDashboardController@updateProfile |
| POST | nt-admin/access-management/editUserProfile (:1376) | UserManagementController@editUserProfile | api, auth.token | AdminDashboardController@updateProfile |
| POST | nt-admin/access-management/features (:1361) | FeaturesController@getFeatures | api, auth.token | AdminDashboardController@editPermissions |
| GET | nt-admin/access-management/getActiveUserDetails (:1367) | UserManagementController@getActiveUserDetails | api, auth.token | AdminDashboardController createUser, dataManagement, userAndTeams, userPatientList, userPreviousVisits |
| GET | nt-admin/access-management/getAllFeatureDetails (:1360) | FeaturesController@getAllFeatureDetails | api, auth.token | AdminDashboardController@userAndTeams; DashboardController@switchToDoctor; loginController (2 methods) |
| GET | nt-admin/access-management/getAllRoles (:1371) | UserManagementController@getAllRoles | api, auth.token | AdminCustomizeController (2); AdminDashboardController (6) |
| GET | nt-admin/access-management/getChildRole (:1372) | UserManagementController@getChildRole | api, auth.token | AdminDashboardController index, userAndTeams |
| GET | nt-admin/access-management/getCurrentUserDetails (:1366) | UserManagementController@getCurrentUserDetails | api, auth.token | AdminDashboardController editProfile, getUserDetails, getUsersByRole, index |
| POST | nt-admin/access-management/getUserDetails (:1368) | UserManagementController@getUserDetails | api, auth.token | AdminCustomizeController (2); AdminDashboardController (8 methods) |
| POST | nt-admin/access-management/getUserWiseActiveClinicDetails (:1369) | UserManagementController@getUserWiseActiveClinicDetails | api, auth.token | AdminDashboardController@getUserClinicDetails |
| POST | nt-admin/access-management/getUsersByRole (:1378) | UserManagementController@getUsersByRole | api, auth.token | AdminDashboardController@getUsersByRole |
| POST | nt-admin/access-management/updateFeatures (:1362) | FeaturesController@updateUserWiseFeatures | api, auth.token | AdminDashboardController@updatePermissions |
| POST | nt-admin/access-management/updateUserPassword (:1375) | UserManagementController@updateUserPassword | api, auth.token | AdminDashboardController@updateUserPassword |
| POST | nt-admin/access-management/updateUserStatus (:1365) | UserManagementController@updateUserStatus | api, auth.token | AdminDashboardController@activeInactiveUser |
| POST | nt-admin/data-management/updateUserWiseDataAccess (:1386) | DataManagementController@updateUserWiseDataAccess | api, auth.token | AdminDashboardController@updateUserDataManagement |
| POST | nt-admin/data-management/userWiseDataAccess (:1384) | DataManagementController@getDataAccess | api, auth.token | AdminDashboardController@dataManagement |
| GET | public/allRoles (:903) | UserManagementController@allRoles | api | App getAllRoles (LoginWithOtpScreen); loginController@getAllRoles |
| POST | report/getTypeWiseFeatureDetails (:1208) | FeaturesController@getTypeWiseFeatureDetails | api, auth.token | App getTypeWiseFeatureDetails; MedicalAssessmentV3Controller@liveNadiV3 |

Source: `atreya-docs/_map/_modules/nt-admin/facts.md` (Backend routes). The Frontend also calls about 40 endpoints owned by other modules (reportManagement, medicalForm, subscriptions, patient, etc.); they are listed in the fact pack's API calls table and are not owned here.

## 7. Data model

Tables the fact pack associates with this module's controllers (`atreya-docs/_map/_modules/nt-admin/facts.md`, Tables). Only listed fields are shown; whether they come from migrations is not checked (§13 Q7).

| Table | Model | Key fields |
|---|---|---|
| calendar_events | CalendarEvent | clinic_id, consultation_type, reception_id |
| common_data | CommonData | created_at, data, id, label, updated_at |
| master_contents | MasterContents | content, create_date, id, is_active, last_modified_on, month_number, title, type, week_number |
| medical_report | MedicalReport | city, country, external_visit_id, field_id_1, ip_address, mark_on_image_url, panchakarma_recom, reception_id, recommendations, state, try_count, user_nadi_capture_type, yoga_recom |
| user_personal_info | UserPersonalInfo | allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken |

## 8. Validations & error handling

| API | Field / case | Rule or message | HTTP | Source |
|---|---|---|---|---|
| addUser | user_name | required; "User name is required" (NT_1238) | 400 | `Ashoka-World-Backend:app/Http/Requests/NTAdmin/UserManagement/AddUserRequest.php:25`, `:71` |
| addUser | password | required; must contain a digit | 400 | `AddUserRequest.php:26`, `:79-80` |
| addUser | firstname, lastname | required; letters and spaces only | 400 | `AddUserRequest.php:27-28`, `:73-77` |
| addUser | email | required; valid email | 400 | `AddUserRequest.php:29`, `:85-86` |
| addUser | gender | required; one of M, F, D, N | 400 | `AddUserRequest.php:30`, `:82-83` |
| addUser | mobile_no | required; numeric | 400 | `AddUserRequest.php:31`, `:88-89` |
| addUser | role_id | required integer; not 2, 3, 4, 7; "Invalid role id" | 400 | `AddUserRequest.php:40`, `:98-100` |
| addUser | salutation_type, profession_type_id, clinic_name, address_line_1, state, country | required | 400 | `AddUserRequest.php:24`, `:32`, `:41-42`, `:46-47` |
| addUser | parent_id | rules at lines 34-39; messages "Invalid parent id", "Parent id is required" | 400 | `AddUserRequest.php:34`, `:95-96` |
| addUser | missing user-id header | "Unauthorized" | 401 | `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:46` |
| addUser | service error | service message | 400 | `UserManagementController.php:58-64` |
| consultationTypeCounts | user_ids / from_date / to_date | see R02 | 400 "Validation failed" | `UserManagementController.php:556-565` |
| editUserProfile | missing target user id | "User id is required" | 401 | `UserManagementController.php:481` |
| getTypeWiseFeatureDetails | type, patient id, medical id, medical report | see R16 | 400 / 404 | `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:122-202` |
| most NTAdmin endpoints | missing user-id header | "Unauthorized" | 401 | see R03-R09 |
| most NTAdmin endpoints | exception | "Internal server error" | 500 | e.g. `UserManagementController.php:116` |

addUser validation failures return 400 with `status_code` and `message` split from the `NT_xxxx|text` string (`Ashoka-World-Backend:app/Http/Requests/NTAdmin/UserManagement/AddUserRequest.php:113-130`). The route-level validation count in the fact pack is 0 (rules sit in FormRequests or inline).

## 9. Non-functional

- **Security**: web access requires session role 7 plus geo-IP check (`Nadi-Tarangini-Frontend:app/Http/Middleware/NTAdminAuthentication.php:23-34`); backend routes require `auth.token` except `public/allRoles` (`Ashoka-World-Backend:routes/api.php:903`). some 500 responses include the exception message in an `errors` field (e.g. `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:147`); whether that is intended is asked in §13 Q9.
- **Languages**: required list is English, Marathi, Hindi, Czech, German, Spanish, Italian (`references/qa-scope-rules.md`). Language files found in module code: only `en` (auth, pagination, passwords, validation) and `en_patient.json` (`Nadi-Tarangini-Frontend:resources/lang/en/auth.php`, `Nadi-Tarangini-Frontend:resources/lang/en_patient.json`). Other-language coverage is asked in §13 Q10.
- **Performance**: `consultationTypeCounts` accepts at most 500 user ids (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:556`). No other limits or timeouts were examined.

## 10. Environment matrix

Copied from `atreya-docs/environments.md` (status TO FILL).

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

## 11. Staging delta

See `atreya-docs/nt/nt-admin/staging-delta.md`. Status: skipped for both repos, waiting for `environments.md` (staging and production refs are TO FILL). No delta has been computed.

## 12. External integrations

- Firebase: used by `addUser` to add an "Account Created" notification (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:67`).
- Razorpay: referenced in `AdminDashboardController` at the transaction verification step (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1728-1730`). Purpose and environments of both systems: Needs confirmation (`atreya-docs/external-systems.md`).

## 13. Open questions

1. (PO/dev) What do role ids 2, 3, 4 and 7 (and the others) stand for? Only the numbers appear in the cited code.
2. (PO) Is the admin panel meant to have no mobile equivalent? The fact pack lists no App admin screen.
3. (dev) Which screen and view use `add-self-admin` (`saveSelfAdminData`)? The fact pack lists no screen for it (R14).
4. (dev) Which screen triggers `activeInactiveUser` (R05)? The fact pack ties it to no view.
5. (dev) What HTTP method do `medicalVisitReport`, `medicalVisitReportV2`, `prescriptionReport`, `dietReport`, `careServicesReport` use when called from `viewVisitReport` (shown as "?" in the fact pack)?
6. (PO/dev) Is `GET currentUserAccessibleUsers` live or dead? No screen in this workspace calls it.
7. (dev) Do the five tables in §7 come from migrations, and which of them does this module write? The fact pack lists model fields only.
8. (dev) Why does `add-self-admin` return 400 with the raw exception message on its error path rather than 500 (`Ashoka-World-Backend:app/Http/Controllers/NTUser/AdminManagementController.php:51-57`)?
9. (PO/dev) Is returning the raw exception message in 500 responses intended?
10. (PO/QA) Required languages other than English: where are the translations for admin-panel screens? Only `en` files were found.
11. (PO) What is the purpose and environment (test/live) of Razorpay and Firebase for this module?
12. (dev/PO) How do the admin pages behave after `DashboardController@switchToDoctor`? The code shows only that feature details are loaded (`Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1499`).
13. (PO) What are the plan, coupon and invoice business rules? The module only calls other modules' endpoints and the rules are not in this module.

## 14. Diagrams

None yet: run /atreya:diagram nt-admin.

## 15. Document control

| Item | Value |
|---|---|
| Status | Draft |
| Date | 2026-11-03 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend 8dfbb37db7d71a400b3656bd50fbed6173908a24; Nadi-Tarangini-Frontend e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d |
