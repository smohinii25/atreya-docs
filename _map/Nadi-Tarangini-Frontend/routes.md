# Routes: Nadi-Tarangini-Frontend

Built from commit `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d` by scripts/routes.sh (static parse, no PHP).

| Route file | URL prefix | Prefix from |
|---|---|---|
| `routes/api.php` | `api` | RouteServiceProvider |
| `routes/web.php` | `` | RouteServiceProvider |

**404 routes** (404 unique), 3 closures, 0 shadowed duplicates, 0 unparsed lines, 26 commented-out route lines, 0 controller files not found, 1 guarded.

| Method | URI | Controller@action | Middleware | Name | Source |
|---|---|---|---|---|---|
| GET | `/` | Closure |  |  | `routes/web.php:104` |
| POST | `activeInactiveReception` | ReceptionistController@activeInactiveReception | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:756` |
| POST | `add-aniruddha-rule` | ResearchDashboardController@addAniruddhaRule | check_research_auth_token | addAniruddhaRule | `routes/web.php:294` |
| GET | `add-appointment` | AppointmentController@addAppointment | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | addAppointment | `routes/web.php:610` |
| GET | `add-clinic` | AddClinicDetailsController@addClinicDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | addClinicDetails | `routes/web.php:582` |
| POST | `add-medicine` | MedicineController@addMedicine | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | addMedicine | `routes/web.php:645` |
| POST | `add-medicine-type` | MedicineTypeController@addMedicineType | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | addMedicineType | `routes/web.php:660` |
| GET | `add-member` | AddMemberController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | addMember | `routes/web.php:434` |
| GET | `add-patient` | AppointmentController@addPatientForAppointment | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | addPatientForAppointment | `routes/web.php:637` |
| POST | `add-pudi` | PudiController@addPudi | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | addPudi | `routes/web.php:684` |
| GET | `add-reception` | ReceptionistController@addReception | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | addReception | `routes/web.php:752` |
| POST | `add-rule` | ResearchDashboardController@addRule | check_research_auth_token | addRule | `routes/web.php:290` |
| GET | `add-self-admin` | DashboardController@addSelfAdmin | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | addSelfAdmin | `routes/web.php:397` |
| POST | `add-self-admin` | DashboardController@saveSelfAdminData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | saveSelfAdminData | `routes/web.php:399` |
| POST | `addCompany` | CompanyController@addCompany | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:669` |
| POST | `addIngredients` | IngredientsController@addIngredients | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:692` |
| POST | `addNewPrescriptionIngredient` | PrescriptionController@addNewPrescriptionIngredient | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:535` |
| GET | `address/countries` | AddressDetailsController@countries |  | address.countries | `routes/web.php:309` |
| POST | `address/lookup-pincode` | AddressDetailsController@lookupPincode |  | address.lookupPincode | `routes/web.php:310` |
| POST | `admin/activeInactiveUser` | AdminDashboardController@activeInactiveUser | nt_admin_authentication | activeInactiveUser | `routes/web.php:134` |
| GET | `admin/add-question` | AdminCustomizeController@index | nt_admin_authentication | addquestion | `routes/web.php:138` |
| POST | `admin/apply-coupon` | AdminDashboardController@applyCoupon | nt_admin_authentication | applyCoupon | `routes/web.php:159` |
| POST | `admin/consultation-type-counts` | AdminDashboardController@getConsultationTypeCounts | nt_admin_authentication | admin.getConsultationTypeCounts | `routes/web.php:113` |
| POST | `admin/create-order` | AdminDashboardController@createNtOrder | nt_admin_authentication | createNtOrder | `routes/web.php:160` |
| GET | `admin/create-user` | AdminDashboardController@createUser | nt_admin_authentication | createUser | `routes/web.php:128` |
| GET | `admin/customize-question` | AdminCustomizeController@customizeQuestion | nt_admin_authentication | customizequestion | `routes/web.php:144` |
| GET | `admin/customize-report` | AdminCustomizeController@customizeReport | nt_admin_authentication | customizereport | `routes/web.php:143` |
| GET | `admin/customize-report-user-wise/{id}` | AdminCustomizeController@getCustomizeReportUserWise | nt_admin_authentication | customizeReportUserWise | `routes/web.php:149` |
| GET | `admin/dashboard` | AdminDashboardController@index | nt_admin_authentication | admin.dashboard | `routes/web.php:111` |
| GET | `admin/data-management/{id}` | AdminDashboardController@dataManagement | nt_admin_authentication | dataManagement | `routes/web.php:117` |
| GET | `admin/edit-profile/{id}` | AdminDashboardController@editProfile | nt_admin_authentication | editNtAdminProfile | `routes/web.php:115` |
| POST | `admin/get-report-pages` | AdminCustomizeController@getReportPages | nt_admin_authentication |  | `routes/web.php:140` |
| POST | `admin/get-user-wise-category-wise-customize-questions/{id}` | AdminCustomizeController@getUserWiseCategoryWiseCustomizeQuestions | nt_admin_authentication |  | `routes/web.php:153` |
| GET | `admin/get-user-wise-customize-question/{id}` | AdminCustomizeController@getUserWiseCustomizeQuestion | nt_admin_authentication | getUserWiseCategoryWiseCustomizeQuestions | `routes/web.php:152` |
| POST | `admin/get-user-wise-report-pages/{id}` | AdminCustomizeController@getUserWiseReportPages | nt_admin_authentication |  | `routes/web.php:148` |
| POST | `admin/get-users-by-role` | AdminDashboardController@getUsersByRole | nt_admin_authentication | admin.getUsersByRole | `routes/web.php:112` |
| POST | `admin/getCategoryWiseCustomizeQuestions` | CustomizeController@getCategoryWiseCustomizeQuestions | nt_admin_authentication | getCategoryWiseCustomizeQuestions | `routes/web.php:145` |
| POST | `admin/getCategoryWiseCustomizeQuestionsList` | CustomizeController@getCategoryWiseCustomizeQuestionsList | nt_admin_authentication | getCategoryWiseCustomizeQuestionsList | `routes/web.php:146` |
| GET | `admin/getPlanDetails` | AdminDashboardController@getPlanDetails | nt_admin_authentication | getPlanDetails | `routes/web.php:158` |
| GET | `admin/getPlanStatus` | AdminDashboardController@getPlanStatus | nt_admin_authentication | getPlanStatus | `routes/web.php:162` |
| POST | `admin/getUserClinicDetails` | AdminDashboardController@getUserClinicDetails | nt_admin_authentication | getUserClinicDetails | `routes/web.php:136` |
| POST | `admin/getUserDetails` | AdminDashboardController@getUserDetails | nt_admin_authentication | getUserDetails | `routes/web.php:135` |
| GET | `admin/patient-list/{id}` | AdminDashboardController@userPatientList | nt_admin_authentication | admin.userPatientList | `routes/web.php:118` |
| POST | `admin/patient-list/{id}/fetch` | AdminDashboardController@fetchUserPatientList | nt_admin_authentication | admin.userPatientList.fetch | `routes/web.php:119` |
| POST | `admin/patient-list/{id}/last-visit-info` | AdminDashboardController@fetchUserLastVisitInformation | nt_admin_authentication | admin.userPatientList.lastVisitInfo | `routes/web.php:121` |
| GET | `admin/patient-list/{id}/previous-visits/{patientId}` | AdminDashboardController@userPreviousVisits | nt_admin_authentication | admin.userPreviousVisits | `routes/web.php:122` |
| POST | `admin/patient-list/{id}/search` | AdminDashboardController@searchUserPatientList | nt_admin_authentication | admin.userPatientList.search | `routes/web.php:120` |
| GET | `admin/payment-invoices` | AdminDashboardController@paymentInvoices | nt_admin_authentication | paymentInvoices | `routes/web.php:163` |
| GET | `admin/payment-invoices/list` | AdminDashboardController@fetchPaymentInvoices | nt_admin_authentication | paymentInvoices.fetch | `routes/web.php:164` |
| GET | `admin/permissions/{id}` | AdminDashboardController@editPermissions | nt_admin_authentication | editPermissions | `routes/web.php:132` |
| POST | `admin/questionstore` | AdminCustomizeController@questionstore | nt_admin_authentication | addquestionstore | `routes/web.php:139` |
| POST | `admin/report/viewAllReport` | AdminDashboardController@viewAllReport | nt_admin_authentication | admin.report.viewAllReport | `routes/web.php:124` |
| POST | `admin/report/viewVisitReport` | AdminDashboardController@viewVisitReport | nt_admin_authentication | admin.report.viewVisitReport | `routes/web.php:125` |
| POST | `admin/saveUser` | AdminDashboardController@saveUser | nt_admin_authentication | saveUser | `routes/web.php:129` |
| GET | `admin/switchToAdminToDoctor` | DashboardController@switchToDoctor | nt_admin_authentication | switchToDoctor | `routes/web.php:156` |
| GET | `admin/update-password/{id}` | AdminDashboardController@updatePassword | nt_admin_authentication | updateUserPasswordForm | `routes/web.php:130` |
| POST | `admin/updateCategory` | AdminCustomizeController@updateCategory | nt_admin_authentication |  | `routes/web.php:141` |
| POST | `admin/updatePermissions` | AdminDashboardController@updatePermissions | nt_admin_authentication | updatePermissions | `routes/web.php:133` |
| POST | `admin/updateProfile` | AdminDashboardController@updateProfile | nt_admin_authentication | updateProfile | `routes/web.php:116` |
| POST | `admin/updateReportPages` | AdminCustomizeController@updateReportPages | nt_admin_authentication |  | `routes/web.php:142` |
| POST | `admin/updateUserDataManagement` | AdminDashboardController@updateUserDataManagement | nt_admin_authentication | updateUserDataManagement | `routes/web.php:127` |
| POST | `admin/updateUserPassword` | AdminDashboardController@updateUserPassword | nt_admin_authentication | updateUserPassword | `routes/web.php:131` |
| POST | `admin/updateUserWiseCategoryQustions` | AdminCustomizeController@updateUserWiseCategoryQustions | nt_admin_authentication |  | `routes/web.php:154` |
| POST | `admin/updateUserWiseRportPages` | AdminCustomizeController@updateUserWiseRportPages | nt_admin_authentication |  | `routes/web.php:150` |
| GET | `admin/user-and-teams` | AdminDashboardController@userAndTeams | nt_admin_authentication | userAndTeams | `routes/web.php:114` |
| POST | `admin/verifyTransaction` | AdminDashboardController@verifyTransaction | nt_admin_authentication | verifyTransaction | `routes/web.php:161` |
| POST | `analyzeExternalNadiData` | ExternalNadiController@analyzeExternalNadiData |  | analyzeExternalNadiData | `routes/web.php:100` |
| GET | `api/user` | Closure | auth:sanctum |  | `routes/api.php:18` |
| POST | `api/webhooks/razorpay/sc` | SamvitPaymentBridgeController@handleRazorpayWebhook (guarded) |  |  | `routes/api.php:23` |
| GET | `api/welcome-tour` | DashboardController@getScreenWelcomeTour | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | welcomeTour.screen | `routes/web.php:358` |
| POST | `api/welcome-tour/complete` | DashboardController@completeScreenWelcomeTour | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | welcomeTour.complete | `routes/web.php:359` |
| GET | `appointment-history` | AppointmentController@appointmentHistory | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | appointmentHistory | `routes/web.php:631` |
| GET | `appointment-list` | AppointmentController@appointmentList | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | appointmentList | `routes/web.php:629` |
| GET | `arogya-darshika` | ReportController@getArogyaDarshika | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getArogyaDarshika | `routes/web.php:506` |
| POST | `callPatientList` | PatientListController@callPatientList | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:403` |
| GET | `change-password` | ChangePasswordController@changePassword | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | changePassword | `routes/web.php:602` |
| POST | `checkDoctorMobileNo` | NewSignUpController@checkDoctorMobileNo |  |  | `routes/web.php:331` |
| POST | `checkDoctorUsername` | NewSignUpController@checkDoctorUsername |  |  | `routes/web.php:332` |
| POST | `checkForgotPassword` | forgotPasswordController@checkForgotPassword |  | check.forgot | `routes/web.php:318` |
| POST | `checkLoginCredintial` | loginController@checkLoginCredentials |  | check.login | `routes/web.php:316` |
| POST | `checkResearchLogin` | ResearchDashboardController@checkResearchLoginCredentials |  | check.researchLogin | `routes/web.php:80` |
| POST | `checkValidationsLinkDevice` | NewSignUpController@checkValidationsLinkDevice |  |  | `routes/web.php:333` |
| GET | `checkout` | DashboardController@checkout | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | checkout | `routes/web.php:744` |
| GET | `clinic` | ClinicListController@clinicList | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | clinicList | `routes/web.php:580` |
| GET | `company` | CompanyController@company | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | company | `routes/web.php:667` |
| GET | `corporate/patientDashboard` | PatientDashboardManagementController@corporatePatientDashboard | check_client_auth_token, corporate_patient_check_auth | corporatePatientDashboard | `routes/web.php:806` |
| POST | `corporate/saveCorporatePatientsPrakrutiQuestions` | PatientDashboardManagementController@saveCorporatePatientsPrakrutiQuestions | check_client_auth_token, corporate_patient_check_auth | saveCorporatePatientsPrakrutiQuestions | `routes/web.php:807` |
| POST | `createReception` | ReceptionistController@createReception | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:753` |
| GET | `currentUserAccessibleUsersWithLocations` | AppointmentController@currentUserAccessibleUsersWithLocations | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | currentUserAccessibleUsersWithLocations | `routes/web.php:612` |
| GET | `customize` | CustomizeController@customize | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | customize | `routes/web.php:450` |
| GET | `dashboard` | DashboardController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | dashboard | `routes/web.php:357` |
| POST | `delete-account` | DashboardController@deleteUserAccount | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | deleteUserAccount | `routes/web.php:702` |
| GET | `delete-rule/{id}` | ResearchDashboardController@deleteRule | check_research_auth_token | deleteRule | `routes/web.php:292` |
| DELETE | `deleteAppointment/{appointmentId}` | AppointmentController@deleteAppointment | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | deleteAppointment | `routes/web.php:633` |
| DELETE | `deleteClinic/{id}` | ClinicListController@deleteClinic | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | deleteClinic | `routes/web.php:600` |
| DELETE | `deleteCompany/{companyId}` | CompanyController@deleteCompany | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | deleteCompany | `routes/web.php:675` |
| DELETE | `deleteIngredient/{ingredientId}` | IngredientsController@deleteIngredient | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | deleteIngredient | `routes/web.php:698` |
| DELETE | `deleteMedicine/{medicalPrescriptionId}` | PrescriptionController@deleteMedicine | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | deleteMedicine | `routes/web.php:537` |
| DELETE | `deleteMedicineinventory/{medicineId}` | MedicineController@deleteMedicineinventory | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | deleteMedicine | `routes/web.php:653` |
| DELETE | `deletePatient/{id}` | PatientListController@deletePatient | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | deletePatient | `routes/web.php:430` |
| DELETE | `deletePudi/{pudiId}` | PudiController@deletePudi | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | deletePudi | `routes/web.php:682` |
| DELETE | `deleteReceptionist/{receptionistId}` | ReceptionistController@deleteReception | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | deleteReception | `routes/web.php:759` |
| DELETE | `deleteReport/{medicalId}/{patientId}` | PreviousVisitsController@deleteReport | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | deleteReport | `routes/web.php:432` |
| GET | `design-form/add` | DesignFormController@addFormDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | addFormDetails | `routes/web.php:707` |
| GET | `design-form/customize-tab` | DesignFormController@customizeTabForm | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | customizeTabForm | `routes/web.php:717` |
| GET | `design-form/edit` | DesignFormController@editForm | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editForm | `routes/web.php:706` |
| GET | `design-form/edit-details` | DesignFormController@editFormDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editFormDetails | `routes/web.php:705` |
| POST | `design-form/getReorderData` | DesignFormController@getReorderData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:711` |
| POST | `design-form/getSymptomInfo` | DesignFormController@getSymptomInfo | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:708` |
| GET | `design-form/keywords` | DesignFormController@selectKeywords | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | selectKeywords | `routes/web.php:714` |
| GET | `design-form/reorder` | DesignFormController@reorderForm | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | reorderForm | `routes/web.php:710` |
| POST | `design-form/updateKeywordsData` | DesignFormController@updateKeywordsData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:715` |
| POST | `design-form/updateReorderData` | DesignFormController@updateReorderData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:712` |
| GET | `diet` | DietController@skipDiet | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | skipDiet | `routes/web.php:510` |
| GET | `diet-lifestyle` | DietController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | diet | `routes/web.php:508` |
| GET | `downloadRutucharya` | DownloadRutucharyaController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | downloadRutucharya | `routes/web.php:448` |
| POST | `edit-aniruddha-rule` | ResearchDashboardController@editAniruddhaRule | check_research_auth_token | editAniruddhaRule | `routes/web.php:295` |
| GET | `edit-appointment/{appointmentId}` | AppointmentController@editAppointment | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editAppointment | `routes/web.php:618` |
| GET | `edit-clinic/{id}` | EditClinicDetailsController@editClinicDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editClinicDetails | `routes/web.php:588` |
| GET | `edit-company/{id}` | CompanyController@editCompany | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editCompany | `routes/web.php:671` |
| GET | `edit-ingredient/{ingredientId}` | IngredientsController@editIngredient | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editIngredient | `routes/web.php:694` |
| GET | `edit-medicine/{medicineId}` | MedicineController@editMedicine | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editMedicine | `routes/web.php:647` |
| GET | `edit-member/{id}` | EditMemberController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editMember | `routes/web.php:440` |
| GET | `edit-payment` | EditDoctorDetailsController@editPaymentDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editPaymentDetails | `routes/web.php:578` |
| GET | `edit-pudi/{pudiId}` | PudiController@editPudi | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editPudi | `routes/web.php:680` |
| GET | `edit-reception/{id}` | ReceptionistController@editReception | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editReception | `routes/web.php:754` |
| POST | `edit-rule` | ResearchDashboardController@editRule | check_research_auth_token | editRule | `routes/web.php:291` |
| GET | `edit-supplement/{medicineId}` | MedicineController@editSupplement | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editSupplement | `routes/web.php:649` |
| POST | `editFcmToken` | loginController@editFcmToken | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editFcmToken | `routes/web.php:367` |
| POST | `editMedicine/{medicalPrescriptionId}` | PrescriptionController@editMedicine | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editMedicine | `routes/web.php:539` |
| GET | `editprofile` | EditDoctorDetailsController@editDoctorProfile | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editDoctorProfile | `routes/web.php:576` |
| GET | `error` | UnauthorizedController@error |  |  | `routes/web.php:352` |
| GET | `error-400` | UnauthorizedController@error400 |  |  | `routes/web.php:345` |
| GET | `error-401` | UnauthorizedController@error401 |  |  | `routes/web.php:346` |
| GET | `error-403` | UnauthorizedController@error403 |  |  | `routes/web.php:347` |
| GET | `error-404` | UnauthorizedController@error404 |  |  | `routes/web.php:348` |
| GET | `error-500` | UnauthorizedController@error500 |  |  | `routes/web.php:349` |
| GET | `error-503` | UnauthorizedController@error503 |  |  | `routes/web.php:350` |
| GET | `error-504` | UnauthorizedController@error504 |  |  | `routes/web.php:351` |
| GET | `fee-details` | FeeDetailsController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | feeDetails | `routes/web.php:543` |
| POST | `fee-details/report-wise-languages` | FeeDetailsController@getReportWiseLanguages | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | feeDetails.reportWiseLanguages | `routes/web.php:545` |
| GET | `fetch-single-appointment/{appointmentId}` | AppointmentController@fetchSingleAppointment | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | fetchSingleAppointment | `routes/web.php:620` |
| POST | `fetchMarkOnImageData` | MarkOnImageController@fetchMarkOnImageData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:492` |
| GET | `forgotPassword` | forgotPasswordController@forgotPassword |  | forgotPassword | `routes/web.php:317` |
| POST | `freeTrial` | DashboardController@freeTrial | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:446` |
| GET | `get-all-clinic-list` | DashboardController@getAllClinicList | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getAllClinicList | `routes/web.php:734` |
| GET | `get-all-roles` | loginController@getAllRoles |  | getAllRoles | `routes/web.php:92` |
| GET | `get-default-clinic-details` | DashboardController@getDefaultClinicDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getDefaultClinicDetails | `routes/web.php:735` |
| GET | `get-languages-for-reports` | DashboardController@getLanguagesForReports | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getLanguagesForReports | `routes/web.php:733` |
| POST | `getAccessUserWisePatientList` | AppointmentController@getAccessUserWisePatientList | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getAccessUserWisePatientList | `routes/web.php:614` |
| POST | `getLastVisitInformation` | PatientListController@getLastVisitInformation | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:473` |
| POST | `getLastVisitMandatoryQuesitons` | PatientListController@getLastVisitQuestions | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:472` |
| POST | `getLastVisitQuestions` | PatientListController@getLastVisitQuestions | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:471` |
| POST | `getManualNadiQuestions` | LiveNadiController@getManualNadiQuestions | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:412` |
| POST | `getMedicalId` | PatientListController@fetchNewMedicalIdV2 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | fetchNewMedicalId | `routes/web.php:460` |
| POST | `getMedicalIdntlite` | PatientListController@fetchNewMedicalIdV2NtLite | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | fetchNewMedicalIdV2NtLite | `routes/web.php:462` |
| POST | `getMedicineNamesRespectToType` | PrescriptionController@getMedicineNamesRespectToType | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:523` |
| GET | `getPatient` | PatientListController@getPatientListData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:419` |
| GET | `getPlanStatus` | DashboardController@getPlanStatus | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | dashboard.getPlanStatus | `routes/web.php:364` |
| POST | `getPrakrutiData` | PrakrutiQuestionsController@getPrakrutiDataOnList | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:468` |
| POST | `getPrakrutiDataForNewPatient` | PrakrutiQuestionsController@getPrakrutiDataForNewPatient | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:469` |
| GET | `getQuantity/{medicineTypeId}` | MedicineController@getQuantity | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getQuantity | `routes/web.php:655` |
| GET | `getReleaseDetails` | DashboardController@getReleaseDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | dashboard.releaseDetails | `routes/web.php:363` |
| POST | `getUserCurrentSummary` | DashboardController@getUserCurrentSummary | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | dashboard.currentSummary | `routes/web.php:365` |
| POST | `getUserCustomizeSummary` | DashboardController@getUserCustomizeSummary | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | dashboard.customizeSummary | `routes/web.php:366` |
| POST | `getUserDetailsOtpBasedLogin` | loginController@getUserDetailsOtpBasedLogin |  | getUserDetailsOtpBasedLogin | `routes/web.php:90` |
| POST | `getVikrutiData` | VikrutiController@getVikrutiData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:410` |
| POST | `getVikrutiWiseDiet` | DietController@getVikrutiWiseDietV2 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getVikrutiWiseDiet | `routes/web.php:513` |
| GET | `getWelcomeTourSteps/{page?}` | DashboardController@getWelcomeTourSteps | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | dashboard.welcomeTourSteps | `routes/web.php:362` |
| GET | `help` | HelpController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | help | `routes/web.php:394` |
| GET | `help-center` | HelpController@helpCenter | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | helpCenter | `routes/web.php:395` |
| GET | `ingredient` | IngredientsController@ingredient | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | ingredient | `routes/web.php:690` |
| GET | `inventory` | InventoryController@inventory | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | inventory | `routes/web.php:661` |
| GET | `invoice/{invoiceId}` | DashboardController@invoice | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | invoice | `routes/web.php:748` |
| POST | `linkDeviceAfterValidation` | NewSignUpController@linkDeviceAfterValidation |  |  | `routes/web.php:334` |
| GET | `linked-device` | DashboardController@linkedDevice | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | linkedDevice | `routes/web.php:737` |
| GET | `login` | loginController@login |  | login | `routes/web.php:313` |
| GET | `logout` | LoginController@logout |  | logout | `routes/web.php:342` |
| POST | `logout` | LoginController@logout |  | logout | `routes/web.php:342` |
| POST | `makeDefaultClinic` | MarkClinicDefaultController@makeDefaultClinic | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:586` |
| GET | `medical-assessment` | LiveNadiController@liveNadi | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | liveNadi | `routes/web.php:497` |
| GET | `medical-assessment-v3` | MedicalAssessmentV3Controller@liveNadiV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | liveNadiV3 | `routes/web.php:554` |
| POST | `medical-assessment-v3/diet/current` | MedicalAssessmentV3Controller@getCurrentVisitInputForDietV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | medicalAssessmentV3.diet.current | `routes/web.php:559` |
| POST | `medical-assessment-v3/diet/generate` | MedicalAssessmentV3Controller@generateWeeklyDietV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | medicalAssessmentV3.diet.generate | `routes/web.php:560` |
| POST | `medical-assessment-v3/diet/update` | MedicalAssessmentV3Controller@updateWeeklyDietV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | medicalAssessmentV3.diet.update | `routes/web.php:561` |
| POST | `medical-assessment-v3/set-state` | MedicalAssessmentV3Controller@setMedicalAssessmentV3State | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | medicalAssessmentV3.setState | `routes/web.php:558` |
| POST | `medical-assessment-v3/yoga/current` | MedicalAssessmentV3Controller@getCurrentVisitInputForYogaV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | medicalAssessmentV3.yoga.current | `routes/web.php:563` |
| POST | `medical-assessment-v3/yoga/update` | MedicalAssessmentV3Controller@updateWeeklyYogaV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | medicalAssessmentV3.yoga.update | `routes/web.php:564` |
| GET | `medicine` | MedicineController@medicine | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | medicine | `routes/web.php:643` |
| GET | `medicine-type` | MedicineTypeController@medicineType | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | medicineType | `routes/web.php:658` |
| POST | `medicineuploadfile` | InventoryController@medicineuploadfile | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | ingredientupload | `routes/web.php:663` |
| GET | `member-progress` | DashboardController@patientProgress | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | patientProgress | `routes/web.php:731` |
| GET | `member-report` | DashboardController@patientReport | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | patientReport | `routes/web.php:732` |
| GET | `nadi-image` | MarkOnImageController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | markOnImage | `routes/web.php:488` |
| GET | `nadi-keywords` | ManualNadiKeywordsController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | manualNadiKeywords | `routes/web.php:484` |
| POST | `notification/{id}` | NotificationController@readNotification | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:608` |
| GET | `notifications` | NotificationController@notifications | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | notifications | `routes/web.php:606` |
| GET | `nt-capture` | ExternalNadiController@externalAssessment |  | externalAssessment | `routes/web.php:98` |
| POST | `nt-chatbot/{endpoint}` | NtChatbotProxyController@forward |  | ntChatbot.forward | `routes/web.php:94` |
| POST | `nt-lite/callPatientList` | NtLiteDashboardController@callPatientList | nt_lite_auth, ensure_nt_lite_dashboard_mode |  | `routes/web.php:765` |
| POST | `nt-lite/checkMobileNo` | NtLiteSignUpController@checkMobileNo |  |  | `routes/web.php:339` |
| POST | `nt-lite/checkUsername` | NtLiteSignUpController@checkUsername |  |  | `routes/web.php:340` |
| GET | `nt-lite/dashboard` | NtLiteDashboardController@index | nt_lite_auth, ensure_nt_lite_dashboard_mode | nt-lite.dashboard | `routes/web.php:764` |
| GET | `nt-lite/edit-payment` | NtLiteDashboardController@editPayment | nt_lite_auth, ensure_nt_lite_dashboard_mode | nt-lite.editPayment | `routes/web.php:772` |
| GET | `nt-lite/getPlanStatus` | NtLiteDashboardController@getPlanStatus | nt_lite_auth, ensure_nt_lite_dashboard_mode | nt-lite.getPlanStatus | `routes/web.php:773` |
| POST | `nt-lite/getVisitPrescription` | NtLiteDashboardController@getVisitPrescription | nt_lite_auth, ensure_nt_lite_dashboard_mode | nt-lite.getVisitPrescription | `routes/web.php:770` |
| POST | `nt-lite/getVisitReports` | NtLiteDashboardController@getVisitReports | nt_lite_auth, ensure_nt_lite_dashboard_mode | nt-lite.getVisitReports | `routes/web.php:769` |
| GET | `nt-lite/live-nadi` | NtLiteLiveNadiController@index | nt_lite_auth, ensure_nt_lite_dashboard_mode | nt-lite.liveNadi | `routes/web.php:768` |
| GET | `nt-lite/logout` | LoginController@logout |  | nt-lite.logout | `routes/web.php:341` |
| POST | `nt-lite/logout` | LoginController@logout |  | nt-lite.logout | `routes/web.php:341` |
| GET | `nt-lite/previousVisits/{id}` | NtLiteDashboardController@previousVisits | nt_lite_auth, ensure_nt_lite_dashboard_mode | nt-lite.previousVisits | `routes/web.php:767` |
| GET | `nt-lite/search-patients` | NtLiteDashboardController@searchPatients | nt_lite_auth, ensure_nt_lite_dashboard_mode | nt-lite.search.patients | `routes/web.php:766` |
| GET | `nt-lite/settings` | NtLiteDashboardController@settings | nt_lite_auth, ensure_nt_lite_dashboard_mode | nt-lite.settings | `routes/web.php:771` |
| GET | `nt-lite/sign-up` | NtLiteSignUpController@showSignUp |  | ntLiteSignUp | `routes/web.php:337` |
| POST | `nt-lite/submitSignUp` | NtLiteSignUpController@submitSignUp |  |  | `routes/web.php:338` |
| GET | `nt-map` | HelpController@collegeDashboard | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | collegeDashboardNew | `routes/web.php:369` |
| GET | `nt-report` | ReportController@getNtReport | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getNtReport | `routes/web.php:504` |
| GET | `patient/ask-queries` | PatientDashboardController@askQueries | check_client_auth_token | askQueries | `routes/web.php:784` |
| GET | `patient/daily-diet-lifestyle/{parameterName}` | PatientDashboardController@dailyDietLifestyle | check_client_auth_token | dailyDietLifestyle | `routes/web.php:794` |
| GET | `patient/dashboard` | PatientDashboardController@index | check_client_auth_token | patientDashboard | `routes/web.php:780` |
| GET | `patient/data-consent` | PatientDashboardController@dataConsent | check_client_auth_token | dataConsent | `routes/web.php:790` |
| POST | `patient/delete-account` | PatientDashboardController@deleteClientAccount | check_client_auth_token | deleteClientAccount | `routes/web.php:793` |
| DELETE | `patient/deletePatientReport/{id}` | PatientVisitController@deletePatientReport | check_client_auth_token | deletePatientReport | `routes/web.php:782` |
| GET | `patient/edit` | PatientDashboardController@editProfile | check_client_auth_token | editProfile | `routes/web.php:787` |
| POST | `patient/report/viewAllReports` | PatientDashboardController@patientViewAllReports | check_client_auth_token |  | `routes/web.php:800` |
| POST | `patient/report/viewSwasthyaDarshika` | PatientDashboardController@patientViewSwasthyaDarshika | check_client_auth_token |  | `routes/web.php:798` |
| POST | `patient/report/viewVisitReport` | PatientDashboardController@patientViewVisitReport | check_client_auth_token |  | `routes/web.php:799` |
| GET | `patient/request-appointment` | RequestAppointmentController@requestAppointment | check_client_auth_token | requestAppointment | `routes/web.php:783` |
| POST | `patient/saveQueries` | PatientDashboardController@saveQueries | check_client_auth_token |  | `routes/web.php:785` |
| POST | `patient/updateConsentData` | PatientDashboardController@updateConsentData | check_client_auth_token |  | `routes/web.php:791` |
| POST | `patient/updateProfileData` | PatientDashboardController@updateProfileData | check_client_auth_token |  | `routes/web.php:788` |
| GET | `patient/visits` | PatientVisitController@visitHistory | check_client_auth_token | visitHistory | `routes/web.php:781` |
| GET | `patientlist` | PatientListController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | patientlist | `routes/web.php:402` |
| GET | `prakruti` | PrakrutiQuestionsController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | prakruti | `routes/web.php:466` |
| GET | `prescription` | PrescriptionController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | prescription | `routes/web.php:521` |
| GET | `previousVisits/{id}` | PreviousVisitsController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | previousVisits | `routes/web.php:425` |
| POST | `previousVisitsSymptomDetails` | VikrutiController@getSymptomHistory | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | patient.getSymptomHistory | `routes/web.php:414` |
| GET | `profile` | EditDoctorDetailsController@editDoctorDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | editDoctorDetails | `routes/web.php:574` |
| GET | `pudi` | PudiController@pudi | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | pudi | `routes/web.php:678` |
| GET | `queries` | DashboardController@patientQueries | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | patientQueries | `routes/web.php:738` |
| GET | `reception` | ReceptionistController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | receptionistList | `routes/web.php:751` |
| GET | `region-restricted` | UnauthorizedController@regionRestricted |  | regionRestricted | `routes/web.php:315` |
| POST | `report/viewAllReport` | ReportController@viewAllReportV2 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | report.viewAllReport | `routes/web.php:722` |
| POST | `report/viewArogyaDarshika` | ReportController@viewArogyaDarshika | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:725` |
| POST | `report/viewNTReport` | ReportController@viewNTReport | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:724` |
| POST | `report/viewSpaReport` | ReportController@viewSpaReport | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:727` |
| POST | `report/viewVisitReport` | ReportController@viewVisitReport | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:726` |
| POST | `report/viewYogaReport` | ReportController@viewYogaReport | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:728` |
| GET | `research-dashboard/college-dashboard` | HelpController@collegeDashboard | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | collegeDashboard | `routes/web.php:376` |
| POST | `research-dashboard/download-nadi-file-data` | HelpController@downloadNadiFileData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | downloadNadiFileData | `routes/web.php:382` |
| POST | `research-dashboard/fetch-patient-visits` | HelpController@fetchPatientVisits | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | fetchPatientVisits | `routes/web.php:380` |
| POST | `research-dashboard/get-labels-using-medicalid` | HelpController@getLabelUsingMedicalId | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getLabelUsingMedicalId | `routes/web.php:383` |
| POST | `research-dashboard/get-nadi-analysis-2` | HelpController@getNadiAnalysis2Data | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | fetchNadiAnalysis2Data | `routes/web.php:387` |
| POST | `research-dashboard/get-nadi-analysis2-data` | HelpController@getNadiAnalysis2Data | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getNadiAnalysis2Data | `routes/web.php:384` |
| POST | `research-dashboard/get-ten-seconds-nadidata` | HelpController@getTenSecondsNadiData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getTenSecondsNadiData | `routes/web.php:381` |
| GET | `research-dashboard/nadi-analysis-1` | HelpController@nadiAnalysis1 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | researchAnalytics1 | `routes/web.php:379` |
| GET | `research-dashboard/nadi-analysis-2` | HelpController@nadiAnalysis2 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | researchAnalytics2 | `routes/web.php:386` |
| GET | `research-dashboard/nadi-tarangini-map` | HelpController@nadiTaranginiMap | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | nadiTaranginiMap | `routes/web.php:375` |
| GET | `research-dashboard/reports` | HelpController@nadiTaranginiMap | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | researchReports | `routes/web.php:388` |
| GET | `research-dashboard/research-dashboard-home` | HelpController@homePage | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | researchDashboardHome | `routes/web.php:373` |
| GET | `research-diet` | ResearchDashboardController@researchTestDiet |  | researchTestDiet | `routes/web.php:102` |
| GET | `researchDashboard` | ResearchDashboardController@researchDashboard | check_research_auth_token | researchDashboard | `routes/web.php:298` |
| POST | `researchDashboard/addNewCommonJson` | ResearchDashboardController@addNewCommonJson | check_research_auth_token |  | `routes/web.php:208` |
| POST | `researchDashboard/addNewDayName` | ResearchDashboardController@addNewDayName | check_research_auth_token |  | `routes/web.php:201` |
| POST | `researchDashboard/addNewExerciseCategory` | ResearchDashboardController@addNewExerciseCategory | check_research_auth_token |  | `routes/web.php:222` |
| POST | `researchDashboard/addNewExerciseTag` | ResearchDashboardController@addNewExerciseTag | check_research_auth_token |  | `routes/web.php:229` |
| POST | `researchDashboard/addNewMealCategory` | ResearchDashboardController@addNewMealCategory | check_research_auth_token |  | `routes/web.php:194` |
| POST | `researchDashboard/addNewMusicLibraryData` | ResearchDashboardController@addNewMusicLibraryData | check_research_auth_token | addNewMusicLibraryData | `routes/web.php:243` |
| POST | `researchDashboard/addNewMusicTag` | ResearchDashboardController@addNewMusicTag | check_research_auth_token | addNewMusicTag | `routes/web.php:235` |
| POST | `researchDashboard/addNewRecipeCategory` | ResearchDashboardController@addNewRecipeCategory | check_research_auth_token | addNewRecipeCategory | `routes/web.php:280` |
| POST | `researchDashboard/addNewRecipePreference` | ResearchDashboardController@addNewRecipePreference | check_research_auth_token |  | `routes/web.php:215` |
| POST | `researchDashboard/addNewRecipeTag` | ResearchDashboardController@addNewRecipeTag | check_research_auth_token | addNewRecipeTag | `routes/web.php:271` |
| POST | `researchDashboard/addNewStateName` | ResearchDashboardController@addNewStateName | check_research_auth_token | addNewStateName | `routes/web.php:262` |
| POST | `researchDashboard/addNewYogaCategory` | ResearchDashboardController@addNewYogaCategory | check_research_auth_token | addNewYogaCategory | `routes/web.php:250` |
| POST | `researchDashboard/addNewYogaJsonData` | ResearchDashboardController@addNewYogaJsonData | check_research_auth_token | addNewYogaJsonData | `routes/web.php:257` |
| GET | `researchDashboard/aniruddhaList` | ResearchDashboardController@getAllAniruddhaRule | check_research_auth_token | aniruddhaList | `routes/web.php:185` |
| GET | `researchDashboard/commonJson` | ResearchDashboardController@getAllCommonJsonData | check_research_auth_token | commonJson | `routes/web.php:205` |
| GET | `researchDashboard/criteriaList` | ResearchDashboardController@getAllRules | check_research_auth_token | criteriaList | `routes/web.php:183` |
| GET | `researchDashboard/dayNames` | ResearchDashboardController@getAllDayNames | check_research_auth_token | dayNames | `routes/web.php:198` |
| DELETE | `researchDashboard/delete-aniruddha-rule/{id}` | ResearchDashboardController@deleteAniruddhaRule | check_research_auth_token | deleteAniruddhaRule | `routes/web.php:181` |
| DELETE | `researchDashboard/delete-rule/{id}` | ResearchDashboardController@deleteRule | check_research_auth_token | deleteRule | `routes/web.php:179` |
| DELETE | `researchDashboard/deleteCommonJson/{id}` | ResearchDashboardController@deleteCommonJson | check_research_auth_token | deleteCommonJson | `routes/web.php:206` |
| DELETE | `researchDashboard/deleteDayName/{id}` | ResearchDashboardController@deleteDayName | check_research_auth_token | deleteDayName | `routes/web.php:199` |
| DELETE | `researchDashboard/deleteExerciseCategory/{id}` | ResearchDashboardController@deleteExerciseCategory | check_research_auth_token | deleteExerciseCategory | `routes/web.php:220` |
| DELETE | `researchDashboard/deleteExerciseTag/{id}` | ResearchDashboardController@deleteExerciseTag | check_research_auth_token | deleteExerciseTag | `routes/web.php:228` |
| DELETE | `researchDashboard/deleteMealCategory/{id}` | ResearchDashboardController@deleteMealCategory | check_research_auth_token | deleteMealCategory | `routes/web.php:192` |
| DELETE | `researchDashboard/deleteMusicLibraryData/{id}` | ResearchDashboardController@deleteMusicLibraryData | check_research_auth_token | deleteMusicLibraryData | `routes/web.php:242` |
| DELETE | `researchDashboard/deleteMusicTag/{id}` | ResearchDashboardController@deleteMusicTag | check_research_auth_token | deleteMusicTag | `routes/web.php:236` |
| DELETE | `researchDashboard/deleteRecipeCategory/{id}` | ResearchDashboardController@deleteRecipeCategory | check_research_auth_token | deleteRecipeCategory | `routes/web.php:278` |
| DELETE | `researchDashboard/deleteRecipePreference/{id}` | ResearchDashboardController@deleteRecipePreference | check_research_auth_token | deleteRecipePreference | `routes/web.php:213` |
| DELETE | `researchDashboard/deleteRecipeTag/{id}` | ResearchDashboardController@deleteRecipeTag | check_research_auth_token | deleteRecipeTag | `routes/web.php:269` |
| DELETE | `researchDashboard/deleteStateName/{id}` | ResearchDashboardController@deleteStateName | check_research_auth_token | deleteStateName | `routes/web.php:263` |
| DELETE | `researchDashboard/deleteYogaCategory/{id}` | ResearchDashboardController@deleteYogaCategory | check_research_auth_token | deleteYogaCategory | `routes/web.php:249` |
| DELETE | `researchDashboard/deleteYogaJson/{id}` | ResearchDashboardController@deleteYogaJson | check_research_auth_token | deleteYogaJson | `routes/web.php:256` |
| POST | `researchDashboard/editCommonJson` | ResearchDashboardController@editCommonJson | check_research_auth_token |  | `routes/web.php:207` |
| POST | `researchDashboard/editDayName` | ResearchDashboardController@editDayName | check_research_auth_token |  | `routes/web.php:200` |
| POST | `researchDashboard/editExerciseCategory` | ResearchDashboardController@editExerciseCategory | check_research_auth_token |  | `routes/web.php:221` |
| POST | `researchDashboard/editMealCategory` | ResearchDashboardController@editMealCategory | check_research_auth_token |  | `routes/web.php:193` |
| POST | `researchDashboard/editMusicTag` | ResearchDashboardController@editMusicTag | check_research_auth_token | editMusicTag | `routes/web.php:234` |
| POST | `researchDashboard/editRecipePreference` | ResearchDashboardController@editRecipePreference | check_research_auth_token |  | `routes/web.php:214` |
| POST | `researchDashboard/editRecipeTag` | ResearchDashboardController@editRecipeTag | check_research_auth_token | editRecipeTag | `routes/web.php:270` |
| POST | `researchDashboard/editStateName` | ResearchDashboardController@editStateName | check_research_auth_token | editStateName | `routes/web.php:264` |
| POST | `researchDashboard/editYogaCategory` | ResearchDashboardController@editYogaCategory | check_research_auth_token | editYogaCategory | `routes/web.php:248` |
| GET | `researchDashboard/exerciseCategory` | ResearchDashboardController@getAllExerciseCategory | check_research_auth_token | exerciseCategory | `routes/web.php:219` |
| GET | `researchDashboard/exerciseData` | ResearchDashboardController@getAllExerciseData | check_research_auth_token | exerciseData | `routes/web.php:226` |
| POST | `researchDashboard/getAniruddhaRecipeTagging` | ResearchDashboardController@getAniruddhaRecipeTagging | check_research_auth_token | getAniruddhaRecipeTagging | `routes/web.php:282` |
| GET | `researchDashboard/getTagging` | ResearchDashboardController@getTagging | check_research_auth_token | getTagging | `routes/web.php:284` |
| GET | `researchDashboard/mealsCategory` | ResearchDashboardController@getAllMealsCategory | check_research_auth_token | mealsCategory | `routes/web.php:191` |
| GET | `researchDashboard/musicData` | ResearchDashboardController@getAllMusicData | check_research_auth_token | musicData | `routes/web.php:240` |
| GET | `researchDashboard/musicTags` | ResearchDashboardController@getAllMusicTags | check_research_auth_token | musicTags | `routes/web.php:233` |
| GET | `researchDashboard/recipeCategory` | ResearchDashboardController@getAllRecipeCategory | check_research_auth_token | recipeCategory | `routes/web.php:274` |
| GET | `researchDashboard/recipePreference` | ResearchDashboardController@getAllRecipePreferenceJsonData | check_research_auth_token | recipePreference | `routes/web.php:212` |
| GET | `researchDashboard/recipeTags` | ResearchDashboardController@recipeTags | check_research_auth_token | recipeTags | `routes/web.php:268` |
| GET | `researchDashboard/researchLogout` | ResearchDashboardController@researchLogout | check_research_auth_token | researchLogout | `routes/web.php:287` |
| POST | `researchDashboard/researchLogout` | ResearchDashboardController@researchLogout | check_research_auth_token | researchLogout | `routes/web.php:287` |
| GET | `researchDashboard/statesNames` | ResearchDashboardController@statesNames | check_research_auth_token | statesNames | `routes/web.php:261` |
| POST | `researchDashboard/updateExerciseData` | ResearchDashboardController@updateExerciseData | check_research_auth_token | updateExerciseData | `routes/web.php:227` |
| POST | `researchDashboard/updateMusicData` | ResearchDashboardController@updateMusicData | check_research_auth_token | updateMusicData | `routes/web.php:241` |
| POST | `researchDashboard/updateRecipeCategory` | ResearchDashboardController@updateRecipeCategory | check_research_auth_token | updateRecipeCategory | `routes/web.php:276` |
| POST | `researchDashboard/updateYogaJsonData` | ResearchDashboardController@updateYogaJsonData | check_research_auth_token | updateYogaJsonData | `routes/web.php:255` |
| GET | `researchDashboard/yogaCategory` | ResearchDashboardController@getAllYogaCategory | check_research_auth_token | yogaCategory | `routes/web.php:247` |
| GET | `researchDashboard/yogaData` | ResearchDashboardController@getAllYogaData | check_research_auth_token | yogaData | `routes/web.php:254` |
| GET | `researchLogin` | ResearchDashboardController@researchLogin |  | researchLogin | `routes/web.php:78` |
| POST | `resumeVisit` | PreviousVisitsController@resumeVisit | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | resumeVisit | `routes/web.php:426` |
| POST | `saveAnonymousData` | AddMemberController@saveAnonymousData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:438` |
| POST | `saveCategoryWiseVikrutiData` | VikrutiController@saveCategoryWiseVikrutiData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | report.saveCategoryWiseVikrutiData | `routes/web.php:482` |
| POST | `saveClinicDetails` | AddClinicDetailsController@saveClinicDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:584` |
| POST | `saveDietAndLifestyle` | DietController@saveDietData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | saveDietData | `routes/web.php:519` |
| POST | `saveDietAndLifestyleNew` | DietController@saveDietAndLifestyleNew | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | saveDietAndLifestyleNew | `routes/web.php:517` |
| POST | `saveDummyUsbNadiData` | LiveNadiController@saveDummyUsbNadiData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:502` |
| POST | `saveFeesData` | FeeDetailsController@saveFeesData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:547` |
| POST | `saveFeesDataAfterDiet` | DietController@saveFeesDataAfterDiet | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:551` |
| POST | `saveFeesDataWithNA` | FeeDetailsController@saveFeesDataWithNA | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | saveFeesDataWithNA | `routes/web.php:549` |
| POST | `saveKeywordsData` | ManualNadiKeywordsController@saveKeywordsData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:486` |
| POST | `saveMarkOnImageData` | MarkOnImageController@saveMarkOnImageData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:490` |
| POST | `saveMemberData` | AddMemberController@saveMemberData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:436` |
| POST | `saveNewPatientAppointment` | AppointmentController@saveNewPatientAppointment | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:626` |
| POST | `savePaymentData` | DashboardController@savePaymentData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:746` |
| POST | `savePrakrutiData` | PrakrutiQuestionsController@savePrakrutiData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:475` |
| POST | `savePrescriptionData` | PrescriptionController@savePrescriptionData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:525` |
| POST | `savePrescriptionDataV2` | PrescriptionController@savePrescriptionDataV2 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:527` |
| POST | `savePrescriptionDataV3` | PrescriptionController@savePrescriptionDataV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:529` |
| POST | `saveRecommendationData` | PrescriptionController@saveRecommendationData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:541` |
| POST | `saveUsbNadiData` | LiveNadiController@saveUsbNadiData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:501` |
| POST | `saveUsbNadiDataV3` | MedicalAssessmentV3Controller@saveUsbNadiDataV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:567` |
| POST | `saveVikrutiDataV2` | VikrutiController@saveVikrutiDataV2 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:480` |
| POST | `saveVirutiWiseDietAndLifestyle` | DietController@saveVikrutiWiseDietData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | saveVikrutiWiseDietData | `routes/web.php:515` |
| POST | `saveVisitedPatientAppointment` | AppointmentController@saveVisitedPatientAppointment | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:624` |
| GET | `sc-checkout` | SamvitPaymentBridgeController@showCheckout (guarded) |  | samvit.checkout | `routes/web.php:813` |
| POST | `sc-checkout/callback` | SamvitPaymentBridgeController@processPaymentCallback (guarded) |  | samvit.callback | `routes/web.php:814` |
| POST | `scheduledAppointments` | PatientListController@scheduledAppointments | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:639` |
| GET | `search-patients` | PatientListController@searchPatients | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | search.patients | `routes/web.php:404` |
| POST | `send-email-login-otp` | loginController@sendEmailLoginOtp |  | sendEmailLoginOtp | `routes/web.php:84` |
| POST | `send-login-otp` | loginController@sendWhatsappLoginOtp |  | sendWhatsappLoginOtp | `routes/web.php:82` |
| POST | `send-verification-otp` | OtpVerificationController@sendVerificationOtpsignup |  |  | `routes/web.php:307` |
| GET | `set-language/{lang}` | Closure |  |  | `routes/web.php:168` |
| GET | `set-permission` | ReceptionistController@setPermission | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | setPermission | `routes/web.php:757` |
| POST | `setCurrentVisitSession` | PreviousVisitsController@setCurrentVisitSession | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | setCurrentVisitSession | `routes/web.php:427` |
| GET | `sign-up` | NewSignUpController@doctorSignUp |  | doctorSignUp | `routes/web.php:325` |
| GET | `sign-up-admin` | NewSignUpController@adminSignUp |  | adminSignUp | `routes/web.php:329` |
| GET | `sign-up-college` | NewSignUpController@collegeSignUp |  | collegeSignUp | `routes/web.php:328` |
| GET | `signup` | NewSignUpController@signup |  | signup | `routes/web.php:326` |
| POST | `store-appointment-id` | AppointmentController@storeAppointmentId | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:635` |
| POST | `storeClinic` | ClinicListController@storeClinic | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:423` |
| POST | `storePatient` | PatientListController@storePatient | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:407` |
| GET | `subscription` | DashboardController@getSubscriptionData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | getSubscriptionData | `routes/web.php:421` |
| POST | `supplementuploadfile` | InventoryController@supplementuploadfile | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | supplementupload | `routes/web.php:664` |
| GET | `switchToAdmin` | DashboardController@switchToAdmin | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | switchToAdmin | `routes/web.php:392` |
| GET | `unauthorized` | UnauthorizedController@index |  | unauthorized | `routes/web.php:314` |
| POST | `update-pudi` | PudiController@updatePudi | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | updatePudi | `routes/web.php:686` |
| POST | `update-report-language` | DashboardController@updateReportLanguage | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | updateReportLanguage | `routes/web.php:736` |
| POST | `updateAppointment` | AppointmentController@updateAppointment | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | updateAppointment | `routes/web.php:622` |
| POST | `updateCompany` | CompanyController@updateCompany | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:673` |
| POST | `updateCurrentNadiTaranginiDevice` | LiveNadiController@updateCurrentNadiTaranginiDevice | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:742` |
| POST | `updateCurrentNadiTaranginiDeviceV3` | MedicalAssessmentV3Controller@updateCurrentNadiTaranginiDeviceV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:569` |
| POST | `updateIngredient` | IngredientsController@updateIngredient | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:696` |
| POST | `updateKycDetails` | EditDoctorDetailsController@updatetDoctorDetails |  |  | `routes/web.php:305` |
| POST | `updateMedicine` | MedicineController@updateMedicine | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:651` |
| POST | `updateNadiCaptureType` | LiveNadiController@updateNadiCaptureType | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | updateNadiCaptureType | `routes/web.php:499` |
| POST | `updateNadiCaptureTypeV3` | MedicalAssessmentV3Controller@updateNadiCaptureTypeV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | updateNadiCaptureTypeV3 | `routes/web.php:571` |
| POST | `updatePassword` | ChangePasswordController@updatePassword | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:604` |
| POST | `updatePaymentDetails` | EditDoctorDetailsController@updatePaymentDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:598` |
| POST | `updatePermission` | ReceptionistController@updatePermission | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | updatePermission | `routes/web.php:758` |
| POST | `updatePrescriptionDataV2` | PrescriptionController@updatePrescriptionDataV2 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:531` |
| POST | `updatePrescriptionDataV3` | PrescriptionController@updatePrescriptionDataV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:533` |
| POST | `updateReceptionist` | ReceptionistController@updateReception | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:755` |
| POST | `updateSessionNadiCaptureType` | MedicalAssessmentV3Controller@updateSessionNadiCaptureType | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | updateSessionNadiCaptureType | `routes/web.php:556` |
| POST | `updateSignUpDetails` | NewSignUpController@updateSignUpDetails |  |  | `routes/web.php:327` |
| POST | `updateTourData` | DashboardController@updateTourData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:740` |
| GET | `update_kyc` | DashboardController@updateKycDetails |  | update_kyc | `routes/web.php:304` |
| POST | `updatedClinicDetails` | EditClinicDetailsController@updatedClinicDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:590` |
| POST | `updatetDoctorDetails` | EditDoctorDetailsController@updatetDoctorDetails | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:592` |
| POST | `updatetMemberData` | EditMemberController@updatetMemberData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode |  | `routes/web.php:442` |
| POST | `uploadfile` | InventoryController@uploadfile | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | ingredient.upload | `routes/web.php:662` |
| POST | `validateAppointment` | AppointmentController@validateAppointment | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | validateAppointment | `routes/web.php:628` |
| POST | `verify-email-login-otp` | loginController@verifyEmailLoginOtp |  | verifyEmailLoginOtp | `routes/web.php:88` |
| POST | `verify-login-otp` | loginController@verifyWhatsappLoginOtp |  | verifyWhatsappLoginOtp | `routes/web.php:86` |
| POST | `verify-verification-otp` | OtpVerificationController@verifyVerificationOtpsignup |  |  | `routes/web.php:308` |
| GET | `view-appointment/{appointmentId}` | AppointmentController@viewAppointment | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | viewAppointment | `routes/web.php:616` |
| GET | `view-member/{id}` | ViewMemberController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | viewMember | `routes/web.php:444` |
| GET | `vikruti` | VikrutiController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | vikruti | `routes/web.php:477` |
| POST | `web-error-report` | WebErrorReportController@store | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | webErrorReport.store | `routes/web.php:356` |
| GET | `welcome-tour` | DashboardController@getScreenWelcomeTour | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | welcomeTour.screen.alias | `routes/web.php:360` |
| POST | `welcome-tour/complete` | DashboardController@completeScreenWelcomeTour | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | welcomeTour.complete.alias | `routes/web.php:361` |

## Unparsed

None.
