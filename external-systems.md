# External systems

Status: **Draft** · 2026-10-26 · built from `_map/*/externals.json` (file and line only).
Purpose and environments: **Needs confirmation** for every row. No keys or URLs from secret files.

## Razorpay

Purpose: Needs confirmation. Environments: Needs confirmation.

| Repo | Files | Where (file:lines) |
|---|---|---|
| Ashoka-World-Backend | 9 | `app/Http/Controllers/NadiPariksha/NPPaymentController.php:295,359,360,362,364`<br>`app/Http/Controllers/NadiPariksha/NpPaymentControllerV2.php:81,82,83,84,133`<br>`app/Http/Controllers/NtTransactionController.php:197,198,201,215,260`<br>`app/Models/NadiParikshaModels/NpExternalServiceLogs.php:16`<br>`app/Services/NpCommonService.php:89,117`<br>`config/services.php:78`<br>`database/migrations/2025_11_10_154116_create_table_external_service_logs.php:21`<br>`resources/views/invoice.blade.php:224,226,461`<br>…and 1 more |
| Nadi-Tarangini-App | 3 | `lib/doctor_dashboard/subscription/utils/launch_payment.dart:9,24,56,57,72`<br>`lib/main.dart:126`<br>`pubspec.yaml:96` |
| Nadi-Tarangini-Frontend | 9 | `app/Http/Controllers/AdminDashboardController.php:1728,1729,1730`<br>`app/Http/Middleware/VerifyCsrfToken.php:16`<br>`composer.json:15`<br>`config/services.php:33,34,35`<br>`resources/views/admin/plan_details.blade.php:546,1002,1011,1013,1060`<br>`resources/views/my_account/billing_details.blade.php:191,193,198,199,209`<br>`resources/views/payments/samvit_checkout.blade.php:296,299,300,302,303`<br>`resources/views/subscription/checkout.blade.php:203,205,213,214,233`<br>…and 1 more |

## ENACH

Purpose: Needs confirmation. Environments: Needs confirmation.

| Repo | Files | Where (file:lines) |
|---|---|---|
| Ashoka-World-Backend | 11 | `app/Http/Controllers/ENACH/ENACHController.php:3,8,9,10,19`<br>`app/Models/EnachCustomers.php:9,16`<br>`app/Models/EnachDebitLog.php:8,12`<br>`app/Models/EnachMandate.php:9,16,83`<br>`database/migrations/2026_02_02_105623_create_table_enach_customers.php:16,35`<br>`database/migrations/2026_02_03_102029_enach_mandate_registration.php:16,18,64`<br>`database/migrations/2026_02_06_142714_add_column_created_by_in_enach_customers_table.php:16,28`<br>`database/migrations/2026_03_16_120000_create_enach_debit_logs_table.php:17,43`<br>…and 3 more |
| Nadi-Tarangini-Frontend | 1 | `public/json/country-wise-state.json:34284,162190,167672,465110,465114` |

## Interakt (WhatsApp)

Purpose: Needs confirmation. Environments: Needs confirmation.

| Repo | Files | Where (file:lines) |
|---|---|---|
| Ashoka-World-Backend | 7 | `app/Http/Controllers/SmsController.php:180,239`<br>`app/Repositories/NTAdmin/Eloquent/NotificationRepository.php:134,137`<br>`app/Services/EmailService.php:302,324,549,571,950`<br>`app/Services/NpOtpSmsService.php:84,85,99,127,128`<br>`app/Services/OtpSmsService.php:49`<br>`app/Services/turyaaDownloadService.php:76`<br>`config/services.php:44,45,46,67,69` |

## ZeptoMail

Purpose: Needs confirmation. Environments: Needs confirmation.

| Repo | Files | Where (file:lines) |
|---|---|---|
| Ashoka-World-Backend | 8 | `app/Http/Controllers/SmsController.php:111,125`<br>`app/Http/Controllers/SubscriptionController.php:512`<br>`app/Repositories/NTAdmin/Eloquent/NotificationRepository.php:66,84,88`<br>`app/Services/AshokaDashboardService.php:20,46,69,97`<br>`app/Services/EmailService.php:32,46,1016,1030,1239`<br>`app/Services/NpEmailService.php:15,40`<br>`config/app.php:111`<br>`config/services.php:61,64` |

## Firebase

Purpose: Needs confirmation. Environments: Needs confirmation.

| Repo | Files | Where (file:lines) |
|---|---|---|
| Ashoka-World-Backend | 23 | `app/Http/Controllers/AppointmentController.php:807,1167`<br>`app/Http/Controllers/AuthController.php:1852,1862`<br>`app/Http/Controllers/FirebaseController.php:6,7,8,10,16`<br>`app/Http/Controllers/NTAdmin/UserManagementController.php:67`<br>`app/Http/Controllers/NadiPariksha/CoachDashboardController.php:22,1458`<br>`app/Http/Controllers/NadiPariksha/NpFirebaseNotificationController.php:7,10,23,36,62`<br>`app/Http/Controllers/NotificationController.php:13,305,307,319,321`<br>`app/Http/Controllers/PatientDetailsController.php:576,838,3011`<br>…and 15 more |
| Nadi-Tarangini-App | 17 | `android/app/src/main/AndroidManifest.xml:75`<br>`assets/SHA key/sha-key.txt:134,160`<br>`firebase.json:5`<br>`lib/common_files/Login/controller/login_bloc/login_bloc.dart:5,173,196,197,198`<br>`lib/common_files/analytics/analytics_route_observer.dart:2,6`<br>`lib/common_files/api_services/api_repository.dart:388,391,395,405`<br>`lib/common_files/constants/strings_const.dart:49,50`<br>`lib/common_files/utilities/app_utils.dart:1,20,22,39`<br>…and 9 more |
| Nadi-Tarangini-Frontend | 5 | `app/Http/Controllers/DashboardController.php:26`<br>`app/Http/Controllers/loginController.php:325,328,332,339,350`<br>`public/firebase-messaging-sw.js:1,2,4,6,12`<br>`resources/views/layouts/main_layout.blade.php:110,111,113,114,116`<br>`routes/web.php:367` |

## S3

Purpose: Needs confirmation. Environments: Needs confirmation.

| Repo | Files | Where (file:lines) |
|---|---|---|
| Ashoka-World-Backend | 94 | `app/Http/Controllers/AuthController.php:139,832,1714`<br>`app/Http/Controllers/Client/EditProfileController.php:84,98`<br>`app/Http/Controllers/ClinicController.php:129,187,295,308,399`<br>`app/Http/Controllers/CustomizeDetailsController.php:1812,1841`<br>`app/Http/Controllers/DinacharyaController.php:13,71`<br>`app/Http/Controllers/DoctorController.php:261,276,628,643,776`<br>`app/Http/Controllers/External/ExternalUserController.php:790,828,854,870`<br>`app/Http/Controllers/MedicalReportSaveController.php:3534,3639,3682,3692,4272`<br>…and 86 more |
| Nadi-Tarangini-App | 4 | `lib/common_files/constants/strings_const.dart:271,272,289`<br>`lib/doctor_dashboard/my_account/view/my_clinic/clinic_list_tab.dart:191`<br>`lib/doctor_dashboard/subscription/view/billing_tab.dart:278`<br>`lib/doctor_dashboard/visit_reports/view/visit_report_list_screen.dart:56` |
| Nadi-Tarangini-Frontend | 10 | `app/Http/Controllers/Corporate/PatientDashboardManagementController.php:67,73,78,83,88`<br>`app/Http/Controllers/HelpController.php:205,213`<br>`app/Http/Controllers/LiveNadiController.php:842,843`<br>`app/Services/samplelang.json:2`<br>`config/translation.php:6,13`<br>`docs/s3-translation-flow.md:142`<br>`resources/views/live_nadi/medical_assessment.blade.php:167`<br>`resources/views/live_nadi/modal/diet/diet_recommendations.blade.php:20`<br>…and 2 more |

## AWS Lambda / API Gateway

Purpose: Needs confirmation. Environments: Needs confirmation.

| Repo | Files | Where (file:lines) |
|---|---|---|
| Ashoka-World-Backend | 22 | `app/Http/Controllers/External/ExternalUserController.php:812,991,992,2379,2380`<br>`app/Http/Controllers/MedicalReportSaveController.php:3557,3798,3799,3802,3834`<br>`app/Http/Controllers/NadiPariksha/NPnadiController.php:289,291,300,447,448`<br>`app/Http/Controllers/NadiPariksha/NadiParikshaController.php:338,340,610,611,1291`<br>`app/Http/Controllers/ReportsWebController.php:4021,4022`<br>`app/Http/Controllers/Turyaa/NadiController.php:237,246,338,339,340`<br>`app/Http/Controllers/V1/DietAndRecipesManagementController.php:965`<br>`app/Http/Controllers/V1/NadiAnalysisController.php:151,266,459,710,909`<br>…and 14 more |
| Nadi-Tarangini-App | 1 | `lib/common_files/constants/strings_const.dart:268` |
| Nadi-Tarangini-Frontend | 4 | `app/Http/Controllers/NtChatbotProxyController.php:14,15,18,19`<br>`config/services.php:46,47,48,49`<br>`resources/views/research_dashboard/nadi_analysis_1.blade.php:573,726,1039,1224,1225`<br>`resources/views/research_dashboard/researchTestDiet.blade.php:1521` |

## Samvit Chakra

Purpose: Needs confirmation. Environments: Needs confirmation.

| Repo | Files | Where (file:lines) |
|---|---|---|
| Ashoka-World-Backend | 5 | `app/Http/Controllers/LinkDeviceContoller.php:428`<br>`app/Http/Controllers/SignUpController.php:662`<br>`app/Http/Controllers/SubscriptionController.php:450,452`<br>`config/app.php:7`<br>`config/database.php:102` |
| Nadi-Tarangini-Frontend | 5 | `resources/views/payments/samvit_checkout.blade.php:261,316,340,348`<br>`resources/views/payments/samvit_checkout_error.blade.php:96,97`<br>`resources/views/subscription_plans.blade.php:255`<br>`routes/api.php:5,22,23`<br>`routes/web.php:59,812,813,814` |

## Other third-party hosts in code (candidates)

Host names only, most used first. Needs confirmation whether each is an integration.

| Repo | Host | Mentions |
|---|---|---|
| Ashoka-World-Backend | `atreyaproduction.s3.ap-south-1.amazonaws.com` | 305 |
| Ashoka-World-Backend | `atreyaproduction.s3.amazonaws.com` | 65 |
| Ashoka-World-Backend | `cdn.datatables.net` | 27 |
| Ashoka-World-Backend | `xmxkm37120.execute-api.ap-south-1.amazonaws.com` | 19 |
| Ashoka-World-Backend | `api.interakt.ai` | 16 |
| Ashoka-World-Backend | `www.youtube.com` | 14 |
| Ashoka-World-Backend | `atreyaproduction.s3.dualstack.ap-south-1.amazonaws.com` | 13 |
| Ashoka-World-Backend | `h23xw26ku1.execute-api.ap-south-1.amazonaws.com` | 13 |
| Ashoka-World-Backend | `ipinfo.io` | 13 |
| Ashoka-World-Backend | `j4co6pc5m7b5gnjjwpuanpwmju0gwgbq.lambda-url.ap-south-1.on.aws` | 13 |
| Ashoka-World-Backend | `chat.googleapis.com` | 11 |
| Ashoka-World-Backend | `api.zeptomail.in` | 10 |
| Ashoka-World-Backend | `momentjs.com` | 10 |
| Ashoka-World-Backend | `f94bf2f46c43.ngrok-free.app` | 9 |
| Ashoka-World-Backend | `7v5op026il.execute-api.ap-south-1.amazonaws.com` | 7 |
| Nadi-Tarangini-App | `play.google.com` | 4 |
| Nadi-Tarangini-App | `atreyaproduction.s3.amazonaws.com` | 3 |
| Nadi-Tarangini-App | `atreyaproduction.s3.ap-south-1.amazonaws.com` | 3 |
| Nadi-Tarangini-App | `atreyaproduction.s3.dualstack.ap-south-1.amazonaws.com` | 3 |
| Nadi-Tarangini-App | `ipinfo.io` | 2 |
| Nadi-Tarangini-App | `aka.ms` | 1 |
| Nadi-Tarangini-App | `api.razorpay.com` | 1 |
| Nadi-Tarangini-App | `docs.gradle.org` | 1 |
| Nadi-Tarangini-App | `firebase.google.com` | 1 |
| Nadi-Tarangini-App | `open.er-api.com` | 1 |
| Nadi-Tarangini-App | `wiki.gnome.org` | 1 |
| Nadi-Tarangini-App | `xqicwgldpwmx7hj6d5k6rmgzjq0mhnak.lambda-url.ap-south-1.on.aws` | 1 |
| Nadi-Tarangini-Frontend | `atreyaproduction.s3.ap-south-1.amazonaws.com` | 85 |
| Nadi-Tarangini-Frontend | `www.youtube.com` | 25 |
| Nadi-Tarangini-Frontend | `atreyaproduction.s3.amazonaws.com` | 6 |
| Nadi-Tarangini-Frontend | `atreyaproduction.s3.dualstack.ap-south-1.amazonaws.com` | 6 |
| Nadi-Tarangini-Frontend | `ieeexplore.ieee.org` | 6 |
| Nadi-Tarangini-Frontend | `jsperf.com` | 6 |
| Nadi-Tarangini-Frontend | `source.unsplash.com` | 6 |
| Nadi-Tarangini-Frontend | `bugs.webkit.org` | 4 |
| Nadi-Tarangini-Frontend | `checkout.razorpay.com` | 4 |
| Nadi-Tarangini-Frontend | `code.google.com` | 4 |
| Nadi-Tarangini-Frontend | `datatables.net` | 4 |
| Nadi-Tarangini-Frontend | `ipinfo.io` | 4 |
| Nadi-Tarangini-Frontend | `www.datatables.net` | 4 |
| Nadi-Tarangini-Frontend | `www.clarity.ms` | 3 |
| Nadi-Tarangini-Frontend | `x464l4z7y534zvvbi5rmfuqu7y0pwflv.lambda-url.ap-south-1.on.aws` | 3 |
