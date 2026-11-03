---
module: "dashboard"
doc: "PRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Doctor dashboard, onboarding & welcome tour: Product Requirements Document

## 1. Overview

The dashboard module covers the doctor's landing screen, the summary numbers shown on it, the screen-wise welcome tour, and the web "account" pages that the web `DashboardController` serves (subscription, checkout, KYC, clinic and report-language settings, linked device). `atreya-docs/_map/_modules/dashboard/facts.md`. The backend exposes 7 routes (summary x4, account data, welcome tour x2), the web app has 30 routes on `DashboardController`, and the mobile app has 4 screens (Dashboard, GeoRestricted, Onboarding, Splash). `Ashoka-World-Backend:routes/api.php:949`, `Nadi-Tarangini-Frontend:routes/web.php:357`, `Nadi-Tarangini-App:lib/doctor_dashboard/dashboard/view/dashboard_screen.dart`. The summary endpoints count patients and nadi assessments (medical reports with `nadi_status = 1`) belonging to the logged-in doctor. `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2091`. One backend route, `POST getUserStatsData`, is not called by any screen in this workspace. `atreya-docs/_map/_modules/dashboard/facts.md`.

## 2. Users, roles & permissions

| Part | Who reaches it | Source |
|---|---|---|
| Backend routes (all 7) | Callers with a valid token (`auth.token` middleware) | `Ashoka-World-Backend:routes/api.php:949`, `Ashoka-World-Backend:routes/api.php:1006` |
| Web routes (28 of 30) | `check_auth_token`, `fetch_notifications`, `ensure_normal_dashboard_mode` | `Nadi-Tarangini-Frontend:routes/web.php:357` |
| Web `GET update_kyc` | No middleware listed | `Nadi-Tarangini-Frontend:routes/web.php:304` |
| Web `GET admin/switchToAdminToDoctor` | `nt_admin_authentication` | `Nadi-Tarangini-Frontend:routes/web.php:156` |
| Welcome tour | Patients (role_id = 2) get an empty step list and a 403 on completion | `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:41`, `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:105` |

Which roles other than patient exist and are meant to see the dashboard is not stated in the module files; see §13.

## 3. User journeys

**Mobile (App).** Splash screen routes to dashboard, geo-restricted, KYC, language, login, onboarding or patient report screens. `Nadi-Tarangini-App:lib/splash_screen.dart`. Onboarding goes to login. `Nadi-Tarangini-App:lib/on_boarding/on_boarding_screen.dart`. The dashboard screen loads summary (`getUserSummary`), current summary, customised summary, and welcome-tour details, and links to add appointment, add patient, appointment list, assessment, drawer menu, notifications, patient list and report screens. `atreya-docs/_map/_modules/dashboard/facts.md` (navigation list), `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:527`.

**Web (Frontend).** `GET dashboard` renders `doctor_dashboard.dashboard`; the controller calls banner list, active-patients list, user plan, summary, date-wise appointments, seasonal tips, help videos and associations count. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:56`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:177`. The page then posts to `getUserCurrentSummary` and `getUserCustomizeSummary`. `atreya-docs/_map/_modules/dashboard/facts.md`.

**Subscription (Web).** `GET subscription` reads plans; `GET checkout` reads user info and plans; `POST savePaymentData` purchases a plan; `POST freeTrial` starts a trial. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:486`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1107`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1191`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:573`.

## 4. Functional requirements

### DASHBOARD-R01: Overall dashboard totals
`POST getUserSummary` returns the logged-in doctor's totals: number of patients, number of reports, total fee charged, total fee paid, total nadi assessments and fee remaining (charged minus paid), plus monthly counts of patients, nadis and revenue. `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2110`.
**Acceptance criteria**
- Given an authenticated doctor, when the dashboard calls `getUserSummary`, then the response is "Success" with `data.number_of_patients`, `number_of_reports`, `total_fee_charged`, `total_fee_paid`, `total_nadi_assessment`, `total_fee_remaining`, plus a top-level `monthly_counts` object beside `data`. `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2110`
- Given an unexpected failure, then the API returns 500 "Internal server error". `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2131`
**Source**: `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1958`, `Ashoka-World-Backend:routes/api.php:949`
**Screens**: DashboardScreen (App), doctor_dashboard.dashboard (Web) · **API**: POST getUserSummary

### DASHBOARD-R02: Today and this-month counts
`POST getUserCurrentSummary` returns daily and monthly patient counts and daily and monthly assessment counts, using the doctor's default locality timezone (falls back to Asia/Kolkata when missing or invalid). `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2136`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2220`.
**Acceptance criteria**
- Given an authenticated doctor, when `getUserCurrentSummary` is called, then `data` has `daily_no_of_patients`, `monthly_no_of_patients`, `daily_no_of_assessments`, `monthly_no_of_assessments`. `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2220`
- Given an unexpected failure, then 500 "Internal server error". `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2233`
**Source**: `Ashoka-World-Backend:routes/api.php:951`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2220`
**Screens**: DashboardScreen (App), doctor_dashboard.dashboard (Web) · **API**: POST getUserCurrentSummary

### DASHBOARD-R03: Patient trend chart (weekly, monthly, yearly)
`POST getUserCustomizeSummary` takes `type` (WEEKLY, MONTHLY or YEARLY, case-insensitive) and returns a list of buckets with a title and patient count (WEEKLY: 7 daily buckets, MONTHLY: 4 weekly buckets, YEARLY: 12 monthly buckets, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2276`); buckets before the doctor's account creation date show 0. `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2242`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2353`.
**Acceptance criteria**
- Given `type` not in WEEKLY/MONTHLY/YEARLY, then 400 "Type must be WEEKLY, MONTHLY or YEARLY". `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2248`
- Given the doctor has no create date, then 404 "Doctor not found". `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2270`
- Given a valid type, then 200 "Success" with `data` buckets. `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2353`
**Source**: `Ashoka-World-Backend:routes/api.php:953`
**Screens**: DashboardScreen (App), doctor_dashboard.dashboard (Web) · **API**: POST getUserCustomizeSummary

### DASHBOARD-R04: Fetch welcome-tour steps
`GET welcome-tour` takes `key` (dashboard, prakruti_fill, add_patient, visit_report, medical_inventory, nadi_flow, live_nadi) and returns the tour steps for that screen; patients (role_id = 2) get an empty `data` list. `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:23`, `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:41`.
**Acceptance criteria**
- Given a missing or unlisted `key`, then 400 "Invalid parameters: ...". `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:30`
- Given a patient user, then 200 "Success" with empty data. `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:42`
- Given a non-patient user, then 200 "Success" with steps from `WelcomeTourService::getTourSteps`. `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:53`
**Source**: `Ashoka-World-Backend:routes/api.php:1005`
**Screens**: DashboardScreen, AddPatientScreen, AddPatientFromAppointmentScreen, EditPatientScreen (App) · **API**: GET welcome-tour (Web proxy routes: GET welcome-tour, GET api/welcome-tour, GET getWelcomeTourSteps/{page?})

### DASHBOARD-R05: Mark a welcome tour as completed
`POST welcome-tour/complete` takes `key` (same list) and optional `platform` (web or mobile, default web) and records the tour as completed for the user. `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:77`, `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:78`, `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:110`.
**Acceptance criteria**
- Given invalid `key` or `platform`, then 400 "Invalid parameters: ...". `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:85`
- Given the user id is unknown, then 404 "User not found.". `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:96`
- Given a patient user, then 403 "Action not allowed for patient role.". `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:105`
- Given a valid request, then 200 "Success". `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:117`
**Source**: `Ashoka-World-Backend:routes/api.php:1006`, `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:110`
**Screens**: DashboardScreen, AddPatientScreen, FillPrakrutiScreen, InventoryScreen (App) · **API**: POST welcome-tour/complete; Web: POST welcome-tour/complete, POST api/welcome-tour/complete, POST updateTourData

### DASHBOARD-R06: Account data
`GET getAccountData` returns the account data of the user identified by the request header; 404 "User not found." when absent. `Ashoka-World-Backend:app/Http/Controllers/UserStatsController.php:196`, `Ashoka-World-Backend:app/Http/Controllers/UserStatsController.php:359`.
**Acceptance criteria**
- Given an unknown user, then 404 "User not found.". `Ashoka-World-Backend:app/Http/Controllers/UserStatsController.php:196`
- Given a known user, then 200 "Success". `Ashoka-World-Backend:app/Http/Controllers/UserStatsController.php:359`
- Given a failure, then 500 "Internal server error". `Ashoka-World-Backend:app/Http/Controllers/UserStatsController.php:367`
**Source**: `Ashoka-World-Backend:routes/api.php:958`
**Screens**: AddAppointmentScreen, AddMedicinePrescription, AddPatientFromAppointmentScreen, AddPatientScreen (App); CheckAuthToken middleware and NtLiteLiveNadiController@syncAccountSettings (Web) · **API**: GET getAccountData

### DASHBOARD-R07: Web dashboard page
`GET dashboard` renders the doctor dashboard and loads banners, active patients, plan, summary, date-wise appointments, seasonal tips, help videos and associations count from backend calls. `Nadi-Tarangini-Frontend:routes/web.php:357`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:56`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:177`.
**Acceptance criteria**
- Given a logged-in web user, when `GET dashboard` is requested, then the controller calls `patient/getBannerList`, `getLimitedActivePatients`, `subscriptions/getUserPlan`, `getUserSummary`, `appointment/dateWiseAppointment`, `v2/getSeasonalTips`, `getNtHelpVideos` and `getAssociationsCount`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:56`
**Source**: `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:131`
**Screens**: doctor_dashboard.dashboard (Web) · **API**: multiple, see §6

### DASHBOARD-R08: Subscription plans, free trial and purchase (web)
Web routes `subscription`, `checkout`, `freeTrial`, `savePaymentData`, and `getPlanStatus` call backend subscription endpoints (`subscriptions/getPlans`, `getEndPoints`, `startTrial`, `purchasePlan`, `planStatus`). `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:486`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:552`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:573`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1191`.
**Acceptance criteria**
- Given `POST freeTrial`, then the controller calls `POST subscriptions/startTrial`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:573`
- Given `POST savePaymentData`, then the controller calls `POST subscriptions/purchasePlan`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1191`
- Given `GET subscription`, then the controller calls `GET subscriptions/getAllFeature`, which has no matching backend route in this workspace. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:515`
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:421`, `Nadi-Tarangini-Frontend:routes/web.php:744`, `Nadi-Tarangini-Frontend:routes/web.php:746`
**Screens**: subscription_plans, subscription.checkout, (Web; `GET invoice/{invoiceId}` reads the session transaction list, renders `profile.invoice` when found and `errors.404` when not, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1156`) · **API**: subscriptions/* (owned by another module's backend routes)

### DASHBOARD-R09: Clinic and report-language settings
Web routes `get-all-clinic-list`, `get-default-clinic-details`, `get-languages-for-reports`, `update-report-language` call `getAllUserClinics`, `getUserDefaultClinicDetails`, `getLanguages` and `v2/updateReportLanguage`; the mobile app calls `getAllUserClinics`, `getUserDefaultClinicDetails`, `getLanguages`, `markClinicAsDefault` and `v2/updateReportLanguage`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:325`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:365`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:394`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:424`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1206`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1225`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1341`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2209`.
**Acceptance criteria**
- Given `POST update-report-language`, then the web controller forwards to `POST v2/updateReportLanguage`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:424`
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:733`, `Nadi-Tarangini-Frontend:routes/web.php:736`
**Screens**: none dedicated in this module (Web JSON routes) · **API**: see §6

### DASHBOARD-R10: Linked device
Web `GET linked-device` calls `POST getLinkDevice`; the mobile app calls `validateDeviceWithSerialNo` and `linkDeviceInHouseV2`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:446`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2102`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2115`.
**Acceptance criteria**
- Given `GET linked-device`, then the controller calls `POST getLinkDevice`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:446`
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:737`
**Screens**: none dedicated in this module · **API**: POST getLinkDevice

### DASHBOARD-R11: Account profile, KYC and admin switch (web)
Web routes `update_kyc`, `add-self-admin` (GET and POST), `switchToAdmin`, `admin/switchToAdminToDoctor` and `delete-account` serve KYC form data, self-admin creation, role switching through `loginOtpBasedUser`, and account deletion through `deleteUserAccount`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:667`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1326`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1374`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1404`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:646`.
**Acceptance criteria**
- Given `POST add-self-admin`, then the controller calls backend `POST add-self-admin`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1326`
- Given `POST delete-account`, then the controller calls `POST deleteUserAccount`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:646`
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:304`, `Nadi-Tarangini-Frontend:routes/web.php:397`, `Nadi-Tarangini-Frontend:routes/web.php:702`
**Screens**: my_account.update_kyc, add_self_admin (Web) · **API**: see §6

### DASHBOARD-R12: Mobile launch and onboarding flow
SplashScreen (route `/`) navigates to dashboard, geo-restricted, KYC, language, login, onboarding or patient report screens; OnboardingScreen navigates to login; the fact pack lists no outgoing navigation for GeoRestrictedScreen (`atreya-docs/_map/_modules/dashboard/facts.md`). `Nadi-Tarangini-App:lib/splash_screen.dart`, `Nadi-Tarangini-App:lib/on_boarding/on_boarding_screen.dart`, `Nadi-Tarangini-App:lib/doctor_dashboard/dashboard/view/geo_restricted_screen.dart`.
**Acceptance criteria**
- Given the language is not set, then the app goes to the language screen; else if onboarding is not done, to onboarding; else if not logged in, to login. `Nadi-Tarangini-App:lib/splash_screen.dart:47`
- Given a logged-in patient (role "2"), then it goes to the patient report screen; given the geo-IP check says not allowed, then to the geo-restricted screen; given a failed geo or login call, then to login. `Nadi-Tarangini-App:lib/splash_screen.dart:63`
- Given `kyc_updated` is "0" from the login call, then KYC screen; otherwise the dashboard. `Nadi-Tarangini-App:lib/splash_screen.dart:81`
**Source**: `Nadi-Tarangini-App:lib/splash_screen.dart`
**Screens**: SplashScreen, OnboardingScreen, GeoRestrictedScreen (App) · **API**: none listed

### DASHBOARD-R13: Release details
Web `GET getReleaseDetails` calls backend `GET getReleaseDetails`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:259`, `Nadi-Tarangini-Frontend:routes/web.php:363`.
**Acceptance criteria**
- Given `GET getReleaseDetails`, then the controller calls `GET getReleaseDetails`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:259`
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:363`
**Screens**: none dedicated · **API**: GET getReleaseDetails

### DASHBOARD-R14: Unused stats endpoint
`POST getUserStatsData` (`UserStatsController@getUserStatsData`) exists behind `auth.token` but no screen in this workspace calls it. `Ashoka-World-Backend:routes/api.php:955`, `atreya-docs/_map/_modules/dashboard/facts.md`. Not described as a live feature; see §13.
**Acceptance criteria**
- None can be written from the fact pack (no validation or error data).
**Source**: `Ashoka-World-Backend:routes/api.php:955`
**Screens**: none · **API**: POST getUserStatsData

## 5. Screens (web / mobile)

| Screen | Platform | File | Route / path | Purpose (provable) |
|---|---|---|---|---|
| DashboardScreen | App | `Nadi-Tarangini-App:lib/doctor_dashboard/dashboard/view/dashboard_screen.dart` | /dashboardScreen | Calls getUserSummary, current/customised summary, welcome tour |
| GeoRestrictedScreen | App | `Nadi-Tarangini-App:lib/doctor_dashboard/dashboard/view/geo_restricted_screen.dart` | /geoRestrictedScreen | Reached from SplashScreen |
| OnboardingScreen | App | `Nadi-Tarangini-App:lib/on_boarding/on_boarding_screen.dart` | /onBoardingScreen | Goes to /loginScreen |
| SplashScreen | App | `Nadi-Tarangini-App:lib/splash_screen.dart` | / | Routes to 7 screens |
| add_self_admin | Web | `Nadi-Tarangini-Frontend:resources/views/add_self_admin.blade.php` | GET add-self-admin | Rendered by addSelfAdmin |
| doctor_dashboard.dashboard | Web | `Nadi-Tarangini-Frontend:resources/views/doctor_dashboard/dashboard.blade.php` | GET dashboard | Main dashboard |
| errors.404 | Web | `Nadi-Tarangini-Frontend:resources/views/errors/404.blade.php` | GET error-404, GET invoice/{invoiceId} | Rendered by DashboardController@invoice and UnauthorizedController@error404 |
| my_account.update_kyc | Web | `Nadi-Tarangini-Frontend:resources/views/my_account/update_kyc.blade.php` | GET update_kyc | KYC form |
| subscription.checkout | Web | `Nadi-Tarangini-Frontend:resources/views/subscription/checkout.blade.php` | GET checkout | Checkout |
| subscription_plans | Web | `Nadi-Tarangini-Frontend:resources/views/subscription_plans.blade.php` | GET subscription | Plans |

## 6. APIs

| Method | Endpoint | Controller | Auth (middleware) | Called by |
|---|---|---|---|---|
| GET | getAccountData | UserStatsController@getUserAccountData | api, auth.token | App (screens listed by the fact pack, more files call it), Web CheckAuthToken, NtLiteLiveNadiController |
| POST | getUserCurrentSummary | AuthController@getUserSummaryV2 | api, auth.token | App DashboardScreen, Web DashboardController |
| POST | getUserCustomizeSummary | AuthController@getUserCustomizeSummary | api, auth.token | App DashboardScreen, Web DashboardController |
| POST | getUserStatsData | UserStatsController@getUserStatsData | api, auth.token | No screen in this workspace |
| POST | getUserSummary | AuthController@getUserSummary | api, auth.token | App DashboardScreen, Web DashboardController@index |
| GET | welcome-tour | WelcomeTourController@getTourSteps | api, auth.token | App (screens per the fact pack; other App files also reference tours) |
| POST | welcome-tour/complete | WelcomeTourController@completeTour | api, auth.token | App (screens per the fact pack; other App files also reference tours) |

Sources: `Ashoka-World-Backend:routes/api.php:949`, `Ashoka-World-Backend:routes/api.php:951`, `Ashoka-World-Backend:routes/api.php:953`, `Ashoka-World-Backend:routes/api.php:955`, `Ashoka-World-Backend:routes/api.php:958`, `Ashoka-World-Backend:routes/api.php:1005`, `Ashoka-World-Backend:routes/api.php:1006`.

Web routes (all `Nadi-Tarangini-Frontend:routes/web.php`, DashboardController, line in brackets): GET add-self-admin (397), POST add-self-admin (399), GET admin/switchToAdminToDoctor (156), GET welcome-tour (360), POST welcome-tour/complete (361), GET api/welcome-tour (358), POST api/welcome-tour/complete (359), GET checkout (744), GET dashboard (357), POST delete-account (702), POST freeTrial (446), GET get-all-clinic-list (734), GET get-default-clinic-details (735), GET get-languages-for-reports (733), GET getPlanStatus (364), GET getReleaseDetails (363), POST getUserCurrentSummary (365), POST getUserCustomizeSummary (366), GET getWelcomeTourSteps/{page?} (362), GET invoice/{invoiceId} (748), GET linked-device (737), GET member-progress (731), GET member-report (732), GET queries (738), POST savePaymentData (746), GET subscription (421), GET switchToAdmin (392), POST update-report-language (736), POST updateTourData (740), GET update_kyc (304).

## 7. Data model

Tables the fact pack associates with this module (columns from migrations, `atreya-docs/_map/_modules/dashboard/facts.md`):

| Table | Key fields from migrations |
|---|---|
| `locality_info` | is_default, timezone (used for the summary timezone: `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2143`) |
| `medical_report` | city, country, external_visit_id, field_id_1, ip_address, mark_on_image_url, panchakarma_recom, reception_id, recommendations, state, try_count, user_nadi_capture_type, yoga_recom |
| `subscriptions` | api_rules, blocked_api_rules, create_date, duration, features, id, limits, name, price, status, updated_at |
| `transactions` | amount, comment, coupon_code, create_date, currency, expire_status, free_expire_date, id, invoice_data, is_trial, month, order_id, pay_gate_order_id, pay_gate_order_json, pay_gate_payment_id, pay_gate_payment_status, pay_gate_response_json, pay_gate_signature, pay_gate_webhook_json, payment_date, payment_status, plan_id, plan_id_v2, report_count, updated_at, user_id |
| `user_nadi_capture_type` | allowed_countries, avoid_device_selection_usb, can_change_capture_type, create_date, expiry_date, free_tier_enrolled, id, is_active, is_star_account, last_modified_on, nadi_capture_type, no_of_reports, plan_type, user_id |
| `user_personal_info` | allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken |
| `languages`, `nadi_report`, `pg_device_mapping` | Columns not in migrations (see §13) |

## 8. Validations & error handling

| API | Field / case | Rule or message | HTTP | Source |
|---|---|---|---|---|
| welcome-tour | `key` | required\|string\|in:dashboard,prakruti_fill,add_patient,visit_report,medical_inventory,nadi_flow,live_nadi; "Invalid parameters: " | 400 | `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:23` |
| welcome-tour/complete | `key` | same rule | 400 | `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:77` |
| welcome-tour/complete | `platform` | nullable\|string\|in:web,mobile | 400 | `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:78` |
| welcome-tour/complete | user missing | "User not found." | 404 | `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:96` |
| welcome-tour/complete | patient role | "Action not allowed for patient role." | 403 | `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:105` |
| getUserCustomizeSummary | `type` | "Type must be WEEKLY, MONTHLY or YEARLY" | 400 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2248` |
| getUserCustomizeSummary | doctor create date missing | "Doctor not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2270` |
| getAccountData | user missing | "User not found." | 404 | `Ashoka-World-Backend:app/Http/Controllers/UserStatsController.php:196` |
| all 6 handled routes | unexpected exception | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2131`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2233`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2361`, `Ashoka-World-Backend:app/Http/Controllers/UserStatsController.php:367`, `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:61`, `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:124` |

## 9. Non-functional

- **Security.** All backend routes sit behind `auth.token`; web routes behind `check_auth_token` except `GET update_kyc`. `Ashoka-World-Backend:routes/api.php:907`, `Nadi-Tarangini-Frontend:routes/web.php:304`. Role switching and `GET update_kyc` post to `loginOtpBasedUser`; `update_kyc` has no auth middleware and redirects to `dashboard` when `kyc_updated` is 1. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:667`. `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1374`.
- **Languages.** Required: English, Marathi, Hindi, Czech, German, Spanish, Italian (`references/qa-scope-rules.md`). Language files found in code: `Nadi-Tarangini-Frontend:resources/lang/en/auth.php`, `en/pagination.php`, `en/passwords.php`, `en/validation.php`, `Nadi-Tarangini-Frontend:resources/lang/en_patient.json`. The fact pack lists only English files for the web (`atreya-docs/_map/_modules/dashboard/facts.md`); the other six required languages are not found there (see §13).
- **Time zone.** Summary APIs use the doctor's default locality timezone, defaulting to Asia/Kolkata. `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2143`.
- **Performance.** No timeouts or limits are shown in the module facts.

## 10. Environment matrix

Copied from `environments.md`; every value is TO FILL.

| Repo | Env | Ref | Host | Feature flags | Integration mode |
|---|---|---|---|---|---|
| Ashoka-World-Backend | dev | TO FILL | TO FILL | TO FILL | TO FILL |
| Ashoka-World-Backend | staging | TO FILL | TO FILL | TO FILL | TO FILL |
| Ashoka-World-Backend | production | TO FILL | TO FILL | TO FILL | TO FILL |
| Nadi-Tarangini-App | dev | TO FILL (build flavor TO FILL) | TO FILL | TO FILL | TO FILL |
| Nadi-Tarangini-App | staging | TO FILL (build flavor TO FILL) | TO FILL | TO FILL | TO FILL |
| Nadi-Tarangini-App | production | TO FILL (build flavor TO FILL) | TO FILL | TO FILL | TO FILL |
| Nadi-Tarangini-Frontend | dev | TO FILL | TO FILL | TO FILL | TO FILL |
| Nadi-Tarangini-Frontend | staging | TO FILL | TO FILL | TO FILL | TO FILL |
| Nadi-Tarangini-Frontend | production | TO FILL | TO FILL | TO FILL | TO FILL |

## 11. Staging delta

See `atreya-docs/nt/dashboard/staging-delta.md`. Status: not computed for any of the 3 repos, waiting for `environments.md` refs. `atreya-docs/nt/dashboard/staging-delta.md`.

## 12. External integrations

None found in the module files. `atreya-docs/_map/_modules/dashboard/facts.md`. The subscription flow calls backend `subscriptions/purchasePlan`; whether a payment gateway is involved is not shown here (the `transactions` table has `pay_gate_*` columns; see §13).

## 13. Open questions

1. (PO) Which roles besides patient (role_id = 2) are meant to see the doctor dashboard and welcome tours (e.g. receptionist, admin, sub-doctors)?
2. (Dev) `POST getUserStatsData` has no caller in this workspace: is it live (another client), or dead code to retire?
3. (Dev) `GET subscriptions/getAllFeature` is called from `DashboardController@getSubscriptionData` but has no matching backend route: is it a missing route or an obsolete call? (`Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:515`)
4. (Dev) What does GeoRestrictedScreen block (which regions or users)?
5. (PO) What are the welcome-tour steps per key (dashboard, prakruti_fill, add_patient, visit_report, medical_inventory, nadi_flow, live_nadi) and is the web `getWelcomeTourSteps/{page?}` set the same?
6. (Dev) Tables `languages`, `nadi_report`, `pg_device_mapping` have columns not in migrations: where are they created?
7. (PO) Web routes `member-progress`, `member-report`, `queries`: what are they for and are they live? Their handler behaviour was not read for this draft.
8. (PO) Required languages beyond English (Marathi, Hindi, Czech, German, Spanish, Italian): where are the dashboard strings for them?
9. (Dev) `getUserSummary` and `getUserCurrentSummary` filter on `doctor_id = user_id` (allowed-doctor-ids filter is commented out): is that intended for sub-doctors/receptionists?
10. (Dev) Is `GET update_kyc` intentionally without auth middleware?
11. (Dev) Does the subscription purchase use a payment gateway, and which module owns the payment flow?
12. (Dev/QA) Environment refs, hosts, flags are TO FILL in `environments.md`: who provides them so the staging delta can be computed?

## 14. Diagrams

None yet: run /atreya:diagram dashboard.

## 15. Document control

| Field | Value |
|---|---|
| Status | Draft |
| Date | 2026-11-03 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend 8dfbb37db7d71a400b3656bd50fbed6173908a24; Nadi-Tarangini-App 0b7deec6de2b0b8b4f05eab4be8c8430523829bf; Nadi-Tarangini-Frontend e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d |
