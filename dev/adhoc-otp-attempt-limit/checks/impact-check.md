# Doc check: atreya-docs/dev/adhoc-otp-attempt-limit/impact.md
Checked 2026-10-26 against commits Ashoka-World-Backend 8dfbb37, Nadi-Tarangini-App 0b7deec, Nadi-Tarangini-Frontend e8a9742 (doc stamp; working tree read, commit hashes not re-verified).
Summary: 62 claims · 60 verified · 0 mismatch · 2 not provable · 0 secret risk

## Mismatch
None.

## Not provable
| # | Doc line | Claim | Why | Suggested fix |
|---|---|---|---|---|
| 1 | 114 | "every login path checks it" (the is_active flag) | Only AuthController.php:475 and :814 were found and cited; "every" is not shown by the cited code | Say "the two login paths at AuthController.php:475 and :814" or cite the rest |
| 2 | 153 | "Doc-checker: Not run in this pass" | Process statement, stale once this check exists | Update after this report (human) |

Minor wording notes (not counted): line 133 labels Q1 as "PO" while PRD §13 Q5 is owned by "Dev"; BRD §12 Q5 is "Product owner / dev". AuthController.php:475 is the `if is_active == 0` line and :814 is the 401 return line of the same check; both are correct for the claim.

## Secret risk
None. The doc holds no key, token or password. (It cites the fixed test-account lines OtpSmsController.php:76 and :378 only by line.)

## Verified (sample)
- OtpSmsController.php:199 and :457: wrong code returns 400 "Invalid OTP" (email adds NT_1213); no attempt counter in either method (no attempt/throttle/increment text in the controller).
- :79 and :381: `Cache::put('otp_' . $phone / $email, $otp, now()->addMinutes(5))`; 6-digit via rand(100000, 999999).
- :136 and :439: "Expired OTP" 400 when no cached OTP; :140 and :443: Cache::forget on a correct code.
- :142: `is-nt-locator` and `user-id` header branch; no app/web caller sends them (only the Frontend verify call at loginController.php:378 posts mobile_no, country_code, otp).
- :242 and :296 (Jiva) use `otp_<phone>`; routes/api.php:798-799 nt-jiva send-otp/verify-otp; :794 verify-verification-otp; :789, :791 the two routes; `otp` group at :787 has no extra middleware (enclosing `Route::middleware('api')` at :736).
- Kernel.php:48 throttle 100000,1; config/cache.php:18 `env('CACHE_DRIVER','file')`.
- Frontend loginController.php:407-409 always "Invalid OTP" after a failed mobile verify; :720 passes the backend message through the email path; login.js:830/833 re-enable button and show response.message; routes/web.php:86, :88, :313.
- App http_api_service.dart:120/122 (NT_0000 logout, NT_1017 generic popup), error_const.dart:4-5, login_bloc.dart:299 and :461 use response['message']; VerifyOtpApi/VerifyEmailOtpApi dispatched only in login_with_otp.dart (367, 374), login_bloc and login_event.
- impact-facts.md match: modules (auth direct, none related), routes and callers, spans 98-201 and 424-459, Medium signals, QA lists, doc/diagram citations (PRD AUTH-R02/R03/§6/§9, BRD §6, seq-AUTH-R02 response 200/400).
- PRD §13 Q5 (PRD.md:354), BRD §12 Q5 (BRD.md:144), PRD §9 sentence (PRD.md:302), AUTH-R12 is free (last is AUTH-R11), no seq diagram for AUTH-R03, seven languages (BRD.md:129), qa-scope-rules OTP rule.
