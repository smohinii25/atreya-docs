# auth: run 1 vs run 2 (PRD and BRD)
Run 1: nt/auth/PRD.md, nt/auth/BRD.md · Run 2: nt/auth/rerun/PRD.md, nt/auth/rerun/BRD.md
Same commits: Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`, Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`, Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d`.
Purpose: measure how stable /atreya:prd and /atreya:brd are, and decide what to merge.
Rule: a difference is kept only if the doc-checker confirms it against code; conflicts are "Needs confirmation". PRD.md and BRD.md are not changed until the user reviews this file.

Notation: R1 = run 1, R2 = run 2. Citations are written as `File.php:line` with the repo prefix shortened to the file name only in the "Cited sources" column (BE = Ashoka-World-Backend, FE = Nadi-Tarangini-Frontend, APP = Nadi-Tarangini-App); line numbers are exactly as written in the docs. Section numbers of open questions differ between runs (mapping in Stability notes).

## Summary
| Doc | Only in run 1 | Only in run 2 | Different | Conflict | Wording only |
|---|---|---|---|---|---|
| PRD | 2 | 41 | 57 | 2 | 12 listed (+3 candidate rows P64, P88, P93) |
| BRD | 1 | 14 | 33 | 1 | 6 listed (+1 candidate row B50) |
| Total | 3 | 55 | 90 | 3 | 18 listed (+4 candidates) |

## PRD differences
| # | Where | Kind | Run 1 says | Run 2 says | Cited sources (both sides) | Verdict | Decision |
|---|---|---|---|---|---|---|---|
| P1 | §1 Overview | Only in run 2 | No route/page line cites in the overview | Cites routes: "e.g. `routes/api.php:737`, `routes/api.php:1639`" and web "`routes/web.php:313`, `routes/web.php:325`" | R1: facts.md only. R2: BE routes/api.php:737, :1639; FE routes/web.php:313, :325 | R1 n/a · R2 Verified | Add from run 2 |
| P2 | §1 Overview | Only in run 2 | Lists mobile app screens as "5 screens" only | Names the app folders `Login/view/` and `signup/view/signup_screen.dart` | R2: APP lib/common_files/Login/view/, signup/view/signup_screen.dart | R1 n/a · R2 Verified | Add from run 2 |
| P3 | §1 Overview | Only in run 2 | Does not name the five unused routes in §1 | Names them: `POST login`, `POST logout`, `POST validateCorporateCode`, `GET checkusernameormobileno`, `GET getdetailsbymobileno` | none vs §6 | R1 n/a · R2 Verified | Add from run 2 |
| P4 | §2 row "Not logged in" evidence | Different | Evidence lines 788, 777, 744; lists "Log in, OTP login, forgot password, sign-up, availability checks, verification OTP" | Evidence lines 739, 777, 788, 793, 759; also lists "salutation and currency lists" | R1: BE routes/api.php:788, :777, :744. R2: :739, :777, :788, :793, :759 | R1 Verified · R2 Verified | Keep run 2 |
| P5 | §2 paragraph after table | Only in run 2 | Roles "not part of this module: see §13 Q1" | "`POST v2/loginValidation` looks up only active users whose `role_id` is not 3 or 5" | R2: BE AuthController.php:459, :461; FE loginController.php:728 | R1 n/a · R2 Verified | Add from run 2 |
| P6 | §3 J1 step list | Only in run 2 | J1 is a paragraph; no controller for GET login | "rendered by `loginController@login`" | R2: FE routes/web.php:313, auth/login.blade.php | R1 n/a · R2 Verified | Add from run 2 |
| P7 | §3 J3 checkGeoIPValidity | Different | `POST checkGeoIPValidity` cited at api_repository.dart:2519 | Login bloc calls `checkGeoIPValidity` "at two places" | R1: APP api_repository.dart:2519. R2: APP login_bloc.dart:125, :375 | R1 Verified · R2 Verified | Merge both |
| P8 | §3 J3 forgot-password link | Only in run 2 | Only ForgotPasswordScreen is tied to /forgotPasswordScreen | "the username screen also leads to `/forgotPasswordScreen`" | R2: APP login_with_username_screen.dart, login_with_otp.dart | R1 n/a · R2 Verified | Add from run 2 |
| P9 | §3 J3 screen-file citations | Only in run 2 | No per-screen file cites in J3 (directory only) | Cites login_screen.dart, login_with_username_screen.dart, login_with_otp.dart | R1: APP lib/common_files/Login/. R2: the three files | R1 Verified · R2 Verified | Add from run 2 |
| P10 | §3 J4 web route | Only in run 2 | No route line for `POST checkForgotPassword` | Cites `routes/web.php:317` | R2: FE routes/web.php:317 | R1 n/a · R2 Mismatch | USER: add, cite routes/web.php:318 |
| P11 | §3 J5 web route lines | Only in run 2 | No route lines for sign-up pages/endpoints | Cites web.php:328, :331, :332, :307, :308 | R2: FE routes/web.php:328, :331, :332, :307, :308 | R1 n/a · R2 Verified | Add from run 2 |
| P12 | §3 J5 NT Lite | Different | NT Lite "has its own sign-up calling `POST v2/signup`" (NtLiteSignUpController.php:77) | NT Lite "has its own username, mobile and submit calls", submit to `POST v2/signup` | R1: FE NtLiteSignUpController.php:77. R2: :77, :132, :170 | R1 Verified · R2 Verified | Keep run 2 |
| P13 | §3 J5 app destination | Only in run 2 | App SignUpScreen goes to `/signupScreen`-> `POST signupV2` only | "goes to `/loginScreen` or `/webViewScreen`" | R2: APP api_repository.dart:675, signup_screen.dart | R1 n/a · R2 Verified | Add from run 2 |
| P14 | AUTH-R01 description | Only in run 2 | No description paragraph | Case-insensitive lookup among active users, roles 3 and 5 excluded, hash check, token returned; token generated if none | R2: BE AuthController.php:415, :459, :481, :514, :493 | R1 n/a · R2 Verified | Add from run 2 |
| P15 | AUTH-R01 blocked user | Different | AC: "Given a blocked user, then 401 'User has been blocked'" in R01 | No blocked-user AC in R01; blocked appears only in §8 row (401, line 476) | R1: BE AuthController.php:476 (in R01 source). R2: :476 only in §8 | R1 Mismatch · R2 Verified | Keep run 2 |
| P16 | AUTH-R01 unknown user | Different | "Given an unknown username, then 401 'Invalid username'" | "unknown username or a user without a role" 401 | R1: AuthController.php:466. R2: :466, :471 | R1 Verified · R2 Verified | Keep run 2 |
| P17 | AUTH-R01 deleted-by-patient | Only in run 2 | not present | "role-2 user flagged `delete_by_patient`, then 401 'Invalid username'" | R2: BE AuthController.php:485 | R1 n/a · R2 Verified | Add from run 2 |
| P18 | AUTH-R01 success and 500 | Only in run 2 | Success response not in R01 AC (500 only in §8) | AC: 200 "Success" with `user_id`, `auth_token`, `role_id`, `doctor_data`; 500 "Internal server error" | R2: BE AuthController.php:514, :528 | R1 n/a · R2 Verified | Add from run 2 |
| P19 | AUTH-R02 description | Only in run 2 | no description | 6-digit code, cache key `otp_<country code> <number>`, 5 minutes, removed on success | R2: BE OtpSmsController.php:77, :79, :89, :136, :188 | R1 n/a · R2 Verified | Add from run 2 |
| P20 | AUTH-R02 verify AC | Different | Wrong OTP 400 "Invalid OTP", expired 400 "Expired OTP", correct 200 | Adds: code "empty, non-numeric or not 6 digits" gives 400 "Invalid OTP"; no cached code gives "Expired OTP" | R1: OtpSmsController.php:127, :136, :197. R2: :127, :136, :197, :199 | R1 Verified · R2 Verified | Keep run 2 |
| P21 | AUTH-R02 fixed test numbers | Only in run 2 | not present anywhere | "Given two fixed test numbers listed in code, the code is a fixed test code and no SMS is sent (§13 Q5)" | R2: BE OtpSmsController.php:76, :77, :81 | R1 n/a · R2 Verified | Add from run 2 |
| P22 | AUTH-R02 5-minute AC | Different | Separate AC "A sent OTP is kept for 5 minutes" | In description only, not an AC | R1: OtpSmsController.php:79. R2: :79 | R1 Verified · R2 Verified | Wording only |
| P23 | AUTH-R02 source line 82 | Only in run 1 | Source list includes OtpSmsController.php:82 | Not cited | R1: BE OtpSmsController.php:82 | R1 Verified · R2 n/a | Keep run 1 |
| P24 | AUTH-R03 description | Only in run 2 | no description | Code cached 5 minutes under `otp_<email>`, emailed | R2: BE OtpSmsController.php:379, :381, :409 | R1 n/a · R2 Verified | Add from run 2 |
| P25 | AUTH-R03 fixed test emails | Only in run 2 | not present | "two fixed test emails listed in code ... no email is sent (§13 Q5)" | R2: BE OtpSmsController.php:378, :379, :383 | R1 n/a · R2 Verified | Add from run 2 |
| P26 | AUTH-R03 verify AC | Different | missing email, missing OTP, expired, wrong, correct (wrong listed before correct) | same list ending "otherwise 400 'Invalid OTP'" | R1: OtpSmsController.php:433-457 listed. R2: :433, :436, :439, :452, :457 | R1 Verified · R2 Verified | Wording only |
| P27 | AUTH-R03 5-minute AC | Different | AC "A sent OTP is kept for 5 minutes" | In description only | R1: :381. R2: :381 | R1 Verified · R2 Verified | Wording only |
| P28 | AUTH-R04 description | Only in run 2 | Only "client signs the user in through `POST loginOtpBasedUser`" | Takes a user `id`, finds active user, creates token; "The code in this method does not check an OTP (§13 Q4)" | R2: BE AuthController.php:798, :806, :820 | R1 Verified · R2 Verified | Add from run 2 |
| P29 | AUTH-R04 "User has been blocked" | Conflict | "Given a blocked user, then 401 'User has been blocked'" (line 814) | "Given a user whose role is not handled by the response branches, then 401 'User has been blocked'" (line 983) | R1: AuthController.php:806, :814. R2: :806, :810, :983 | R1 Mismatch · R2 Verified | USER: code as it runs (Y1) |
| P30 | AUTH-R04 unknown user | Different | "Given an unknown user, then 401 'Invalid username'" | "no active user with that id or a user without a role" | R1: :806. R2: :806, :810 | R1 Verified · R2 Verified | Keep run 2 |
| P31 | AUTH-R04 callers | Different | Source cites FE loginController.php:446, DashboardController.php:1374, APP :431 | Also cites DashboardController.php:1404 | R1: DashboardController.php:1374. R2: :1374, :1404 | R1 Verified · R2 Verified | Keep run 2 |
| P32 | AUTH-R05 description | Only in run 2 | "backend sends the password by WhatsApp and/or email" | New password of the form [prefix] plus four digits, for active non-deleted user, sent by email and WhatsApp | R2: BE AuthController.php:1684, :1710, :1740 | R1 Verified · R2 Verified | Add from run 2 |
| P33 | AUTH-R05 missing username | Different | "the request fails validation (`user_name` required)", no status or text | Message "The username is required" and status 404 | R1: AuthController.php:1652. R2: :1655, :1666 | R1 Verified · R2 Verified | Keep run 2 |
| P34 | AUTH-R05 unknown user | Different | "unknown username, then 404 'Invalid username'" | "unknown or deleted user" 404 | R1: :1679. R2: :1679 | R1 Verified · R2 Verified | Keep run 2 |
| P35 | AUTH-R05 success status | Only in run 2 | Success messages without status | "200 'Forgot password successfully. Password sent to whatsapp/email'" (200 on all three) | R2: BE AuthController.php:1751, :1762, :1773 | R1 Verified · R2 Verified | Add from run 2 |
| P36 | AUTH-R05 no contact info | Different | "No contact information found. Please contact customer care." no status | 422 with the message "and the change is rolled back" | R1: :1784. R2: :1784 | R1 Verified · R2 Verified | Keep run 2 |
| P37 | AUTH-R06 description | Only in run 2 | no description | `v2/signup` and `signupV2` both run `SignUpV2`; confirmation email and WhatsApp carry the plain password; older `POST signup` (line 43) has extra fields, age check, Samvit Chakra and S3 | R2: BE SignUpController.php:701, :927, :1033, :1055, :43, :220, :491, :662 | R1 n/a · R2 Verified | Add from run 2 |
| P38 | AUTH-R06 mobile exists | Different | "Given a mobile number that already exists, then 400" | "already registered (and not on the master whitelist)" 400 | R1: SignUpController.php:825. R2: :825 | R1 Verified · R2 Verified | Keep run 2 |
| P39 | AUTH-R06 duplicate username | Only in run 2 | not in AC | 400 "User already exists with same username. Please try with another username"; wording differs from `checkUsername` | R2: BE SignUpController.php:853, :858, :859; CheckUserExistOrNotController.php:195 | R1 n/a · R2 Verified | Add from run 2 |
| P40 | AUTH-R06 password length | Only in run 2 | not in AC | 400 "Minimum 6 digits password is required" for password shorter than 6 | R2: BE SignUpController.php:908 | R1 n/a · R2 Verified | Add from run 2 |
| P41 | AUTH-R06 gender | Different | "an invalid gender, 400 'Please select a valid gender'" | "Given a salutation and gender that do not fit" gives that message | R1: SignUpController.php:838. R2: :838, :842, :847 | R1 Mismatch · R2 Verified | Keep run 2 |
| P42 | AUTH-R06 country code | Different | message with no status | 400 "Provided country code is not valid for the given phone number" | R1: :727. R2: :727 | R1 Verified · R2 Verified | Keep run 2 |
| P43 | AUTH-R06 required fields cites | Different | Required-fields line has no per-bullet cite (source list 706, 708, 712, 717, 722, 727, 766) | Cites 706, 708, 709, 712, 714, 717, 722 | R1/R2: BE SignUpController.php lines as listed | R1 Verified · R2 Verified | Keep run 2 |
| P44 | AUTH-R07 description | Only in run 2 | no description | `checkUsername` looks for an active user; `checkMobileNumber` validates number and code | R2: BE CheckUserExistOrNotController.php:176, :229 | R1 n/a · R2 Verified | Add from run 2 |
| P45 | AUTH-R07 country-code mismatch | Only in run 2 | not in R07 AC (only in §8) | AC: 400 "The provided country code is not valid for the given phone number" | R2: BE CheckUserExistOrNotController.php:301 | R1 n/a · R2 Verified | Add from run 2 |
| P46 | AUTH-R07 500 | Only in run 2 | not present | "An unexpected error gives 500 'Internal server error'" | R2: BE CheckUserExistOrNotController.php:209, :282 | R1 n/a · R2 Verified | Add from run 2 |
| P47 | AUTH-R08 5-minute validity | Only in run 2 | R08 does not state validity | "the code is cached for 5 minutes" | R2: BE OtpSmsController.php:480, :612 | R1 n/a · R2 Verified | Add from run 2 |
| P48 | AUTH-R08 mobile send failure | Only in run 2 | only email failure 500 | also mobile failure 500 "OTP not sent. Please check the phone number" | R2: BE OtpSmsController.php:564, :606, :617 | R1 n/a · R2 Verified | Add from run 2 |
| P49 | AUTH-R08 mobile checks | Only in run 2 | not present | 400 "Invalid phone number length" and 400 country-code mismatch | R2: BE OtpSmsController.php:597, :600 | R1 n/a · R2 Verified | Add from run 2 |
| P50 | AUTH-R08 field names | Different | "country code and mobile number are required when type is mobile" | "`country_code` and numeric `mobile_no` are required" | R1: :479, :480. R2: :481, :482, :483 | R1 Verified · R2 Verified | Keep run 2 |
| P51 | AUTH-R08 Screens | Different | auth.signup (web) only | auth.signup (Web), SignUpScreen, KycScreen, AddClinicScreen, EditClinicScreen (App) | none | R1 Verified · R2 Verified | Keep run 2 |
| P52 | AUTH-R09 description | Only in run 2 | AC "Requires a logged-in user and the current password" | Identifies user by `user_id` header; requires `current_password` and `new_password`; replaces hash | R2: BE UpdatePasswordController.php:12, :16, :58 | R1 Verified · R2 Verified | Add from run 2 |
| P53 | AUTH-R09 no active user | Only in run 2 | not in AC (not in §8) | 400 "User not found" | R2: BE UpdatePasswordController.php:51 | R1 n/a · R2 Verified | Add from run 2 |
| P54 | AUTH-R09 no-digit HTTP status | Different | message only, no status, no question | "HTTP behaviour of this branch is §13 Q8" (unconfirmed) | R1: :24. R2: :24 | R1 Verified · R2 Verified | Keep run 2 |
| P55 | AUTH-R09 Screens | Different | "web change-password (`POST updatePassword`), app MyAccountScreen" | "MyAccountScreen (App), web change-password controller (`ChangePasswordController@updatePassword`)" | none | R1 Verified · R2 Verified | Merge both |
| P56 | AUTH-R10 description | Only in run 2 | "web and app send the device's push token" | saves `fcm_token` for `user_id` header, returns "Fcm Token Updated Successfully." | R2: BE AuthController.php:1859, :1862, :1865 | R1 Verified · R2 Verified | Add from run 2 |
| P57 | AUTH-R10 failure | Different | "A server failure gives 500 'Internal server error'" | "database error, then 500 ... and the transaction is rolled back" | R1: :1874. R2: :1874 | R1 Verified · R2 Verified | Keep run 2 |
| P58 | AUTH-R10 Screens | Different | "after login (web and app)" | LoginScreen, LoginWithOtpScreen, LoginWithUsernameScreen (App); web login pages | none | R1 Verified · R2 Verified | Keep run 2 |
| P59 | AUTH-R11 callers | Only in run 2 | no caller detail | GET variants "called by no screen"; POST by SignUpScreen, KycScreen, web pages | R2: APP api_repository.dart:812, :1709; FE NewSignUpController.php:24 | R1 n/a · R2 Verified | Add from run 2 |
| P60 | AUTH-R11 500 cites | Different | 500 "Internal server error" without line | cites SignUpController.php:1373, :1151 | R1: :1353, :1130. R2: :1353, :1130, :1373, :1151 | R1 Verified · R2 Verified | Keep run 2 |
| P61 | AUTH-R11 Screens | Different | sign-up, profile, KYC, admin create-user pages (web); SignUpScreen and clinic screens (app) | SignUpScreen, KycScreen (App); auth.signup and other web forms | none | R1 Mismatch · R2 Verified | Keep run 2 |
| P62 | §5 table columns | Only in run 2 | 4 columns | Extra column "Purpose (provable)" for each screen | various | R1 n/a · R2 Verified | Add from run 2 |
| P63 | §5 LoginWithUsernameScreen and LoginWithOtpScreen route | Different | "(opened from LoginScreen)" | "no route in the fact pack" | none | R1 Verified · R2 Verified | Merge both |
| P64 | §5 platform label | Wording only candidate | "Mobile" | "App" | - | R1 Verified · R2 Verified | Wording only |
| P65 | §6 table columns | Different | Separate "Route" column | Route cited inside the Auth cell; no Route column | all `routes/api.php` lines same | R1 Verified · R2 Verified | Wording only |
| P66 | §6 loginOtpBasedUser "Called by" | Only in run 2 | "web OTP login, admin switch, app" | adds "KYC update page" | none | R1 Verified · R2 Verified | Add from run 2 |
| P67 | §6 send/verify-verification-otp "Called by" | Different | "web sign-up, app" | "Web sign-up, App SignUp, Kyc, AddClinic, EditClinic screens" | none | R1 Verified · R2 Verified | Keep run 2 |
| P68 | §6 getSalutationTypes and getCurrencyType "Called by" | Different | "web pages, app" / "app" | "Web pages, App SignUpScreen (POST)" / "App KycScreen (POST)" | none | R1 Verified · R2 Verified | Keep run 2 |
| P69 | §6 updatepassword and editFcmToken "Called by" | Different | "web, app" for both | "Web ChangePasswordController, App MyAccountScreen" / "Web loginController, App login screens" | none | R1 Verified · R2 Verified | Keep run 2 |
| P70 | §6 signup "Called by" | Different | "only `SignUpController`, which has no web route (§13 Q6)" | "Frontend `SignUpController@updateSignUpDetails` only, which has no web route" | R1/R2: BE routes/api.php:741 | R1 Verified · R2 Verified | Keep run 2 |
| P71 | §7 transactions columns | Different | "amount, payment_status, plan_id, user_id, … (26 columns)" | "id, user_id, plan_id, amount, currency, payment_status, order_id, payment_date and 18 more" | R1: models.md. R2: facts.md | R1 Verified · R2 Verified | Wording only |
| P72 | §7 subscriptions columns | Different | "id, name, price, duration, features, limits, status, …" | adds api_rules, blocked_api_rules, create_date, updated_at | R1: models.md. R2: facts.md | R1 Verified · R2 Verified | Keep run 2 |
| P73 | §7 columns outside migrations | Only in run 2 | not present | Code uses `user_personal_info` columns not in migrations (user_name, password, auth_token, fcm_token, role_id, is_active, delete_by_patient); §13 Q9 | R2: BE AuthController.php:459, :493, :485, :1862 | R1 n/a · R2 Verified | Add from run 2 |
| P74 | §7 intro/source | Different | Source: `_map/Ashoka-World-Backend/models.md`; models `UserPersonalInfo.php` | Source: `_map/_modules/auth/facts.md` (Tables) | n/a | R1 Verified · R2 Verified | Wording only |
| P75 | §8 row count | Different | 12 rows | about 26 rows (adds loginOtpBasedUser, otp send/verify, send-email, verify-email, forgotPassword 404/422/500, checkUsername, updatepassword, editFcmToken, signup rows) | various | R1 Verified · R2 Verified | Keep run 2 |
| P76 | §8 loginValidation 401 | Different | Only blocked user 401 row (line 476) | One row: unknown, wrong password, blocked 401 (466, 481, 476) | R1: :476. R2: :466, :481, :476 | R1 Mismatch · R2 Mismatch (override, see X1) | USER: two rows as code runs (Y1) |
| P77 | §8 forgotPassword user_name HTTP | Different | HTTP "—" | 404 | R1: :1652. R2: :1652, :1679 | R1 Verified · R2 Verified | Keep run 2 |
| P78 | §8 signup validation HTTP | Different | password, names, gender rows HTTP "—" | HTTP 400 | R1/R2: SignUpController.php:708, :709, :711, :712 | R1 Verified · R2 Verified | Keep run 2 |
| P79 | §8 send-verification-otp HTTP | Different | "—" | "not stated in fact pack"; cites :479, :480 | R1: :479. R2: :479, :480 | R1 Verified · R2 Verified | Keep run 2 |
| P80 | §8 signup v1 age | Different | cite :220, "younger than 100 years old" abbreviated | cites :220 and :226, full messages | R1: :220. R2: :220, :226 | R1 Verified · R2 Verified | Keep run 2 |
| P81 | §8 closing line | Only in run 1 | "More error messages per endpoint are listed in §4 acceptance criteria." | not present | none | R1 Verified · R2 n/a | Keep run 1 |
| P82 | §9 Security cites | Different | Cites only 1639, 1636 and OTP lines; lists the four auth.token routes without cites | Cites 968, 971, 972, 975 for auth.token routes | R1: routes/api.php:1639, :1636. R2: also :968, :971, :972, :975 | R1 Verified · R2 Verified | Keep run 2 |
| P83 | §9 OTP expiry cites | Different | Cites 79, 381, 612 and "Expired OTP" at :136 | Cites 79, 381, 612; no :136; "No attempt counter appears in the methods read" | R1: :136. R2: none | R1 Verified · R2 Verified | Merge both |
| P84 | §9 password rules | Different | Sign-up: digit (708); change: digit and min 6 (24, 38) | Sign-up: digit (708) and min 6 (908); change: digit, 6 (24, 38); login uses hash check (481) | R1: :708, :24, :38. R2: :708, :908, :24, :38, :481 | R1 Verified · R2 Verified | Keep run 2 |
| P85 | §9 plain password | Only in run 2 | not present | Bullet "Plain password copies": password in confirmation email and WhatsApp (SignUpV2) and Samvit Chakra call (older SignUp) | R2: BE SignUpController.php:1033, :1055, :590, :668 | R1 n/a · R2 Verified | Add from run 2 |
| P86 | §9 language files | Different | `lang/en/auth.php`, `lang/en_patient.json` | adds `lang/en/pagination.php`, `passwords.php`, `validation.php` | R1: FE auth.php, en_patient.json. R2: those plus 3 | R1 Verified · R2 Verified | Keep run 2 |
| P87 | §9 performance source | Different | "the map found no request limits or timeouts" | "the fact pack lists no request limits or timeouts" (cites facts.md) | none | R1 Not provable · R2 Verified | Keep run 2 |
| P88 | §11 staging-delta | Wording candidate | "See `staging-delta.md` in this folder" | link `../staging-delta.md` (and path) | n/a | R1 Verified · R2 Verified | Wording only |
| P89 | §12 Firebase backend | Only in run 2 | not present | Row "Firebase (Backend)": adds "Account Created" notification after sign-up | R2: BE SignUpController.php:1085 | R1 n/a · R2 Verified | Add from run 2 |
| P90 | §12 S3 | Different | "Sign-up uploads a file to S3 (`uploadFileToS3`); what is uploaded is §13 Q9" | Older `SignUp` uploads profile-picture and clinic-logo; `AuthController` builds URL only; "`SignUpV2` has no upload call" | R1: SignUpController.php:491. R2: :491, :539; AuthController.php:141 | R1 Verified · R2 Verified | Keep run 2 |
| P91 | §12 Samvit Chakra | Different | "Referenced in sign-up code (§13 Q9)" | Only older `SignUp` posts name, email, mobile, password to `/api/register-student`; `SignUpV2` does not | R1: :662. R2: :662 | R1 Verified · R2 Verified | Keep run 2 |
| P92 | §12 WhatsApp and email | Conflict | "message text only; the sending code and provider are §13 Q9" (cite :1751) | "Forgot password sends the new password by email and WhatsApp"; OTP email at :409, SMS via `otpSmsService` at :89; providers §13 Q12 | R1: AuthController.php:1751. R2: AuthController.php:1710, :1740; OtpSmsController.php:409, :89 | R1 Mismatch · R2 Verified | USER: run 2, email cite :1717 |
| P93 | §12 Firebase App row | Wording candidate | "Firebase (Cloud Messaging)", cites also AuthController.php:1862 | "Firebase Cloud Messaging (App)", no :1862 | R1: login_bloc.dart:173, :196; AuthController.php:1862. R2: login_bloc.dart:173, :196 | R1 Verified · R2 Verified | Wording only |
| P94 | §13 count | Different | 10 questions | 13 questions | n/a | R1 Verified · R2 Verified | Keep run 2 |
| P95 | §13 Q1 roles | Different | Which roles exist, who may use web, app, OTP login | adds "what are roles 3 and 5 that `v2/loginValidation` excludes" | R2: AuthController.php:459, :461 | R1 Verified · R2 Verified | Keep run 2 |
| P96 | §13 Q3 geo | Different | what decides the next screen | adds "what does `checkGeoIPValidity` decide?" | none | R1 Verified · R2 Verified | Keep run 2 |
| P97 | §13 Q4 | Different | Is it intended that loginValidation and v2/signup have no middleware, "while the older `signupV2`/`login` routes use `api`" | middleware question plus "`POST loginOtpBasedUser` accepts a user `id` without checking an OTP" | none | R1 Verified · R2 Verified | Keep run 2 |
| P98 | §13 Q5 | Different | wrong attempts allowed before OTP or account is blocked | wrong attempts allowed, and are fixed test numbers/emails with fixed test code meant to exist in production | R2: OtpSmsController.php | R1 Verified · R2 Verified (evidence corrected, X2) | Keep run 2 |
| P99 | §13 Q6 | Different | retire the five routes and `POST signup` | same, plus "web `GET/POST logout` routes point to `LoginController`, not covered by this module's fact pack" | none | R1 Verified · R2 Verified | Keep run 2 |
| P100 | §13 forgot-password policy question | Only in run 2 | not present | R2 Q7: forgot password needs only a username, resets immediately, [prefix] plus four digits | R2: AuthController.php | R1 n/a · R2 Verified | Add from run 2 |
| P101 | §13 updatepassword status question | Only in run 2 | not present | R2 Q8: HTTP status of `updatepassword` "no digit" case | R2: UpdatePasswordController.php:24 | R1 n/a · R2 Verified | Add from run 2 |
| P102 | §13 plain password question | Only in run 2 | not present | R2 Q10: plain password in confirmation email/WhatsApp, and to Samvit Chakra in older `POST signup` | R2: SignUpController.php:1033, :1055 | R1 n/a · R2 Verified | Add from run 2 |
| P103 | §13 columns question | Different | columns of currency_type, salutation_types, pg_device_mapping | adds which `user_personal_info` columns come from outside migrations | none | R1 Verified · R2 Verified | Keep run 2 |
| P104 | §13 S3/provider question | Different | R1 Q9: what is uploaded to S3, what Samvit Chakra does, which provider delivers WhatsApp and email | R2 Q12: how SignUpV2 stores pictures/logos given only older SignUp uploads to S3; providers for WhatsApp, SMS and email (Samvit moved to Q10) | none | R1 Verified · R2 Verified | Keep run 2 |
| P105 | §14 content | Different | Intro sentence, "Shows" column, "11 tables" | Table with Diagram, Kind, File only; adds folder path note | n/a | R1 Verified · R2 Verified | Merge both |

## BRD differences
| # | Where | Kind | Run 1 says | Run 2 says | Cited sources (both sides) | Verdict | Decision |
|---|---|---|---|---|---|---|---|
| B1 | §1 | Only in run 2 | not present | "Five older functions exist in the system that no screen uses today (see §4 and §12)" | R2: PRD rerun §1, §3 | R1 n/a · R2 Verified | Add from run 2 |
| B2 | §1 forgot password | Different | "can have it sent to them" | "get a new one sent to them" | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B3 | §1 Source | Different | PRD `nt/auth/PRD.md` §1; modules.yaml | PRD `nt/auth/rerun/PRD.md` §1, §3; facts.md | n/a | R1 Verified · R2 Verified | Merge both |
| B4 | §3 roles | Only in run 2 | not present | Row "College and admin sign-up users (to confirm)": separate sign-up pages | R2: FE routes/web.php:328, :329 | R1 n/a · R2 Verified | Add from run 2 |
| B5 | §3 Administrator cite | Different | cites DashboardController.php:1374 | cites :1374 and :1404 | R1: :1374. R2: :1374, :1404 | R1 Verified · R2 Verified | Keep run 2 |
| B6 | §3 Patient cite | Different | Patient / client, cite `login_with_otp.dart:163` | Patient, cite `facts.md` (Screens) | R1: APP login_with_otp.dart:163. R2: facts.md | R1 Verified · R2 Verified | Merge both |
| B7 | §3 Customer care source | Different | cite :1784 only | adds AUTH-R05 | R1/R2: AuthController.php:1784 | R1 Verified · R2 Verified | Keep run 2 |
| B8 | §3 closing line | Different | "full list of roles ... is in §12 Q2" | "not stated in the code read (§12 Q2)" | n/a | R1 Not provable · R2 Not provable | USER: neutral pointer to §12 Q2 |
| B9 | §4 In scope | Only in run 2 | 7 bullets | extra bullet "The lists (titles, currencies) shown on registration forms" | n/a | R1 n/a · R2 Verified | Add from run 2 |
| B10 | §4 Out of scope: payments | Different | "(module `payments`)" | "(other modules)" | n/a | R1 Verified · R2 Verified | Merge both |
| B11 | §4 Out of scope: unused functions | Different | "Older sign-in functions that no screen uses today (see §12 Q6)" | Five named unused functions (password login, sign out, corporate code, two lookups) plus older registration function used only by a website controller with no page route | R2: not-in-use.md (auth: 5 of 25 routes) | R1 Verified · R2 Verified | Keep run 2 |
| B12 | §4 Source table | Only in run 2 | none | Source: AUTH-R01 to R11; `atreya-docs/not-in-use.md`; PRD §1 | R2: not-in-use.md | R1 n/a · R2 Verified | Add from run 2 |
| B13 | §5 step 5 | Different | "receives the password by WhatsApp and/or email" | "the system sets a new password and sends it" | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B14 | §5 steps 4/6 | Different | step 4: "blocked users and wrong details are refused with a clear message" | step 3 similar plus "unknown" users; step 6 adds device registration and later password change; step 5 adds "then the account is created" | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B15 | §5 Source | Different | PRD §3 (J1-J5) | PRD §3 (J1 to J5); AUTH-R01 to AUTH-R10 | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B16 | §6 rule: blocked user | Conflict | "A blocked user cannot sign in." source AUTH-R01, AuthController.php:476 | Same rule sourced to AUTH-R04, AuthController.php:814 | R1: :476. R2: :814 | R1 Verified (rule) · R2 Verified (rule); both cite dead code (X1) | USER: keep rule, cite :460 and :802 |
| B17 | §6 rule: both fields | Different | cite AuthController.php:415 | cite :429 | R1: :415. R2: :429 | R1 Verified · R2 Verified | Merge both |
| B18 | §6 rule: wrong password or unknown username | Only in run 2 | not present | "A wrong password, or an unknown username, is refused." | R2: AuthController.php:466, :481 | R1 n/a · R2 Verified | Add from run 2 |
| B19 | §6 rule: OTP validity | Different | AUTH-R02, AUTH-R03 | adds AUTH-R08; "refused as expired" | R1/R2: OtpSmsController.php:79, :136 | R1 Verified · R2 Verified | Keep run 2 |
| B20 | §6 rule: mobile vs country code | Different | "must match the chosen country code" (AUTH-R02, R07; :57) | "right length and match" (AUTH-R02, R07, R08; :54, :57) | R1: :57. R2: :54, :57 | R1 Verified · R2 Verified | Keep run 2 |
| B21 | §6 rule: passwords | Different | One rule: digit; changed password min 6 and differs (AUTH-R06, R09; :708, :38) | Split: registration digit (:708); change password needs current, digit, 6, differ (AUTH-R09; :16, :38, :56) | R1: SignUpController.php:708; UpdatePasswordController.php:38. R2: plus :16, :56 | R1 Verified · R2 Verified | Keep run 2 |
| B22 | §6 rule: change needs current password | Different | separate rule (UpdatePasswordController.php:16) | merged into the change-password rule | R1/R2: :16 | R1 Verified · R2 Verified | Keep run 2 |
| B23 | §6 rule: title and gender | Only in run 2 | not present | "The title ... must exist in the system and fit the gender" | R2: SignUpController.php:832, :838 | R1 n/a · R2 Verified | Add from run 2 |
| B24 | §6 rule: recovery needs only username | Only in run 2 | not present | "needs only the username and replaces the password at once" | R2: AuthController.php:1652, :1684 | R1 n/a · R2 Verified | Add from run 2 |
| B25 | §6 rule: recovery rollback | Only in run 2 | not present | If password reaches user by neither channel, change undone, contact customer care | R2: AuthController.php:1784 | R1 n/a · R2 Verified | Add from run 2 |
| B26 | §6 rule count | Different | 10 rules | 14 rules | n/a | counts corrected (X3) | Wording only (follows the B rows) |
| B27 | §7 BR-04 | Different | "have it sent by WhatsApp and/or email" | "have a new one sent by email and/or WhatsApp" | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B28 | §7 BR-05 source | Different | AUTH-R06 | AUTH-R06, AUTH-R11 | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B29 | §7 BR-10 | Different | "switch to a doctor's account and back" | "switch to a doctor view and back" | n/a | R1 Verified · R2 Verified | Merge both |
| B30 | §9 row count | Different | 4 rows | 7 rows | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B31 | §9 Firebase backend | Only in run 2 | not present | "After registration the system adds an 'Account Created' notification" | R2: SignUpController.php:1085 | R1 n/a · R2 Verified | Add from run 2 |
| B32 | §9 SMS service | Only in run 2 | not present | Row "SMS service": sends mobile one-time codes | R2: OtpSmsController.php:89 | R1 n/a · R2 Verified | Add from run 2 |
| B33 | §9 Email and WhatsApp | Different | One row, provider "not named", cite AuthController.php:1751 | Two rows: email delivery (OtpSmsController.php:409, AuthController.php:1710) and WhatsApp (:1740) | R1: :1751. R2: :409, :1710, :1740 | R1 Verified · R2 Verified | Keep run 2 |
| B34 | §9 S3 | Different | "Registration uploads a file to storage" (SignUpController.php:491) | "Used in the sign-in and registration code; what is stored is not stated" (:491, AuthController.php:139) | R1: :491. R2: :491, AuthController.php:139 | R1 Verified · R2 Verified | Keep run 2 |
| B35 | §9 Samvit Chakra | Different | "Referenced in registration code; purpose to confirm" | "Only the older registration function calls this external system; the current registration does not (§12 Q7)" | R1/R2: SignUpController.php:662 | R1 Verified · R2 Verified | Keep run 2 |
| B36 | §9 Firebase app cite | Different | cite login_bloc.dart:196 | cites :173 and :196 | R1: :196. R2: :173, :196 | R1 Verified · R2 Verified | Keep run 2 |
| B37 | §10 languages | Different | cites qa-scope-rules.md; PRD §9 | adds `lang/en/auth.php`; "language files ... English only" | R2: FE resources/lang/en/auth.php | R1 Verified · R2 Verified | Keep run 2 |
| B38 | §10 older functions | Only in run 1 | Assumption: "Some older sign-in functions remain ... no current screen uses them" (PRD §6, §13 Q6) | moved to §1 and §4 | n/a | R1 Verified · R2 n/a | Keep run 1 |
| B39 | §10 same backend registration | Only in run 2 | not present | "website sign-up and the app sign-up both run the same backend registration function" | R2: routes/api.php:744, :1636 | R1 n/a · R2 Verified | Add from run 2 |
| B40 | §10 environments | Only in run 2 | not present (stated in §8 only) | Assumption: environments sheet not filled in | R2: environments.md | R1 n/a · R2 Verified | Add from run 2 |
| B41 | §11 | Different | Single paragraph with 4 example measures | Three questions, adds "how many should finish" and "what is acceptable" | n/a | R1 n/a · R2 n/a | Wording only |
| B42 | §12 count | Different | 9 questions | 12 questions | n/a | R1 n/a · R2 n/a | Wording only |
| B43 | §12 Q2 | Different | roles, who sees patient report screen | adds "Are the administrator and college sign-up pages in use?" | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B44 | §12 Q5 | Different | how many wrong attempts should be allowed | adds fixed test numbers and emails with fixed code in production | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B45 | §12 Q6 | Different | "older sign-in and registration functions that no screen uses" | "five unused functions and the older registration function ... or do other clients use them?" | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B46 | §12 Samvit Chakra question | Different | R1 Q9 merged: provider, S3 upload, what Samvit Chakra does | R2 Q7: older registration sends plain password to Samvit Chakra; still needed? | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B47 | §12 S3 and providers | Different | R1 Q9: provider for WhatsApp and email | R2 Q8: S3 content; providers for SMS, WhatsApp and email | n/a | R1 Verified · R2 Verified | Keep run 2 |
| B48 | §12 no-token and user id question | Only in run 2 | not present | R2 Q9: website sign-in/registration need no token; session step accepts user id without checking code | n/a | R1 n/a · R2 Verified | Add from run 2 |
| B49 | §12 forgot-password policy | Only in run 2 | not present | R2 Q10: recovery needs only username, replaces password at once, "atreya" plus four digits pattern | n/a | R1 n/a · R2 Verified | Add from run 2 |
| B50 | §12 age rule | Wording candidate | "18-100 age limit of the older registration also apply to the current one" | "enforce the 18 to 100 age rule" (R2 Q11) | n/a | R1 Verified · R2 Verified | Wording only |

## Wording only (same meaning)
- P-J1 §3 J1: both list the same five backend calls in code order (R2 as numbered steps).
- P-J2 §3 J2: same OTP calls; R2 says "session data is fetched", R1 "session is created".
- P-J4 §3 J4: same web and app forgot-password flow; R2 adds the "goes to /loginScreen" in J4 (R1 puts it in J3).
- P-2a §2 rows 3 and 4: "Logged-in user" vs "Logged in"; "doctor account" vs "doctor view".
- P-2b §2 column header: "Can use" vs "What they can reach".
- P-R04s AUTH-R04 Screens: same three screens, labelled differently.
- P-R07s AUTH-R07 Screens: "NT Lite sign-up" vs "NT Lite sign-up (Web)".
- P-5 §5 platform label: "Mobile" vs "App" (also P64).
- P-10 §10: same TO FILL environment tables, intro sentence differs.
- P-11 §11: same "not computed, waiting for environments.md" statement.
- P-12 §12 Firebase App row: same finding, slightly different title (also P93).
- P-15 §15: identical.
- B-2 §2: both TO CONFIRM; R2 adds "no ticket or document states why".
- B-5 §5 steps 1-2: same sign-in flow.
- B-7 BR-01, BR-02, BR-03, BR-06, BR-08, BR-09: same requirement text.
- B-8 §8: same TO FILL table; R2 cites environments.md.
- B-11 §11: same success-measure ideas (also B41 for the extras).
- B-13 §13: identical.

## Stability notes
- Totals: PRD rows P1-P105; BRD rows B1-B50 (counts by kind in the Summary).
- Sections that differ most (PRD): §4 requirements (R2 adds a description paragraph to every R, more acceptance criteria and a cite per bullet), §8 (R1 12 rows vs R2 about 26), §13 (10 vs 13 questions), §12 integrations (R2 splits and specifies). Identical or near-identical: front matter, §10, §11, §15.
- Sections that differ most (BRD): §6 rules (9 vs 13), §9 dependencies (4 vs 7), §12 questions (9 vs 12). Identical: front matter, §8, §13; BR-01 to BR-10 differ only in wording and source IDs.
- ID drift: AUTH-R01..R11 and BR-01..BR-10 are the same set with the same titles in both runs. Open-question numbers drift: PRD R1 Q7 (languages) = R2 Q11; R1 Q8 (columns) = R2 Q9; R1 Q9 (S3, Samvit, providers) = R2 Q10 and Q12; R1 Q10 (age) = R2 Q13. BRD R1 Q7 (languages) = R2 Q12; R1 Q8 (age) = R2 Q11; R1 Q9 = R2 Q7 and Q8.
- Cross-references in the docs shift with the question numbers (for example R1 PRD §7 points to Q8, R2 to Q9).
- Run 2 consistently adds code-reading findings absent from run 1: fixed test numbers/emails, no OTP check in `loginOtpBasedUser`, roles 3 and 5 excluded, plain password in sign-up messages and Samvit Chakra call, [prefix] plus four digits password pattern, S3/Samvit only in older `POST signup`. Run 1 states none of these (all "Only in run 2").
- Run 1 only items are few: blocked-user AC in R01, the 5-minute ACs in R02/R03, source line 82, the §8 closing line, the §10 older-functions assumption.
- Two direct disagreements in subject matter: which condition yields "User has been blocked" in `loginOtpBasedUser` (P29, B16 differs in which AUTH-R and line), and whether the WhatsApp/email sending code was located (P92).
- Cite counts: R2 cites nearly every acceptance bullet with line numbers; R1 lists lines in a single Source line per requirement. R2 BRD cites S3 at AuthController.php:139 while R2 PRD cites :141 for the same item (internal difference in run 2).
- P64, P88, P93 and B50 were entered as rows but are likely wording only; the checker may move them.

## Decisions after verification
Verdicts: three independent doc-checker passes (`checks/run-compare-check-P1.md`,
`-P2.md`, `-B.md`, 2026-10-26), merged by row number; 4 rows overridden after a
cross-check (next section). Nothing in PRD.md or BRD.md has changed yet.

| Decision | PRD | BRD |
|---|---|---|
| Add from run 2 | 40 | 14 |
| Keep run 2 (replaces run 1) | 45 | 24 |
| Merge both | 5 | 5 |
| Keep run 1 | 2 | 1 |
| Keep rule, fix citation | 0 | 1 (B16) |
| Fix both runs | 1 (P76) | 0 |
| Drop (run 2 claim with a wrong citation) | 1 (P10) | 0 |
| Needs confirmation | 2 (P29, P92) | 1 (B8) |
| Wording only | 9 | 4 |

Rows to decide: P10, P29, P76, P92, B8, B16. Every other row follows the rule
(keep only what the checker confirmed).

## Cross-check overrides (lead reviewer, with evidence)
- **X1 · blocked users (P76, B16; also explains P15, P29).** Both login queries
  already filter `is_active = 1` (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:460`,
  `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:802`), so the
  "User has been blocked" branches at `:475-476` and `:813-814` never run: a
  blocked user gets 401 "Invalid username" (NT_1005, `:466`). The P2 and B
  checkers verified the dead lines as written; the P1 checker caught it (P15,
  P29). P76: both runs list "blocked 401" in §8 → fix both. B16: the business
  rule "a blocked user cannot sign in" is true, but must cite `:460` / `:802`.
- **X2 · P98 evidence.** The checker wrote that the fixed test values live only
  in `app/Support/MasterWhitelist.php`. `OtpSmsController.php:76` and `:378`
  also hold inline test lists (see `atreya-docs/security/test-accounts.md`).
  Verdict unchanged.
- **X3 · B26 counts.** BRD §6 has 10 rule rows in run 1 and 14 in run 2 (not
  9 / 13 as first listed).
- P75: run 2 §8 has 24 rows (not "about 26"). P10: true claim, cite off by one
  (`routes/web.php:318`, not `:317`); re-add with the right line if wanted.

## Outside this file (not changed yet)
- **Run 1 errors** the first doc-checker passed: AUTH-R01 blocked-user criterion
  (P15), AUTH-R04 blocked-user source (P29), invalid-gender message (P41), "sending
  code not shown" (P92), app "clinic screens" use the lists (P61).
- **Impact pilot** `dev/adhoc-otp-attempt-limit/impact.md` §9 cites `:475` and
  `:814` as where login checks `is_active`; the live checks are the query
  filters at `:460` and `:802` (X1). Its risk reasoning is unchanged.
- **Stability:** IDs were stable (AUTH-R01..R11, BR-01..BR-10); 3 conflicts in
  155 rows; most differences are run 2 adding detail. Both runs and their
  checkers missed or mis-verified the dead-code branch: a checker confirms that a
  cited line says something, not that the line can run.

## User decisions (2026-10-26)
| Row | Decision | Evidence |
|---|---|---|
| P10 | Add run 2's forgot-password POST route to J4 with the corrected citation `Nadi-Tarangini-Frontend:routes/web.php:318` | `:317` is `GET /forgotPassword`, `:318` is `POST /checkForgotPassword` |
| P29 | AUTH-R04 criteria as the code runs (Y1) | see Y1 |
| P76 | PRD §8, `v2/loginValidation`: two 401 rows as the code runs (Y1) | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:466`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481` |
| P92 | Run 2's §12 text; forgot-password email cited at `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1717` (`send_email`; `:1710` is the email body), WhatsApp at `:1740`; providers stay a §13 question | |
| B8 | BRD §3 ends with a neutral pointer: "Which roles exist and who may use each sign-in method is a question for the product owner (§12 Q2)." | no role list in code |
| B16 | Keep "A blocked (inactive) user cannot sign in; they are told the username is invalid." Sources AUTH-R01, AUTH-R04; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:460`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:802` | X1 |

- **Y1 · blocked users and "User has been blocked".** Password login and the
  session step load only active users (`:460`, `:802`), so an inactive/blocked or
  (password login) role 3/5 user gets 401 "Invalid username" (NT_1005, `:466`,
  `:806`); a wrong password gets 401 "Invalid password" (NT_1006, `:481`). New §13
  question for dev: the explicit blocked checks at `:475-476` and `:813-814` can
  never run; is that intended?
  - **Correction (doc-checker on the merged PRD, verified by the lead reviewer):**
    an earlier version of Y1 said `:983` returns "User has been blocked" for a
    role the session step does not handle. That is wrong: every role has a
    branch (`:865`, `:902`, `:909`, `:917`), each returns "Invalid username" when
    its handler returns null, and every handler returns a non-empty `user_id`
    (`:1249`, `:1287`, `:1382`, `:1463`, `:1551`), so the `else` at `:981-983`
    can never run either. `loginOtpBasedUser` never returns "User has been
    blocked"; Q14 covers all three dead checks. The user's rule ("code as it
    runs") is unchanged; only its application to `:983` is corrected.
- **Item 6 (session step).** `POST loginOtpBasedUser` belongs to AUTH-R04 only;
  R04 is widened to every caller; R01–R03 say "then creates the session
  (AUTH-R04)" with their call site (PHASE2-STATUS.md, item 6).
