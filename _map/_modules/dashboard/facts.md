# Fact pack: dashboard (Doctor dashboard, onboarding & welcome tour)

Generated 2026-11-03 by scripts/module-facts.sh. Product nt, critical false. Every line below is from code or a human-owned doc; cite the source given.

Commits: Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`, Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`, Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d`

## Backend routes (7)

### GET getAccountData
- controller: UserStatsController@getUserAccountData (found) · route: `Ashoka-World-Backend:routes/api.php:958` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getAccountData (AddAppointmentScreen, AddMedicinePrescription, AddPatientFromAppointmentScreen, AddPatientScreen); Nadi-Tarangini-Frontend ?@?; Nadi-Tarangini-Frontend NtLiteLiveNadiController@syncAccountSettings
- errors: 404 "User not found." (`Ashoka-World-Backend:app/Http/Controllers/UserStatsController.php:196`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/UserStatsController.php:359`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/UserStatsController.php:367`)

### POST getUserCurrentSummary
- controller: AuthController@getUserSummaryV2 (found) · route: `Ashoka-World-Backend:routes/api.php:951` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getUserCurrentSummary (DashboardScreen); Nadi-Tarangini-Frontend DashboardController@getUserCurrentSummary
- errors: ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2220`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2233`)

### POST getUserCustomizeSummary
- controller: AuthController@getUserCustomizeSummary (found) · route: `Ashoka-World-Backend:routes/api.php:953` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getUserCustomizeSummary (DashboardScreen); Nadi-Tarangini-Frontend DashboardController@getUserCustomizeSummary
- errors: 400 "Type must be WEEKLY, MONTHLY or YEARLY" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2248`); 404 "Doctor not found" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2270`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2353`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2361`)

### POST getUserStatsData
- controller: UserStatsController@getUserStatsData (found) · route: `Ashoka-World-Backend:routes/api.php:955` · middleware: api, auth.token
- called by: no screen in this workspace

### POST getUserSummary
- controller: AuthController@getUserSummary (found) · route: `Ashoka-World-Backend:routes/api.php:949` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getAnanysisDataDashbord (DashboardScreen); Nadi-Tarangini-Frontend DashboardController@index (doctor_dashboard.dashboard)
- errors: ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2110`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2131`)

### GET welcome-tour
- controller: WelcomeTourController@getTourSteps (found) · route: `Ashoka-World-Backend:routes/api.php:1005` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getWelcomeTourDetails (AddPatientFromAppointmentScreen, AddPatientScreen, DashboardScreen, EditPatientScreen)
- validation: `key`: required|string|in:dashboard,prakruti_fill,add_patient,visit_report,medical_inventory,nadi_flow,live_nadi (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:23`)
- errors: 400 "Invalid parameters: " (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:30`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:42`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:53`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:61`)

### POST welcome-tour/complete
- controller: WelcomeTourController@completeTour (found) · route: `Ashoka-World-Backend:routes/api.php:1006` · middleware: api, auth.token
- called by: Nadi-Tarangini-App completeWelcomeTour (AddPatientScreen, DashboardScreen, FillPrakrutiScreen, InventoryScreen)
- validation: `key`: required|string|in:dashboard,prakruti_fill,add_patient,visit_report,medical_inventory,nadi_flow,live_nadi (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:77`); `platform`: nullable|string|in:web,mobile (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:78`)
- errors: 400 "Invalid parameters: " (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:85`); 404 "User not found." (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:96`); 403 "Action not allowed for patient role." (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:105`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:117`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:124`)

## Backend routes no screen calls

`POST getUserStatsData`

## Web routes (30)

- Nadi-Tarangini-Frontend `GET add-self-admin` → DashboardController@addSelfAdmin · `Nadi-Tarangini-Frontend:routes/web.php:397` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST add-self-admin` → DashboardController@saveSelfAdminData · `Nadi-Tarangini-Frontend:routes/web.php:399` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET admin/switchToAdminToDoctor` → DashboardController@switchToDoctor · `Nadi-Tarangini-Frontend:routes/web.php:156` · nt_admin_authentication
- Nadi-Tarangini-Frontend `GET api/welcome-tour` → DashboardController@getScreenWelcomeTour · `Nadi-Tarangini-Frontend:routes/web.php:358` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST api/welcome-tour/complete` → DashboardController@completeScreenWelcomeTour · `Nadi-Tarangini-Frontend:routes/web.php:359` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET checkout` → DashboardController@checkout · `Nadi-Tarangini-Frontend:routes/web.php:744` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET dashboard` → DashboardController@index · `Nadi-Tarangini-Frontend:routes/web.php:357` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST delete-account` → DashboardController@deleteUserAccount · `Nadi-Tarangini-Frontend:routes/web.php:702` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST freeTrial` → DashboardController@freeTrial · `Nadi-Tarangini-Frontend:routes/web.php:446` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET get-all-clinic-list` → DashboardController@getAllClinicList · `Nadi-Tarangini-Frontend:routes/web.php:734` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET get-default-clinic-details` → DashboardController@getDefaultClinicDetails · `Nadi-Tarangini-Frontend:routes/web.php:735` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET get-languages-for-reports` → DashboardController@getLanguagesForReports · `Nadi-Tarangini-Frontend:routes/web.php:733` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET getPlanStatus` → DashboardController@getPlanStatus · `Nadi-Tarangini-Frontend:routes/web.php:364` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET getReleaseDetails` → DashboardController@getReleaseDetails · `Nadi-Tarangini-Frontend:routes/web.php:363` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getUserCurrentSummary` → DashboardController@getUserCurrentSummary · `Nadi-Tarangini-Frontend:routes/web.php:365` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getUserCustomizeSummary` → DashboardController@getUserCustomizeSummary · `Nadi-Tarangini-Frontend:routes/web.php:366` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET getWelcomeTourSteps/{page?}` → DashboardController@getWelcomeTourSteps · `Nadi-Tarangini-Frontend:routes/web.php:362` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET invoice/{invoiceId}` → DashboardController@invoice · `Nadi-Tarangini-Frontend:routes/web.php:748` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET linked-device` → DashboardController@linkedDevice · `Nadi-Tarangini-Frontend:routes/web.php:737` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET member-progress` → DashboardController@patientProgress · `Nadi-Tarangini-Frontend:routes/web.php:731` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET member-report` → DashboardController@patientReport · `Nadi-Tarangini-Frontend:routes/web.php:732` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET queries` → DashboardController@patientQueries · `Nadi-Tarangini-Frontend:routes/web.php:738` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST savePaymentData` → DashboardController@savePaymentData · `Nadi-Tarangini-Frontend:routes/web.php:746` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET subscription` → DashboardController@getSubscriptionData · `Nadi-Tarangini-Frontend:routes/web.php:421` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET switchToAdmin` → DashboardController@switchToAdmin · `Nadi-Tarangini-Frontend:routes/web.php:392` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST update-report-language` → DashboardController@updateReportLanguage · `Nadi-Tarangini-Frontend:routes/web.php:736` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST updateTourData` → DashboardController@updateTourData · `Nadi-Tarangini-Frontend:routes/web.php:740` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET update_kyc` → DashboardController@updateKycDetails · `Nadi-Tarangini-Frontend:routes/web.php:304`
- Nadi-Tarangini-Frontend `GET welcome-tour` → DashboardController@getScreenWelcomeTour · `Nadi-Tarangini-Frontend:routes/web.php:360` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST welcome-tour/complete` → DashboardController@completeScreenWelcomeTour · `Nadi-Tarangini-Frontend:routes/web.php:361` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode

## Screens (10)

- Nadi-Tarangini-App **DashboardScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/dashboard/view/dashboard_screen.dart` · route /dashboardScreen · goes to /addAppointmentScreen, /addPatientScreen, /appointmentListScreen, /assessmentScreen, /drawerMenu, /notificationScreen, /patientScreen, /reportScreen
- Nadi-Tarangini-App **GeoRestrictedScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/dashboard/view/geo_restricted_screen.dart` · route /geoRestrictedScreen
- Nadi-Tarangini-App **OnboardingScreen** `Nadi-Tarangini-App:lib/on_boarding/on_boarding_screen.dart` · route /onBoardingScreen · goes to /loginScreen
- Nadi-Tarangini-App **SplashScreen** `Nadi-Tarangini-App:lib/splash_screen.dart` · route / · goes to /dashboardScreen, /geoRestrictedScreen, /kycScreen, /languageScreen, /loginScreen, /onBoardingScreen, /reportScreenPatient
- Nadi-Tarangini-Frontend **add_self_admin** `Nadi-Tarangini-Frontend:resources/views/add_self_admin.blade.php` · route GET add-self-admin · rendered by DashboardController@addSelfAdmin
- Nadi-Tarangini-Frontend **doctor_dashboard.dashboard** `Nadi-Tarangini-Frontend:resources/views/doctor_dashboard/dashboard.blade.php` · route GET dashboard · rendered by DashboardController@index · goes to GET add-appointment, GET add-member, GET appointment-list, GET edit-member/{id}, GET patientlist, GET previousVisits/{id}, POST getUserCurrentSummary, POST getUserCustomizeSummary
- Nadi-Tarangini-Frontend **errors.404** `Nadi-Tarangini-Frontend:resources/views/errors/404.blade.php` · route GET error-404, GET invoice/{invoiceId} · rendered by DashboardController@invoice, UnauthorizedController@error404
- Nadi-Tarangini-Frontend **my_account.update_kyc** `Nadi-Tarangini-Frontend:resources/views/my_account/update_kyc.blade.php` · route GET update_kyc · rendered by DashboardController@updateKycDetails
- Nadi-Tarangini-Frontend **subscription.checkout** `Nadi-Tarangini-Frontend:resources/views/subscription/checkout.blade.php` · route GET checkout · rendered by DashboardController@checkout · goes to /, GET checkout, GET subscription
- Nadi-Tarangini-Frontend **subscription_plans** `Nadi-Tarangini-Frontend:resources/views/subscription_plans.blade.php` · route GET subscription · rendered by DashboardController@getSubscriptionData

## API calls (69)

| Client | Caller | Call | Route | Status | Source |
|---|---|---|---|---|---|
| Nadi-Tarangini-App | completeWelcomeTour | POST `/welcome-tour/complete` | POST welcome-tour/complete | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2537` |
| Nadi-Tarangini-App | dashboardPatientList | POST `/getLimitedActivePatients` | POST getLimitedActivePatients | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:563` |
| Nadi-Tarangini-App | fetchNotificationsData | POST `/notification/fetchAllNotifications` | POST notification/fetchAllNotifications | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1926` |
| Nadi-Tarangini-App | fetchReportFormLanguages | GET `/getLanguages` | GET getLanguages | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1206` |
| Nadi-Tarangini-App | getAccountData | GET `/getAccountData` | GET getAccountData | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:545` |
| Nadi-Tarangini-App | getAllUserClinic | POST `/getAllUserClinics` | POST getAllUserClinics | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2209` |
| Nadi-Tarangini-App | getAnanysisDataDashbord | POST `/getUserSummary` | POST getUserSummary | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:527` |
| Nadi-Tarangini-App | getDateWiseAppointment | POST `/appointment/dateWiseAppointment` | POST appointment/dateWiseAppointment | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:573` |
| Nadi-Tarangini-App | getDateWisePatientAppointments | POST `/appointment/dateWisePatientAppointment` | POST appointment/dateWisePatientAppointment | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:344` |
| Nadi-Tarangini-App | getUserCurrentSummary | POST `/getUserCurrentSummary` | POST getUserCurrentSummary | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2227` |
| Nadi-Tarangini-App | getUserCustomizeSummary | POST `/getUserCustomizeSummary` | POST getUserCustomizeSummary | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2236` |
| Nadi-Tarangini-App | getUserDefaultClinicDetails | GET `/getUserDefaultClinicDetails` | GET getUserDefaultClinicDetails | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2218` |
| Nadi-Tarangini-App | getWelcomeTourDetails | GET `/welcome-tour` | GET welcome-tour | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2528` |
| Nadi-Tarangini-App | linkDeviceInHouseV2 | POST `/linkDeviceInHouseV2` | POST linkDeviceInHouseV2 | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2115` |
| Nadi-Tarangini-App | markClinicAsDefault | POST `/markClinicAsDefault` | POST markClinicAsDefault | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1341` |
| Nadi-Tarangini-App | saveReportLanguages | POST `/v2/updateReportLanguage` | POST v2/updateReportLanguage | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1225` |
| Nadi-Tarangini-App | validateDeviceWithSerialNo | POST `/validateDeviceWithSerialNo` | POST validateDeviceWithSerialNo | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2102` |
| Nadi-Tarangini-Frontend | ?@? | GET `/getAccountData` | GET getAccountData | matched | `Nadi-Tarangini-Frontend:app/Http/Middleware/CheckAuthToken.php:79` |
| Nadi-Tarangini-Frontend | DashboardController@addSelfAdmin | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1288` |
| Nadi-Tarangini-Frontend | DashboardController@addSelfAdmin | GET `/getProfessionType` | GET getProfessionType | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1293` |
| Nadi-Tarangini-Frontend | DashboardController@addSelfAdmin | POST `/getSalutationTypes` | POST getSalutationTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1283` |
| Nadi-Tarangini-Frontend | DashboardController@checkout | POST `/fetchUserInfo` | POST fetchUserInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1107` |
| Nadi-Tarangini-Frontend | DashboardController@checkout | GET `/subscriptions/getPlans` | GET subscriptions/getPlans | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1128` |
| Nadi-Tarangini-Frontend | DashboardController@deleteUserAccount | POST `/deleteUserAccount` | POST deleteUserAccount | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:646` |
| Nadi-Tarangini-Frontend | DashboardController@freeTrial | GET `/subscriptions/getEndPoints` | GET subscriptions/getEndPoints | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:586` |
| Nadi-Tarangini-Frontend | DashboardController@freeTrial | GET `/subscriptions/getPlans` | GET subscriptions/getPlans | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:593` |
| Nadi-Tarangini-Frontend | DashboardController@freeTrial | POST `/subscriptions/startTrial` | POST subscriptions/startTrial | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:573` |
| Nadi-Tarangini-Frontend | DashboardController@getAllClinicList | POST `/getAllUserClinics` | POST getAllUserClinics | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:365` |
| Nadi-Tarangini-Frontend | DashboardController@getDefaultClinicDetails | GET `/getUserDefaultClinicDetails` | GET getUserDefaultClinicDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:394` |
| Nadi-Tarangini-Frontend | DashboardController@getLanguagesForReports | POST `/getLanguages` | POST getLanguages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:325` |
| Nadi-Tarangini-Frontend | DashboardController@getPlanStatus | GET `/planStatus` | GET planStatus | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:552` |
| Nadi-Tarangini-Frontend | DashboardController@getReleaseDetails | GET `/getReleaseDetails` | GET getReleaseDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:259` |
| Nadi-Tarangini-Frontend | DashboardController@getSubscriptionData | GET `/subscriptions/getAllFeature` | - | no-route | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:515` |
| Nadi-Tarangini-Frontend | DashboardController@getSubscriptionData | GET `/subscriptions/getPlans` | GET subscriptions/getPlans | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:486` |
| Nadi-Tarangini-Frontend | DashboardController@getUserCurrentSummary | POST `/getUserCurrentSummary` | POST getUserCurrentSummary | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:237` |
| Nadi-Tarangini-Frontend | DashboardController@getUserCustomizeSummary | POST `/getUserCustomizeSummary` | POST getUserCustomizeSummary | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:293` |
| Nadi-Tarangini-Frontend | DashboardController@index | POST `/appointment/dateWiseAppointment` | POST appointment/dateWiseAppointment | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:140` |
| Nadi-Tarangini-Frontend | DashboardController@index | POST `/getAssociationsCount` | POST getAssociationsCount | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:177` |
| Nadi-Tarangini-Frontend | DashboardController@index | POST `/getLimitedActivePatients` | POST getLimitedActivePatients | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:86` |
| Nadi-Tarangini-Frontend | DashboardController@index | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:158` |
| Nadi-Tarangini-Frontend | DashboardController@index | POST `/getUserSummary` | POST getUserSummary | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:131` |
| Nadi-Tarangini-Frontend | DashboardController@index | POST `/patient/getBannerList` | POST patient/getBannerList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:56` |
| Nadi-Tarangini-Frontend | DashboardController@index | GET `/subscriptions/getUserPlan` | GET subscriptions/getUserPlan | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:123` |
| Nadi-Tarangini-Frontend | DashboardController@index | GET `/v2/getSeasonalTips` | GET v2/getSeasonalTips | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:151` |
| Nadi-Tarangini-Frontend | DashboardController@linkedDevice | POST `/getLinkDevice` | POST getLinkDevice | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:446` |
| Nadi-Tarangini-Frontend | DashboardController@savePaymentData | GET `/subscriptions/getEndPoints` | GET subscriptions/getEndPoints | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1210` |
| Nadi-Tarangini-Frontend | DashboardController@savePaymentData | GET `/subscriptions/getPlans` | GET subscriptions/getPlans | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1217` |
| Nadi-Tarangini-Frontend | DashboardController@savePaymentData | POST `/subscriptions/purchasePlan` | POST subscriptions/purchasePlan | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1191` |
| Nadi-Tarangini-Frontend | DashboardController@saveSelfAdminData | POST `/add-self-admin` | POST add-self-admin | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1326` |
| Nadi-Tarangini-Frontend | DashboardController@switchToAdmin | POST `/loginOtpBasedUser` | POST loginOtpBasedUser | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1374` |
| Nadi-Tarangini-Frontend | DashboardController@switchToDoctor | POST `/loginOtpBasedUser` | POST loginOtpBasedUser | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1404` |
| Nadi-Tarangini-Frontend | DashboardController@switchToDoctor | GET `/nt-admin/access-management/getAllFeatureDetails` | GET nt-admin/access-management/getAllFeatureDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1499` |
| Nadi-Tarangini-Frontend | DashboardController@switchToDoctor | GET `/subscriptions/getEndPoints` | GET subscriptions/getEndPoints | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1545` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/fetchUserInfo` | POST fetchUserInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:724` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:714` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/getCurrencyTypes` | POST getCurrencyTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:699` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/getDocumentTypes` | POST getDocumentTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:719` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/getExperienceList` | POST getExperienceList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:694` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/getFormLanguages` | POST getFormLanguages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:709` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/getLanguages` | POST getLanguages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:704` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/getMaritialList` | POST getMaritialList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:689` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/getSalutationTypes` | POST getSalutationTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:684` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/loginOtpBasedUser` | POST loginOtpBasedUser | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:667` |
| Nadi-Tarangini-Frontend | DashboardController@updateReportLanguage | POST `/v2/updateReportLanguage` | POST v2/updateReportLanguage | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:424` |
| Nadi-Tarangini-Frontend | DashboardController@updateTourData | POST `/updateWelcomeTour` | POST updateWelcomeTour | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:808` |
| Nadi-Tarangini-Frontend | NtLiteLiveNadiController@syncAccountSettings | GET `/getAccountData` | GET getAccountData | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteLiveNadiController.php:314` |

## Tables (9)

- `languages` (models: Languages): columns not in migrations
- `locality_info` (models: LocalityInfo): is_default, timezone
- `medical_report` (models: MedicalReport): city, country, external_visit_id, field_id_1, ip_address, mark_on_image_url, panchakarma_recom, reception_id, recommendations, state, try_count, user_nadi_capture_type, yoga_recom
- `nadi_report` (models: NadiReport): columns not in migrations
- `pg_device_mapping` (models: PgDeviceMapping): columns not in migrations
- `subscriptions` (models: Subscription): api_rules, blocked_api_rules, create_date, duration, features, id, limits, name, price, status, updated_at
- `transactions` (models: Transaction): amount, comment, coupon_code, create_date, currency, expire_status, free_expire_date, id, invoice_data, is_trial, month, order_id, pay_gate_order_id, pay_gate_order_json, pay_gate_payment_id, pay_gate_payment_status, pay_gate_response_json, pay_gate_signature, pay_gate_webhook_json, payment_date, payment_status, plan_id, plan_id_v2, report_count, updated_at, user_id
- `user_nadi_capture_type` (models: UserNadiCaptureType): allowed_countries, avoid_device_selection_usb, can_change_capture_type, create_date, expiry_date, free_tier_enrolled, id, is_active, is_star_account, last_modified_on, nadi_capture_type, no_of_reports, plan_type, user_id
- `user_personal_info` (models: UserPersonalInfo): allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken

## External systems

None found in the module files.

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
