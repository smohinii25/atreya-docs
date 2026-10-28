---
module: "auth"
doc: "PRD"
status: "Draft"
date: "2026-10-26"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Authentication & sign-up: Product Requirements Document

## 1. Overview

The auth module groups the routes and screens that let a user enter Nadi Tarangini: password login, OTP login (mobile and email), forgotten-password recovery, doctor sign-up with availability checks and one-time-code verification, in-session password change, and push-token registration (`atreya-docs/_map/_modules/auth/facts.md`). The backend exposes 25 routes in `Ashoka-World-Backend:routes/api.php` (e.g. `Ashoka-World-Backend:routes/api.php:737`, `Ashoka-World-Backend:routes/api.php:1639`). The web dashboard has 26 web routes in this module and 6 auth pages (`Nadi-Tarangini-Frontend:routes/web.php:313`, `Nadi-Tarangini-Frontend:routes/web.php:325`). The mobile app has 5 screens under `Nadi-Tarangini-App:lib/common_files/Login/view/` and `Nadi-Tarangini-App:lib/common_files/signup/view/signup_screen.dart`. Five backend routes are called by no screen in this workspace (`POST login`, `POST logout`, `POST validateCorporateCode`, `GET checkusernameormobileno`, `GET getdetailsbymobileno`), and `POST signup` is called only from a Frontend controller that has no web route (§6, §13 Q6).

## 2. Users, roles & permissions

| Who | What they can reach | Evidence |
|---|---|---|
| Not logged in | Password login, OTP send/verify, forgot password, sign-up, username and mobile checks, verification OTP, salutation and currency lists (middleware `api` only) | `Ashoka-World-Backend:routes/api.php:739`, `Ashoka-World-Backend:routes/api.php:777`, `Ashoka-World-Backend:routes/api.php:788`, `Ashoka-World-Backend:routes/api.php:793`, `Ashoka-World-Backend:routes/api.php:759` |
| Not logged in, no middleware at all | `POST v2/loginValidation`, `POST v2/signup` | `Ashoka-World-Backend:routes/api.php:1639`, `Ashoka-World-Backend:routes/api.php:1636` |
| Logged in (`auth.token`) | `POST updatepassword`, `POST editFcmToken`, `POST logout`, `POST validateCorporateCode` | `Ashoka-World-Backend:routes/api.php:975`, `Ashoka-World-Backend:routes/api.php:971`, `Ashoka-World-Backend:routes/api.php:968`, `Ashoka-World-Backend:routes/api.php:972` |
| Web admin switching to a doctor view and back | Calls `POST loginOtpBasedUser` for the switch | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1374`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1404` |

`POST v2/loginValidation` looks up only active users whose `role_id` is not 3 or 5 (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:459`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:461`). What roles 3 and 5 are, and the full role list served by `GET public/allRoles` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:728`), is not stated in code read for this module (§13 Q1).

## 3. User journeys

**J1. Web login with username and password.**
1. The user opens `GET login`, rendered by `loginController@login` (`Nadi-Tarangini-Frontend:routes/web.php:313`, `Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php`).
2. The form posts to `POST checkLoginCredintial` (`Nadi-Tarangini-Frontend:routes/web.php:316`).
3. That controller calls `POST v2/loginValidation` first (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:63`), then `POST loginOtpBasedUser` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:79`), `GET v2/client/getClientDetails` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:94`), `GET nt-admin/access-management/getAllFeatureDetails` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:209`) and `GET subscriptions/getEndPoints` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:255`). Which of these run for which user is §13 Q2.
4. The page links to `forgotPassword` and `signup` (`Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php:181`, `Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php:279`).

**J2. Web login with OTP.**
1. Mobile: `POST send-login-otp` calls backend `POST otp/send-otp` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:319`). `POST verify-login-otp` calls `POST otp/verify-otp` and then `POST getUserDetailsUsingMobileNumber` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:378`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:386`).
2. Email: `POST send-email-login-otp` calls `POST otp/send-email-otp`, and `POST verify-email-login-otp` calls `POST otp/verify-email-otp` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:684`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:696`).
3. The session data is then fetched by `POST getUserDetailsOtpBasedLogin`, which calls `POST loginOtpBasedUser` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:446`).

**J3. Mobile app login.**
1. `LoginScreen` (route `/loginScreen`) leads to `/signupScreen` (`Nadi-Tarangini-App:lib/common_files/Login/view/login_screen.dart`, facts.md Screens).
2. `LoginWithUsernameScreen` and `LoginWithOtpScreen` lead to `/dashboardScreen`, `/kycScreen`, `/geoRestrictedScreen` or `/reportScreenPatient`; the username screen also leads to `/forgotPasswordScreen` (`Nadi-Tarangini-App:lib/common_files/Login/view/login_with_username_screen.dart`, `Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart`).
3. API calls are `POST v2/loginValidation`, `POST otp/send-otp`, `POST otp/verify-otp`, `POST otp/send-email-otp`, `POST otp/verify-email-otp`, `POST loginOtpBasedUser` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:357`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:448`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:465`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:481`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:494`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:431`).
4. The login bloc calls `checkGeoIPValidity` at two places (`Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:125`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:375`). What decides the next screen is §13 Q3.

**J4. Forgot password.**
1. Web: `GET forgotPassword` (`auth.forgot_password`) then `POST checkForgotPassword`, which calls backend `POST forgotPassword` (`Nadi-Tarangini-Frontend:routes/web.php:317`, `Nadi-Tarangini-Frontend:app/Http/Controllers/forgotPasswordController.php:51`).
2. App: `ForgotPasswordScreen` calls `POST forgotPassword` and goes to `/loginScreen` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:718`).

**J5. Sign-up.**
1. Web: `GET signup` (`auth.tabs`) links to `GET sign-up` (doctor) and `GET sign-up-admin` (`Nadi-Tarangini-Frontend:resources/views/auth/tabs.blade.php:27`, `Nadi-Tarangini-Frontend:resources/views/auth/tabs.blade.php:53`). `GET sign-up-college` renders `auth.college_signUp` (`Nadi-Tarangini-Frontend:routes/web.php:328`).
2. The doctor form calls `POST checkDoctorUsername` and `POST checkDoctorMobileNo` (availability), `POST send-verification-otp` and `POST verify-verification-otp` (code check), then `POST updateSignUpDetails`, which calls backend `POST v2/signup` (`Nadi-Tarangini-Frontend:routes/web.php:331`, `Nadi-Tarangini-Frontend:routes/web.php:332`, `Nadi-Tarangini-Frontend:routes/web.php:307`, `Nadi-Tarangini-Frontend:routes/web.php:308`, `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:91`).
3. Device linking uses `POST checkValidationsLinkDevice` and `POST linkDeviceAfterValidation` (`Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:251`, `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:295`).
4. NT Lite has its own username, mobile and submit calls, the submit going to `POST v2/signup` (`Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:77`, `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:132`, `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:170`).
5. App: `SignUpScreen` (route `/signupScreen`) calls `POST signupV2` and goes to `/loginScreen` or `/webViewScreen` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:675`, `Nadi-Tarangini-App:lib/common_files/signup/view/signup_screen.dart`).

## 4. Functional requirements

### AUTH-R01: Log in with username and password
`POST v2/loginValidation` takes `user_name` and `password`, rejects missing values, looks the user up case-insensitively among active users (roles 3 and 5 excluded), checks the password hash and returns a token with user id and role id (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:415`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:459`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:514`). If the user has no token yet, one is generated and saved (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:493`).
**Acceptance criteria**
- Given both fields are missing, when the user logs in, then 400 "Both username and password are required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:429`).
- Given only the username is missing, then 400 "Username is required"; given only the password is missing, then 400 "Password is required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:438`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:447`).
- Given an unknown username or a user without a role, then 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:466`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:471`).
- Given a wrong password, then 401 "Invalid password" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481`).
- Given a role-2 user flagged `delete_by_patient`, then 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:485`).
- Given a correct login, then 200 "Success" with `user_id`, `auth_token`, `role_id` and `doctor_data` (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:514`).
- Given an unexpected exception, then 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:528`).
**Source**: `Ashoka-World-Backend:routes/api.php:1639`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:415`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:429`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:459`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:514`
**Screens**: auth.login (Web), LoginWithUsernameScreen (App) · **API**: POST v2/loginValidation

### AUTH-R02: Request and verify a login OTP by mobile number
`POST otp/send-otp` checks the number, generates a 6-digit code, stores it in the cache for 5 minutes under the key `otp_<country code> <number>` and sends it through the OTP SMS service (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:77`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:89`). `POST otp/verify-otp` compares the submitted code with the cached one and removes it on success (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:188`).
**Acceptance criteria**
- Given a number whose length does not match the country, then 400 "Invalid phone number length" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:54`).
- Given a country code that does not fit the number, then 400 "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:57`).
- Given a number not registered, then 400 "Phone number not registered" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:71`).
- Given a registered number, then 200 "OTP sent successfully"; if the SMS service reports failure, 500 "OTP not sent. Please check the phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:92`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:94`).
- When verifying, a code that is empty, non-numeric or not 6 digits gives 400 "Invalid OTP"; no cached code gives 400 "Expired OTP"; a matching code gives 200 "OTP verified successfully"; a different code gives 400 "Invalid OTP" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:127`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:197`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:199`).
- Given two fixed test numbers listed in code, the code is a fixed test code and no SMS is sent (§13 Q5) (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:76`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:77`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:81`).
**Source**: `Ashoka-World-Backend:routes/api.php:788`, `Ashoka-World-Backend:routes/api.php:789`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:54`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:71`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136`
**Screens**: auth.login (Web), LoginWithOtpScreen (App) · **API**: POST otp/send-otp, POST otp/verify-otp

### AUTH-R03: Request and verify a login OTP by email
`POST otp/send-email-otp` generates a 6-digit code, caches it for 5 minutes under `otp_<email>` and emails it; `POST otp/verify-email-otp` checks it (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:379`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:381`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:409`).
**Acceptance criteria**
- Given no email, then 400 "Email is required"; given an unregistered email, then 400 "Email not registered" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:359`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:373`).
- Given a registered email, then 200 "OTP sent successfully"; if sending fails, 500 "OTP not sent. Please check the email" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:415`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:420`).
- When verifying, missing email gives 400 "Email is required", missing OTP 400 "OTP is required", expired 400 "Expired OTP", correct 200 "OTP verified successfully", otherwise 400 "Invalid OTP" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:433`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:436`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:439`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:452`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:457`).
- Given two fixed test emails listed in code, the code is a fixed test code and no email is sent (§13 Q5) (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:378`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:379`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:383`).
**Source**: `Ashoka-World-Backend:routes/api.php:790`, `Ashoka-World-Backend:routes/api.php:791`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:373`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:381`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:439`
**Screens**: auth.login (Web), LoginWithOtpScreen (App) · **API**: POST otp/send-email-otp, POST otp/verify-email-otp

### AUTH-R04: Create the session after OTP login (and for account switching)
`POST loginOtpBasedUser` takes a user `id` from the request, finds the active user, creates an auth token if none exists and returns the session data (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:798`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:806`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:820`). The code in this method does not check an OTP (§13 Q4). Clients call it after OTP verification and when an admin switches to a doctor view and back (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:446`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1374`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1404`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:431`).
**Acceptance criteria**
- Given no active user with that id or a user without a role, then 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:806`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:810`).
- Given a user whose role is not handled by the response branches, then 401 "User has been blocked" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:983`).
**Source**: `Ashoka-World-Backend:routes/api.php:739`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:806`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:814`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:983`
**Screens**: auth.login (Web), LoginWithOtpScreen (App), admin switch (Web) · **API**: POST loginOtpBasedUser

### AUTH-R05: Recover a forgotten password
`POST forgotPassword` takes `user_name`, finds the active, non-deleted user, sets a newly generated password of the form "atreya" plus four digits, and sends it by email and by WhatsApp (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1652`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1684`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1710`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1740`). The request needs only the username (§13 Q7).
**Acceptance criteria**
- Given no username, then the validation fails with the message "The username is required" and status 404 (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1655`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1666`).
- Given an unknown or deleted user, then 404 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1679`).
- If the password cannot be saved, then 422 "Password not updated" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1696`).
- Given sending to both channels, then 200 "Forgot password successfully. Password sent to whatsapp/email"; email only, 200 "...sent to email but not on whatsapp"; WhatsApp only, 200 "...sent to whatsapp but not on email" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1751`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1762`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1773`).
- Given neither channel works, then 422 "No contact information found. Please contact customer care." and the change is rolled back (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1784`).
**Source**: `Ashoka-World-Backend:routes/api.php:777`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1652`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1679`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1684`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1751`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1784`
**Screens**: auth.forgot_password (Web), ForgotPasswordScreen (App) · **API**: POST forgotPassword

### AUTH-R06: Sign up as a new doctor
`POST v2/signup` (web, NT Lite) and `POST signupV2` (app) both run `SignUpController@SignUpV2`, which validates the form, checks the mobile number and username are unused, checks salutation and gender, creates the user through `saveDoctor`, and sends the confirmation email and a WhatsApp sign-up message that both carry the plain password (`Ashoka-World-Backend:routes/api.php:1636`, `Ashoka-World-Backend:routes/api.php:744`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:701`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:927`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1033`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1055`). The older `POST signup` runs `SignUpController@SignUp` (starts at line 43), with additional required fields and an age check; the Samvit Chakra registration call and the S3 file uploads are in that older method, not in `SignUpV2` (`Ashoka-World-Backend:routes/api.php:741`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:43`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:220`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:491`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:662`).
**Acceptance criteria**
- Required: salutation type, username, password (must contain a digit), first and last name (letters and spaces only), email, gender (M, F, D or N), numeric mobile number, address line 1, clinic name, state, country; country code is required when a mobile number is given. Optional: numeric profession type, AYUSH number (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:706`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:708`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:709`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:712`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:714`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:717`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:722`).
- Given a country code that is not valid for the number, then 400 "Provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:727`).
- Given a mobile number already registered (and not on the master whitelist), then 400 "Phone number already exists" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:825`).
- Given a username already in use, then 400 "User already exists with same username. Please try with another username" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:853`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:858`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:859`). The wording differs from `checkUsername` (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:195`).
- Given a salutation not in the salutation table, then 400 "Invalid salutation type" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:832`).
- Given a salutation and gender that do not fit, then 400 "Please select a valid gender" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:838`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:842`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:847`).
- Given a password shorter than 6 characters, then 400 "Minimum 6 digits password is required" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:908`).
- Given no clinic name, then the message "Clinic name is required" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:766`).
**Source**: `Ashoka-World-Backend:routes/api.php:744`, `Ashoka-World-Backend:routes/api.php:1636`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:706`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:727`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:825`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:832`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:838`
**Screens**: auth.signup, auth.admin_signUp, auth.college_signUp (Web), SignUpScreen (App) · **API**: POST v2/signup (Web, NT Lite), POST signupV2 (App)

### AUTH-R07: Check that a username or mobile number is free during sign-up
`POST checkUsername` looks for an active user with the given username; `POST checkMobileNumber` validates the number and country code (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:176`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:229`).
**Acceptance criteria**
- Username missing gives 400 "User name is required"; taken gives 400 "User already exists with the same username. Please try with another username"; free gives "Valid username" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:182`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:195`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:201`).
- Mobile number missing gives 400 "Phone number is required"; non-numeric gives 400 "Phone number must be numeric" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:229`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:236`).
- Country code missing gives 400 "Country code field is required if phone number is provided"; invalid gives 400 "Invalid country code" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:243`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:251`).
- A wrong length gives 400 "Invalid phone number length. The required length is ..."; a mismatching code gives 400 "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:298`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:301`).
- An unexpected error gives 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:209`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:282`).
**Source**: `Ashoka-World-Backend:routes/api.php:763`, `Ashoka-World-Backend:routes/api.php:764`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:182`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:201`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:229`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:298`
**Screens**: auth.signup (Web), NT Lite sign-up (Web) · **API**: POST checkUsername, POST checkMobileNumber

### AUTH-R08: Verify an email or mobile number with a one-time code
`POST otp/send-verification-otp` and `POST otp/verify-verification-otp` serve sign-up and the actions `profile_edit`, `kyc_update`, `add_clinic`, `update_clinic`, `admin_add_user` and `admin_update_user`; the code is cached for 5 minutes (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:480`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:612`).
**Acceptance criteria**
- `type` must be `email` or `mobile`, and `action` one of the seven listed values (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:479`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:480`).
- `email` is required when type is email; `country_code` and numeric `mobile_no` are required when type is mobile (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:481`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:482`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:483`).
- Sending succeeds with "OTP sent successfully via {type} for {action}."; an email failure gives 500 "Failed to send OTP via email."; a mobile failure gives 500 "OTP not sent. Please check the phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:617`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:564`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:606`).
- A mobile number of the wrong length gives 400 "Invalid phone number length"; a mismatching country code gives 400 "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:597`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:600`).
- Verifying needs a numeric `otp`; a wrong or expired code gives 422 "The code is invalid or has expired. Please try again."; a right one gives "OTP verified successfully." (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:630`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:656`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:666`).
**Source**: `Ashoka-World-Backend:routes/api.php:793`, `Ashoka-World-Backend:routes/api.php:794`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:479`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:612`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:656`
**Screens**: auth.signup (Web), SignUpScreen, KycScreen, AddClinicScreen, EditClinicScreen (App) · **API**: POST otp/send-verification-otp, POST otp/verify-verification-otp

### AUTH-R09: Change the password while logged in
`POST updatepassword` identifies the user by the `user_id` header, requires `current_password` and `new_password`, and replaces the stored hash when the current password matches (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:12`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:16`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:58`). The route requires `auth.token` (`Ashoka-World-Backend:routes/api.php:975`).
**Acceptance criteria**
- A new password without a digit gives "New password must contain at least one digit." (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:24`; HTTP behaviour of this branch is §13 Q8).
- A new password shorter than 6 characters gives 400 "Minimum 6 digits password is required" (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:38`).
- No active user for the header id gives 400 "User not found" (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:51`).
- A wrong current password gives 400 "Incorrect current password"; a new password equal to the current one gives 400 "New password must be different from the old password." (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:64`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:56`).
- Success gives 200 "Password updated successfully" (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:62`).
**Source**: `Ashoka-World-Backend:routes/api.php:975`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:16`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:38`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:62`
**Screens**: MyAccountScreen (App), web change-password controller (`ChangePasswordController@updatePassword`) · **API**: POST updatepassword

### AUTH-R10: Register the device for push notifications
`POST editFcmToken` saves `fcm_token` on the user identified by the `user_id` header and returns "Fcm Token Updated Successfully." (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1859`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1862`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1865`). The app obtains the token and subscribes to topics in the login bloc, and the web calls the route from `loginController@editFcmToken` (`Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:173`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:196`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:350`).
**Acceptance criteria**
- Given no valid token, the route is refused by `auth.token` (`Ashoka-World-Backend:routes/api.php:971`).
- Given a database error, then 500 "Internal server error" and the transaction is rolled back (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1874`).
**Source**: `Ashoka-World-Backend:routes/api.php:971`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1862`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1874`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:391`
**Screens**: after login in LoginScreen, LoginWithOtpScreen, LoginWithUsernameScreen (App); web login pages · **API**: POST editFcmToken

### AUTH-R11: Provide sign-up reference lists (salutation and currency types)
`getSalutationTypes` and `getCurrencyType` are registered for both GET and POST and return the lists (`Ashoka-World-Backend:routes/api.php:759`, `Ashoka-World-Backend:routes/api.php:760`).
**Acceptance criteria**
- `getSalutationTypes` returns with message "Get salutation types" and `getCurrencyType` with "Get currency types" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1353`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1130`).
- Both return 500 "Internal server error" on failure (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1373`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1151`).
- The GET variants are called by no screen in this workspace; the POST variants are called by SignUpScreen, KycScreen and several web pages (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:812`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1709`, `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:24`).
**Source**: `Ashoka-World-Backend:routes/api.php:759`, `Ashoka-World-Backend:routes/api.php:760`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1353`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1130`
**Screens**: SignUpScreen, KycScreen (App); auth.signup and other web forms · **API**: GET/POST getSalutationTypes, GET/POST getCurrencyType

## 5. Screens (web / mobile)

| Screen | Platform | File | Route / path | Purpose (provable) |
|---|---|---|---|---|
| auth.login | Web | `Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php` | GET login | Login page, links to forgot password and sign-up (`Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php:181`) |
| auth.forgot_password | Web | `Nadi-Tarangini-Frontend:resources/views/auth/forgot_password.blade.php` | GET forgotPassword | Forgot-password page, goes to GET login (facts.md Screens) |
| auth.tabs | Web | `Nadi-Tarangini-Frontend:resources/views/auth/tabs.blade.php` | GET signup | Links to doctor and admin sign-up (`Nadi-Tarangini-Frontend:resources/views/auth/tabs.blade.php:27`) |
| auth.signup | Web | `Nadi-Tarangini-Frontend:resources/views/auth/signup.blade.php` | GET sign-up | Doctor sign-up page (`Nadi-Tarangini-Frontend:routes/web.php:325`) |
| auth.admin_signUp | Web | `Nadi-Tarangini-Frontend:resources/views/auth/admin_signUp.blade.php` | GET sign-up-admin | Admin sign-up page (`Nadi-Tarangini-Frontend:routes/web.php:329`) |
| auth.college_signUp | Web | `Nadi-Tarangini-Frontend:resources/views/auth/college_signUp.blade.php` | GET sign-up-college | College sign-up page (`Nadi-Tarangini-Frontend:routes/web.php:328`) |
| LoginScreen | App | `Nadi-Tarangini-App:lib/common_files/Login/view/login_screen.dart` | /loginScreen | Goes to /signupScreen (facts.md Screens) |
| LoginWithUsernameScreen | App | `Nadi-Tarangini-App:lib/common_files/Login/view/login_with_username_screen.dart` | no route in the fact pack | Goes to dashboard, forgot password, geo-restricted, KYC and patient report screens (facts.md Screens) |
| LoginWithOtpScreen | App | `Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart` | no route in the fact pack | Goes to dashboard, geo-restricted, KYC and patient report screens (facts.md Screens) |
| ForgotPasswordScreen | App | `Nadi-Tarangini-App:lib/common_files/Login/view/forgot_password_screen.dart` | /forgotPasswordScreen | Goes to /loginScreen (facts.md Screens) |
| SignUpScreen | App | `Nadi-Tarangini-App:lib/common_files/signup/view/signup_screen.dart` | /signupScreen | Goes to /loginScreen and /webViewScreen (facts.md Screens) |

## 6. APIs

| Method | Endpoint | Controller | Auth (middleware) | Called by |
|---|---|---|---|---|
| POST | v2/loginValidation | AuthController@loginValidation | none (`Ashoka-World-Backend:routes/api.php:1639`) | Web login, App login screens |
| POST | loginOtpBasedUser | AuthController@loginOtpBasedUser | api (`Ashoka-World-Backend:routes/api.php:739`) | Web login and OTP login, admin switch, KYC update page, App login screens |
| POST | otp/send-otp | OtpSmsController@sendOtp | api (`Ashoka-World-Backend:routes/api.php:788`) | Web, App login screens |
| POST | otp/verify-otp | OtpSmsController@verifyOtp | api (`Ashoka-World-Backend:routes/api.php:789`) | Web, App login screens |
| POST | otp/send-email-otp | OtpSmsController@sendEmailOtp | api (`Ashoka-World-Backend:routes/api.php:790`) | Web, App login screens |
| POST | otp/verify-email-otp | OtpSmsController@verifyEmailOtp | api (`Ashoka-World-Backend:routes/api.php:791`) | Web, App login screens |
| POST | otp/send-verification-otp | OtpSmsController@sendVerificationOtp | api (`Ashoka-World-Backend:routes/api.php:793`) | Web sign-up, App SignUp, Kyc, AddClinic, EditClinic screens |
| POST | otp/verify-verification-otp | OtpSmsController@verifyVerificationOtp | api (`Ashoka-World-Backend:routes/api.php:794`) | Web sign-up, App SignUp, Kyc, AddClinic, EditClinic screens |
| POST | forgotPassword | AuthController@getForgotPassword | api (`Ashoka-World-Backend:routes/api.php:777`) | Web forgot password, App ForgotPasswordScreen |
| POST | v2/signup | SignUpController@SignUpV2 | none (`Ashoka-World-Backend:routes/api.php:1636`) | Web sign-up, NT Lite sign-up |
| POST | signupV2 | SignUpController@SignUpV2 | api (`Ashoka-World-Backend:routes/api.php:744`) | App SignUpScreen |
| POST | signup | SignUpController@SignUp | api (`Ashoka-World-Backend:routes/api.php:741`) | Frontend `SignUpController@updateSignUpDetails` only, which has no web route (§13 Q6) |
| POST | checkUsername | CheckUserExistOrNotController@checkUsername | api (`Ashoka-World-Backend:routes/api.php:764`) | Web sign-up, NT Lite |
| POST | checkMobileNumber | CheckUserExistOrNotController@checkMobileNumberV2 | api (`Ashoka-World-Backend:routes/api.php:763`) | Web sign-up, NT Lite |
| GET, POST | getSalutationTypes | SignUpController@salutationTypes | api (`Ashoka-World-Backend:routes/api.php:759`) | Web pages, App SignUpScreen (POST) |
| GET, POST | getCurrencyType | SignUpController@getCurrencyType | api (`Ashoka-World-Backend:routes/api.php:760`) | App KycScreen (POST) |
| POST | updatepassword | UpdatePasswordController@updatePassword | api, auth.token (`Ashoka-World-Backend:routes/api.php:975`) | Web ChangePasswordController, App MyAccountScreen |
| POST | editFcmToken | AuthController@updateFcmToken | api, auth.token (`Ashoka-World-Backend:routes/api.php:971`) | Web loginController, App login screens |
| POST | login | AuthController@login | api (`Ashoka-World-Backend:routes/api.php:737`) | no screen in this workspace |
| POST | logout | AuthController@logout | api, auth.token (`Ashoka-World-Backend:routes/api.php:968`) | no screen in this workspace |
| POST | validateCorporateCode | AuthController@corporateCode | api, auth.token (`Ashoka-World-Backend:routes/api.php:972`) | no screen in this workspace |
| GET | checkusernameormobileno | CheckUserExistOrNotController@checkMobileNumberOrEmail | api (`Ashoka-World-Backend:routes/api.php:1426`) | no screen in this workspace |
| GET | getdetailsbymobileno | CheckUserExistOrNotController@getDetailsByMobileNo | api (`Ashoka-World-Backend:routes/api.php:1427`) | no screen in this workspace |

## 7. Data model

Tables touched by the controllers behind this module, with columns known from migrations (`atreya-docs/_map/_modules/auth/facts.md`, Tables).

| Table | Model | Columns known from migrations |
|---|---|---|
| user_personal_info | UserPersonalInfo | app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken |
| transactions | Transaction | id, user_id, plan_id, amount, currency, payment_status, order_id, payment_date and 18 more |
| subscriptions | Subscription | id, name, price, duration, features, limits, status, api_rules, blocked_api_rules, create_date, updated_at |
| user_nadi_capture_type | UserNadiCaptureType | can_change_capture_type, expiry_date, free_tier_enrolled, no_of_reports, plan_type |
| api_endpoints | ApiEndpoints | id, name, url, method, is_active, is_public, is_public_reception, create_date, updated_date |
| corporate_info | CorporateInfo | city, corp_role_id, corporate_id, country, pincode, profile_image, state |
| locality_info | LocalityInfo | is_default, timezone |
| country_wise_states | CountryWiseStates | timezone |
| currency_type | CurrencyType | columns not in migrations (§13 Q9) |
| salutation_types | SalutationTypes | columns not in migrations (§13 Q9) |
| pg_device_mapping | PgDeviceMapping | columns not in migrations (§13 Q9) |

Code also reads and writes `user_personal_info` columns that the migrations list does not show, for example `user_name`, `password`, `auth_token`, `fcm_token`, `role_id`, `is_active`, `delete_by_patient` (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:459`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:493`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:485`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1862`); their definitions are §13 Q9.

## 8. Validations & error handling

| API | Field / case | Rule or message | HTTP | Source |
|---|---|---|---|---|
| v2/loginValidation | user_name, password | required, string; messages per missing field | 400 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:415` |
| v2/loginValidation | unknown user, wrong password, blocked | "Invalid username", "Invalid password", "User has been blocked" | 401 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:466`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:476` |
| v2/loginValidation | exception | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:528` |
| loginOtpBasedUser | unknown or blocked user | "Invalid username", "User has been blocked" | 401 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:806`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:814` |
| otp/send-otp | length, country code, registration | "Invalid phone number length", "The provided country code is not valid for the given phone number", "Phone number not registered" | 400 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:54`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:57`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:71` |
| otp/send-otp | send failure | "OTP not sent. Please check the phone number" | 500 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:94` |
| otp/verify-otp | code | "Invalid OTP", "Expired OTP" | 400 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:127`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136` |
| otp/send-email-otp | email | "Email is required", "Email not registered" | 400 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:359`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:373` |
| otp/verify-email-otp | email, otp, code | "Email is required", "OTP is required", "Expired OTP", "Invalid OTP" | 400 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:433`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:436`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:439`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:457` |
| otp/send-verification-otp | type, action | `in:email,mobile`; `in:signup,profile_edit,kyc_update,add_clinic,update_clinic,admin_add_user,admin_update_user` | not stated in fact pack | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:479`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:480` |
| otp/verify-verification-otp | otp | required, numeric; invalid or expired gives "The code is invalid or has expired. Please try again." | 422 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:630`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:656` |
| forgotPassword | user_name | required, string; unknown user "Invalid username" | 404 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1652`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1679` |
| forgotPassword | save failure; no channel | "Password not updated"; "No contact information found. Please contact customer care." | 422 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1696`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1784` |
| forgotPassword | exception | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1806` |
| v2/signup, signupV2 | password | required, must contain a digit | 400 | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:708` |
| v2/signup, signupV2 | firstname, lastname | required, letters and spaces only | 400 | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:709`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:711` |
| v2/signup, signupV2 | gender | required, one of M, F, D, N | 400 | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:712` |
| v2/signup, signupV2 | mobile exists, salutation, gender fit | "Phone number already exists", "Invalid salutation type", "Please select a valid gender" | 400 | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:825`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:832`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:838` |
| signup (v1) | age | "User must be at least 18 years old", "User must be younger than 100 years old" | 400 | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:220`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:226` |
| checkUsername | username | "User name is required"; "User already exists with the same username. Please try with another username" | 400 | `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:182`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:195` |
| checkMobileNumber | phone, country code | "Phone number is required", "Phone number must be numeric", "Country code field is required if phone number is provided", "Invalid country code", "The provided country code is not valid for the given phone number" | 400 | `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:229`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:236`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:243`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:251`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:301` |
| updatepassword | new password length | "Minimum 6 digits password is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:38` |
| updatepassword | user, current password, reuse | "User not found", "Incorrect current password", "New password must be different from the old password." | 400 | `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:51`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:64`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:56` |
| editFcmToken | exception | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1874` |

## 9. Non-functional

- **Security.** Four routes in this module require `auth.token`: `updatepassword`, `editFcmToken`, `logout`, `validateCorporateCode` (`Ashoka-World-Backend:routes/api.php:968`, `Ashoka-World-Backend:routes/api.php:971`, `Ashoka-World-Backend:routes/api.php:972`, `Ashoka-World-Backend:routes/api.php:975`). The routes used by current web login and sign-up, `v2/loginValidation` and `v2/signup`, have no middleware (`Ashoka-World-Backend:routes/api.php:1639`, `Ashoka-World-Backend:routes/api.php:1636`; §13 Q4).
- **OTP.** Login and verification codes are cached for 5 minutes (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:381`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:612`). No attempt counter appears in the methods read (§13 Q5).
- **Passwords.** Sign-up and change-password require a digit and a minimum length of 6 (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:708`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:908`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:24`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:38`). Login compares with a hash check (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481`).
- **Plain password copies.** In `SignUpV2` (used by web and app) the plain password goes into the confirmation email and the WhatsApp sign-up message (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1033`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1055`). In the older `SignUp` it also goes to the Samvit Chakra registration call (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:590`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:668`; §13 Q10).
- **Languages.** Required: English, Marathi, Hindi, Czech, German, Spanish, Italian (`references/qa-scope-rules.md`). Language files found in code are English only: `Nadi-Tarangini-Frontend:resources/lang/en/auth.php`, `Nadi-Tarangini-Frontend:resources/lang/en/pagination.php`, `Nadi-Tarangini-Frontend:resources/lang/en/passwords.php`, `Nadi-Tarangini-Frontend:resources/lang/en/validation.php`, `Nadi-Tarangini-Frontend:resources/lang/en_patient.json`. The backend messages cited in §8 are English strings, for example `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481` (§13 Q11).
- **Performance.** The only time limit found is the 5-minute OTP validity; the fact pack lists no request limits or timeouts for this module (`atreya-docs/_map/_modules/auth/facts.md`).

## 10. Environment matrix

Copied from `atreya-docs/environments.md`; every value is still "TO FILL".

Ashoka-World-Backend and Nadi-Tarangini-Frontend (same columns):

| Env | Ref | Host | Feature flags | Integration mode |
|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL |

Nadi-Tarangini-App:

| Env | Ref | Build flavor | Host | Feature flags | Integration mode |
|---|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |

## 11. Staging delta

Not computed: all three repos are "waiting for environments.md" because staging and production refs are TO FILL. See [staging-delta.md](../staging-delta.md) (`atreya-docs/nt/auth/staging-delta.md`).

## 12. External integrations

| System | Where | What the code shows |
|---|---|---|
| Firebase Cloud Messaging (App) | `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:173`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:196` | The app gets the device token and subscribes to topics; the backend stores the token (AUTH-R10) |
| Firebase (Backend) | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1085` | After sign-up the backend adds an "Account Created" notification through a Firebase notification service |
| S3 | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:491`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:539`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:141` | The older `SignUp` method uploads profile-picture and clinic-logo files to S3 (`uploadFileToS3`); `AuthController` builds a profile-picture S3 URL only. `SignUpV2` has no upload call (§13 Q12) |
| Samvit Chakra | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:662` | Only the older `SignUp` (`POST signup`) posts name, email, mobile and password to `/api/register-student` of the configured Samvit Chakra URL; `SignUpV2` does not (AUTH-R06; §13 Q10) |
| WhatsApp and email delivery | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1710`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1740` | Forgot password sends the new password by email and WhatsApp (AUTH-R05); OTP email is sent from `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:409`, OTP SMS through `otpSmsService` (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:89`); providers are §13 Q12 |

## 13. Open questions

1. **PO:** Which roles exist (`GET public/allRoles`), what are roles 3 and 5 that `v2/loginValidation` excludes, and which roles may use web login, app login and OTP login?
2. **Dev:** In web login (`loginController@checkLoginCredentials`) which of the five backend calls run for which user type?
3. **Dev/PO:** What decides whether the app opens the dashboard, KYC, geo-restricted or patient report screen after login, and what does `checkGeoIPValidity` decide?
4. **Dev:** Is it intended that `POST v2/loginValidation` and `POST v2/signup` have no middleware, and that `POST loginOtpBasedUser` accepts a user `id` without checking an OTP in its own code?
5. **Dev/PO:** How many wrong OTP attempts are allowed, and are the fixed test numbers and emails with a fixed test code in `OtpSmsController` meant to exist in production?
6. **Dev:** Can `POST login`, `POST logout`, `POST validateCorporateCode`, `GET checkusernameormobileno`, `GET getdetailsbymobileno` and `POST signup` be retired, or are other clients using them? (`POST signup` is called only by a Frontend controller with no route; web `GET/POST logout` routes point to `LoginController`, not covered by this module's fact pack.)
7. **PO/Dev:** Is it intended that forgot password needs only a username, resets the password immediately, and uses a pattern of "atreya" plus four digits?
8. **Dev:** What HTTP status does `updatepassword` return for the "no digit" case, since the error handler reads a message array in a way I could not confirm?
9. **Dev:** What are the columns of `currency_type`, `salutation_types` and `pg_device_mapping`, and which `user_personal_info` columns (for example `user_name`, `password`, `auth_token`, `fcm_token`) come from outside the migrations?
10. **PO/Dev:** Is it intended that sign-up puts the plain password in the confirmation email and WhatsApp message (`SignUpV2`), and that the older `POST signup` also sends it to Samvit Chakra? Is `POST signup` still the path that registers users with Samvit Chakra, and does `SignUpV2` need to?
11. **PO/QA:** How do Marathi, Hindi, Czech, German, Spanish and Italian reach login and sign-up screens and backend messages?
12. **Dev:** How do web and app sign-up (`SignUpV2`) store profile pictures and clinic logos given that only the older `SignUp` uploads to S3, and which providers deliver WhatsApp, SMS and email?
13. **PO:** Should `v2/signup` and `signupV2` enforce the 18 to 100 age rule that `POST signup` has?
## 14. Diagrams

| Diagram | Kind | File |
|---|---|---|
| Screen flow, app | flow | `diagrams/flow-app.drawio` |
| Screen flow, web | flow | `diagrams/flow-web.drawio` |
| AUTH-R01 username and password login | sequence | `diagrams/seq-AUTH-R01.drawio` |
| AUTH-R02 mobile OTP login | sequence | `diagrams/seq-AUTH-R02.drawio` |
| Data model | ER | `diagrams/er.drawio` |

(Files are in `atreya-docs/nt/auth/diagrams/`.)

## 15. Document control

| Field | Value |
|---|---|
| Status | Draft |
| Date | 2026-10-26 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`, Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`, Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d` |
