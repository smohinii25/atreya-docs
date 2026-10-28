# Doc check: atreya-docs/nt/auth/rerun/PRD.md
Checked 2026-10-26 against commits Ashoka-World-Backend 8dfbb37db7d71a400b3656bd50fbed6173908a24, Nadi-Tarangini-App 0b7deec6de2b0b8b4f05eab4be8c8430523829bf, Nadi-Tarangini-Frontend e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d.
Summary: ~150 claims · ~143 verified · 3 mismatch · 4 not provable · 2 secret risk

(Claim counts are approximate: every cited message, status, route, middleware, call site and screen transition was checked; the many "TO FILL" and Open-question items were not counted.)

## Mismatch
| # | Doc line | Claim | What the code shows | Source |
|---|---|---|---|---|
| 1 | 116 (AUTH-R06), 312 (§12 Samvit Chakra) | `POST v2/signup` / `signupV2` (`SignUpController@SignUpV2`) "registers the same person with the Samvit Chakra system"; "Sign-up posts name, email, mobile and password to `/api/register-student`" | The only `register-student` call (and the only `samvit_chakra_url` use) is at line 662 inside `SignUp` (v1, starts line 43, `POST signup`). `SignUpV2` starts at line 701 and has no Samvit/LMS call. So the Samvit registration is done by the older `POST signup`, not by the routes the web and app actually use. | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:43`, `:662`, `:701` |
| 2 | 277 (§9 Plain password copies), 313/§13 Q10 | "Sign-up passes the plain password to the confirmation message and to the Samvit Chakra registration call (`SignUpController.php:590`, `:668`)" | Lines 590 and 668 are both in `SignUp` v1. In `SignUpV2` the plain password (`password_original`) goes into the confirmation email (line 1033) and the WhatsApp sign-up message (lines 1055-1062), but not to Samvit Chakra. Cite 1033/1055 for the live path and say the Samvit call is v1 only. | `SignUpController.php:590`, `:668`, `:1033`, `:1055` |
| 3 | 311 (§12 S3) | S3 evidence `AuthController.php:139` | Line 139 is a commented-out URL. Active S3 use in AuthController is `S3BucketUrlService::generateUrl(...)` at 141/151 (URL building only). The `uploadFileToS3` calls (491, 539) are in `SignUp` v1, not V2. | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:139`, `:141`; `SignUpController.php:491` |

## Not provable
| # | Doc line | Claim | Why | Suggested fix (cite X / move to Needs confirmation) |
|---|---|---|---|---|
| 1 | 121 (AUTH-R06), 330 (Q14) | Username in use gives "a 4xx response"; Q14 asks which HTTP status | Code is specific: 400 with status_code NT_1383, message "User already exists with same username. Please try with another username" | Cite `SignUpController.php:858-859` and state 400; answer Q14 (wording differs from `checkUsername` NT_1366 at `CheckUserExistOrNotController.php:195`) |
| 2 | 154 (AUTH-R09), 324 (Q8) | HTTP behaviour of the "no digit" branch unknown | Code at `UpdatePasswordController.php:28-34` returns 400, but reads `$message['status_code']` from a `['message'=>...]` array, so a missing-index error may occur first; honestly unresolved, keep in Needs confirmation | Keep Q8 as is |
| 3 | 278 (§9 Languages) | "Backend messages in this module are English strings" | No citation; true of the messages read, but not a cited fact | Cite one message line, or move to Needs confirmation |
| 4 | 116 (AUTH-R06) | "creates the user" in SignUpV2 | No line cited for the creation step (helpers `saveDoctor` 1219, `savePatientAccount` 1311 exist) | Cite `SignUpController.php:1219` |

## Secret risk
| # | Doc line | Type |
|---|---|---|
| 1 | 82 (AUTH-R02 last criterion) | Fixed bypass OTP value "123456" stated in plain text (the test numbers themselves are not copied; the value is an auth-bypass credential in production code) |
| 2 | 92 (AUTH-R03 last criterion) | Same fixed OTP value "123456" for the test emails |

(Line 105 gives the forgot-password format "atreya" plus four digits; that is a generation pattern, not a live password, noted only for awareness.)

## Verified (sample)
- Route list and middleware (737, 739, 741, 744, 759, 760, 763, 764, 777, 788-791, 793, 794, 968, 971, 972, 975, 1426, 1427, 1636, 1639): `Ashoka-World-Backend:routes/api.php`; v2 group has no middleware, auth.token group covers logout/editFcmToken/validateCorporateCode/updatepassword.
- `v2/loginValidation` messages and codes (400 x3, 401 Invalid username/Invalid password, role 3 and 5 excluded, delete_by_patient for role 2, 500): `AuthController.php:415-528`.
- `loginOtpBasedUser` takes `id`, no OTP check, 401 blocked fallback: `AuthController.php:798-983`.
- Forgot password: "atreya"+rand(1000,9999), 404 Invalid username, 422 Password not updated, three 200 messages, 422 no contact info with rollback: `AuthController.php:1652-1806`.
- `editFcmToken` uses `user_id` header, "Fcm Token Updated Successfully.", 500 rollback: `AuthController.php:1859-1874`.
- OTP send/verify (mobile and email): lengths, "Phone number not registered", 5-minute cache keys `otp_<code> <number>` / `otp_<email>`, dummy numbers/emails skip sending, Expired/Invalid OTP: `OtpSmsController.php:54-199`, `:359-457`.
- Verification OTP: type/action `in:` lists, 422 "The code is invalid or has expired...", success message: `OtpSmsController.php:479-483`, `:564`, `:597-666`.
- Sign-up V2 validation rules, 400 messages (phone exists with whitelist, salutation, gender, min 6 password), Firebase "Account Created": `SignUpController.php:706-908`, `:1085`; v1 age checks 220/226.
- `checkUsername`/`checkMobileNumber` messages: `CheckUserExistOrNotController.php:182-301`; `updatepassword` messages: `UpdatePasswordController.php:24-64`.
- Web routes (313, 316, 317, 325, 328, 329, 331, 332, 307, 308), frontend call sites (loginController 63/79/94/209/255/319/350/378/386/446/684/696/728; NewSignUpController 91/251/295; NtLiteSignUpController 77/132/170; DashboardController 1374/1404), app API repository lines and screen transitions all match.
