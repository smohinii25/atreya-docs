# Secret scan (read-only)

- Date: 2026-10-26
- Scope: every tracked file in repos/ (git ls-files), text files under 5 MB
- Values are never shown. Only file, line and key type.
- Status: **Needs confirmation**: each finding must be checked and, if real, rotated by the owner.

| Repo | Commit scanned |
|---|---|
| Ashoka-World-Backend | `8dfbb37db7d71a400b3656bd50fbed6173908a24` |
| Nadi-Tarangini-App | `0b7deec6de2b0b8b4f05eab4be8c8430523829bf` |
| Nadi-Tarangini-Frontend | `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d` |

## Summary

53 findings (3 high confidence).

| Key type | Confidence | Findings | Files |
|---|---|---|---|
| assignment to a key/secret/token/password name | medium | 50 | 25 |
| Google API key | high | 2 | 2 |
| Razorpay live key | high | 1 | 1 |

## Candidate files to add to the guard

Files with at least one **high-confidence** finding that the guard does not block yet.
Proposal only: nothing changes until approved.

| Repo | File | High findings | Types |
|---|---|---|---|
| Nadi-Tarangini-Frontend | `app/Http/Controllers/SamvitPaymentBridgeController.php` | 1 | Razorpay live key |
| Nadi-Tarangini-Frontend | `public/firebase-messaging-sw.js` | 1 | Google API key |
| Nadi-Tarangini-Frontend | `resources/views/layouts/main_layout.blade.php` | 1 | Google API key |

## All findings

| Repo | File | Line | Type | Confidence | Commented out |
|---|---|---|---|---|---|
| Nadi-Tarangini-App | `ios/Podfile` | 40 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/AdminCustomizeController.php` | 131 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/AdminCustomizeController.php` | 457 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/AdminCustomizeController.php` | 583 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/AdminDashboardController.php` | 322 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/AdminDashboardController.php` | 433 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/AdminDashboardController.php` | 657 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/AdminDashboardController.php` | 942 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/AdminDashboardController.php` | 1135 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/AdminDashboardController.php` | 1251 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/AdminDashboardController.php` | 1448 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/AppointmentController.php` | 856 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/MedicalAssessmentV3Controller.php` | 254 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/NtLiteLiveNadiController.php` | 351 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/PatientDashboardController.php` | 195 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/PatientDashboardController.php` | 403 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/PatientVisitController.php` | 85 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/SamvitPaymentBridgeController.php` | 17 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/SamvitPaymentBridgeController.php` | 20 | Razorpay live key | high | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/SamvitPaymentBridgeController.php` | 21 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Http/Controllers/SamvitPaymentBridgeController.php` | 22 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `app/Services/S3TranslationService.php` | 12 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `docs/docker-development.md` | 273 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `docs/s3-translation-flow.md` | 46 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `docs/s3-translation-flow.md` | 402 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/firebase-messaging-sw.js` | 5 | Google API key | high | no |
| Nadi-Tarangini-Frontend | `public/js/admin/adminSignup.js` | 13 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/customize/customize_report.js` | 654 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/customize/user_wise_customize_report.js` | 316 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/live_nadi/dietPlanner.js` | 6 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/live_nadi/dietPlanner.js` | 7 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/live_nadi/dietPlanner.js` | 12 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/live_nadi/dietPlanner.js` | 13 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/live_nadi/dietPlanner.js` | 17 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/live_nadi/dietPlanner.js` | 18 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/live_nadi/nadiFlow.js` | 4816 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/live_nadi/yogaPlanner.js` | 2085 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/prescription_v2.js` | 3227 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/prescription_v2.js` | 3240 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/prescription_v2.js` | 3253 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `public/js/prescription_v2.js` | 3266 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `resources/views/doctor_dashboard/dashboard.blade.php` | 317 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `resources/views/layouts/main_layout.blade.php` | 124 | Google API key | high | no |
| Nadi-Tarangini-Frontend | `resources/views/layouts/main_layout.blade.php` | 143 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `resources/views/medical_assessment/nadi_tab.blade.php` | 602 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `resources/views/research_dashboard/nadi_analysis_1.blade.php` | 222 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `resources/views/research_dashboard/nadi_analysis_1.blade.php` | 562 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `resources/views/research_dashboard/nt_map.blade_old.php` | 126 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `resources/views/research_dashboard/nt_map.blade_old.php` | 228 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `resources/views/research_dashboard/nt_map.blade_old.php` | 278 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `resources/views/research_dashboard/nt_map.blade.php` | 126 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `resources/views/research_dashboard/nt_map.blade.php` | 228 | assignment to a key/secret/token/password name | medium | no |
| Nadi-Tarangini-Frontend | `resources/views/research_dashboard/nt_map.blade.php` | 278 | assignment to a key/secret/token/password name | medium | no |

## Already guarded (not opened by this scan)

| Repo | File |
|---|---|
| Ashoka-World-Backend | `.env` |
| Ashoka-World-Backend | `config/firebase-admin-key-dev.json` |
| Ashoka-World-Backend | `config/firebase-admin-key-staging.json` |
| Ashoka-World-Backend | `config/firebase-admin-key.json` |
| Ashoka-World-Backend | `config/firebase-nadi-pariksha.json` |
| Ashoka-World-Backend | `config/firebase-turyaa-app.json` |
| Nadi-Tarangini-App | `android/app/src/prod/google-services.json` |
| Nadi-Tarangini-App | `android/app/src/staging/google-services.json` |
| Nadi-Tarangini-App | `ios/config/prod/GoogleService-Info.plist` |
| Nadi-Tarangini-App | `ios/config/staging/GoogleService-Info.plist` |
| Nadi-Tarangini-App | `ios/Runner/GoogleService-Info.plist` |
| Nadi-Tarangini-App | `key/new-nt-guna-beta-keystore.jks` |
| Nadi-Tarangini-App | `key/nt-guna-beta-keystore.jks` |
| Nadi-Tarangini-App | `lib/common_files/api_services/gchat_logger.dart` |
| Nadi-Tarangini-App | `lib/common_files/utilities/flavor_config.dart` |
| Nadi-Tarangini-Frontend | `.env` |
| Nadi-Tarangini-Frontend | `.env.docker.example` |
