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

The auth module covers how a user gets into Nadi Tarangini: logging in with a
username and password, logging in with a one-time password (OTP) sent to a mobile
number or an email address, recovering a forgotten password, signing up as a new
doctor, verifying a mobile number or email during sign-up and profile changes,
changing the password while logged in, and registering the device for push
notifications. It is served by 25 backend routes in Ashoka-World-Backend (for
example `Ashoka-World-Backend:routes/api.php:737` and `Ashoka-World-Backend:routes/api.php:1639`) and used by the web dashboard
(Nadi-Tarangini-Frontend, 26 web routes, 6 pages, for example `Nadi-Tarangini-Frontend:routes/web.php:313` and
`Nadi-Tarangini-Frontend:routes/web.php:325`) and the mobile app (Nadi-Tarangini-App, 5 screens, under
`Nadi-Tarangini-App:lib/common_files/Login/view/` and
`Nadi-Tarangini-App:lib/common_files/signup/view/signup_screen.dart`). Five
backend routes are called by no screen in this workspace (`POST login`,
`POST logout`, `POST validateCorporateCode`, `GET checkusernameormobileno`,
`GET getdetailsbymobileno`), and `POST signup` is called only from a Frontend
controller that has no web route (§6, §13 Q6).
Source (including the route, page and screen counts): `atreya-docs/modules.yaml` (module `auth`), `atreya-docs/_map/_modules/auth/facts.md`.

## 2. Users, roles & permissions

| Who | Can use | Evidence |
|---|---|---|
| Not logged in | Password login, OTP send/verify, forgot password, sign-up, username and mobile checks, verification OTP, salutation and currency lists (middleware `api` only) | `Ashoka-World-Backend:routes/api.php:739`, `Ashoka-World-Backend:routes/api.php:777`, `Ashoka-World-Backend:routes/api.php:788`, `Ashoka-World-Backend:routes/api.php:793`, `Ashoka-World-Backend:routes/api.php:759` |
| Anyone (only the `api` group, no `auth.token`) | `POST v2/loginValidation`, `POST v2/signup` | `Ashoka-World-Backend:routes/api.php:1639`, `Ashoka-World-Backend:routes/api.php:1636`; the `api` group wraps `routes/api.php` (`Ashoka-World-Backend:app/Providers/RouteServiceProvider.php:32`) and rate-limits to 100000 requests per minute (`Ashoka-World-Backend:app/Http/Kernel.php:48`) |
| Logged-in user (`auth.token`) | Change password, register push token, logout, validate corporate code | `Ashoka-World-Backend:routes/api.php:975`, `Ashoka-World-Backend:routes/api.php:971`, `Ashoka-World-Backend:routes/api.php:968`, `Ashoka-World-Backend:routes/api.php:972` |
| Web admin switching to a doctor account and back | Re-login through `POST loginOtpBasedUser` | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1374`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1404` |

`POST v2/loginValidation` looks up only active users whose `role_id` is not 3 or 5
(`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:459`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:461`). The web login loads the list of roles from `GET public/allRoles`
(`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:728`). Which roles exist, what roles 3 and 5 are, and what each role may do is
not part of this module: see §13 Q1.

## 3. User journeys

**J1. Web login (username and password).** The login page is `auth.login`
(`Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php`, route `GET login`,
rendered by `loginController@login`, `Nadi-Tarangini-Frontend:routes/web.php:313`). The form posts to
`POST checkLoginCredintial` (`Nadi-Tarangini-Frontend:routes/web.php:316`), whose controller calls, in code
order: `POST v2/loginValidation` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:63`),
`POST loginOtpBasedUser` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:79`),
`GET v2/client/getClientDetails` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:94`),
`GET nt-admin/access-management/getAllFeatureDetails` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:209`)
and `GET subscriptions/getEndPoints` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:255`).
Which calls run for which user type is not visible from the call list (§13 Q2).
The page links to forgot password and sign-up (`GET forgotPassword`, `GET signup`;
`Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php:181`, `Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php:279`).

**J2. Web login with OTP.** WhatsApp/mobile: `POST send-login-otp` → backend
`POST otp/send-otp` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:319`), then
`POST verify-login-otp` → `POST otp/verify-otp` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:378`)
and `POST getUserDetailsUsingMobileNumber` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:386`).
Email: `POST send-email-login-otp` → `POST otp/send-email-otp`
(`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:684`), then
`POST verify-email-login-otp` → `POST otp/verify-email-otp`
(`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:696`). The session is then
created with `POST getUserDetailsOtpBasedLogin` → `POST loginOtpBasedUser`
(`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:446`).

**J3. Mobile app login.** Screens in `Nadi-Tarangini-App:lib/common_files/Login/`:
`LoginScreen` (route `/loginScreen`, goes to `/signupScreen`;
`Nadi-Tarangini-App:lib/common_files/Login/view/login_screen.dart`),
`LoginWithUsernameScreen` and `LoginWithOtpScreen` (go to `/dashboardScreen`,
`/kycScreen`, `/geoRestrictedScreen` or `/reportScreenPatient`;
`Nadi-Tarangini-App:lib/common_files/Login/view/login_with_username_screen.dart`,
`Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart`; the username
screen also leads to `/forgotPasswordScreen`,
`Nadi-Tarangini-App:lib/common_files/Login/view/login_with_username_screen.dart:232`), and
`ForgotPasswordScreen` (route `/forgotPasswordScreen`, goes to `/loginScreen`).
The app calls `POST v2/loginValidation` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:357`),
`POST otp/send-otp` / `POST otp/verify-otp` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:448`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:465`),
`POST otp/send-email-otp` / `POST otp/verify-email-otp` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:481`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:494`),
`POST loginOtpBasedUser` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:431`)
and `POST checkGeoIPValidity` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2519`), which the login bloc calls at two places
(`Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:125`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:375`).
What decides the next screen (dashboard, KYC, geo-restricted, patient report) is
§13 Q3.

**J4. Forgot password.** Web: `GET forgotPassword` page `auth.forgot_password`
→ `POST checkForgotPassword` (`Nadi-Tarangini-Frontend:routes/web.php:318`) → backend `POST forgotPassword`
(`Nadi-Tarangini-Frontend:app/Http/Controllers/forgotPasswordController.php:51`). App:
`ForgotPasswordScreen` → `POST forgotPassword`
(`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:718`).

**J5. Doctor sign-up.** Web: `GET signup` (`auth.tabs`) links to `GET sign-up`
(`auth.signup`) and `GET sign-up-admin` (`auth.admin_signUp`)
(`Nadi-Tarangini-Frontend:resources/views/auth/tabs.blade.php:27`, `Nadi-Tarangini-Frontend:resources/views/auth/tabs.blade.php:53`); `GET sign-up-college`
shows `auth.college_signUp` (`Nadi-Tarangini-Frontend:routes/web.php:328`). The web routes for availability checks are `POST checkDoctorUsername` (`Nadi-Tarangini-Frontend:routes/web.php:332`) and `POST checkDoctorMobileNo` (`Nadi-Tarangini-Frontend:routes/web.php:331`); no page that calls them was found in this workspace. The form uses verification OTP
(`POST send-verification-otp` `Nadi-Tarangini-Frontend:routes/web.php:307`, `POST verify-verification-otp` `Nadi-Tarangini-Frontend:routes/web.php:308`) and submits with
`POST updateSignUpDetails` → backend `POST v2/signup`
(`Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:91`). It can also
link a device (`POST checkValidationsLinkDevice`, `POST linkDeviceAfterValidation`,
`Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:251`,
`Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:295`). NT Lite has its own
username, mobile and submit calls, the submit going to `POST v2/signup`
(`Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:77`, `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:132`, `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:170`). App:
`SignUpScreen` (route `/signupScreen`) → `POST signupV2`
(`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:675`), then goes to `/loginScreen` or `/webViewScreen`
(`Nadi-Tarangini-App:lib/common_files/signup/view/signup_screen.dart`).

## 4. Functional requirements

### AUTH-R01: Log in with username and password
`POST v2/loginValidation` takes `user_name` and `password`, rejects missing values, looks the user up case-insensitively among active users (roles 3 and 5 excluded), checks the password hash and returns a token with user id and role id (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:415`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:459`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:480`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:514`). If the user has no token yet, one is generated and saved (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:493`).
For every role except 2 (patient) the client then creates the session through `POST loginOtpBasedUser` (AUTH-R04): web `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:79` (role 7) and `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:96` (other roles), app `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:110`. A patient (role 2) skips it: the web calls `GET v2/client/getClientDetails` instead (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:94`) and the app calls `getPatientData` (`Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:104`).
**Acceptance criteria**
- Given username and password are both missing, when the user logs in, then the API returns 400 "Both username and password are required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:429`).
- Given only the username is missing, then 400 "Username is required"; given only the password is missing, then 400 "Password is required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:438`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:447`).
- Given an unknown username, an inactive (blocked) user, a user with role 3 or 5, or a user without a role, then 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:460`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:461`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:466`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:471`).
- Given a role-2 user flagged `delete_by_patient`, then 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:485`).
- Given a wrong password, then 401 "Invalid password" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481`).
- Given a correct login, then 200 "Success" with `user_id`, `auth_token`, `role_id` and `doctor_data` (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:514`).
- Given an unexpected exception, then 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:528`).
**Source**: `Ashoka-World-Backend:routes/api.php:1639`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:415`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:429`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:438`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:447`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:459`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:460`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:461`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:466`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:471`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:480`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:485`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:493`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:514`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:528`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:79`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:94`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:96`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:104`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:110`
**Screens**: auth.login (web), LoginWithUsernameScreen (app) · **API**: POST v2/loginValidation

### AUTH-R02: Request and verify a login OTP by mobile number
`POST otp/send-otp` checks the number, generates a 6-digit code, stores it in the cache for 5 minutes under the key `otp_<country code> <number>` and sends it through the OTP SMS service (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:77`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:89`). `POST otp/verify-otp` compares the submitted code with the cached one and removes it on success (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:188`).
After the code is verified, the client then creates the session (AUTH-R04): web `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:446`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:458`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:464`, app `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:369`.
**Acceptance criteria**
- Given a phone number of the wrong length, then 400 "Invalid phone number length" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:54`).
- Given a country code that does not match the number, then 400 "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:57`).
- Given a number that is not registered, then 400 "Phone number not registered" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:71`).
- Given a valid registered number, then 200 "OTP sent successfully"; if sending fails, 500 "OTP not sent. Please check the phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:94`).
- When verifying, a code that is empty, non-numeric or not 6 digits gives 400 "Invalid OTP"; no cached code gives 400 "Expired OTP"; a matching code gives 200 "OTP verified successfully"; a different code gives 400 "Invalid OTP" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:127`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:197`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:199`).
- A sent OTP is kept for 5 minutes (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79`).
- Given two fixed test numbers listed in code, the code is a fixed test code and no SMS is sent (§13 Q5) (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:76`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:77`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:81`).
**Source**: `Ashoka-World-Backend:routes/api.php:788`, `Ashoka-World-Backend:routes/api.php:789`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:54`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:57`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:71`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:76`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:77`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:81`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:82`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:89`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:94`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:127`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:197`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:199`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:446`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:458`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:464`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:369`
**Screens**: auth.login (web), LoginWithOtpScreen (app) · **API**: POST otp/send-otp, POST otp/verify-otp

### AUTH-R03: Request and verify a login OTP by email
`POST otp/send-email-otp` generates a 6-digit code, caches it for 5 minutes under `otp_<email>` and emails it; `POST otp/verify-email-otp` checks it (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:379`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:381`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:409`).
After the code is verified, the client then creates the session (AUTH-R04): web `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:446`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:458`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:464`, app `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:369`.
**Acceptance criteria**
- Given no email, then 400 "Email is required"; given an unregistered email, then 400 "Email not registered" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:359`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:373`).
- Given a registered email, then 200 "OTP sent successfully"; if sending fails, 500 "OTP not sent. Please check the email" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:415`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:420`).
- When verifying: missing email 400 "Email is required", missing OTP 400 "OTP is required", expired 400 "Expired OTP", wrong 400 "Invalid OTP", correct 200 "OTP verified successfully" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:433`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:436`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:439`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:452`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:457`).
- A sent OTP is kept for 5 minutes (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:381`).
- Given two fixed test emails listed in code, the code is a fixed test code and no email is sent (§13 Q5) (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:378`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:379`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:383`).
**Source**: `Ashoka-World-Backend:routes/api.php:790`, `Ashoka-World-Backend:routes/api.php:791`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:381`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:359`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:373`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:378`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:379`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:383`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:384`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:409`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:415`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:420`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:433`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:436`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:439`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:452`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:457`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:446`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:458`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:464`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:369`
**Screens**: auth.login (web), LoginWithOtpScreen (app) · **API**: POST otp/send-email-otp, POST otp/verify-email-otp

### AUTH-R04: Create the session after a login or an account switch
`POST loginOtpBasedUser` is the shared "create the session" step (`AuthController@loginOtpBasedUser`, `Ashoka-World-Backend:routes/api.php:739`). It takes a user `id` from the request (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:798`), loads the user only if the user is active (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:802`), creates an auth token if none exists (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:819`) and returns the session data. The code in this method does not check an OTP itself (§13 Q4). Every caller below reaches it after its own check:
- Password login (after AUTH-R01), roles other than 2: web `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:79` (role 7), `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:96` (other roles); app `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:110`. A patient (role 2) does not call it: the web calls `GET v2/client/getClientDetails` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:94`) and the app calls `getPatientData` (`Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:104`).
- OTP login (after AUTH-R02 or AUTH-R03): web `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:446`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:458`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:464`; app `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:369`; app API layer `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:431`.
- App start (auto-login): `Nadi-Tarangini-App:lib/splash_screen.dart:80`.
- Admin switching to a doctor view and back: `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1374`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1404`.
- After a KYC update on the web: `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:667`.
**Acceptance criteria**
- Given no active user with that id (an inactive or blocked user is not loaded) or a user without a role, then 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:802`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:806`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:810`).
**Source**: `Ashoka-World-Backend:routes/api.php:739`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:798`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:802`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:806`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:810`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:819`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:94`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:104`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:79`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:96`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:446`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:458`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:464`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:667`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1374`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1404`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:110`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:369`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:431`, `Nadi-Tarangini-App:lib/splash_screen.dart:80`
**Screens**: LoginWithUsernameScreen, LoginWithOtpScreen, SplashScreen (app); web login and OTP login, admin switch, my_account.update_kyc (web) · **API**: POST loginOtpBasedUser

### AUTH-R05: Recover a forgotten password
`POST forgotPassword` takes `user_name`, finds the active, non-deleted user, sets a newly generated password (a fixed prefix plus four digits) and sends it by email and by WhatsApp (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1652`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1684`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1710`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1717`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1740`). The request needs only the username (§13 Q7).
**Acceptance criteria**
- Given no username, then the validation fails with the message "The username is required" and status 404 (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1655`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1666`).
- Given an unknown or deleted user, then 404 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1679`).
- If the password cannot be saved, then 422 "Password not updated" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1696`).
- Given sending to both channels, then 200 "Forgot password successfully. Password sent to whatsapp/email"; email only, 200 "...sent to email but not on whatsapp"; WhatsApp only, 200 "...sent to whatsapp but not on email" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1751`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1762`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1773`).
- Given neither channel works, then 422 "No contact information found. Please contact customer care." and the change is rolled back (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1784`).
**Source**: `Ashoka-World-Backend:routes/api.php:777`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1652`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1679`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1684`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1696`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1717`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1740`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1751`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1762`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1773`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1784`
**Screens**: auth.forgot_password (web), ForgotPasswordScreen (app) · **API**: POST forgotPassword

### AUTH-R06: Sign up as a new doctor
`POST v2/signup` (web, NT Lite) and `POST signupV2` (app) both run `SignUpController@SignUpV2`, which validates the form, checks the mobile number and username are unused, checks salutation and gender, creates the user through `saveDoctor`, and sends the confirmation email and a WhatsApp sign-up message that both carry the plain password (`Ashoka-World-Backend:routes/api.php:1636`, `Ashoka-World-Backend:routes/api.php:744`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:701`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:927`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1033`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1055`). The older `POST signup` runs `SignUpController@SignUp` (starts at line 43), with additional required fields and an age check; the Samvit Chakra registration call and the S3 file uploads are in that older method, not in `SignUpV2` (`Ashoka-World-Backend:routes/api.php:741`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:43`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:220`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:491`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:662`).
**Acceptance criteria**
- Required: salutation type, username, password (must contain a digit), first and last name (letters and spaces only), email, gender (M, F, D or N), numeric mobile number, address line 1, clinic name, state, country; a country code is required when a mobile number is given. Optional: numeric profession type, AYUSH number (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:706`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:708`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:709`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:712`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:714`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:717`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:722`).
- Given a country code that is not valid for the number, then 400 "Provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:727`).
- Given a mobile number already registered (and not on the master whitelist), then 400 "Phone number already exists" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:825`).
- Given a username already in use, then 400 "User already exists with same username. Please try with another username" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:853`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:858`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:859`). The wording differs from `checkUsername` (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:195`).
- Given a salutation not in the salutation table, then 400 "Invalid salutation type" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:832`).
- Given a salutation and gender that do not fit, then 400 "Please select a valid gender" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:838`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:842`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:847`).
- Given a password shorter than 6 characters, then 400 "Minimum 6 digits password is required" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:908`).
- Given no clinic name, then the message "Clinic name is required" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:766`).
**Source**: `Ashoka-World-Backend:routes/api.php:744`, `Ashoka-World-Backend:routes/api.php:1636`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:706`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:708`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:709`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:712`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:714`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:717`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:722`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:727`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:766`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:825`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:832`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:838`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:853`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:908`
**Screens**: auth.signup, auth.admin_signUp, auth.college_signUp, auth.nt_lite_signup (web), SignUpScreen (app) · **API**: POST v2/signup (web, NT Lite), POST signupV2 (app)

### AUTH-R07: Check that a username or mobile number is free during sign-up
`POST checkUsername` looks for an active user with the given username; `POST checkMobileNumber` validates the number and country code and then looks for the number among users with role 1 or 4 (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:176`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:229`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:312`).
**Acceptance criteria**
- Username missing gives 400 "User name is required"; taken gives 400 "User already exists with the same username. Please try with another username"; free gives "Valid username" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:182`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:195`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:201`).
- Mobile number missing gives 400 "Phone number is required"; non-numeric gives 400 "Phone number must be numeric" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:229`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:236`).
- Country code missing gives 400 "Country code field is required if phone number is provided"; invalid gives 400 "Invalid country code" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:243`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:251`).
- A wrong length gives 400 "Invalid phone number length. The required length is ..."; a mismatching code gives 400 "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:298`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:301`).
- A number already used by a user with role 1 or 4 gives 400 "Phone number already exists" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:312`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:324`); a free number gives "Valid phone number" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:330`).
- An unexpected error gives 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:209`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:282`).
**Source**: `Ashoka-World-Backend:routes/api.php:763`, `Ashoka-World-Backend:routes/api.php:764`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:176`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:182`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:195`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:201`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:209`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:229`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:236`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:243`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:251`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:282`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:298`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:301`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:312`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:324`, `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:330`
**Screens**: web routes `POST checkDoctorUsername`, `POST checkDoctorMobileNo` and the NT Lite checks (no page that calls them was found) · **API**: POST checkUsername, POST checkMobileNumber

### AUTH-R08: Verify an email or mobile number with a one-time code
`POST otp/send-verification-otp` and `POST otp/verify-verification-otp` serve sign-up and the actions `profile_edit`, `kyc_update`, `add_clinic`, `update_clinic`, `admin_add_user` and `admin_update_user`; the code is cached for 5 minutes (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:480`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:612`).
**Acceptance criteria**
- `type` must be `email` or `mobile`, and `action` one of the seven listed values (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:479`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:480`).
- `email` is required when type is email; `country_code` and numeric `mobile_no` are required when type is mobile (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:481`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:482`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:483`).
- Sending succeeds with "OTP sent successfully via {type} for {action}."; an email failure gives 500 "Failed to send OTP via email."; a mobile failure gives 500 "OTP not sent. Please check the phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:617`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:564`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:606`).
- A mobile number of the wrong length gives 400 "Invalid phone number length"; a mismatching country code gives 400 "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:597`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:600`).
- Verifying needs a numeric `otp`; a wrong or expired code gives 422 "The code is invalid or has expired. Please try again."; a right one gives "OTP verified successfully." (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:630`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:656`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:666`).
**Source**: `Ashoka-World-Backend:routes/api.php:793`, `Ashoka-World-Backend:routes/api.php:794`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:479`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:480`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:481`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:482`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:483`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:564`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:597`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:600`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:606`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:612`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:617`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:630`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:656`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:666`
**Screens**: web pages auth.signup, auth.admin_signUp, auth.college_signUp, auth.nt_lite_signup, admin.create_user, admin.edit_profile, my_account.editClinicDetails, my_account.update_kyc; SignUpScreen, KycScreen, AddClinicScreen, EditClinicScreen, EditDoctorAccount (App) · **API**: POST otp/send-verification-otp, POST otp/verify-verification-otp

### AUTH-R09: Change the password while logged in
`POST updatepassword` identifies the user by the `user_id` header, requires `current_password` and `new_password`, and replaces the stored hash when the current password matches (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:12`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:16`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:58`). The route requires a logged-in user (`auth.token`) (`Ashoka-World-Backend:routes/api.php:975`).
**Acceptance criteria**
- A new password without a digit gives "New password must contain at least one digit." (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:24`; HTTP behaviour of this branch is §13 Q8).
- A new password shorter than 6 characters gives 400 "Minimum 6 digits password is required" (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:38`).
- No active user for the header id gives 400 "User not found" (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:51`).
- A wrong current password gives 400 "Incorrect current password"; reusing the old password gives 400 "New password must be different from the old password." (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:64`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:56`).
- Success gives 200 "Password updated successfully" (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:62`).
**Source**: `Ashoka-World-Backend:routes/api.php:975`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:12`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:16`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:24`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:38`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:51`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:56`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:58`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:62`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:64`
**Screens**: MyAccountScreen (app), my_account.myaccount (web, through `POST updatePassword` → `ChangePasswordController@updatePassword`) · **API**: POST updatepassword

### AUTH-R10: Register the device for push notifications
`POST editFcmToken` saves `fcm_token` on the user identified by the `user_id` header and returns "Fcm Token Updated Successfully." (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1859`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1862`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1865`). The app obtains the token and subscribes to topics in the login bloc (`Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:173`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:196`), only for users whose role is not 2 (`Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:190`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:413`). The web calls the route from `loginController@editFcmToken` (`Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:350`); the call is made on page load by the shared layout (`Nadi-Tarangini-Frontend:resources/views/layouts/main_layout.blade.php:154`).
**Acceptance criteria**
- Given no valid token, the route is refused by `auth.token` (`Ashoka-World-Backend:routes/api.php:971`).
- Given a database error, then 500 "Internal server error" and the transaction is rolled back (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1874`).
**Source**: `Ashoka-World-Backend:routes/api.php:971`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1852`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1859`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1862`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1865`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1874`, `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:350`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:391`, `Nadi-Tarangini-Frontend:resources/views/layouts/main_layout.blade.php:154`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:190`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:413`
**Screens**: after login in LoginWithOtpScreen and LoginWithUsernameScreen (app, roles other than 2); every web page that uses the shared layout (`Nadi-Tarangini-Frontend:resources/views/layouts/main_layout.blade.php`) · **API**: POST editFcmToken

### AUTH-R11: Provide sign-up reference lists (salutation and currency types)
`getSalutationTypes` and `getCurrencyType` are registered for both GET and POST and return the lists (`Ashoka-World-Backend:routes/api.php:759`, `Ashoka-World-Backend:routes/api.php:760`).
**Acceptance criteria**
- `getSalutationTypes` returns the list with "Get salutation types"; `getCurrencyType` returns it with "Get currency types" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1353`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1130`).
- Both return 500 "Internal server error" on failure (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1373`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1151`).
- The GET variants are called by no screen in this workspace; the POST variant of `getSalutationTypes` is called by SignUpScreen and by several web pages (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:812`, `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:24`), and the POST variant of `getCurrencyType` by KycScreen and EditDoctorAccount (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1709`). Web pages use the separate route `getCurrencyTypes` (`Ashoka-World-Backend:routes/api.php:767`).
**Source**: `Ashoka-World-Backend:routes/api.php:759`, `Ashoka-World-Backend:routes/api.php:760`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1353`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1130`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1151`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1373`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:812`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1709`, `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:24`, `Ashoka-World-Backend:routes/api.php:767`
**Screens**: SignUpScreen (salutation), KycScreen and EditDoctorAccount (currency) (app); auth.signup, add_self_admin, admin.create_user, my_account.edit_profile, my_account.myaccount, my_account.update_kyc (web) · **API**: GET/POST getSalutationTypes, GET/POST getCurrencyType

## 5. Screens (web / mobile)

| Screen | Platform | File | Route / path | Purpose (provable) |
|---|---|---|---|---|
| auth.login | Web | `Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php` | GET login | Login page, links to forgot password and sign-up (`Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php:181`) |
| auth.forgot_password | Web | `Nadi-Tarangini-Frontend:resources/views/auth/forgot_password.blade.php` | GET forgotPassword | Forgot-password page, goes to GET login (facts.md Screens) |
| auth.tabs | Web | `Nadi-Tarangini-Frontend:resources/views/auth/tabs.blade.php` | GET signup | Links to doctor and admin sign-up (`Nadi-Tarangini-Frontend:resources/views/auth/tabs.blade.php:27`) |
| auth.signup | Web | `Nadi-Tarangini-Frontend:resources/views/auth/signup.blade.php` | GET sign-up | Doctor sign-up page (`Nadi-Tarangini-Frontend:routes/web.php:325`) |
| auth.admin_signUp | Web | `Nadi-Tarangini-Frontend:resources/views/auth/admin_signUp.blade.php` | GET sign-up-admin | Admin sign-up page (`Nadi-Tarangini-Frontend:routes/web.php:329`) |
| auth.college_signUp | Web | `Nadi-Tarangini-Frontend:resources/views/auth/college_signUp.blade.php` | GET sign-up-college | College sign-up page (`Nadi-Tarangini-Frontend:routes/web.php:328`) |
| LoginScreen | Mobile | `Nadi-Tarangini-App:lib/common_files/Login/view/login_screen.dart` | /loginScreen | Goes to /signupScreen (facts.md Screens) |
| LoginWithUsernameScreen | Mobile | `Nadi-Tarangini-App:lib/common_files/Login/view/login_with_username_screen.dart` | no route in the fact pack (opened from LoginScreen, `Nadi-Tarangini-App:lib/common_files/Login/view/login_screen.dart:205`) | Goes to dashboard, forgot password, geo-restricted, KYC and patient report screens (facts.md Screens) |
| LoginWithOtpScreen | Mobile | `Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart` | no route in the fact pack (opened from LoginScreen, `Nadi-Tarangini-App:lib/common_files/Login/view/login_screen.dart:212`) | Goes to dashboard, geo-restricted, KYC and patient report screens (facts.md Screens) |
| ForgotPasswordScreen | Mobile | `Nadi-Tarangini-App:lib/common_files/Login/view/forgot_password_screen.dart` | /forgotPasswordScreen | Goes to /loginScreen (facts.md Screens) |
| SignUpScreen | Mobile | `Nadi-Tarangini-App:lib/common_files/signup/view/signup_screen.dart` | /signupScreen | Goes to /loginScreen and /webViewScreen (facts.md Screens) |

## 6. APIs

| Method | Endpoint | Controller | Auth (middleware) | Called by | Route |
|---|---|---|---|---|---|
| POST | v2/loginValidation | AuthController@loginValidation | api group only, no `auth.token` | web login, app | `Ashoka-World-Backend:routes/api.php:1639` |
| POST | loginOtpBasedUser | AuthController@loginOtpBasedUser | api | web password login (roles other than 2) and OTP login, admin switch, KYC update page, app password login (roles other than 2), OTP login and app start (AUTH-R04) | `Ashoka-World-Backend:routes/api.php:739` |
| POST | otp/send-otp | OtpSmsController@sendOtp | api | web, app | `Ashoka-World-Backend:routes/api.php:788` |
| POST | otp/verify-otp | OtpSmsController@verifyOtp | api | web, app | `Ashoka-World-Backend:routes/api.php:789` |
| POST | otp/send-email-otp | OtpSmsController@sendEmailOtp | api | web, app | `Ashoka-World-Backend:routes/api.php:790` |
| POST | otp/verify-email-otp | OtpSmsController@verifyEmailOtp | api | web, app | `Ashoka-World-Backend:routes/api.php:791` |
| POST | otp/send-verification-otp | OtpSmsController@sendVerificationOtp | api | Web: auth.signup, auth.admin_signUp, auth.college_signUp, auth.nt_lite_signup, admin.create_user, admin.edit_profile, my_account.editClinicDetails, my_account.update_kyc; App: SignUpScreen, KycScreen, AddClinicScreen, EditClinicScreen, EditDoctorAccount | `Ashoka-World-Backend:routes/api.php:793` |
| POST | otp/verify-verification-otp | OtpSmsController@verifyVerificationOtp | api | Web: the same pages as for send; App: the same screens, through the shared verification widget (`Nadi-Tarangini-App:lib/common_files/common_widgets/otp_verification_bottomsheet.dart:331`) | `Ashoka-World-Backend:routes/api.php:794` |
| POST | forgotPassword | AuthController@getForgotPassword | api | web, app | `Ashoka-World-Backend:routes/api.php:777` |
| POST | v2/signup | SignUpController@SignUpV2 | api group only, no `auth.token` | web sign-up, NT Lite sign-up | `Ashoka-World-Backend:routes/api.php:1636` |
| POST | signupV2 | SignUpController@SignUpV2 | api | app | `Ashoka-World-Backend:routes/api.php:744` |
| POST | signup | SignUpController@SignUp | api | Frontend `SignUpController@updateSignUpDetails` only, which has no web route (§13 Q6) | `Ashoka-World-Backend:routes/api.php:741` |
| POST | checkUsername | CheckUserExistOrNotController@checkUsername | api | Frontend `checkDoctorUsername` and NT Lite controllers (`Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:170`); no page that calls them was found | `Ashoka-World-Backend:routes/api.php:764` |
| POST | checkMobileNumber | CheckUserExistOrNotController@checkMobileNumberV2 | api | Frontend `checkDoctorMobileNo` and NT Lite controllers (`Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:132`); no page that calls them was found | `Ashoka-World-Backend:routes/api.php:763` |
| GET, POST | getSalutationTypes | SignUpController@salutationTypes | api | Web pages, App SignUpScreen (POST) | `Ashoka-World-Backend:routes/api.php:759` |
| GET, POST | getCurrencyType | SignUpController@getCurrencyType | api | App KycScreen, EditDoctorAccount (POST); web pages use `getCurrencyTypes` | `Ashoka-World-Backend:routes/api.php:760` |
| POST | updatepassword | UpdatePasswordController@updatePassword | api, auth.token | Web ChangePasswordController, App MyAccountScreen | `Ashoka-World-Backend:routes/api.php:975` |
| POST | editFcmToken | AuthController@updateFcmToken | api, auth.token | Web loginController, App login screens | `Ashoka-World-Backend:routes/api.php:971` |
| POST | login | AuthController@login | api | no screen in this workspace | `Ashoka-World-Backend:routes/api.php:737` |
| POST | logout | AuthController@logout | api, auth.token | no screen in this workspace | `Ashoka-World-Backend:routes/api.php:968` |
| POST | validateCorporateCode | AuthController@corporateCode | api, auth.token | no screen in this workspace | `Ashoka-World-Backend:routes/api.php:972` |
| GET | checkusernameormobileno | CheckUserExistOrNotController@checkMobileNumberOrEmail | api | no screen in this workspace | `Ashoka-World-Backend:routes/api.php:1426` |
| GET | getdetailsbymobileno | CheckUserExistOrNotController@getDetailsByMobileNo | api | no screen in this workspace | `Ashoka-World-Backend:routes/api.php:1427` |

## 7. Data model

Tables read or written by the controller methods behind this module's routes
(from model usage). Columns are those created or altered in migrations.

| Table | Model | Columns known from migrations | Migration files |
|---|---|---|---|
| user_personal_info | UserPersonalInfo | app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken | `Ashoka-World-Backend:database/migrations/2025_03_17_123123_add_plan_to_user_personal_info.php`, `Ashoka-World-Backend:database/migrations/2026_08_12_150000_add_welcome_tours_taken_to_user_personal_info_table.php` |
| transactions | Transaction | amount, payment_status, plan_id, user_id, … (26 columns) | `Ashoka-World-Backend:database/migrations/2025_03_17_123142_create_transactions_table.php`, `Ashoka-World-Backend:database/migrations/2026_07_07_130605_add_subscription_fields_to_transactions_table.php` |
| subscriptions | Subscription | id, name, price, duration, features, limits, status, api_rules, blocked_api_rules, create_date, updated_at | `Ashoka-World-Backend:database/migrations/2025_03_17_123100_create_subscriptions_table.php`, `Ashoka-World-Backend:database/migrations/2025_04_10_143119_nad_tarangini_add_api_access_columns_to_subscriptions_table.php` |
| user_nadi_capture_type | UserNadiCaptureType | can_change_capture_type, expiry_date, free_tier_enrolled, no_of_reports, plan_type | `Ashoka-World-Backend:database/migrations/2026_07_09_111953_nadi_tarangini_add_can_change_capture_type_to_user_nadi_capture_type_table.php`, `Ashoka-World-Backend:database/migrations/2026_09_29_121051_add_plan_type_and_nullable_expiry_to_report_grants.php` |
| api_endpoints | ApiEndpoints | id, name, url, method, is_active, is_public, is_public_reception, create_date, updated_date | `Ashoka-World-Backend:database/migrations/2025_04_10_121830_create_table_api_endpoints_table.php`, `Ashoka-World-Backend:database/migrations/2025_10_08_162449_nadi_tarangini_add_is_public_reception_to_api_endpoints_table.php` |
| corporate_info | CorporateInfo | city, corp_role_id, corporate_id, country, pincode, profile_image, state | `Ashoka-World-Backend:database/migrations/2025_04_26_163818_nadi_tarangini_add_columns_in_corporate_info.php`, `Ashoka-World-Backend:database/migrations/2025_05_28_122123_nadi_tarangini_add_columns_in_corporate_info.php` |
| locality_info | LocalityInfo | is_default, timezone | `Ashoka-World-Backend:database/migrations/2025_08_28_123744_nadi_tarangini_add_timezone_column_in_locality_info.php`, `Ashoka-World-Backend:database/migrations/2025_09_27_160902_nadi_tarangini_add_is_default_column_in_locality_info.php` |
| country_wise_states | CountryWiseStates | timezone | `Ashoka-World-Backend:database/migrations/2025_08_20_104235_add_timezone_country_wise_states.php` |
| currency_type | CurrencyType | columns not in migrations (§13 Q9) | none |
| salutation_types | SalutationTypes | columns not in migrations (§13 Q9) | none |
| pg_device_mapping | PgDeviceMapping | columns not in migrations (§13 Q9) | none |

Code also reads and writes `user_personal_info` columns that the migrations list does not show, for example `user_name`, `password`, `auth_token`, `fcm_token`, `role_id`, `is_active`, `delete_by_patient` (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:459`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:493`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:485`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1862`); their definitions are §13 Q9.

Source: `atreya-docs/_map/Ashoka-World-Backend/models.json` (migration files per table) and `atreya-docs/_map/Ashoka-World-Backend/models.md`; models such as
`Ashoka-World-Backend:app/Models/UserPersonalInfo.php`.

## 8. Validations & error handling

| API | Field / case | Rule or message | HTTP | Source |
|---|---|---|---|---|
| v2/loginValidation | user_name, password | required, string; messages per missing field | 400 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:415` |
| v2/loginValidation | unknown user, inactive (blocked) user, role 3 or 5 | "Invalid username" | 401 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:460`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:461`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:466` |
| v2/loginValidation | wrong password | "Invalid password" | 401 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481` |
| v2/loginValidation | exception | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:528` |
| loginOtpBasedUser | no active user with that id (inactive or blocked included), no role | "Invalid username" | 401 | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:802`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:806`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:810` |
| otp/send-otp | length, country code, registration | "Invalid phone number length", "The provided country code is not valid for the given phone number", "Phone number not registered" | 400 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:54`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:57`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:71` |
| otp/send-otp | send failure | "OTP not sent. Please check the phone number" | 500 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:94` |
| otp/verify-otp | code | "Invalid OTP", "Expired OTP" | 400 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:127`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136` |
| otp/send-email-otp | email | "Email is required", "Email not registered" | 400 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:359`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:373` |
| otp/verify-email-otp | email, otp, code | "Email is required", "OTP is required", "Expired OTP", "Invalid OTP" | 400 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:433`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:436`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:439`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:457` |
| otp/send-verification-otp | type, action | `in:email,mobile`; `in:signup,profile_edit,kyc_update,add_clinic,update_clinic,admin_add_user,admin_update_user` | not shown in code | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:479`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:480` |
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

More error messages per endpoint are listed in §4 acceptance criteria.

## 9. Non-functional

- **Security.** Four routes in this module require a logged-in user (`auth.token`):
  `updatepassword`, `editFcmToken`, `logout`, `validateCorporateCode` (`Ashoka-World-Backend:routes/api.php:968`, `Ashoka-World-Backend:routes/api.php:971`, `Ashoka-World-Backend:routes/api.php:972`, `Ashoka-World-Backend:routes/api.php:975`; §2). The
  two routes used by the current login and sign-up, `v2/loginValidation` and
  `v2/signup`, have no `auth.token` and sit only in the `api` group (`Ashoka-World-Backend:app/Providers/RouteServiceProvider.php:32`, `Ashoka-World-Backend:app/Http/Kernel.php:48`) (`Ashoka-World-Backend:routes/api.php:1639`,
  `Ashoka-World-Backend:routes/api.php:1636`); see §13 Q4.
- **OTP.** Login and verification codes are kept for 5 minutes (login by mobile
  `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79`, by email
  `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:381`, verification codes
  `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:612`) and are then refused as
  "Expired OTP" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136`). No attempt counter appears in the methods read (§13 Q5).
- **Passwords.** Sign-up requires a digit (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:708`) and a minimum length of 6 (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:908`);
  change password requires a digit and a minimum of 6
  (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:24`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:38`). Login compares with a hash check (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:480`).
- **Plain password copies.** In `SignUpV2` (used by web and app) the plain password goes into the confirmation email and the WhatsApp sign-up message (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1033`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1055`). In the older `SignUp` it also goes to the Samvit Chakra registration call (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:590`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:668`; §13 Q10).
- **Languages.** Required: English, Marathi, Hindi, Czech, German, Spanish,
  Italian (`references/qa-scope-rules.md`). Language files in code are English only
  (`Nadi-Tarangini-Frontend:resources/lang/en/auth.php`, `Nadi-Tarangini-Frontend:resources/lang/en/pagination.php`, `Nadi-Tarangini-Frontend:resources/lang/en/passwords.php`, `Nadi-Tarangini-Frontend:resources/lang/en/validation.php`, `Nadi-Tarangini-Frontend:resources/lang/en_patient.json`);
  backend messages above are English strings, for example `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481`. How the other languages reach these
  screens is §13 Q11.
- **Performance.** Apart from the 5-minute OTP validity, the only limit found is the `api` group rate limit of 100000 requests per minute (`Ashoka-World-Backend:app/Http/Kernel.php:48`); the fact pack lists no other request
  limits or timeouts for this module (`atreya-docs/_map/_modules/auth/facts.md`).

## 10. Environment matrix

Copied from `atreya-docs/environments.md` (not yet filled in).

Ashoka-World-Backend and Nadi-Tarangini-Frontend:

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

Not computed: all three repos are **waiting for environments.md** (staging and
production refs not filled in). See `staging-delta.md` in this folder.

## 12. External integrations

| System | Where | What the code shows |
|---|---|---|
| Firebase (Cloud Messaging) | `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:173`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:196` | The app gets the device token and subscribes to topics at login; the backend stores the token (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1862`) (AUTH-R10) |
| Firebase (Backend) | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1085` | After sign-up the backend adds an "Account Created" notification through a Firebase notification service |
| S3 | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:491`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:539`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:141` | The older `SignUp` method uploads profile-picture and clinic-logo files to S3 (`uploadFileToS3`); `AuthController` builds a profile-picture S3 URL only. `SignUpV2` has no upload call (§13 Q12) |
| Samvit Chakra | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:662` | Only the older `SignUp` (`POST signup`) posts name, email, mobile and password to `/api/register-student` of the configured Samvit Chakra URL; `SignUpV2` does not (AUTH-R06; §13 Q10) |
| WhatsApp and email delivery | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1717`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1740` | Forgot password sends the new password by email and WhatsApp (AUTH-R05); OTP email is sent from `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:409`, OTP SMS through `otpSmsService` (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:89`); providers are §13 Q12 |

## 13. Open questions

1. **PO:** Which roles exist (`GET public/allRoles`), what are roles 3 and 5 that `v2/loginValidation` excludes, and which roles may use web login, app login and OTP login?
2. **Dev:** In the web login (`loginController@checkLoginCredentials`), which of the five backend calls run for which user type (doctor, patient/client, admin)?
3. **Dev/PO:** What decides whether the app goes to the dashboard, KYC, geo-restricted or patient report screen after login (`LoginWithOtpScreen`, `LoginWithUsernameScreen`), and what does `checkGeoIPValidity` decide?
4. **Dev:** Is it intended that `POST v2/loginValidation` and `POST v2/signup` have no `auth.token` (only the `api` group), and that `POST loginOtpBasedUser` accepts a user `id` without checking an OTP in its own code?
5. **Dev/PO:** How many wrong OTP attempts are allowed, and are the fixed test numbers and emails with a fixed test code in `OtpSmsController` meant to exist in production?
6. **Dev:** Can `POST login`, `POST logout`, `POST validateCorporateCode`, `GET checkusernameormobileno`, `GET getdetailsbymobileno` and `POST signup` be retired, or are other clients using them? (`POST signup` is called only by a Frontend controller with no route; web `GET/POST logout` routes point to `LoginController`, not covered by this module's fact pack.)
7. **PO/Dev:** Is it intended that forgot password needs only a username, resets the password immediately, and uses a fixed prefix plus four digits as the new password?
8. **Dev:** What HTTP status does `updatepassword` return for the "no digit" case, since the error handler reads the message array in a way static reading cannot confirm?
9. **Dev:** What are the columns of `currency_type`, `salutation_types` and `pg_device_mapping`, and which `user_personal_info` columns (for example `user_name`, `password`, `auth_token`, `fcm_token`) come from outside the migrations?
10. **PO/Dev:** Is it intended that sign-up puts the plain password in the confirmation email and WhatsApp message (`SignUpV2`), and that the older `POST signup` also sends it to Samvit Chakra? Is `POST signup` still the path that registers users with Samvit Chakra, and does `SignUpV2` need to?
11. **PO/QA:** How do Marathi, Hindi, Czech, German, Spanish and Italian reach login and sign-up screens and backend messages?
12. **Dev:** How do web and app sign-up (`SignUpV2`) store profile pictures and clinic logos given that only the older `SignUp` uploads to S3, and which providers deliver WhatsApp, SMS and email?
13. **PO:** Should `v2/signup` and `signupV2` enforce the 18 to 100 age rule that `POST signup` has?
14. **Dev:** The explicit "User has been blocked" checks in `POST v2/loginValidation` (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:475-476`) and in `POST loginOtpBasedUser` (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:813-814` and `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:981-983`) can never run. The two queries already load only active users (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:460`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:802`), and every role branch returns "Invalid username" when its handler returns nothing, while each handler returns a user id otherwise (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:927`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:977`), so a blocked user gets "Invalid username" and `loginOtpBasedUser` never returns "User has been blocked". Is that intended?

## 14. Diagrams

Generated from code by `/atreya:diagram auth` (draw.io files in `diagrams/`; every
box and arrow carries its source; checked in `checks/diagrams-check.md`).

| Diagram | Kind | Shows | File |
|---|---|---|---|
| Screen flow (app) | flow | App login, OTP and username tabs, forgot password, sign-up, and where login leads | `diagrams/flow-app.drawio` |
| Screen flow (web) | flow | Web login, forgot password, sign-up tabs | `diagrams/flow-web.drawio` |
| AUTH-R01 | sequence | Username/password login: screens → callers → `POST v2/loginValidation` → AuthController → table, responses 400/401/500 | `diagrams/seq-AUTH-R01.drawio` |
| AUTH-R02 | sequence | Mobile OTP login: send OTP → verify OTP, with responses (the session step is AUTH-R04) | `diagrams/seq-AUTH-R02.drawio` |
| AUTH-R03 | sequence | Email OTP login: `POST otp/send-email-otp` → `POST otp/verify-email-otp`, with responses (the session step is AUTH-R04) | `diagrams/seq-AUTH-R03.drawio` |
| AUTH-R04 | sequence | The session step `POST loginOtpBasedUser`: every caller (web and app login, app start, admin switch, KYC update) → AuthController → tables, responses | `diagrams/seq-AUTH-R04.drawio` |
| AUTH-R05 | sequence | Forgot password: screens → callers → `POST forgotPassword`, with responses | `diagrams/seq-AUTH-R05.drawio` |
| AUTH-R06 | sequence | Doctor sign-up: web and NT Lite → `POST v2/signup`, app → `POST signupV2`, with responses | `diagrams/seq-AUTH-R06.drawio` |
| AUTH-R07 | sequence | Sign-up availability checks: `POST checkUsername`, `POST checkMobileNumber`, with responses | `diagrams/seq-AUTH-R07.drawio` |
| AUTH-R08 | sequence | Email/mobile verification code: `POST otp/send-verification-otp` → `POST otp/verify-verification-otp`, with responses | `diagrams/seq-AUTH-R08.drawio` |
| AUTH-R09 | sequence | Change password while logged in: screens → callers → `POST updatepassword`, with responses | `diagrams/seq-AUTH-R09.drawio` |
| AUTH-R10 | sequence | Push-notification device registration: callers → `POST editFcmToken`, with responses | `diagrams/seq-AUTH-R10.drawio` |
| AUTH-R11 | sequence | Sign-up reference lists: callers → `GET/POST getSalutationTypes`, `GET/POST getCurrencyType`, with responses | `diagrams/seq-AUTH-R11.drawio` |
| Data model | ER | The 11 tables of §7 with columns known from migrations (no model relations between them) | `diagrams/er.drawio` |

## 15. Document control

| Field | Value |
|---|---|
| Status | Draft |
| Date | 2026-10-26 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`, Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`, Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d` |
