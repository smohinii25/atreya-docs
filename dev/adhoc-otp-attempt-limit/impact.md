---
module: "auth"
doc: "impact"
status: "Draft"
date: "2026-10-26"
reviewer: "TBD"
ticket: "adhoc-otp-attempt-limit"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Limit wrong OTP attempts on login: Impact analysis

## 1. Change

- **Source:** free text (no Zoho Sprints item): "Limit wrong OTP attempts on login OTP verification".
- **Origin:** the open question in the auth PRD, §13 Q5 ("how many wrong attempts are allowed before an OTP or account is blocked?"), repeated in the BRD, §12 Q5.
- **What is asked:** a login OTP check (mobile and email, web and app) must stop accepting codes after a set number of wrong attempts. Today the backend answers every wrong code with 400 "Invalid OTP" and keeps the OTP valid until it expires or is used: mobile `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:199`, email `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:457`. The number of attempts, what happens at the limit and the message shown are not decided yet (§11).

## 2. Summary

- **Risk: Medium** (script). Both changed backend routes are called by the web dashboard and by the app.
- **Modules:** 1 direct (auth), 0 related (impact-facts.md).
- **Main reason:** the change sits in two backend methods, `OtpSmsController@verifyOtp` (from `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:98`) and `OtpSmsController@verifyEmailOtp` (from `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:424`). Every login OTP check on web and app goes through them. If the PO decides that the account itself is blocked, the risk becomes High (§9).

## 3. Affected modules

**Direct**
- **auth** owns `OtpSmsController.php` and the routes `POST otp/verify-otp` and `POST otp/verify-email-otp` (impact-facts.md, "Modules").

**Related (by the script's rules: shared changed table or caller of a changed route)**
- None (impact-facts.md).

**Not related by those rules, but close to the change (for the developer)**
- **nt-jiva**: `POST nt-jiva/send-otp` and `POST nt-jiva/verify-otp` (`Ashoka-World-Backend:routes/api.php:798`, `Ashoka-World-Backend:routes/api.php:799`) live in the same controller. They read and write the same cache entry name as mobile login, `'otp_' . $phone` (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:242`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:296`; login uses it at `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79` and `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:133`). Whether the limit applies there is §11 Q6.
- **Sign-up / profile verification codes** (`POST otp/verify-verification-otp`, `Ashoka-World-Backend:routes/api.php:794`, auth module) are a separate method with their own cache key (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:650`). The free text names only login, so they are out of scope unless §11 Q6 says otherwise.

## 4. Code: files, routes & APIs

**Seeds (what must change)**

| Seed | Why | Changed span (impact-facts.md) |
|---|---|---|
| `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:199` | Mobile login OTP: a wrong code returns 400 "Invalid OTP" with no attempt count; the cached OTP stays valid | method `verifyOtp`, lines 98-201 |
| `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:457` | Email login OTP: same, status_code NT_1213 | method `verifyEmailOtp`, lines 424-459 |

**What the verify methods do today (context for the change)**
- The OTP is a 6-digit number held in the Laravel cache for 5 minutes under `otp_<country code> <mobile>` or `otp_<email>`: `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:381`.
- With no cached OTP the answer is 400 "Expired OTP": `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:439`.
- A correct code deletes the cached OTP: `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:140`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:443`.
- Requesting a new OTP overwrites the cache entry: `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:381`. How resend relates to the attempt count is §11 Q3.
- No attempt counter exists in either method (lines 98-201 and 424-459). The only request limit on these routes is the `api` middleware group's throttle of 100000 requests per minute (`Ashoka-World-Backend:app/Http/Kernel.php:48`). The `otp` route group adds none (`Ashoka-World-Backend:routes/api.php:787`).
- `verifyOtp` has a second success branch for requests carrying `is-nt-locator` and `user-id` headers (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:142`). No client in this workspace sends them (§11 Q7).
- The cache store comes from the environment, defaulting to `file` (`Ashoka-World-Backend:config/cache.php:18`); see §11 Q8.

**Backend routes changed** (impact-facts.md)

| Route | Controller | Callers |
|---|---|---|
| `POST otp/verify-otp` (`Ashoka-World-Backend:routes/api.php:789`) | OtpSmsController@verifyOtp | App `verifyMobileOtp` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:465`); Web `loginController@verifyWhatsappLoginOtp` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:378`) |
| `POST otp/verify-email-otp` (`Ashoka-World-Backend:routes/api.php:791`) | OtpSmsController@verifyEmailOtp | App `verifyEmailOtp` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:494`); Web `loginController@verifyEmailLoginOtp` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:696`) |

**How each caller shows a refusal today** (relevant because a limit adds a new kind of refusal)
- **Web, mobile:** `verifyWhatsappLoginOtp` ignores the backend's message and always returns "Invalid OTP" when verification fails (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:407`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:409`). A lockout message from the backend would not reach the user on this path unless this caller changes too (§11 Q5).
- **Web, email:** `verifyEmailLoginOtp` passes the backend message through (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:720`).
- **Web page script:** shows the returned message and re-enables the Verify button (`Nadi-Tarangini-Frontend:public/js/auth/login.js:830`, `Nadi-Tarangini-Frontend:public/js/auth/login.js:833`).
- **App:** on a non-200 answer the HTTP service returns the error body (`Nadi-Tarangini-App:lib/common_files/api_services/http_api_service.dart:150`). The login bloc then shows its `message`, for mobile (`Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:299`) and for email (`Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:461`). Two `status_code` values get special handling before that: `NT_0000` logs the user out and `NT_1017` shows a generic "Something went wrong" popup (`Nadi-Tarangini-App:lib/common_files/api_services/http_api_service.dart:120`, `Nadi-Tarangini-App:lib/common_files/api_services/http_api_service.dart:122`, `Nadi-Tarangini-App:lib/common_files/constants/error_const.dart:4`, `Nadi-Tarangini-App:lib/common_files/constants/error_const.dart:5`).

**Web routes changed:** none. **API calls from changed client code:** none (impact-facts.md; the seeds are backend only).

## 5. Screens (web / mobile)

**Web**
- **auth.login** (`Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php:356` loads `login.js`; page route `GET login`, `Nadi-Tarangini-Frontend:routes/web.php:313`). Its OTP form posts to `POST verify-login-otp` or `POST verify-email-login-otp` (`Nadi-Tarangini-Frontend:public/js/auth/login.js:783`; routes `Nadi-Tarangini-Frontend:routes/web.php:86`, `Nadi-Tarangini-Frontend:routes/web.php:88`). The script lists these two POST routes as "web pages to check" (impact-facts.md); the page a tester opens is `auth.login`.

**App**
- **LoginWithOtpScreen** sends both checks: `VerifyEmailOtpApi` and `VerifyOtpApi` (`Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart:367`, `Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart:374`). It shows the error at `Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart:155` and `Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart:266`.
- impact-facts.md credits the verify calls only to **LoginWithOtpScreen**, the screen that sends the verify events (`Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart:367`, `Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart:374`). LoginScreen and LoginWithUsernameScreen use the same login bloc but send no OTP verify event, so they are not affected.

## 6. Data

- **Changed tables:** none (impact-facts.md). The OTP and any attempt state today live in the cache, not in a table (§4).
- **Read by the changed routes (context):** `user_personal_info`, used by 21 modules (impact-facts.md). It is read after a correct code (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:150`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:445`).
- **If the PO chooses to block the account** (§11 Q2), the existing "blocked" state is `user_personal_info.is_active = 0`. Password login and the session step only load active users (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:460`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:802`), so a blocked user gets 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:466`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:806`); the explicit "User has been blocked" checks can never run (PRD §13 Q14). The OTP send only finds active users (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:62`). Using that flag would change the meaning of a table shared by 21 modules (§9).

## 7. External systems

- None inside the changed code (impact-facts.md). The SMS/WhatsApp and email senders are called only by the send methods (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:89`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:409`), which are outside the changed spans.

## 8. Docs & diagrams to update

From impact-facts.md ("Docs and diagrams citing the changed code"), plus the two open questions that started this change:

| Doc / diagram | What to update |
|---|---|
| nt/auth/PRD.md AUTH-R02 | Add the wrong-attempt limit and its response to the acceptance criteria (mobile) |
| nt/auth/PRD.md AUTH-R03 | Same for email |
| nt/auth/PRD.md §9 Non-functional | Replace "An attempt limit is §13 Q5" with the agreed rule |
| nt/auth/PRD.md §6 APIs | Cited by the script; check only (route, controller and callers do not change) |
| nt/auth/PRD.md §13 Q5 | Close the question with the PO's answer (not cited by the script; added here) |
| nt/auth/BRD.md §6 Business rules | Add a business rule for the attempt limit next to the "valid for 5 minutes" rule |
| nt/auth/BRD.md §12 Q5 | Close the question (not cited by the script; added here) |
| nt/auth/diagrams/seq-AUTH-R02.drawio | `POST otp/verify-otp` responses show 200/400; add the limit response |
| nt/auth/diagrams/seq-AUTH-R03.drawio | `POST otp/verify-email-otp` responses show 200/400; add the limit response (email) |

Suggestion: either extend AUTH-R02 and AUTH-R03 or add a new requirement (next free ID, AUTH-R12) for the attempt limit, so Phase-3 test cases can link to it.

## 9. Risk

- **Script level: Medium.** Signals (impact-facts.md):
  - `POST otp/verify-otp` is called by web and app;
  - `POST otp/verify-email-otp` is called by web and app.
  - No High signals: auth is not critical, there is no Razorpay/ENACH code in the changed spans, no changed table, and only one module is directly changed.
- **Claude's view: Medium, conditional.** Medium holds if the limit acts on the OTP itself or on a time lock kept outside the user's record. It becomes **High** if the PO decides to block the account (PRD §13 Q5 asks "OTP or account") through the existing `user_personal_info.is_active` flag. That flag lives in a table used by 21 modules (impact-facts.md), and the two login paths filter on it when loading the user (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:460` in `v2/loginValidation`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:802` in `loginOtpBasedUser`). That would hit the guide's High rule "a changed table is used by 3 or more modules".
- **Behaviour risks to note (not part of the script's rules):**
  - A real user can be locked out of web and app at the same time, because both use the same backend routes.
  - On web mobile login the user would see "Invalid OTP" instead of a lockout message (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:409`).
  - In the app, a lockout `status_code` equal to `NT_0000` or `NT_1017` would log the user out or show a generic popup (`Nadi-Tarangini-App:lib/common_files/api_services/http_api_service.dart:120`).

## 10. QA to rerun

- **Sanity (web staging):** auth, on page `auth.login` (`GET login`), OTP login by mobile and by email.
- **Regression:** auth only; no related modules (impact-facts.md).
- **What QA can and cannot do here** (references/qa-scope-rules.md: no real OTP codes; skip steps that need one):
  - Entering wrong codes does not need the real code. It does need an OTP to have been sent first: with none cached, the answer is "Expired OTP" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136`). Sending one delivers a real code to a registered mobile or email. Whether QA may do this on staging is §11 Q9.
  - Steps that need the correct code are skipped: success before the limit, and "the correct code is refused after the limit". Note them as skipped (no real OTP codes).
- **Not covered by QA (developer must test):**
  - App: **LoginWithOtpScreen**, mobile and email (`Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart:367`). This is the only app screen the change reaches (§5); impact-facts.md lists it under "Not covered by QA" (QA tests web only).
  - The `is-nt-locator` branch of `POST otp/verify-otp` (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:142`): no caller in this workspace.

## 11. Needs confirmation

1. **PO:** How many wrong attempts are allowed? This is a product decision, so it goes to the PO; PRD §13 Q5 asks Dev, and BRD §12 Q5 asks PO / dev.
2. **PO:** What happens when the limit is reached: the current OTP is invalidated and a new one must be requested, the mobile/email is locked for a time (how long?), or the account is blocked? If the account is blocked, is it the existing inactive state (`user_personal_info.is_active = 0`, which login turns away as "Invalid username", `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:460`), and who unblocks it? (This decides Medium vs High, §9.)
3. **PO:** What does the count apply to: one OTP, one mobile number or email, or one user across both? Does requesting a new OTP reset it? (Resend overwrites the OTP today: `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:381`.)
4. **PO:** Should requesting OTPs (send) also be limited, or only verifying? The free text names verification only.
5. **PO / Dev:** What message should the user see at the limit, in all seven required languages? On web mobile login the Frontend currently replaces any backend message with "Invalid OTP" (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:409`). Should that caller change so the message is shown?
6. **Dev / PO:** Should the same limit apply to the other OTP checks in this controller: sign-up/profile verification codes (`POST otp/verify-verification-otp`, `Ashoka-World-Backend:routes/api.php:794`) and Jiva (`POST nt-jiva/verify-otp`, `Ashoka-World-Backend:routes/api.php:799`)? Jiva shares the `otp_<phone>` cache entry with mobile login (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:296`).
7. **Dev:** Which client sends the `is-nt-locator` and `user-id` headers to `POST otp/verify-otp` (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:142`)? None in this workspace does, but that caller would also meet the limit.
8. **Dev:** Which cache store do staging and production use (`Ashoka-World-Backend:config/cache.php:18` reads it from the environment, default `file`)? Is it shared by all backend servers? OTPs already depend on it.
9. **QA:** May QA send login OTPs to a registered staging mobile/email and enter wrong codes to test the limit? May the fixed-code test accounts in code (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:76`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:378`) be used on staging? **PO / Dev:** should those test accounts be exempt from the limit?
10. **Dev:** Which HTTP status and `status_code` will the limit response use? The app treats `NT_0000` as "log out" and `NT_1017` as a generic error (`Nadi-Tarangini-App:lib/common_files/constants/error_const.dart:4`, `Nadi-Tarangini-App:lib/common_files/constants/error_const.dart:5`).

## 12. Document control

| Field | Value |
|---|---|
| Status | Draft (only a human changes it) |
| Date | 2026-10-26 |
| Reviewer | TBD: auth owner (modules.yaml owner is TBD) for dev; PO for §11 Q1-Q5; QA lead for §10 and §11 Q9 |
| Ticket | adhoc-otp-attempt-limit (free text) |
| Built from | atreya-docs/dev/adhoc-otp-attempt-limit/impact-facts.md; commits in the front matter |
| Doc-checker | Ran: checks/impact-check.md (62 claims: 60 verified, 0 mismatch, 2 not provable; both fixed) |
