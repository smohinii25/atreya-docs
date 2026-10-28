# Doc check: atreya-docs/nt/auth/BRD.md

Checked 2026-10-26 by the doc-checker (fresh context, read-only) against commits
Ashoka-World-Backend 8dfbb37, Nadi-Tarangini-App 0b7deec, Nadi-Tarangini-Frontend e8a9742.

Summary: 52 claims · 47 verified · 0 mismatch · 3 not provable · 0 secret risk

All 17 cited backend lines, 6 App/Frontend citations and ~25 of the PRD's own
citations behind AUTH-R01-R10 were read; the code matches in every case.

## Mismatch
None.

## Not provable
| # | Claim | Why | Resolution |
|---|---|---|---|
| 1 | §5 "username and mobile number are checked while typing" | Endpoints exist; timing (per keystroke) not shown | Now "checked during registration" |
| 2 | BR-06 "told immediately" | "Immediately" not shown by AUTH-R07 | "immediately" removed |
| 3 | §3 Patient / client role | Citation without line; who reaches the patient screen is open | Cited `login_with_otp.dart:163`, reworded, added to §12 Q2 |

## Secret risk
None.

## Plain-language issues
| Text | Problem | Resolution |
|---|---|---|
| `atreya-docs/environments.md` in §8 and §12 Q3 | File path in body text | "the environments sheet" |
| "Notification service (Firebase)", "File storage (S3)" | Technical names | "Phone notification service (Firebase)", "Cloud file storage (S3)" |
| "Customer care" as a role | A message, not a role in code | Reworded as a contact point named in a message |
| "Samvit Chakra" | Unexplained name | Kept: flagged "purpose to confirm" |

## Verified (sample)
Sign-in rules (`AuthController.php:415`, `:476`), OTP validity 5 minutes and expiry
(`OtpSmsController.php:79`, `:136`), registered-only OTP (`:71`, `:373`), country code
match (`:57`), unique mobile and username (`SignUpController.php:825`,
`CheckUserExistOrNotController.php:195`), password and name rules
(`SignUpController.php:708`, `:709`, `UpdatePasswordController.php:16`, `:38`, `:56`),
forgot-password channel and customer-care messages (`AuthController.php:1751`, `:1784`),
push token (`login_bloc.dart:196`, `AuthController.php:1862`), admin switch
(`DashboardController.php:1374`, `:1404`), S3 upload and Samvit Chakra call
(`SignUpController.php:491`, `:662`), TO FILL environments, language list.
