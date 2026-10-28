# Doc check: atreya-docs/nt/auth/diagrams/

Checked 2026-10-26 by the doc-checker (fresh context, read-only) against commits
Ashoka-World-Backend 8dfbb37, Nadi-Tarangini-App 0b7deec, Nadi-Tarangini-Frontend e8a9742.
Diagrams: er, flow-app, flow-web, seq-AUTH-R01, seq-AUTH-R02.

Summary: ~100 claims · ~92 verified · 0 mismatch · 8 not provable / misleading · 0 secret risk

Every .drawio contains exactly the boxes and arrows of its spec.json, and every
cited line lands on the claimed code.

## Mismatch
None.

## Not provable / misleading
| # | Diagram | Finding | Resolution |
|---|---|---|---|
| 1 | flow-app | ForgotPasswordScreen → LoginScreen fires on the system back gesture (`forgot_password_screen.dart:60`, `onPopInvokedWithResult`) | Kept: real navigation; the arrow cites the line |
| 2 | flow-app | LoginWithUsernameScreen → ForgotPasswordScreen is `goNamed("forgotPasswordScreen")`; label shows the path | Kept: name resolved to its path through `lib/route/router.dart` |
| 3 | flow-web | `auth.college_signUp` has no incoming link (only `GET sign-up-college`) | Kept: correct; reached by URL only. Noted for the PRD reviewer |
| 4 | flow-web | Labels show URLs while code uses route names | Kept: route names resolve to these URLs (`routes/web.php:325-329`) |
| 5 | seq-AUTH-R01 | "4 screens" included ForgotPasswordScreen, which does not log in | **Fixed** in `calls.sh`/`link-apis.sh`: App calls are now traced through the bloc to the screens that use it; R01 shows LoginScreen, LoginWithOtpScreen, LoginWithUsernameScreen |
| 6 | seq-AUTH-R02 | Same grouping | **Fixed** as #5 |
| 7 | seq-AUTH-R01/R02 | Web `checkLoginCredentials` also calls `POST loginOtpBasedUser` (`loginController.php:79`) | Open: the password login on web also creates the session via loginOtpBasedUser; PRD §3 J1 states it. Decide whether AUTH-R01's API line should include it (PRD reviewer) |
| 8 | seq-AUTH-R02 | Response codes are those found in a 688-line method, not every path | Kept: the arrow lists codes found in code; not claimed exhaustive |

## Layout / readability notes
- "7 tables" box: tables used by `AuthController@loginOtpBasedUser`; read vs write is not shown (diagrams show "uses").
- ER: title says "columns from migrations only"; tables created before the migrations
  (e.g. `user_personal_info`) show only later-added columns; three tables have no migrations.
- External boxes in flows (DashboardScreen, KycScreen, …) are screens of other modules; their routes exist in `lib/route/router.dart`.

## Verified (sample)
- flow-app: 5 screens and 15 arrows (`context.go` at `login_with_otp.dart` 147/163/167/176, `login_with_username_screen.dart` 81/90/92/99, `signup_screen.dart:228`, `login_screen.dart:243`, "contains" at `login_screen.dart:205`, `:212`).
- flow-web: 6 views and 5 `route(...)` links (`forgot_password.blade.php:55`, `login.blade.php:181`, `:279`, `tabs.blade.php:27`, `:53`).
- seq-AUTH-R01: `loginUser` → `/v2/loginValidation` (`api_repository.dart:357`), web caller `loginController.php:63`, route `api.php:1639`, `AuthController@loginValidation` uses `user_personal_info`, returns 400/401/500.
- seq-AUTH-R02: send/verify OTP and session calls at `api_repository.dart:448`, `:465`, `:431` and `loginController.php:319`, `:378`, `:446`; routes `api.php:788`, `:789`, `:739`; controller tables and response codes match.
- er: 11 tables with `$table` models; listed columns exist in migrations; none of the 11 models defines a relation, so no arrow is missing.
