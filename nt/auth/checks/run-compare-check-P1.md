# Run-compare check: P1–P52
Checked against workspace code at the commits in run-compare.md. Cites are Repo:path:line (BE = Ashoka-World-Backend, FE = Nadi-Tarangini-Frontend, APP = Nadi-Tarangini-App). No secret files opened; no values copied.

| # | Run 1 | Run 2 | Decision | Evidence (short; cite Repo:path:line; no values) |
|---|---|---|---|---|
| P1 | n/a | Verified | Add from run 2 | BE:routes/api.php:737 (login), :1639 (loginValidation); FE:routes/web.php:313 (GET login), :325 (GET sign-up) all exist as described. |
| P2 | n/a | Verified | Add from run 2 | APP:lib/common_files/Login/view/ holds 4 screen files; APP:lib/common_files/signup/view/signup_screen.dart exists. |
| P3 | n/a | Verified | Add from run 2 | Routes exist: BE:routes/api.php:737, :968, :972, :1426, :1427. No caller in APP api_repository.dart/strings_const.dart or FE:app (grep found none). |
| P4 | Verified | Verified | Keep run 2 | BE:routes/api.php:736 `middleware('api')` group; 739/744/777/788/793/759/760 inside it, auth.token group is :907-:1420 so :968-:975 are in it. R2 is a superset (adds salutation/currency lists :759). |
| P5 | n/a | Verified | Add from run 2 | BE:app/Http/Controllers/AuthController.php:459-461 (whereRaw LOWER, is_active=1, whereNotIn role_id 3,5); FE:app/Http/Controllers/loginController.php:728 calls public/allRoles. |
| P6 | n/a | Verified | Add from run 2 | FE:routes/web.php:313 `GET /login` -> loginController@login. |
| P7 | Verified | Verified | Merge both | APP:lib/common_files/api_services/api_repository.dart:2517-2519 defines checkGeoIPValidity (POST); APP:.../login_bloc/login_bloc.dart:125 and :375 call it. Complementary facts. |
| P8 | n/a | Verified | Add from run 2 | APP:lib/common_files/Login/view/login_with_username_screen.dart:232 goes to forgotPasswordScreen; route APP:lib/route/router.dart:359. (login_with_otp.dart has no such link, but R2 cites both files for the combined sentence about both screens.) |
| P9 | Verified | Verified | Add from run 2 | R1 directory exists; the three files exist under APP:lib/common_files/Login/view/. R2 strictly more precise. |
| P10 | n/a | Mismatch | Drop | FE:routes/web.php:317 is `GET /forgotPassword`; `POST /checkForgotPassword` is at :318. Cite is off by one (fix to :318 if re-added). |
| P11 | n/a | Verified | Add from run 2 | FE:routes/web.php:328 (sign-up-college), :331 checkDoctorMobileNo, :332 checkDoctorUsername, :307/:308 send/verify-verification-otp. |
| P12 | Verified | Verified | Keep run 2 | FE:app/Http/Controllers/NtLiteSignUpController.php:77 posts v2/signup; :132 checkMobileNumber, :170 checkUsername. R2 superset. |
| P13 | n/a | Verified | Add from run 2 | APP:lib/common_files/api_services/api_repository.dart:675 signUpV2Url; APP:lib/common_files/signup/view/signup_screen.dart:228/:249/:358 go('/loginScreen'), :1342/:1351 push('/webViewScreen'). |
| P14 | n/a | Verified | Add from run 2 | BE:AuthController.php:459 (case-insensitive), :460 active, :461 roles 3/5 excluded, :481 Hash::check, :493 token generated if none, :512-:522 returns user_id/auth_token/role_id. |
| P15 | Mismatch | Verified | Keep run 2 | BE:AuthController.php:459-460 query already filters is_active=1, so the "User has been blocked" branch at :475-:476 is unreachable; a blocked user gets 401 "Invalid username" (:466). R2 omitting the AC is accurate. |
| P16 | Verified | Verified | Keep run 2 | BE:AuthController.php:466 and :471 both return 401 "Invalid username" (unknown user / no role_id). R2 superset. |
| P17 | n/a | Verified | Add from run 2 | BE:AuthController.php:484-:486 role 2 and delete_by_patient==1 -> 401 "Invalid username". |
| P18 | n/a | Verified | Add from run 2 | BE:AuthController.php:512-:522 200 "Success" with user_id, auth_token, role_id, doctor_data; :528 500 "Internal server error". |
| P19 | n/a | Verified | Add from run 2 | BE:app/Http/Controllers/OtpSmsController.php:77 six-digit rand, :79 Cache::put 'otp_'.$phone (cc + space + number) 5 min, :89 otpSmsService, :140 Cache::forget on success (R2 cites :188, success block). |
| P20 | Verified | Verified | Keep run 2 | BE:OtpSmsController.php:126-:127 empty/non-numeric/not-6 -> 400 Invalid OTP; :136 no cache -> Expired OTP; :197 success; :199 mismatch -> Invalid OTP. R2 superset. |
| P21 | n/a | Verified | Add from run 2 | BE:OtpSmsController.php:76 two fixed numbers, :77 fixed code, :81-:82 returns without sending SMS. |
| P22 | Verified | Verified | Wording only | Same fact (cache 5 min) at BE:OtpSmsController.php:79; only placement (AC vs description) differs. |
| P23 | Verified | n/a | Keep run 1 | BE:OtpSmsController.php:82 is the early success return in the fixed-number case; a valid source line. |
| P24 | n/a | Verified | Add from run 2 | BE:OtpSmsController.php:379 six-digit code, :381 Cache::put 'otp_'.$email 5 min, :409 send_email. |
| P25 | n/a | Verified | Add from run 2 | BE:OtpSmsController.php:378 two fixed emails, :379 fixed code, :383-:384 returns without emailing. |
| P26 | Verified | Verified | Wording only | BE:OtpSmsController.php:433/:436/:439 missing email/OTP/expired, :452 success, :457 else Invalid OTP. Same set, different order/cites. |
| P27 | Verified | Verified | Wording only | BE:OtpSmsController.php:381 5 min; same fact, AC vs description. |
| P28 | Verified | Verified | Add from run 2 | BE:AuthController.php:795-:798 takes `id`, :801-:803 active user, :819-:821 creates token if none; no OTP check anywhere in the method (:795-:984). R1 statement also true but thinner. |
| P29 | Mismatch | Verified | Needs confirmation | Conflict. BE:AuthController.php:801-:803 query filters is_active=1, so R1's "blocked user" branch at :813-:814 is unreachable; the message is actually returned at :983 (else branch of role handling), as R2 says. |
| P30 | Verified | Verified | Keep run 2 | BE:AuthController.php:806 (no active user) and :810 (no role_id) both 401 "Invalid username". R2 superset. |
| P31 | Verified | Verified | Keep run 2 | FE:app/Http/Controllers/DashboardController.php:1374 and :1404 both post to loginOtpBasedUser; FE:loginController.php:446 (role 7 branch); APP:api_repository.dart:429-431. |
| P32 | Verified | Verified | Add from run 2 | BE:AuthController.php:1673-:1677 active, not deleted; :1684 new password = [prefix]+4 digits; :1710 email body, :1740 WhatsApp send. R1 "WhatsApp and/or email" also true. |
| P33 | Verified | Verified | Keep run 2 | BE:AuthController.php:1652 required rule, :1655 message "The username is required", :1668 status 404 (R2 cites :1666 in same response). R2 superset. |
| P34 | Verified | Verified | Keep run 2 | BE:AuthController.php:1673-:1679 unknown or deleted user -> 404 "Invalid username". |
| P35 | Verified | Verified | Add from run 2 | BE:AuthController.php:1751, :1762, :1773 each `], 200)` with the three messages. |
| P36 | Verified | Verified | Keep run 2 | BE:AuthController.php:1779-:1789 `DB::rollBack()` then 422 with the message at :1784. |
| P37 | n/a | Verified | Add from run 2 | BE:routes/api.php:1636 and :744 -> SignUpV2 (BE:SignUpController.php:701); :1033 email and :1055/:1061 WhatsApp use password_original; SignUp starts :43, age check :216-:227, S3 :491/:539, Samvit :662/:668. |
| P38 | Verified | Verified | Keep run 2 | BE:SignUpController.php:821-:826 400 only when `!MasterWhitelist::isMobile(...)`. |
| P39 | n/a | Verified | Add from run 2 | BE:SignUpController.php:853-:859 400 "…with same username…"; BE:CheckUserExistOrNotController.php:195 says "…with the same username…" (wording differs as stated). |
| P40 | n/a | Verified | Add from run 2 | BE:SignUpController.php:907-:908 strlen<6 -> 400 "Minimum 6 digits password is required". |
| P41 | Mismatch | Verified | Keep run 2 | BE:SignUpController.php:838/:842/:847 message is returned for a salutation/gender mismatch. A gender outside M,F,D,N fails validation at :712 with "Invalid value for gender" (:750), not R1's message. |
| P42 | Verified | Verified | Keep run 2 | BE:SignUpController.php:727 message; :769-:775 validator failure returns it with 400. R2 adds the status. |
| P43 | Verified | Verified | Keep run 2 | BE:SignUpController.php:706 salutation, :708 password digit, :709 lastname, :712 gender, :714 profession numeric, :717 address, :722 country code; :707/:710/:713/:716/:719/:720 other required fields; :766 clinic message. R2 cites per bullet. |
| P44 | n/a | Verified | Add from run 2 | BE:CheckUserExistOrNotController.php:174-:189 checkUsername looks up active user (is_active=1); :220-:302 checkMobileNumberV2 validates number and country code. |
| P45 | n/a | Verified | Add from run 2 | BE:CheckUserExistOrNotController.php:301 400 "The provided country code is not valid for the given phone number". |
| P46 | n/a | Verified | Add from run 2 | BE:CheckUserExistOrNotController.php:209 (checkUsername catch) and :282 (mobile) 500 "Internal server error". |
| P47 | n/a | Verified | Add from run 2 | BE:OtpSmsController.php:612 `Cache::put($cacheKey, $otp, now()->addMinutes(5))`. (R2 also cites :480, which is the action list.) |
| P48 | n/a | Verified | Add from run 2 | BE:OtpSmsController.php:564 email failure 500; :605-:606 mobile failure 500 "OTP not sent. Please check the phone number". |
| P49 | n/a | Verified | Add from run 2 | BE:OtpSmsController.php:597 "Invalid phone number length" 400; :600 country-code mismatch 400. |
| P50 | Verified | Verified | Keep run 2 | BE:OtpSmsController.php:481 email required_if email, :482 country_code required_if mobile, :483 mobile_no required_if mobile + numeric. R1 claim true but cites :479/:480 (type/action lines). |
| P51 | Verified | Verified | Keep run 2 | APP:lib/common_files/signup/view/signup_screen.dart:1016/:1100 sendOtp; APP:lib/doctor_dashboard/kyc/view/kyc_screen.dart, my_account/view/my_clinic/add_clinic.dart, edit_clinic.dart use OtpVerificationCubit (APP:common_files/utilities/otp_verification/otp_verification_cubit.dart calls the two endpoints). Web: FE:routes/web.php:307/:308. R2 superset (my_account/view/my_account/edit_account.dart also uses it; not claimed by either run). |
| P52 | Verified | Verified | Add from run 2 | BE:UpdatePasswordController.php:14 `header('user_id')`, :16 current_password, :17 new_password, :58 hash replaced; BE:routes/api.php:975 inside auth.token group (:907-:1420). |
