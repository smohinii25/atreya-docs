# Fact pack: nt-admin (NT admin panel (users, access, data management, customise by user))

Generated 2026-11-03 by scripts/module-facts.sh. Product nt, critical false. Every line below is from code or a human-owned doc; cite the source given.

Commits: Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`, Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d`

## Backend routes (23)

### POST add-self-admin
- controller: AdminManagementController@addSelfAdmin (found) · route: `Ashoka-World-Backend:routes/api.php:1356` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend DashboardController@saveSelfAdminData (add_self_admin)
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTUser/AdminManagementController.php:27`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTUser/AdminManagementController.php:47`)

### GET currentUserAccessibleUsers
- controller: DataManagementController@getCurrentUserDataAccess (found) · route: `Ashoka-World-Backend:routes/api.php:1041` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:84`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:93`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:102`)

### GET currentUserAccessibleUsersWithLocations
- controller: DataManagementController@getCurrentAccessibleUsersWithClinics (found) · route: `Ashoka-World-Backend:routes/api.php:1043` · middleware: api, auth.token
- called by: Nadi-Tarangini-App currentUserAccessibleUsersWithLocations (AddAppointmentScreen, AddPatientScreen); Nadi-Tarangini-Frontend AppointmentController@currentUserAccessibleUsersWithLocations
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:117`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:126`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:133`)

### POST nt-admin/access-management/addUser
- controller: UserManagementController@addUser (found) · route: `Ashoka-World-Backend:routes/api.php:1364` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@saveUser (admin.create_user)
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:46`); 200 "User signup successfully" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:84`)

### POST nt-admin/access-management/consultationTypeCounts
- controller: UserManagementController@getConsultationTypeCounts (found) · route: `Ashoka-World-Backend:routes/api.php:1380` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@getConsultationTypeCounts (admin.admin_dashboard)
- errors: 400 "Validation failed" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:565`); ? "Consultation type counts fetched successfully" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:676`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:696`)

### POST nt-admin/access-management/editProfile
- controller: UserManagementController@editProfile (found) · route: `Ashoka-World-Backend:routes/api.php:1374` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@updateProfile (admin.edit_profile)
- errors: 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:314`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:323`)

### POST nt-admin/access-management/editUserProfile
- controller: UserManagementController@editUserProfile (found) · route: `Ashoka-World-Backend:routes/api.php:1376` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@updateProfile (admin.edit_profile)
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:471`); 401 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:481`); 200 "User details update successfully" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:498`)

### POST nt-admin/access-management/features
- controller: FeaturesController@getFeatures (found) · route: `Ashoka-World-Backend:routes/api.php:1361` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@editPermissions (admin.user_permissions)
- errors: 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:32`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:40`)

### GET nt-admin/access-management/getActiveUserDetails
- controller: UserManagementController@getActiveUserDetails (found) · route: `Ashoka-World-Backend:routes/api.php:1367` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@createUser (admin.create_user); Nadi-Tarangini-Frontend AdminDashboardController@dataManagement (admin.data_management); Nadi-Tarangini-Frontend AdminDashboardController@userAndTeams (admin.user_and_teams); Nadi-Tarangini-Frontend AdminDashboardController@userPatientList (admin.user_patient_list); Nadi-Tarangini-Frontend AdminDashboardController@userPreviousVisits (admin.user_previous_visits)
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:99`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:108`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:116`)

### GET nt-admin/access-management/getAllFeatureDetails
- controller: FeaturesController@getAllFeatureDetails (found) · route: `Ashoka-World-Backend:routes/api.php:1360` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@userAndTeams (admin.user_and_teams); Nadi-Tarangini-Frontend DashboardController@switchToDoctor (admin.admin_dashboard, admin.all_report_view, admin.create_user, admin.data_management); Nadi-Tarangini-Frontend loginController@checkLoginCredentials (auth.login); Nadi-Tarangini-Frontend loginController@getUserDetailsOtpBasedLogin (auth.login)
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:88`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:97`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:105`)

### GET nt-admin/access-management/getAllRoles
- controller: UserManagementController@getAllRoles (found) · route: `Ashoka-World-Backend:routes/api.php:1371` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminCustomizeController@getCustomizeReportUserWise (customize.user_wise_customize_report); Nadi-Tarangini-Frontend AdminCustomizeController@getUserWiseCustomizeQuestion (customize.user_wise_customize_questionnaire); Nadi-Tarangini-Frontend AdminDashboardController@createUser (admin.create_user); Nadi-Tarangini-Frontend AdminDashboardController@dataManagement (admin.data_management); Nadi-Tarangini-Frontend AdminDashboardController@editPermissions (admin.user_permissions); Nadi-Tarangini-Frontend AdminDashboardController@userAndTeams (admin.user_and_teams); Nadi-Tarangini-Frontend AdminDashboardController@userPatientList (admin.user_patient_list); Nadi-Tarangini-Frontend AdminDashboardController@userPreviousVisits (admin.user_previous_visits)
- errors: 200 "success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:169`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:177`)

### GET nt-admin/access-management/getChildRole
- controller: UserManagementController@getChildRole (found) · route: `Ashoka-World-Backend:routes/api.php:1372` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@index (admin.admin_dashboard); Nadi-Tarangini-Frontend AdminDashboardController@userAndTeams (admin.user_and_teams)
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:226`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:243`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:251`)

### GET nt-admin/access-management/getCurrentUserDetails
- controller: UserManagementController@getCurrentUserDetails (found) · route: `Ashoka-World-Backend:routes/api.php:1366` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@editProfile (admin.edit_profile); Nadi-Tarangini-Frontend AdminDashboardController@getUserDetails (add_self_admin); Nadi-Tarangini-Frontend AdminDashboardController@getUsersByRole (admin.admin_dashboard); Nadi-Tarangini-Frontend AdminDashboardController@index (admin.admin_dashboard)
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:382`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:416`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:424`)

### POST nt-admin/access-management/getUserDetails
- controller: UserManagementController@getUserDetails (found) · route: `Ashoka-World-Backend:routes/api.php:1368` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminCustomizeController@getCustomizeReportUserWise (customize.user_wise_customize_report); Nadi-Tarangini-Frontend AdminCustomizeController@getUserWiseCustomizeQuestion (customize.user_wise_customize_questionnaire); Nadi-Tarangini-Frontend AdminDashboardController@dataManagement (admin.data_management); Nadi-Tarangini-Frontend AdminDashboardController@editPermissions (admin.user_permissions); Nadi-Tarangini-Frontend AdminDashboardController@editProfile (admin.edit_profile); Nadi-Tarangini-Frontend AdminDashboardController@getUserDetails (add_self_admin); Nadi-Tarangini-Frontend AdminDashboardController@resolveTargetUserAuthToken; Nadi-Tarangini-Frontend AdminDashboardController@updatePassword (admin.update_password); Nadi-Tarangini-Frontend AdminDashboardController@userPatientList (admin.user_patient_list); Nadi-Tarangini-Frontend AdminDashboardController@userPreviousVisits (admin.user_previous_visits)
- errors: 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:276`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:284`)

### POST nt-admin/access-management/getUserWiseActiveClinicDetails
- controller: UserManagementController@getUserWiseActiveClinicDetails (found) · route: `Ashoka-World-Backend:routes/api.php:1369` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@getUserClinicDetails (admin.create_user)
- errors: 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:449`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:457`)

### POST nt-admin/access-management/getUsersByRole
- controller: UserManagementController@getUsersByRole (found) · route: `Ashoka-World-Backend:routes/api.php:1378` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@getUsersByRole (admin.admin_dashboard)
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:513`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:535`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:543`)

### POST nt-admin/access-management/updateFeatures
- controller: FeaturesController@updateUserWiseFeatures (found) · route: `Ashoka-World-Backend:routes/api.php:1362` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@updatePermissions (admin.user_permissions)
- errors: 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:66`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:73`)

### POST nt-admin/access-management/updateUserPassword
- controller: UserManagementController@updateUserPassword (found) · route: `Ashoka-World-Backend:routes/api.php:1375` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@updateUserPassword (admin.update_password)
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:339`); 200 "Password updated successfully" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:359`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:367`)

### POST nt-admin/access-management/updateUserStatus
- controller: UserManagementController@updateUserStatus (found) · route: `Ashoka-World-Backend:routes/api.php:1365` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@activeInactiveUser
- errors: 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:139`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:146`)

### POST nt-admin/data-management/updateUserWiseDataAccess
- controller: DataManagementController@updateUserWiseDataAccess (found) · route: `Ashoka-World-Backend:routes/api.php:1386` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@updateUserDataManagement (admin.data_management)
- errors: 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:63`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:69`)

### POST nt-admin/data-management/userWiseDataAccess
- controller: DataManagementController@getDataAccess (found) · route: `Ashoka-World-Backend:routes/api.php:1384` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@dataManagement (admin.data_management)
- errors: 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:27`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/DataManagementController.php:36`)

### GET public/allRoles
- controller: UserManagementController@allRoles (found) · route: `Ashoka-World-Backend:routes/api.php:903` · middleware: api
- called by: Nadi-Tarangini-App getAllRoles (LoginWithOtpScreen); Nadi-Tarangini-Frontend loginController@getAllRoles (auth.login)
- errors: 200 "success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:201`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:209`)

### POST report/getTypeWiseFeatureDetails
- controller: FeaturesController@getTypeWiseFeatureDetails (found) · route: `Ashoka-World-Backend:routes/api.php:1208` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getTypeWiseFeatureDetails; Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment)
- errors: 400 "Type is required" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:122`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:130`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:138`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:157`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:170`); 400 "Invalid medical report" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:182`); 404 "Invalid type" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:202`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:226`)

## Backend routes no screen calls

`GET currentUserAccessibleUsers`

## Web routes (44)

- Nadi-Tarangini-Frontend `POST admin/activeInactiveUser` → AdminDashboardController@activeInactiveUser · `Nadi-Tarangini-Frontend:routes/web.php:134` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/add-question` → AdminCustomizeController@index · `Nadi-Tarangini-Frontend:routes/web.php:138` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/apply-coupon` → AdminDashboardController@applyCoupon · `Nadi-Tarangini-Frontend:routes/web.php:159` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/consultation-type-counts` → AdminDashboardController@getConsultationTypeCounts · `Nadi-Tarangini-Frontend:routes/web.php:113` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/create-order` → AdminDashboardController@createNtOrder · `Nadi-Tarangini-Frontend:routes/web.php:160` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/create-user` → AdminDashboardController@createUser · `Nadi-Tarangini-Frontend:routes/web.php:128` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/customize-question` → AdminCustomizeController@customizeQuestion · `Nadi-Tarangini-Frontend:routes/web.php:144` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/customize-report` → AdminCustomizeController@customizeReport · `Nadi-Tarangini-Frontend:routes/web.php:143` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/customize-report-user-wise/{id}` → AdminCustomizeController@getCustomizeReportUserWise · `Nadi-Tarangini-Frontend:routes/web.php:149` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/dashboard` → AdminDashboardController@index · `Nadi-Tarangini-Frontend:routes/web.php:111` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/data-management/{id}` → AdminDashboardController@dataManagement · `Nadi-Tarangini-Frontend:routes/web.php:117` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/edit-profile/{id}` → AdminDashboardController@editProfile · `Nadi-Tarangini-Frontend:routes/web.php:115` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/get-report-pages` → AdminCustomizeController@getReportPages · `Nadi-Tarangini-Frontend:routes/web.php:140` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/get-user-wise-category-wise-customize-questions/{id}` → AdminCustomizeController@getUserWiseCategoryWiseCustomizeQuestions · `Nadi-Tarangini-Frontend:routes/web.php:153` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/get-user-wise-customize-question/{id}` → AdminCustomizeController@getUserWiseCustomizeQuestion · `Nadi-Tarangini-Frontend:routes/web.php:152` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/get-user-wise-report-pages/{id}` → AdminCustomizeController@getUserWiseReportPages · `Nadi-Tarangini-Frontend:routes/web.php:148` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/get-users-by-role` → AdminDashboardController@getUsersByRole · `Nadi-Tarangini-Frontend:routes/web.php:112` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/getPlanDetails` → AdminDashboardController@getPlanDetails · `Nadi-Tarangini-Frontend:routes/web.php:158` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/getPlanStatus` → AdminDashboardController@getPlanStatus · `Nadi-Tarangini-Frontend:routes/web.php:162` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/getUserClinicDetails` → AdminDashboardController@getUserClinicDetails · `Nadi-Tarangini-Frontend:routes/web.php:136` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/getUserDetails` → AdminDashboardController@getUserDetails · `Nadi-Tarangini-Frontend:routes/web.php:135` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/patient-list/{id}` → AdminDashboardController@userPatientList · `Nadi-Tarangini-Frontend:routes/web.php:118` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/patient-list/{id}/fetch` → AdminDashboardController@fetchUserPatientList · `Nadi-Tarangini-Frontend:routes/web.php:119` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/patient-list/{id}/last-visit-info` → AdminDashboardController@fetchUserLastVisitInformation · `Nadi-Tarangini-Frontend:routes/web.php:121` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/patient-list/{id}/previous-visits/{patientId}` → AdminDashboardController@userPreviousVisits · `Nadi-Tarangini-Frontend:routes/web.php:122` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/patient-list/{id}/search` → AdminDashboardController@searchUserPatientList · `Nadi-Tarangini-Frontend:routes/web.php:120` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/payment-invoices` → AdminDashboardController@paymentInvoices · `Nadi-Tarangini-Frontend:routes/web.php:163` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/payment-invoices/list` → AdminDashboardController@fetchPaymentInvoices · `Nadi-Tarangini-Frontend:routes/web.php:164` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/permissions/{id}` → AdminDashboardController@editPermissions · `Nadi-Tarangini-Frontend:routes/web.php:132` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/questionstore` → AdminCustomizeController@questionstore · `Nadi-Tarangini-Frontend:routes/web.php:139` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/report/viewAllReport` → AdminDashboardController@viewAllReport · `Nadi-Tarangini-Frontend:routes/web.php:124` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/report/viewVisitReport` → AdminDashboardController@viewVisitReport · `Nadi-Tarangini-Frontend:routes/web.php:125` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/saveUser` → AdminDashboardController@saveUser · `Nadi-Tarangini-Frontend:routes/web.php:129` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/update-password/{id}` → AdminDashboardController@updatePassword · `Nadi-Tarangini-Frontend:routes/web.php:130` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/updateCategory` → AdminCustomizeController@updateCategory · `Nadi-Tarangini-Frontend:routes/web.php:141` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/updatePermissions` → AdminDashboardController@updatePermissions · `Nadi-Tarangini-Frontend:routes/web.php:133` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/updateProfile` → AdminDashboardController@updateProfile · `Nadi-Tarangini-Frontend:routes/web.php:116` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/updateReportPages` → AdminCustomizeController@updateReportPages · `Nadi-Tarangini-Frontend:routes/web.php:142` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/updateUserDataManagement` → AdminDashboardController@updateUserDataManagement · `Nadi-Tarangini-Frontend:routes/web.php:127` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/updateUserPassword` → AdminDashboardController@updateUserPassword · `Nadi-Tarangini-Frontend:routes/web.php:131` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/updateUserWiseCategoryQustions` → AdminCustomizeController@updateUserWiseCategoryQustions · `Nadi-Tarangini-Frontend:routes/web.php:154` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/updateUserWiseRportPages` → AdminCustomizeController@updateUserWiseRportPages · `Nadi-Tarangini-Frontend:routes/web.php:150` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET admin/user-and-teams` → AdminDashboardController@userAndTeams · `Nadi-Tarangini-Frontend:routes/web.php:114` · nt_admin_authentication
- Nadi-Tarangini-Frontend `POST admin/verifyTransaction` → AdminDashboardController@verifyTransaction · `Nadi-Tarangini-Frontend:routes/web.php:161` · nt_admin_authentication

## Screens (18)

- Nadi-Tarangini-Frontend **admin.admin_dashboard** `Nadi-Tarangini-Frontend:resources/views/admin/admin_dashboard.blade.php` · route GET admin/dashboard · rendered by AdminDashboardController@index
- Nadi-Tarangini-Frontend **admin.all_report_view** `Nadi-Tarangini-Frontend:resources/views/admin/all_report_view.blade.php` · route POST admin/report/viewAllReport · rendered by AdminDashboardController@viewAllReport · goes to GET admin/patient-list/{id}/previous-visits/{patientId}, GET admin/user-and-teams
- Nadi-Tarangini-Frontend **admin.create_user** `Nadi-Tarangini-Frontend:resources/views/admin/create_user.blade.php` · route GET admin/create-user · rendered by AdminDashboardController@createUser · goes to GET admin/user-and-teams
- Nadi-Tarangini-Frontend **admin.data_management** `Nadi-Tarangini-Frontend:resources/views/admin/data_management.blade.php` · route GET admin/data-management/{id} · rendered by AdminDashboardController@dataManagement · goes to GET admin/user-and-teams
- Nadi-Tarangini-Frontend **admin.edit_profile** `Nadi-Tarangini-Frontend:resources/views/admin/edit_profile.blade.php` · route GET admin/edit-profile/{id} · rendered by AdminDashboardController@editProfile · goes to GET admin/user-and-teams
- Nadi-Tarangini-Frontend **admin.payment_invoices** `Nadi-Tarangini-Frontend:resources/views/admin/payment_invoices.blade.php` · route GET admin/payment-invoices · rendered by AdminDashboardController@paymentInvoices · goes to GET admin/getPlanDetails, GET admin/payment-invoices/list
- Nadi-Tarangini-Frontend **admin.plan_details** `Nadi-Tarangini-Frontend:resources/views/admin/plan_details.blade.php` · route GET admin/getPlanDetails · rendered by AdminDashboardController@getPlanDetails · goes to GET admin/payment-invoices, POST admin/apply-coupon, POST admin/create-order, POST admin/verifyTransaction
- Nadi-Tarangini-Frontend **admin.update_password** `Nadi-Tarangini-Frontend:resources/views/admin/update_password.blade.php` · route GET admin/update-password/{id} · rendered by AdminDashboardController@updatePassword · goes to GET admin/user-and-teams
- Nadi-Tarangini-Frontend **admin.user_and_teams** `Nadi-Tarangini-Frontend:resources/views/admin/user_and_teams.blade.php` · route GET admin/user-and-teams · rendered by AdminDashboardController@userAndTeams · goes to GET admin/create-user, GET admin/customize-report-user-wise/{id}, GET admin/data-management/{id}, GET admin/edit-profile/{id}, GET admin/get-user-wise-customize-question/{id}, GET admin/patient-list/{id}, GET admin/permissions/{id}, GET admin/update-password/{id}
- Nadi-Tarangini-Frontend **admin.user_patient_list** `Nadi-Tarangini-Frontend:resources/views/admin/user_patient_list.blade.php` · route GET admin/patient-list/{id} · rendered by AdminDashboardController@userPatientList · goes to GET admin/user-and-teams
- Nadi-Tarangini-Frontend **admin.user_permissions** `Nadi-Tarangini-Frontend:resources/views/admin/user_permissions.blade.php` · route GET admin/permissions/{id} · rendered by AdminDashboardController@editPermissions · goes to GET admin/user-and-teams
- Nadi-Tarangini-Frontend **admin.user_previous_visits** `Nadi-Tarangini-Frontend:resources/views/admin/user_previous_visits.blade.php` · route GET admin/patient-list/{id}/previous-visits/{patientId} · rendered by AdminDashboardController@userPreviousVisits · goes to GET admin/patient-list/{id}, GET admin/user-and-teams, POST admin/report/viewAllReport, POST admin/report/viewVisitReport
- Nadi-Tarangini-Frontend **admin.visit_report_view** `Nadi-Tarangini-Frontend:resources/views/admin/visit_report_view.blade.php` · route POST admin/report/viewVisitReport · rendered by AdminDashboardController@viewVisitReport · goes to GET admin/patient-list/{id}/previous-visits/{patientId}, GET admin/user-and-teams
- Nadi-Tarangini-Frontend **customize.add_question** `Nadi-Tarangini-Frontend:resources/views/customize/add_question.blade.php` · route GET admin/add-question · rendered by AdminCustomizeController@index, CustomizeController@index · goes to GET admin/customize-question
- Nadi-Tarangini-Frontend **customize.add_question_v2** `Nadi-Tarangini-Frontend:resources/views/customize/add_question_v2.blade.php` · route GET admin/customize-question · rendered by AdminCustomizeController@customizeQuestion
- Nadi-Tarangini-Frontend **customize.customize_report** `Nadi-Tarangini-Frontend:resources/views/customize/customize_report.blade.php` · route GET admin/customize-report · rendered by AdminCustomizeController@customizeReport · goes to GET admin/user-and-teams
- Nadi-Tarangini-Frontend **customize.user_wise_customize_questionnaire** `Nadi-Tarangini-Frontend:resources/views/customize/user_wise_customize_questionnaire.blade.php` · route GET admin/get-user-wise-customize-question/{id} · rendered by AdminCustomizeController@getUserWiseCustomizeQuestion · goes to GET admin/customize-question, GET admin/user-and-teams
- Nadi-Tarangini-Frontend **customize.user_wise_customize_report** `Nadi-Tarangini-Frontend:resources/views/customize/user_wise_customize_report.blade.php` · route GET admin/customize-report-user-wise/{id} · rendered by AdminCustomizeController@getCustomizeReportUserWise · goes to GET admin/user-and-teams

## API calls (121)

| Client | Caller | Call | Route | Status | Source |
|---|---|---|---|---|---|
| Nadi-Tarangini-App | currentUserAccessibleUsersWithLocations | GET `/currentUserAccessibleUsersWithLocations` | GET currentUserAccessibleUsersWithLocations | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2396` |
| Nadi-Tarangini-App | getAllRoles | GET `/public/allRoles` | GET public/allRoles | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:63` |
| Nadi-Tarangini-App | getTypeWiseFeatureDetails | POST `/report/getTypeWiseFeatureDetails` | POST report/getTypeWiseFeatureDetails | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2038` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@customizeQuestion | POST `/getAnswerTypes` | POST getAnswerTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:112` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@customizeQuestion | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:136` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@customizeQuestion | POST `/medicalForm/getFormCategories` | POST medicalForm/getFormCategories | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:123` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@customizeReport | POST `/reportManagement/getReportWiseNoOfPages` | POST reportManagement/getReportWiseNoOfPages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:75` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@getCustomizeReportUserWise | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:462` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@getCustomizeReportUserWise | GET `/nt-admin/access-management/getAllRoles` | GET nt-admin/access-management/getAllRoles | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:440` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@getCustomizeReportUserWise | POST `/nt-admin/access-management/getUserDetails` | POST nt-admin/access-management/getUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:426` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@getCustomizeReportUserWise | POST `/reportManagement/getReportWiseNoOfPages` | POST reportManagement/getReportWiseNoOfPages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:417` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@getReportPages | POST `/reportManagement/getReportPages` | POST reportManagement/getReportPages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:275` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@getUserWiseCategoryWiseCustomizeQuestions | POST `/medicalForm/getCateogoryWiseQuestionsForSingleUser` | POST medicalForm/getCateogoryWiseQuestionsForSingleUser | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:621` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@getUserWiseCustomizeQuestion | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:588` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@getUserWiseCustomizeQuestion | POST `/medicalForm/getFormCategories` | POST medicalForm/getFormCategories | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:542` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@getUserWiseCustomizeQuestion | GET `/nt-admin/access-management/getAllRoles` | GET nt-admin/access-management/getAllRoles | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:566` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@getUserWiseCustomizeQuestion | POST `/nt-admin/access-management/getUserDetails` | POST nt-admin/access-management/getUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:551` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@getUserWiseReportPages | POST `/reportManagement/fetchSingleUserWiseReportPages` | POST reportManagement/fetchSingleUserWiseReportPages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:384` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@index | POST `/getAnswerTypes` | POST getAnswerTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:304` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@index | POST `/medicalForm/getFormCategories` | POST medicalForm/getFormCategories | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:315` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@questionstore | POST `/addnewDetails` | POST addnewDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:351` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@updateCategory | POST `/medicalForm/updateCateogoryWiseQuestions` | POST medicalForm/updateCateogoryWiseQuestions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:234` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@updateReportPages | POST `/reportManagement/customizeReportPages` | POST reportManagement/customizeReportPages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:170` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@updateUserWiseCategoryQustions | POST `/medicalForm/updateCateogoryWiseQuestionsForSingleUser` | POST medicalForm/updateCateogoryWiseQuestionsForSingleUser | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:647` |
| Nadi-Tarangini-Frontend | AdminCustomizeController@updateUserWiseRportPages | POST `/reportManagement/customizeSingleUserReportPages` | POST reportManagement/customizeSingleUserReportPages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminCustomizeController.php:502` |
| Nadi-Tarangini-Frontend | AdminDashboardController@activeInactiveUser | POST `/nt-admin/access-management/updateUserStatus` | POST nt-admin/access-management/updateUserStatus | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1515` |
| Nadi-Tarangini-Frontend | AdminDashboardController@applyCoupon | POST `/calculatePlanPrice` | POST calculatePlanPrice | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1650` |
| Nadi-Tarangini-Frontend | AdminDashboardController@createNtOrder | POST `/createNtOrder` | POST createNtOrder | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1699` |
| Nadi-Tarangini-Frontend | AdminDashboardController@createUser | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1205` |
| Nadi-Tarangini-Frontend | AdminDashboardController@createUser | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1233` |
| Nadi-Tarangini-Frontend | AdminDashboardController@createUser | GET `/getProfessionType` | GET getProfessionType | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1210` |
| Nadi-Tarangini-Frontend | AdminDashboardController@createUser | POST `/getSalutationTypes` | POST getSalutationTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1200` |
| Nadi-Tarangini-Frontend | AdminDashboardController@createUser | GET `/nt-admin/access-management/getActiveUserDetails` | GET nt-admin/access-management/getActiveUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1220` |
| Nadi-Tarangini-Frontend | AdminDashboardController@createUser | GET `/nt-admin/access-management/getAllRoles` | GET nt-admin/access-management/getAllRoles | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1215` |
| Nadi-Tarangini-Frontend | AdminDashboardController@dataManagement | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1140` |
| Nadi-Tarangini-Frontend | AdminDashboardController@dataManagement | GET `/nt-admin/access-management/getActiveUserDetails` | GET nt-admin/access-management/getActiveUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1093` |
| Nadi-Tarangini-Frontend | AdminDashboardController@dataManagement | GET `/nt-admin/access-management/getAllRoles` | GET nt-admin/access-management/getAllRoles | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1104` |
| Nadi-Tarangini-Frontend | AdminDashboardController@dataManagement | POST `/nt-admin/access-management/getUserDetails` | POST nt-admin/access-management/getUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1112` |
| Nadi-Tarangini-Frontend | AdminDashboardController@dataManagement | POST `/nt-admin/data-management/userWiseDataAccess` | POST nt-admin/data-management/userWiseDataAccess | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1079` |
| Nadi-Tarangini-Frontend | AdminDashboardController@editPermissions | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1453` |
| Nadi-Tarangini-Frontend | AdminDashboardController@editPermissions | POST `/nt-admin/access-management/features` | POST nt-admin/access-management/features | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1397` |
| Nadi-Tarangini-Frontend | AdminDashboardController@editPermissions | GET `/nt-admin/access-management/getAllRoles` | GET nt-admin/access-management/getAllRoles | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1431` |
| Nadi-Tarangini-Frontend | AdminDashboardController@editPermissions | POST `/nt-admin/access-management/getUserDetails` | POST nt-admin/access-management/getUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1417` |
| Nadi-Tarangini-Frontend | AdminDashboardController@editProfile | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:916` |
| Nadi-Tarangini-Frontend | AdminDashboardController@editProfile | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:947` |
| Nadi-Tarangini-Frontend | AdminDashboardController@editProfile | GET `/nt-admin/access-management/getCurrentUserDetails` | GET nt-admin/access-management/getCurrentUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:926` |
| Nadi-Tarangini-Frontend | AdminDashboardController@editProfile | POST `/nt-admin/access-management/getUserDetails` | POST nt-admin/access-management/getUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:931` |
| Nadi-Tarangini-Frontend | AdminDashboardController@fetchPaymentInvoices | GET `/payment-invoices` | GET payment-invoices | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1808` |
| Nadi-Tarangini-Frontend | AdminDashboardController@fetchUserLastVisitInformation | POST `/v2/report/getLastVisitInformation` | POST v2/report/getLastVisitInformation | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:855` |
| Nadi-Tarangini-Frontend | AdminDashboardController@fetchUserPatientList | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:476` |
| Nadi-Tarangini-Frontend | AdminDashboardController@getConsultationTypeCounts | POST `/nt-admin/access-management/consultationTypeCounts` | POST nt-admin/access-management/consultationTypeCounts | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:186` |
| Nadi-Tarangini-Frontend | AdminDashboardController@getPlanDetails | POST `/subscriptions/getReportWisePlans` | POST subscriptions/getReportWisePlans | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1619` |
| Nadi-Tarangini-Frontend | AdminDashboardController@getPlanStatus | GET `/planStatus` | GET planStatus | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1774` |
| Nadi-Tarangini-Frontend | AdminDashboardController@getUserClinicDetails | POST `/nt-admin/access-management/getUserWiseActiveClinicDetails` | POST nt-admin/access-management/getUserWiseActiveClinicDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1591` |
| Nadi-Tarangini-Frontend | AdminDashboardController@getUserDetails | GET `/nt-admin/access-management/getCurrentUserDetails` | GET nt-admin/access-management/getCurrentUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1556` |
| Nadi-Tarangini-Frontend | AdminDashboardController@getUserDetails | POST `/nt-admin/access-management/getUserDetails` | POST nt-admin/access-management/getUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1561` |
| Nadi-Tarangini-Frontend | AdminDashboardController@getUsersByRole | GET `/nt-admin/access-management/getCurrentUserDetails` | GET nt-admin/access-management/getCurrentUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:114` |
| Nadi-Tarangini-Frontend | AdminDashboardController@getUsersByRole | POST `/nt-admin/access-management/getUsersByRole` | POST nt-admin/access-management/getUsersByRole | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:147` |
| Nadi-Tarangini-Frontend | AdminDashboardController@index | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:64` |
| Nadi-Tarangini-Frontend | AdminDashboardController@index | GET `/nt-admin/access-management/getChildRole` | GET nt-admin/access-management/getChildRole | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:24` |
| Nadi-Tarangini-Frontend | AdminDashboardController@index | GET `/nt-admin/access-management/getCurrentUserDetails` | GET nt-admin/access-management/getCurrentUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:41` |
| Nadi-Tarangini-Frontend | AdminDashboardController@resolveTargetUserAuthToken | POST `/nt-admin/access-management/getUserDetails` | POST nt-admin/access-management/getUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:893` |
| Nadi-Tarangini-Frontend | AdminDashboardController@saveUser | POST `/nt-admin/access-management/addUser` | POST nt-admin/access-management/addUser | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1290` |
| Nadi-Tarangini-Frontend | AdminDashboardController@searchUserPatientList | POST `/searchPatientUsingName` | POST searchPatientUsingName | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:519` |
| Nadi-Tarangini-Frontend | AdminDashboardController@updatePassword | POST `/nt-admin/access-management/getUserDetails` | POST nt-admin/access-management/getUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1348` |
| Nadi-Tarangini-Frontend | AdminDashboardController@updatePermissions | POST `/nt-admin/access-management/updateFeatures` | POST nt-admin/access-management/updateFeatures | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1485` |
| Nadi-Tarangini-Frontend | AdminDashboardController@updateProfile | POST `/nt-admin/access-management/editProfile` | POST nt-admin/access-management/editProfile | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1002` |
| Nadi-Tarangini-Frontend | AdminDashboardController@updateProfile | POST `/nt-admin/access-management/editUserProfile` | POST nt-admin/access-management/editUserProfile | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1037` |
| Nadi-Tarangini-Frontend | AdminDashboardController@updateUserDataManagement | POST `/nt-admin/data-management/updateUserWiseDataAccess` | POST nt-admin/data-management/updateUserWiseDataAccess | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1176` |
| Nadi-Tarangini-Frontend | AdminDashboardController@updateUserPassword | POST `/nt-admin/access-management/updateUserPassword` | POST nt-admin/access-management/updateUserPassword | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1371` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userAndTeams | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:327` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userAndTeams | GET `/nt-admin/access-management/getActiveUserDetails` | GET nt-admin/access-management/getActiveUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:207` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userAndTeams | GET `/nt-admin/access-management/getAllFeatureDetails` | GET nt-admin/access-management/getAllFeatureDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:218` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userAndTeams | GET `/nt-admin/access-management/getAllRoles` | GET nt-admin/access-management/getAllRoles | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:258` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userAndTeams | GET `/nt-admin/access-management/getChildRole` | GET nt-admin/access-management/getChildRole | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:269` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPatientList | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:438` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPatientList | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:358` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPatientList | GET `/nt-admin/access-management/getActiveUserDetails` | GET nt-admin/access-management/getActiveUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:391` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPatientList | GET `/nt-admin/access-management/getAllRoles` | GET nt-admin/access-management/getAllRoles | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:402` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPatientList | POST `/nt-admin/access-management/getUserDetails` | POST nt-admin/access-management/getUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:380` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPreviousVisits | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:662` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPreviousVisits | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:568` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPreviousVisits | GET `/nt-admin/access-management/getActiveUserDetails` | GET nt-admin/access-management/getActiveUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:630` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPreviousVisits | GET `/nt-admin/access-management/getAllRoles` | GET nt-admin/access-management/getAllRoles | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:636` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPreviousVisits | POST `/nt-admin/access-management/getUserDetails` | POST nt-admin/access-management/getUserDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:642` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPreviousVisits | POST `/v2/patient/patientPreviousVisit` | POST v2/patient/patientPreviousVisit | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:600` |
| Nadi-Tarangini-Frontend | AdminDashboardController@verifyTransaction | POST `/verifyTransaction` | POST verifyTransaction | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1727` |
| Nadi-Tarangini-Frontend | AdminDashboardController@viewAllReport | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:748` |
| Nadi-Tarangini-Frontend | AdminDashboardController@viewAllReport | POST `/report/visitWiseAllowedReports` | POST report/visitWiseAllowedReports | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:710` |
| Nadi-Tarangini-Frontend | AdminDashboardController@viewVisitReport | ? `/careServicesReport` | GET careServicesReport | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:804` |
| Nadi-Tarangini-Frontend | AdminDashboardController@viewVisitReport | ? `/dietReport` | GET dietReport | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:800` |
| Nadi-Tarangini-Frontend | AdminDashboardController@viewVisitReport | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:812` |
| Nadi-Tarangini-Frontend | AdminDashboardController@viewVisitReport | ? `/medicalVisitReport` | GET medicalVisitReport | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:797` |
| Nadi-Tarangini-Frontend | AdminDashboardController@viewVisitReport | ? `/medicalVisitReportV2` | GET medicalVisitReportV2 | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:798` |
| Nadi-Tarangini-Frontend | AdminDashboardController@viewVisitReport | ? `/prescriptionReport` | GET prescriptionReport | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:799` |
| Nadi-Tarangini-Frontend | AppointmentController@currentUserAccessibleUsersWithLocations | GET `/currentUserAccessibleUsersWithLocations` | GET currentUserAccessibleUsersWithLocations | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AppointmentController.php:133` |
| Nadi-Tarangini-Frontend | DashboardController@saveSelfAdminData | POST `/add-self-admin` | POST add-self-admin | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1326` |
| Nadi-Tarangini-Frontend | DashboardController@switchToDoctor | GET `/nt-admin/access-management/getAllFeatureDetails` | GET nt-admin/access-management/getAllFeatureDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1499` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/report/getTypeWiseFeatureDetails` | POST report/getTypeWiseFeatureDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1261` |
| Nadi-Tarangini-Frontend | loginController@checkLoginCredentials | GET `/nt-admin/access-management/getAllFeatureDetails` | GET nt-admin/access-management/getAllFeatureDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:209` |
| Nadi-Tarangini-Frontend | loginController@getAllRoles | GET `/public/allRoles` | GET public/allRoles | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:728` |
| Nadi-Tarangini-Frontend | loginController@getUserDetailsOtpBasedLogin | GET `/nt-admin/access-management/getAllFeatureDetails` | GET nt-admin/access-management/getAllFeatureDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:589` |

## Tables (5)

- `calendar_events` (models: CalendarEvent): clinic_id, consultation_type, reception_id
- `common_data` (models: CommonData): created_at, data, id, label, updated_at
- `master_contents` (models: MasterContents): content, create_date, id, is_active, last_modified_on, month_number, title, type, week_number
- `medical_report` (models: MedicalReport): city, country, external_visit_id, field_id_1, ip_address, mark_on_image_url, panchakarma_recom, reception_id, recommendations, state, try_count, user_nadi_capture_type, yoga_recom
- `user_personal_info` (models: UserPersonalInfo): allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken

## External systems

- Firebase (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:67`
- Razorpay (Nadi-Tarangini-Frontend): `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1728,1729,1730`

## Environment matrix (verbatim from atreya-docs/environments.md)

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

## Languages

Required: English, Marathi, Hindi, Czech, German, Spanish, Italian (source: references/qa-scope-rules.md).
Language files in code: Nadi-Tarangini-Frontend:resources/lang/en/auth.php, Nadi-Tarangini-Frontend:resources/lang/en/pagination.php, Nadi-Tarangini-Frontend:resources/lang/en/passwords.php, Nadi-Tarangini-Frontend:resources/lang/en/validation.php, Nadi-Tarangini-Frontend:resources/lang/en_patient.json
