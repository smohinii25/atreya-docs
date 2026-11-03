---
module: "dashboard"
doc: "BRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Doctor dashboard, onboarding & welcome tour: Business Requirements Document

## 1. Purpose & overview

This part of the product is the doctor's home screen. It shows a doctor how many patients and nadi assessments they have handled, how much they have charged and been paid, and a patient-growth chart (last 7 days, last 4 weeks or last 12 months). It also guides new doctors through short on-screen "welcome tours", and on the website it holds account pages such as subscription plans, free trial, checkout, KYC details, clinic and report-language settings, and linked devices. On the mobile app it also covers the first-launch flow (splash, onboarding, region restriction).

| Source |
|---|
| DASHBOARD-R01 to R14; `atreya-docs/_map/_modules/dashboard/facts.md` |

## 2. Business objectives

TO CONFIRM. The code does not state why the dashboard exists or what it should achieve. See §12.

## 3. Stakeholders & user roles

| Role | How they use it | Source |
|---|---|---|
| Doctor | Sees own totals, daily and monthly counts and the patient chart; takes welcome tours | DASHBOARD-R01, R02, R03, R04; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2143` |
| Patient | Gets no welcome tour and cannot mark a tour complete | DASHBOARD-R04, R05; `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:41` |
| Admin (switching) | The website lets a user switch to an admin view and back to a doctor view | DASHBOARD-R11; `Nadi-Tarangini-Frontend:routes/web.php:156` |
| Other roles (receptionist, sub-doctor) | Not stated; see §12 | DASHBOARD-R01 |

## 4. Scope

### In scope
- Doctor summary numbers and the patient chart (website and app). DASHBOARD-R01, R02, R03
- Welcome tours for seven screens. DASHBOARD-R04, R05
- Website dashboard page. DASHBOARD-R07
- Subscription plans, free trial, checkout and payment on the website. DASHBOARD-R08
- Clinic and report-language settings, linked device, KYC, self-admin, role switch, account deletion on the website. DASHBOARD-R09, R10, R11
- App launch, onboarding and region-restricted screen. DASHBOARD-R12

### Out of scope
- The detailed payment and subscription back-office logic (belongs to other modules). DASHBOARD-R08
- A statistics service that no screen in the workspace uses. DASHBOARD-R14
- Member progress, member report and queries pages: purpose not confirmed; see §12. DASHBOARD-R07

## 5. Current business process (as-is)

1. A doctor opens the app. If no language is chosen, language choice is shown; then onboarding if not done; then login if not signed in. A signed-in patient goes to the patient report; a doctor outside the allowed region sees a restricted-region notice; a doctor whose KYC is not updated goes to KYC; otherwise the dashboard opens. DASHBOARD-R12
2. On the dashboard the doctor sees overall totals, today's and this month's counts, and a chart of new patients (last 7 days, last 4 weeks or last 12 months). DASHBOARD-R01, R02, R03
3. The first time a doctor visits a screen with a tour, step-by-step guidance is shown; finishing it is recorded so it is not repeated. DASHBOARD-R04, R05
4. On the website, the doctor also sees banners, recent patients, plan, appointments, seasonal tips and help videos. DASHBOARD-R07
5. A doctor can view plans, start a free trial or purchase a plan on the website. DASHBOARD-R08

| Source |
|---|
| `Nadi-Tarangini-App:lib/splash_screen.dart:47`; `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:56` |

## 6. Business rules

| Rule | Source |
|---|---|
| Totals and counts only include the doctor's own active patients and their nadi assessments. | DASHBOARD-R01; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2091` |
| Daily and monthly counts follow the doctor's default time zone; if none is set or it is invalid, India time (Asia/Kolkata) is used. | DASHBOARD-R02; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2143` |
| The patient chart can only be shown for weekly, monthly or yearly periods; any other choice is rejected. | DASHBOARD-R03; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2248` |
| Periods before the doctor joined show zero patients. | DASHBOARD-R03; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2353` |
| A welcome tour exists only for these screens: dashboard, prakruti fill, add patient, visit report, medical inventory, nadi flow, live nadi. | DASHBOARD-R04; `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:23` |
| Patients get no tours and cannot complete one. | DASHBOARD-R05; `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:105` |
| A tour completion is recorded for either the website or the mobile app (website by default). | DASHBOARD-R05; `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:78` |
| A user must be signed in to use any dashboard function, except the KYC page on the website which has no sign-in check listed. | DASHBOARD-R06, R11; `Nadi-Tarangini-Frontend:routes/web.php:304` |

## 7. Business requirements

| ID | Requirement | Source |
|---|---|---|
| BR-01 | A doctor can see overall totals: patients, reports, fees charged, fees paid, fees remaining and nadi assessments. | DASHBOARD-R01; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2110` |
| BR-02 | A doctor can see today's and this month's patient and assessment counts. | DASHBOARD-R02; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2220` |
| BR-03 | A doctor can view new-patient counts for the last 7 days, last 4 weeks or last 12 months. | DASHBOARD-R03; `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:2353` |
| BR-04 | A doctor is shown a guided welcome tour for each supported screen. | DASHBOARD-R04; `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:53` |
| BR-05 | The system remembers when a doctor has finished a tour, per screen and per platform. | DASHBOARD-R05; `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:117` |
| BR-06 | Patients are never shown or recorded against welcome tours. | DASHBOARD-R04, R05; `Ashoka-World-Backend:app/Http/Controllers/WelcomeTourController.php:105` |
| BR-07 | A signed-in user's account information is available to other screens (appointments, patients, prescriptions). | DASHBOARD-R06; `Ashoka-World-Backend:app/Http/Controllers/UserStatsController.php:359` |
| BR-08 | On the website, the dashboard page brings together banners, recent patients, plan, summary, appointments, seasonal tips, help videos and associations. | DASHBOARD-R07; `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:56` |
| BR-09 | A doctor can view plans, start a free trial and purchase a plan on the website. | DASHBOARD-R08; `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:573` |
| BR-10 | A doctor can choose and change the clinic and the languages used for reports. | DASHBOARD-R09; `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:424` |
| BR-11 | A doctor can view and link devices. | DASHBOARD-R10; `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:446` |
| BR-12 | A user can update KYC details, create a self-admin profile, switch between admin and doctor views, and delete their account on the website. | DASHBOARD-R11; `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:646` |
| BR-13 | The app guides a new user from splash through onboarding to login, and shows a restricted-region screen where applicable. | DASHBOARD-R12; `Nadi-Tarangini-App:lib/splash_screen.dart` |

## 8. Availability by environment

Every environment detail is still TO FILL in `environments.md`, so availability in dev, staging and production is unknown. PRD §10 has the full table. A staging-versus-production comparison has not been computed (waiting for `environments.md`).

| Repo | dev | staging | production | Source |
|---|---|---|---|---|
| Ashoka-World-Backend | TO FILL | TO FILL | TO FILL | `atreya-docs/environments.md` |
| Nadi-Tarangini-App | TO FILL | TO FILL | TO FILL | `atreya-docs/environments.md` |
| Nadi-Tarangini-Frontend | TO FILL | TO FILL | TO FILL | `atreya-docs/environments.md` |

## 9. Dependencies & external systems

No external systems were found in this module's files (`atreya-docs/_map/_modules/dashboard/facts.md`). The module depends on other parts of the product: subscription and plan services, clinic and language lists, device linking, patient and appointment lists, banners, help videos and seasonal tips. Source: DASHBOARD-R07, R08, R09, R10; `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:56`. Whether a payment provider is involved is not shown; see §12.

## 10. Assumptions & constraints

- Everything is tied to a signed-in user. Source: `Ashoka-World-Backend:routes/api.php:907`
- Required languages are English, Marathi, Hindi, Czech, German, Spanish and Italian; only English language files are listed for the website in the fact pack. Source: `references/qa-scope-rules.md`; `atreya-docs/_map/_modules/dashboard/facts.md`
- Numbers on the dashboard are counted for the signed-in doctor only. Source: DASHBOARD-R01

## 11. Success measures (TO CONFIRM)

TO CONFIRM with the product owner; none are in code. See §12 items 1 and 2.

## 12. Needs confirmation

1. (Product owner) What business goals does the dashboard serve (for example doctor engagement, tour completion, subscription conversion)?
2. (Product owner) How is success measured for the dashboard and welcome tours?
3. (Product owner) Which roles other than doctor and patient (receptionist, sub-doctor, admin) should see the dashboard and tours, and should their numbers include the doctors they work for?
4. (Product owner) What are the welcome tour contents for each of the seven screens?
5. (Product owner) What are the member progress, member report and queries pages on the website for, and are they in use?
6. (Developer) Is the unused statistics service live for some other client, or can it be retired?
7. (Developer) The website's subscription page asks for a feature list that has no matching service in this workspace: is that a gap?
8. (Product owner) Which regions or users does the restricted-region screen block?
9. (Developer) Is it intended that the KYC page on the website has no sign-in check?
10. (Product owner) Does buying a plan use an external payment provider, and which module owns that flow?
11. (Owner) When will the environment details be filled in so staging versus production can be compared?
12. (Product owner) Which languages besides English must the dashboard support, and where are those texts?

## 13. Document control

| Field | Value |
|---|---|
| Status | Draft |
| Date | 2026-11-03 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend 8dfbb37db7d71a400b3656bd50fbed6173908a24; Nadi-Tarangini-App 0b7deec6de2b0b8b4f05eab4be8c8430523829bf; Nadi-Tarangini-Frontend e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d |
