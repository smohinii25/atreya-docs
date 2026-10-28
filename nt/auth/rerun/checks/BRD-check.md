# Doc check: atreya-docs/nt/auth/rerun/BRD.md
Checked 2026-10-26 against commits Ashoka-World-Backend 8dfbb37db7d71a400b3656bd50fbed6173908a24, Nadi-Tarangini-App 0b7deec6de2b0b8b4f05eab4be8c8430523829bf, Nadi-Tarangini-Frontend e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d.
Summary: 58 claims · 56 verified · 1 mismatch · 1 not provable · 0 secret risk

## Mismatch
| # | Doc line | Claim | What the code shows | Source |
|---|---|---|---|---|
| 1 | 85 (§6) | "A mobile number can be registered only once." | The "already exists" refusal applies only when the number is not on the master whitelist: `if ($response['status'] == true && !MasterWhitelist::isMobile(...))` then "Phone number already exists". Whitelisted numbers can be registered again. Needs "(except numbers on the master whitelist)". | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:823-825` |

## Not provable
| # | Doc line | Claim | Why | Suggested fix |
|---|---|---|---|---|
| 1 | 136 (§10) | "the website and app both rely on the same backend rules" | Cites only AUTH-R01/R06/R08 (PRD IDs), no code showing both clients call the same endpoints with no client-side rules. The web signup uses `v2/signup` and the app `signupV2`; both map to `SignUpV2`, but login code on each client was not cited. | Cite `routes/api.php:744`, `:1636` and the client call sites, or soften the wording |

## Secret risk
None found. The BRD shows no keys, tokens or passwords. It mentions the "atreya" plus four digits password pattern in words only (line 160), which is a design concern, not a credential value.

## Verified (sample)
- Both username and password required: "Both username and password are required" (`AuthController.php:429`).
- Unknown username refused: "Invalid username" 401 (`AuthController.php:466`); wrong password: `Hash::check` then "Invalid password" (`AuthController.php:481`).
- Blocked user refused in `loginOtpBasedUser`: `is_active == 0` gives "User has been blocked" (`AuthController.php:814`).
- Code sent only to a registered number or email: "Phone number not registered" (`OtpSmsController.php:71`), "Email not registered" (`:373`). Cache lasts 5 minutes (`:79`); "Expired OTP" (`:136`).
- Length and country code checks: "Invalid phone number length" (`OtpSmsController.php:54`), "The provided country code is not valid..." (`:57`).
- Registration password needs a digit; names letters and spaces only (`SignUpController.php:708-709`); "Invalid salutation type" (`:832`); "Please select a valid gender" (`:838`).
- Change password: current password required (`UpdatePasswordController.php:16`), digit message (`:24`), min 6 (`:38`), must differ from old (`:56`).
- Forgot password: needs only `user_name` (`AuthController.php:1652`), "atreya" plus rand(1000, 9999) (`:1684`), email and WhatsApp send (`:1710`, `:1740`), `DB::rollBack()` plus "No contact information found. Please contact customer care." (`:1784`).
- Admin switch: `switchToAdmin` and `switchToDoctor` call `loginOtpBasedUser` (`DashboardController.php:1374`, `:1404`); college and admin sign-up routes exist (`routes/web.php:328-329`).
- Dependencies: FCM token and topic subscription in `login_bloc.dart:173,196`; "Account Created" notification (`SignUpController.php:1085`); S3 upload (`SignUpController.php:491`); Samvit Chakra `register-student` call (`:662`).
- Environments all "TO FILL" (`atreya-docs/environments.md`); five unused auth routes (`atreya-docs/not-in-use.md` line 63); required languages (`qa-scope-rules.md:13`); web lang folder holds only `en/` and `en_patient.json`.
- Needs-confirmation items Q5, Q7, Q9, Q10 match code: fixed test numbers and emails with code 123456 (`OtpSmsController.php:76`, `:378`); plain password passed to Samvit Chakra (`SignUpController.php:668`).

Not checked in depth: PRD-only sourced rows (BR-01 to BR-10 rely on AUTH-R IDs, whose underlying code claims were spot-checked above).
