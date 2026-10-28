---
module: "auth"
doc: "BRD"
status: "Draft"
date: "2026-10-26"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Authentication & sign-up: Business Requirements Document

## 1. Purpose & overview

This part of Nadi Tarangini is the front door of the product. It lets people sign in on the website or in the mobile app, either with a username and password or with a one-time code sent to their mobile number or email. A user who forgot the password can get a new one sent to them. A new doctor can register, and the system checks that the chosen username and mobile number are free and confirms contact details with a one-time code. Once signed in, a user can change the password, and the device is registered so it can receive notifications. Five older functions exist in the system that no screen uses today (see §4 and §12).

| Source |
|---|
| PRD `nt/auth/rerun/PRD.md` §1, §3; `atreya-docs/_map/_modules/auth/facts.md` |

## 2. Business objectives

TO CONFIRM: no ticket or document states why this area exists in business terms (for example more doctors registering, fewer support calls about lost passwords). The code cannot answer this. See §12 Q1.

## 3. Stakeholders & user roles

| Role | How they are involved | Source |
|---|---|---|
| Doctor | Registers, signs in, recovers or changes the password | AUTH-R01, AUTH-R05, AUTH-R06, AUTH-R09 |
| Administrator (website) | Signs in; can switch to a doctor view and back | AUTH-R04; `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1374`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1404` |
| Patient (to confirm) | The app can send a signed-in user to a patient report screen; who that is, is not stated | `atreya-docs/_map/_modules/auth/facts.md` (Screens); §12 Q2 |
| College and admin sign-up users (to confirm) | The website has separate sign-up pages for administrators and colleges | `Nadi-Tarangini-Frontend:routes/web.php:328`, `Nadi-Tarangini-Frontend:routes/web.php:329`; §12 Q2 |
| Customer care | Users with no contact details are told to contact customer care | AUTH-R05; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1784` |

Which roles exist and what each may do is not stated in the code read (§12 Q2).

## 4. Scope

### In scope

- Signing in with a username and password (website and app).
- Signing in with a one-time code sent to a mobile number or an email.
- Recovering a forgotten password.
- Registering as a new doctor, including checking that a username or mobile number is free.
- Confirming an email or mobile number with a one-time code (registration and some later changes).
- Changing the password while signed in.
- Registering the device for notifications after sign-in.
- The lists (titles, currencies) shown on registration forms.

### Out of scope

- What users can do after signing in (dashboard, patients, reports and other modules).
- Payments and subscriptions (other modules).
- Five functions that no screen in this workspace calls: older password login, sign out, corporate code check, and two lookups by mobile number or username. They are not presented as live; whether to retire them is §12 Q6.
- The older registration function, used only by a website controller that has no page route (§12 Q6).

| Source |
|---|
| AUTH-R01 to AUTH-R11; `atreya-docs/not-in-use.md` (auth: 5 of 25 routes); PRD §1 |

## 5. Current business process (as-is)

1. A user opens the sign-in page on the website or the sign-in screen in the app.
2. They sign in with a username and password, or ask for a one-time code by mobile number or email and enter it.
3. If the details are right the user gets in; unknown, blocked or wrongly entered details are refused with a message.
4. A user who forgot the password enters the username; the system sets a new password and sends it by email and/or WhatsApp.
5. A new doctor fills in the registration form. Username and mobile number are checked as free, the email or mobile number is confirmed with a one-time code, then the account is created.
6. After sign-in the device is registered for notifications, and the user can change the password later.

| Source |
|---|
| PRD §3 (journeys J1 to J5); AUTH-R01 to AUTH-R10 |

## 6. Business rules

| Rule | Source |
|---|---|
| Both a username and a password must be entered to sign in. | AUTH-R01; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:429` |
| A wrong password, or an unknown username, is refused. | AUTH-R01; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:466`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481` |
| A blocked user cannot sign in. | AUTH-R04; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:814` |
| A sign-in code is sent only to a mobile number or email that is already registered. | AUTH-R02, AUTH-R03; `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:71`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:373` |
| A one-time code stays valid for 5 minutes; after that it is refused as expired. | AUTH-R02, AUTH-R03, AUTH-R08; `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:79`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136` |
| The mobile number must have the right length and match the chosen country code. | AUTH-R02, AUTH-R07, AUTH-R08; `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:54`, `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:57` |
| A mobile number can be registered only once, except numbers on the master whitelist. | AUTH-R06; `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:821`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:825` |
| A username can belong to only one account. | AUTH-R07; `Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:195` |
| A registration password must contain at least one digit. | AUTH-R06; `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:708` |
| First and last names may contain only letters and spaces. | AUTH-R06; `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:709` |
| The title chosen at registration must exist in the system and fit the gender chosen. | AUTH-R06; `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:832`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:838` |
| Changing the password needs the current password; the new one needs a digit, at least 6 characters, and must differ from the old one. | AUTH-R09; `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:16`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:38`, `Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:56` |
| Forgotten-password recovery needs only the username and replaces the password at once. | AUTH-R05; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1652`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1684` |
| If a new password reaches the user by neither email nor WhatsApp, the change is undone and the user is told to contact customer care. | AUTH-R05; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1784` |

## 7. Business requirements

| ID | Requirement | Source |
|---|---|---|
| BR-01 | A user can sign in with a username and password on the website and in the app. | AUTH-R01 |
| BR-02 | A user can sign in with a one-time code sent to a registered mobile number. | AUTH-R02, AUTH-R04 |
| BR-03 | A user can sign in with a one-time code sent to a registered email address. | AUTH-R03, AUTH-R04 |
| BR-04 | A user who forgot the password can have a new one sent by email and/or WhatsApp, and is told which channel worked. | AUTH-R05 |
| BR-05 | A new doctor can register on the website or in the app with personal, contact and clinic details. | AUTH-R06, AUTH-R11 |
| BR-06 | While registering, a doctor is told if the chosen username or mobile number is already taken. | AUTH-R07 |
| BR-07 | An email address or mobile number is confirmed with a one-time code during registration and during later profile, KYC and clinic changes. | AUTH-R08 |
| BR-08 | A signed-in user can change the password. | AUTH-R09 |
| BR-09 | After sign-in, the user's device is registered to receive notifications. | AUTH-R10 |
| BR-10 | An administrator on the website can switch to a doctor view and back. | AUTH-R04 |

## 8. Availability by environment

Not yet known: `atreya-docs/environments.md` is still "TO FILL" for all three parts of the product. See §12 Q3.

| Environment | Website | App | Backend |
|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL |

## 9. Dependencies & external systems

| Dependency | Why it matters | Source |
|---|---|---|
| Firebase push notifications (app) | The app gets a device token after sign-in so the user can receive notifications. | AUTH-R10; `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:173`, `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:196` |
| Firebase (backend) | After registration the system adds an "Account Created" notification. | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1085` |
| SMS service | Sends mobile one-time codes. | AUTH-R02; `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:89` |
| Email delivery | Sends email one-time codes and the new password. | AUTH-R03, AUTH-R05; `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:409`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1710` |
| WhatsApp delivery | Sends the new password after a forgotten-password request. | AUTH-R05; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1740` |
| Cloud file storage (S3) | Used in the sign-in and registration code; what is stored is not stated (§12 Q8). | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:491`, `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:139` |
| Samvit Chakra | Only the older registration function calls this external system; the current registration does not (§12 Q7). | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:662` |

## 10. Assumptions & constraints

| Item | Source |
|---|---|
| The required product languages are English, Marathi, Hindi, Czech, German, Spanish and Italian; the language files found for the website are English only, and the messages in this area are English. | `references/qa-scope-rules.md`; `Nadi-Tarangini-Frontend:resources/lang/en/auth.php`; PRD §9 |
| The website sign-up and the app sign-up both run the same backend registration function. | AUTH-R06; `Ashoka-World-Backend:routes/api.php:744`, `Ashoka-World-Backend:routes/api.php:1636` |
| The environments sheet is not filled in, so no statement about what runs where can be made. | `atreya-docs/environments.md` |

## 11. Success measures (TO CONFIRM)

For the product owner to decide; none is stated in the code:

- Which share of sign-ins should use a password and which a one-time code?
- Is the number of failed sign-ins or "forgot password" requests tracked, and what is acceptable?
- How long should it take a new doctor to finish registration, and how many should finish?

See §12 Q4.

## 12. Needs confirmation

1. **Product owner:** What are the business objectives for sign-in and registration?
2. **Product owner:** Which user roles exist, which may sign in on the website, in the app and with a one-time code, and who is sent to the patient report screen after app sign-in? Are the administrator and college sign-up pages in use?
3. **Product owner / dev:** In which environments (dev, staging, production) is each sign-in method available? (the environments sheet is empty)
4. **Product owner:** Which success measures should be tracked for this area?
5. **Product owner / dev:** How many wrong one-time code attempts should be allowed, and are the fixed test numbers and emails with a fixed code in the code meant to exist in production?
6. **Dev:** May the five unused functions and the older registration function be retired, or do other clients use them?
7. **Product owner / dev:** The older registration function sends the plain password to Samvit Chakra; the current registration does not call it. Is Samvit Chakra still needed, and should the older function be retired?
8. **Dev:** What is stored in cloud file storage during sign-in and registration, and which providers deliver SMS, WhatsApp and email?
9. **Dev / product owner:** Is it intended that the website sign-in and registration calls need no sign-in token, and that the session step after a one-time code accepts a user id without checking the code in its own code?
10. **Product owner:** Is it intended that forgotten-password recovery needs only a username, replaces the password at once, and uses a "atreya" plus four digits pattern?
11. **Product owner:** Should the current registration also enforce the 18 to 100 age rule that the older registration has?
12. **Product owner / QA:** How are Marathi, Hindi, Czech, German, Spanish and Italian provided on these screens and messages?

## 13. Document control

| Field | Value |
|---|---|
| Status | Draft |
| Date | 2026-10-26 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`, Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`, Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d` |
