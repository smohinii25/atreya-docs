# Doc check: atreya-docs/nt/auth/diagrams/ (er, flow-app, flow-web, seq-AUTH-R01 … seq-AUTH-R11)
Checked 2026-10-27 against commits Ashoka-World-Backend 8dfbb37db7, Nadi-Tarangini-App 0b7deec6de, Nadi-Tarangini-Frontend e8a9742b97 (from the diagram stamps).
Summary: 288 elements · 288 verified · 0 mismatch · 0 not provable · 0 secret risk

Elements = nodes + edges of each `.spec.json` (same content as the `.drawio`). A source may hold several citations separated by "; " (a box grouping several screens cites each screen and the page-JS call site that reaches the caller); each part was checked.

## How this run went

1. Doc-checker pass on the 14 regenerated diagrams: 290 elements, 288 verified, 2 mismatch (seq-AUTH-R11: box `SignUpController@doctorSignUp` and its arrow `POST /getSalutationTypes`, `Nadi-Tarangini-Frontend:app/Http/Controllers/SignUpController.php:23`; every web route to `SignUpController` is commented out, `routes/web.php:319-324`).
2. Cause: `link-apis.sh` counted `route('doctorSignUp')` (a route name, `resources/views/auth/tabs.blade.php:27`) as a call to the method. Fixed in the script (strings passed to `route(` / `name(` are not method references); `SignUpController@doctorSignUp` is now marked dead code.
3. seq-AUTH-R11 regenerated from its saved options: the only change is the removal of those two elements (spec diff checked); the other 13 specs are unchanged. All 14 pass `check-doc` with every citation checked.

## Summary per diagram

| Diagram | Elements | Verified | Mismatch | Not provable | Secret risk |
|---|---|---|---|---|---|
| er | 11 | 11 | 0 | 0 | 0 |
| flow-app | 24 | 24 | 0 | 0 | 0 |
| flow-web | 11 | 11 | 0 | 0 | 0 |
| seq-AUTH-R01 | 14 | 14 | 0 | 0 | 0 |
| seq-AUTH-R02 | 25 | 25 | 0 | 0 | 0 |
| seq-AUTH-R03 | 25 | 25 | 0 | 0 | 0 |
| seq-AUTH-R04 | 29 | 29 | 0 | 0 | 0 |
| seq-AUTH-R05 | 14 | 14 | 0 | 0 | 0 |
| seq-AUTH-R06 | 21 | 21 | 0 | 0 | 0 |
| seq-AUTH-R07 | 19 | 19 | 0 | 0 | 0 |
| seq-AUTH-R08 | 21 | 21 | 0 | 0 | 0 |
| seq-AUTH-R09 | 14 | 14 | 0 | 0 | 0 |
| seq-AUTH-R10 | 12 | 12 | 0 | 0 | 0 |
| seq-AUTH-R11 | 48 | 48 | 0 | 0 | 0 |
| **Total** | **288** | **288** | **0** | **0** | **0** |

## Verified (counts only)

- **ER (11 tables):** columns match every migration that creates or alters the table, including `Schema::connection('mysql')->create/table` (`corporate_info` 10, `user_personal_info` 13, `user_nadi_capture_type` 14 incl. `plan_type` from 2026_09_29_121051); `currency_type`, `pg_device_mapping`, `salutation_types` have no migrations ("columns not in migrations" is correct); all `$table` names match their models.
- **flow-app:** external boxes cite the `GoRoute(` line in `lib/route/router.dart` (one line above `path:`); every navigation edge is a `context.go` / `goNamed` / `push` at the cited line; "contains" edges at `login_screen.dart` 205 and 212.
- **flow-web:** links use `route('login')`, `route('forgotPassword')`, `route('signup')`, `route('doctorSignUp')`, `route('adminSignUp')` at the cited lines; routes live, controllers return the named views.
- **Sequences:** every `routes/api.php` line and backend controller method at its cited line; tables confirmed in each controller body (`loginOtpBasedUser` 7, `SignUpV2` 5; none comes only from `DB::beginTransaction()`); response codes exist in code; App repository methods use the named `StringsConst` URLs; App screens reach them through their bloc/cubit (`splash_screen.dart:80` directly); every Frontend caller has a live web route.
- **Grouped-screen boxes:** R04's 18 admin/customize views extend `admin_nav_layout` → `admin_main_layout`, which loads `adminCommon.js`; R08's signup views load `common.js` through `auth_layout` → `main_layout`, plus `nt_lite_signup.js` / `adminCommon.js`; R06's sign-up views load `college.js`, `signup.js`, `adminSignup.js`.
- **Page-JS call sites:** `login.js` 302, 581, 708, 812, 1052; `forgotpassword.js:87`; `changePassword.js:170`; `signup.js:993`; `college.js:324`; `adminSignup.js:533`; `nt_lite_signup.js` 185, 247, 647; `common.js` 898, 989; `adminCommon.js` 189, 643, 734.

## Notes (not counted)

1. R09 web: `changePassword.js` is commented out in `my_account/myaccount.blade.php:106` but loaded via `my_account.tabs` → `my_account.my_devices_tab:61`; the box holds, but the cited view is not the file that loads the script.
2. R09 App: the change-password event is sent from `ChangePasswordTab` (hosted by `MyAccountScreen`, line 61).
3. R02: `verifyOtp` reads `user_personal_info` only in the `is-nt-locator` header branch (conditional edge).
4. R08: no screen arrow to the App `verifyVerificationOtp` client (only `sendVerificationOtp`); no table box for `validateEmailOrMobileNo` (omission, not error).
5. ER has no relationship arrows; migrations define FKs `transactions.plan_id` → `subscriptions` (2025_03_17_123142) and `user_personal_info.plan_id` → `subscriptions` (2025_03_17_123123). The ER script draws model relations only.
6. Not checked: 500 branches not read to the end; block comments in `web.php` beyond `//`.
