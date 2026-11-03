---
module: "nt-admin"
doc: "BRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# NT admin panel (users, access, data management, customise by user): Business Requirements Document

## 1. Purpose & overview

The admin panel is the part of the Nadi Tarangini website where an administrator manages the people who use the product. An administrator can add users, switch them on or off, change their details and passwords, decide which features and which data each user can use, look at a user's patients and past visits, and tailor the reports and questionnaires a user sees. The panel also shows plan details, lets the administrator apply a coupon and pay for a plan, and lists payment invoices. Source: PRD §1, NT-ADMIN-R02 to R13; `Nadi-Tarangini-Frontend:routes/web.php:111-164`.

## 2. Business objectives

Not stated in code. See §11 and §12 Q1. Source: none (TO CONFIRM).

## 3. Stakeholders & user roles

| Role | How they use it | Source |
|---|---|---|
| Administrator (role number 7) | The only role that can open the admin pages on the website; anyone else is sent to the login page. | NT-ADMIN-R01; `Nadi-Tarangini-Frontend:app/Http/Middleware/NTAdminAuthentication.php:23-34` |
| Users created by the administrator | Receive an account, features and data access set by the administrator. | NT-ADMIN-R04, R08, R09 |
| Mobile app users | Use three shared services: the list of roles at login, the list of users and clinic locations when adding an appointment or patient, and feature details for an assessment. | NT-ADMIN-R09, R15, R16; `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:63`, `:2038`, `:2396` |

The names and meaning of the other role numbers are not in the code (§12 Q2).

## 4. Scope

### In scope
- Admin sign-in restriction and region check (NT-ADMIN-R01).
- Dashboard with user and consultation counts (R02), users and teams overview (R03).
- Create user, activate/deactivate, edit profile, change password (R04 to R07).
- Feature permissions and data access per user (R08, R09).
- Viewing a user's patients, visits and reports (R10).
- Customising report pages and questionnaires, for everyone or for one user (R11, R12).
- Plans, coupons, orders, payment checks and invoices from the admin side (R13).
- Role and feature lookups used at login and in assessments (R14 to R16).

### Out of scope
- The report, questionnaire, subscription and patient services that the admin pages call but which belong to other modules (PRD §6 note).
- One service that lists accessible users has no screen using it, so it is treated as a question, not a live feature (`atreya-docs/not-in-use.md:75`; NT-ADMIN-R17).
- Environment details and the staging comparison, which are not filled in yet (§8).

## 5. Current business process (as-is)

1. The administrator signs in and opens the dashboard, which shows the administrator's details, the roles below them and counts of users and consultations (NT-ADMIN-R02).
2. From the users and teams page the administrator chooses a user and then one action: edit profile, change password, set permissions, set data access, view patients, or customise reports or questionnaire (R03; screen links in `atreya-docs/_map/_modules/nt-admin/facts.md`).
3. To add a user, the administrator fills in a form with personal, login and clinic details and saves. The new user gets an "Account Created" notification (R04; `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:67`).
4. To change what a user may do, the administrator opens the permissions page, adjusts features and saves (R08).
5. To review a user's work, the administrator opens that user's patient list, a patient's earlier visits and the reports (R10).
6. To pay for a plan, the administrator opens plan details, may apply a coupon, creates an order and the payment is verified (R13).

## 6. Business rules

| Rule | Source |
|---|---|
| Only an administrator (role 7) who is signed in can open admin pages; others go to the login page. | NT-ADMIN-R01; `Nadi-Tarangini-Frontend:app/Http/Middleware/NTAdminAuthentication.php:23-34` |
| For administrators, access can also be blocked by region. | `Nadi-Tarangini-Frontend:app/Http/Middleware/NTAdminAuthentication.php:25-27` |
| A new user must have a user name, password, first and last name, email, gender, mobile number, profession, role, clinic name, address, state and country. | NT-ADMIN-R04; `Ashoka-World-Backend:app/Http/Requests/NTAdmin/UserManagement/AddUserRequest.php:24-47` |
| A password must contain at least one digit. | `Ashoka-World-Backend:app/Http/Requests/NTAdmin/UserManagement/AddUserRequest.php:26` |
| First and last names accept only letters and spaces. | `Ashoka-World-Backend:app/Http/Requests/NTAdmin/UserManagement/AddUserRequest.php:27-28` |
| Gender must be one of four allowed codes (M, F, D, N); mobile number must be numeric; email must be valid. | `Ashoka-World-Backend:app/Http/Requests/NTAdmin/UserManagement/AddUserRequest.php:29-31` |
| The administrator cannot create a user with role numbers 2, 3, 4 or 7. | `Ashoka-World-Backend:app/Http/Requests/NTAdmin/UserManagement/AddUserRequest.php:40` |
| If creating a user fails, the person sees the reason; if only the welcome notification fails, the user is still created. | `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:58-84` |
| Consultation counts can be requested for 1 to 500 users at a time, with an optional date range where the end date is not before the start date. | NT-ADMIN-R02; `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:556-559` |
| Editing another user's profile needs the user to be identified. | NT-ADMIN-R06; `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:481` |
| A feature-details request needs a type and a valid patient; a medical visit is checked only when one is given. | NT-ADMIN-R16; `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:122-202` |
| Several admin services (for example the user list, child roles, create user, password change) reject a request that does not identify the signed-in user; others do not check this in the service itself. | NT-ADMIN-R03, R04, R07; `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:99` |

## 7. Business requirements

| ID | Requirement | Source |
|---|---|---|
| BR-01 | Only a signed-in administrator can use the admin panel, subject to a region check. | NT-ADMIN-R01 |
| BR-02 | An administrator can see a dashboard of their users by role and consultation counts. | NT-ADMIN-R02 |
| BR-03 | An administrator can see all their users, roles and teams in one place. | NT-ADMIN-R03 |
| BR-04 | An administrator can create a new user with login, personal and clinic details. | NT-ADMIN-R04 |
| BR-05 | An administrator can switch a user on or off. | NT-ADMIN-R05 |
| BR-06 | An administrator can edit their own or another user's profile. | NT-ADMIN-R06 |
| BR-07 | An administrator can set a new password for a user. | NT-ADMIN-R07 |
| BR-08 | An administrator can choose which features each user has. | NT-ADMIN-R08 |
| BR-09 | An administrator can choose which data each user can access, and apps can show the users and clinic locations a person may work with. | NT-ADMIN-R09 |
| BR-10 | An administrator can view a user's patients, previous visits and reports. | NT-ADMIN-R10 |
| BR-11 | An administrator can customise report pages for everyone or for one user. | NT-ADMIN-R11 |
| BR-12 | An administrator can customise the questionnaire for everyone or for one user. | NT-ADMIN-R12 |
| BR-13 | An administrator can view plans, apply a coupon, place an order, verify the payment and see invoices. | NT-ADMIN-R13 |
| BR-14 | A signed-in user can add themselves as an administrator, and feature details are loaded when switching to the doctor view. | NT-ADMIN-R14 |
| BR-15 | The list of roles is available before sign-in, and feature details are available after sign-in. | NT-ADMIN-R15 |
| BR-16 | Feature details can be fetched for a patient's medical assessment. | NT-ADMIN-R16 |

## 8. Availability by environment

Environment details (version, address, switches, test or live mode) are still TO FILL in `atreya-docs/environments.md` for Ashoka-World-Backend and Nadi-Tarangini-Frontend, so availability in dev, staging and production is not known. The staging comparison was skipped for the same reason (`atreya-docs/nt/nt-admin/staging-delta.md`). Source: PRD §10, §11.

## 9. Dependencies & external systems

| System | Used for | Source |
|---|---|---|
| Push notification service (Firebase) | The "Account Created" notification to a new user. | `Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:67` |
| Online payment provider (Razorpay) | Payment verification for plans on the admin side. | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1728-1730` |
| Other product services | Reports, questionnaires, subscriptions and patient lists are provided by other parts of the product. | PRD §6; NT-ADMIN-R10 to R13 |

## 10. Assumptions & constraints

- Admin pages are website-only; the fact pack lists no mobile admin screen. Source: `atreya-docs/_map/_modules/nt-admin/facts.md` (Screens).
- Administrators are limited by region check. Source: `Nadi-Tarangini-Frontend:app/Http/Middleware/NTAdminAuthentication.php:25-27`.
- The required languages are English, Marathi, Hindi, Czech, German, Spanish and Italian, but only English language files were found for this module. Source: `references/qa-scope-rules.md`; `Nadi-Tarangini-Frontend:resources/lang/en/auth.php`.

## 11. Success measures (TO CONFIRM)

Questions for the product owner (none are stated in the code):
- How many users should an administrator be able to manage, and how fast should creating a user be?
- What proportion of new users should be created without errors?
- What would show that customising reports and questionnaires per user is working?

## 12. Needs confirmation

1. (PO) What business goals does the admin panel serve (objectives in §2)?
2. (PO/dev) What do role numbers 2, 3, 4, 7 and the others stand for?
3. (PO) Should there be a mobile admin experience, or is the website the only intended place?
4. (dev) Which screen is used to switch users on or off, and which one to add yourself as an administrator?
5. (PO/dev) Is the service that lists accessible users (without locations) still needed?
6. (PO) What are the business rules for plans, coupons and invoices (pricing, eligibility)?
7. (PO) What are Razorpay and Firebase used for in each environment (test or live)?
8. (PO/QA) Must admin screens be translated into the other required languages?
9. (PO/dev) Is showing the technical error text to the caller on some failures intended?
10. (PO) What are the success measures in §11?

## 13. Document control

| Item | Value |
|---|---|
| Status | Draft |
| Date | 2026-11-03 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend 8dfbb37db7d71a400b3656bd50fbed6173908a24; Nadi-Tarangini-Frontend e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d |
