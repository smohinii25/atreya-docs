# Doc check: atreya-docs/nt/patient-portal/BRD.md
Checked 2026-11-03 (doc-checker agent, fresh context). Repos were not git repos, so commits not confirmed. facts.md and PRD not re-checked.

Summary: about 45 claims, 36 verified, 4 mismatch, 5 not provable, 0 secret risk

## Mismatch
1. Duplicate phone rule is narrower: checked only when the number changes and only among patients of the same doctor (`Ashoka-World-Backend:app/Http/Controllers/Client/EditProfileController.php:68-79`).
2. Patient role citation `routes/api.php:1451` is the unused askQuery route; better cite the `client.authentication` group at line 1446.
3. BR-01 "refuses unknown usernames" not supported by cited line 713 (only "Invalid client id", `AuthController.php:707-714`).
4. BR-05 cited line 82 is only the Success line; getPreviousVisits lists only visits with `share_with_patient = 1`, returns fee_charged/fee_paid (`VisitManagementController.php:20-84`); used by web and app.

## Not provable
1. "Ask-a-question not reachable from any screen": web side verified (`PatientDashboardController.php:320`, `:357`, `api.php:1451-1452`); app not checked (search blocked).
2. Appointment page "no data service found": uncited, `RequestAppointmentController` not opened.
3. Coming soon / Contact screens: question only, acceptable.
4. Doctor/staff answer questions: inferred, marked to confirm.
5. environments.md claim: human doc, not opened.

## Secret risk
None found.
