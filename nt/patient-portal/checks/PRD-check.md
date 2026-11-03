# Doc check: atreya-docs/nt/patient-portal/PRD.md
Checked 2026-11-03 against commits Backend 8dfbb37, App 0b7deec, Frontend e8a9742 (doc-checker agent, fresh context; report saved verbatim in substance).

Summary: about 120 claims, about 100 verified, 6 mismatch, 6 not provable, 0 secret risk

Not checked: app route paths (`/dietScreen` etc.; content search of app `lib/` blocked by guard hook), §7 table columns and the `api` middleware (taken from facts.md / bootstrap).

## Mismatch
1. Overview "13 of 17 behind client.authentication": all 17 are (`Ashoka-World-Backend:routes/api.php:1446-1472`, `:1673-1674`); doc contradicted itself in §2.
2. Overview "7 patient screens": `lib/patient_module/view/` has 10 files; missing patient_dashboard.dart, drawer_menu_patient.dart, change_password_patient.dart.
3. Corporate dashboard route exists: `GET corporate/patientDashboard` (`Nadi-Tarangini-Frontend:routes/web.php:804-806`), middleware `corporate_patient_check_auth` inside `check_client_auth_token` group.
4. Image message is "Image shouldn't be greater than 1 MB" (400) (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:93`); doc used a truncation.
5. changePassword validation failures return 400 (`AccountManagementController.php:292-303`), also "Current password is required" / "New password is required"; updateDataConsent validation failures return 400 (`DataConsentController.php:57-71`). Doc said unknown.
6. getBannerList also defined in the app (`Nadi-Tarangini-App:lib/common_files/constants/strings_const.dart:94`, `:144`); use by app dashboard not proven; doc said Web only.

## Not provable
1. `my_account.myaccount` view name not tied to a cited line.
2. ComingSoonPage / ContactScreen purposes (already in open questions).
3. Middleware `api` not written in route file (framework bootstrap).
4. §7 columns cite only facts.md.
5. App route paths not confirmed (blocked search).
6. Required languages: human doc, accepted.

## Secret risk
None found.
