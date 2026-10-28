# Doc check: atreya-docs/nt/auth/BRD.md
Checked 2026-10-26 against commits Ashoka-World-Backend 8dfbb37, Nadi-Tarangini-App 0b7deec, Nadi-Tarangini-Frontend e8a9742 (doc stamp).
Summary: 72 claims · 67 verified · 4 mismatch · 1 not provable · 0 secret risk

## Mismatch
| # | Doc line | Claim | What the code shows | Source |
|---|---|---|---|---|
| 1 | 138 (§9 Cloud file storage) | S3 "used in the sign-in and registration code" | `AuthController.php:139` is a commented-out line (`// $url = 'https://atreyaproduction.s3...'`). `SignUpController.php:491` (`uploadFileToS3`) is in the older `SignUp` method (starts line 43), which the BRD itself calls unused by any page. The live S3 use is `S3BucketUrlService::generateUrl` at `AuthController.php:141` and `SignUpController.php:834`, which are not cited. | Ashoka-World-Backend:app/Http/Controllers/AuthController.php:139, SignUpController.php:491 |
| 2 | 115 (BR-09) and 133 (§9) | "After sign-in, the user's device is registered to receive notifications" | The app calls `updateFCMtokenAshoka` only inside `if (userData['role_id'] != 2)`, so role-2 users (sent to `/reportScreenPatient`) are not registered by the app. The BR does not say so. | Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:~190-196 |
| 3 | 99 (§6 change-password rule) | "the new one needs a digit" | Cited lines 16, 38, 56 show current-password-required, the 6-character check and the differ-from-old check. The digit rule is at `UpdatePasswordController.php:19` (regex) and its message at line 24, which are not cited. | Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:16,38,56 |
| 4 | 97 (§6) | "First and last names may contain only letters and spaces" | Cited line 709 shows only `lastname`; `firstname` is at line 713. | Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:709 |

## Not provable
| # | Doc line | Claim | Why | Suggested fix |
|---|---|---|---|---|
| 1 | 79 (§5 step 6) | "the email or mobile number is confirmed with a one-time code, then the account is created" | Sources are PRD J5 only. `SignUpV2` (lines 701 to 1130) has no OTP or verification check, so the order is not enforced or shown in backend code. | Cite the web/app sign-up code that gates submit on verification, or move the ordering to Needs confirmation |

## Secret risk
None. Lines 8-10 and 178 hold git commit hashes only.

## Verified (sample)
- Line 88: both username and password required, 400 message: AuthController.php:415, 429.
- Line 90: inactive user gets "Invalid username": AuthController.php:460, 466; loginOtpBasedUser 802. The later "User has been blocked" branch is dead code, but the BRD does not rely on it.
- Line 92: OTP cached 5 min, "Expired OTP": OtpSmsController.php:79, 136.
- Line 94: "Phone number already exists" except master whitelist: SignUpController.php:821, 825.
- Line 95 and BR-06: username taken, and mobile "Phone number already exists": CheckUserExistOrNotController.php:195 and the mobile check in `checkMobileNumberV2`.
- Line 100: forgot password needs only `user_name`, sets new password 'atreya'+4 digits: AuthController.php:1652, 1684.
- Line 101: both channels fail, rollback and "contact customer care": AuthController.php:1784.
- Line 134: "Account Created" notification: SignUpController.php:1085.
- Line 147: both routes run `SignUpV2`: routes/api.php:744, 1636.
- Q9, Q11, Q5: 1636/1639 have no middleware; the age 18-100 check is in the old method (SignUpController.php:215-222); fixed test numbers and emails (OtpSmsController.php:76, 378).
- Line 39 and BR-10: admin switch calls `loginOtpBasedUser`: DashboardController.php:1374, 1404.
