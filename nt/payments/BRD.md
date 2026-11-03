---
module: "payments"
doc: "BRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Subscriptions & payments (Razorpay): Business Requirements Document

## 1. Purpose & overview

This part of the product lets a user see the available subscription plans, try a plan free for 30 days, pay online for a plan, and then see their plan, remaining reports and past payments. A paid purchase adds reports to the user's balance and extends the plan's end date. Payments are taken through Razorpay. | Source: PAYMENTS-R01, R03, R04, R06, R08; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1052`

## 2. Business objectives

TO CONFIRM by the product owner; no objectives are stated in code. See §12 item 1. | Source: none

## 3. Stakeholders & user roles

| Role | What they do here | Source |
|---|---|---|
| Logged-in user (doctor or other account holder) | Views plans, starts a trial, pays, sees plan status and history | PAYMENTS-R01, R07, R08, R11; `Ashoka-World-Backend:routes/api.php:1340` |
| Admin dashboard user (web) | Buys report-wise plans with coupons and views invoices | PAYMENTS-R02, R03, R11; `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1699` |
| Sub-user under a doctor or clinic | Report credit and plan status are held on the top-level account | PAYMENTS-R06, R07; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1060` |
| Payment provider (Razorpay) | Confirms payments back to the system | PAYMENTS-R05 |

Which exact roles may buy is not stated; see §12 item 7.

## 4. Scope

### In scope
- Listing plans and report-wise plans. (PAYMENTS-R01)
- Price with coupon discount. (PAYMENTS-R02)
- Online payment through Razorpay and its confirmation. (PAYMENTS-R03, R04, R05)
- Adding reports and extending the end date after payment. (PAYMENTS-R06)
- Plan and report-balance status. (PAYMENTS-R07)
- Free trial. (PAYMENTS-R08)
- Recording a purchase reported by the app or website. (PAYMENTS-R09)
- Plan details, payment history and invoices. (PAYMENTS-R10, R11)

### Out of scope
- Recurring auto-debit (ENACH), which is a separate module. (`atreya-docs/modules.yaml`)
- Two backend functions listed as not in use: single-plan lookup and test invoice generation. The Razorpay confirmation callback is also on that list but is used for BR-10; both are questions in §12 item 3. (`atreya-docs/not-in-use.md`)
- The partner-site "Samvit Chakra" checkout: behaviour unknown, see §12 item 6. (PAYMENTS-R12)

## 5. Current business process (as-is)

1. The user opens the plans list. (PAYMENTS-R01)
2. The user may start a free trial, once. (PAYMENTS-R08)
3. To pay, the user may enter a coupon and sees the discounted price. (PAYMENTS-R02)
4. The system creates a Razorpay payment order and the user pays. (PAYMENTS-R03)
5. The system confirms the payment, either when the user's screen reports back (checked with Razorpay) or when Razorpay reports it directly (checked by its security signature only), and adds the reports and extends the end date once. (PAYMENTS-R04, R05, R06)
6. The user sees their plan, report balance, history and invoices. (PAYMENTS-R07, R10, R11)

Sources: `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1619`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:939`

## 6. Business rules

| # | Rule | Source |
|---|---|---|
| 1 | A user can use a free trial only once; a trial lasts 30 days; there is no trial for the free plan. | PAYMENTS-R08; `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:220` |
| 2 | A coupon works only if it is active and, when both a start and end date are set, within them. A discount over 100 percent counts as 100 percent. | PAYMENTS-R02; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1152` |
| 3 | An order needs the number of months, number of reports and an amount of at least 1. | PAYMENTS-R03; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:50` |
| 4 | GST type must be CGST plus SGST, or IGST; GST amounts cannot be negative. | PAYMENTS-R03; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:56` |
| 5 | A payment is accepted only if its security signature is valid and it matches the order. | PAYMENTS-R04, R05; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:353` |
| 6 | Reports for one payment are added only once, even if both confirmations arrive. | PAYMENTS-R05, R06; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1010` |
| 7 | A new purchase extends the current end date if the plan is still running, otherwise starts from today. An unlimited plan stays unlimited. | PAYMENTS-R06; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1067` |
| 8 | The system marks the user as able to take readings, add patients and add appointments only if the plan is not expired and has reports left or is unlimited. | PAYMENTS-R07; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1254`, `Nadi-Tarangini-Frontend:app/Http/Middleware/CheckAuthToken.php:18` |
| 9 | Reports and plan status are held on the top-level account, even when a sub-user pays. | PAYMENTS-R06, R07; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1060` |
| 10 | A purchase reported by the app or website needs a valid plan, month option and currency, and a repeat of the same order is rejected only when it matches the user's first record for that plan. | PAYMENTS-R09; `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:380` |

## 7. Business requirements

| ID | Requirement | Source |
|---|---|---|
| BR-01 | A user can see the active subscription plans and the report-wise plan options. | PAYMENTS-R01; `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:31` |
| BR-02 | A user can see the price of a plan after applying a valid coupon. | PAYMENTS-R02; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1175` |
| BR-03 | A user can pay online for a number of reports and months, including GST details. | PAYMENTS-R03; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:184` |
| BR-04 | The system confirms an online payment, either by checking it with Razorpay or by a signed Razorpay notification, before giving the user the purchase. | PAYMENTS-R04, R05; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:353` |
| BR-05 | After a confirmed payment the system adds the purchased reports and extends the end date, once per payment. | PAYMENTS-R06; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1052` |
| BR-06 | A user can see whether their plan is active, how many reports remain and when it ends, and the system reports whether they can take readings, add patients and add appointments (the website and the reading step enforce this; mobile enforcement is unconfirmed). | PAYMENTS-R07; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1254` |
| BR-07 | A user can start one 30-day free trial and is told by message when it starts. | PAYMENTS-R08; `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:244` |
| BR-08 | A purchase made through the app or website can be recorded against a plan, and may also register the user on the Samvit Chakra learning site if the plan includes it. | PAYMENTS-R09; `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:450` |
| BR-09 | A user can see their current plan, remaining days, payment history, trial details and invoices. | PAYMENTS-R10, R11; `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:129` |
| BR-10 | Payment confirmations from Razorpay must be accepted even when the user's screen never reports back. | PAYMENTS-R05; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:925` |

## 8. Availability by environment

From `atreya-docs/environments.md`: all three environments (dev, staging, production) of the backend, website and app are TO FILL, so availability and whether Razorpay runs in test or live mode are unknown. See §12 item 8. The staging comparison is also waiting for those values. (`atreya-docs/nt/payments/staging-delta.md`)

## 9. Dependencies & external systems

| System (plain name) | Used for | Source |
|---|---|---|
| Razorpay | Online payments and confirmations | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:197` |
| File storage (S3) | Storing invoices | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:679` |
| Email service (ZeptoMail) | Sending invoice emails | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:512` |
| WhatsApp and email messages | Trial-started message | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:274`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:285` |
| Samvit Chakra learning site | Student registration on purchase of a plan that includes it | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:450` |

## 10. Assumptions & constraints

- The app's own Razorpay payment launcher is commented out in the code, so the app's current payment route is unconfirmed (§12 item 4). (`Nadi-Tarangini-App:lib/doctor_dashboard/subscription/utils/launch_payment.dart:9`)
- Language support: seven languages are required; only English files were found in the website. (`references/qa-scope-rules.md`, `Nadi-Tarangini-Frontend:resources/lang/en/auth.php`)
- A hard-coded email-service credential is present in backend code and is recorded as a security question (§12 item 5). The value is [REDACTED]. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:507`)

## 11. Success measures (TO CONFIRM)

- What should the module achieve (for example paid conversions, trial-to-paid rate, failed-payment rate)? Product owner. Not in code.

## 12. Needs confirmation

1. (Product owner) What are the business objectives and success measures for plans and payments? (Source: none)
2. (Product owner) Which of two ways to record a purchase is current: Razorpay-confirmed (BR-03 to BR-05), or app/website-reported (BR-08), which does not check with Razorpay? (PAYMENTS-R09; `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:414`)
3. (Product owner) Are single-plan lookup (open to anyone), test invoice generation and the Razorpay confirmation callback in use? No screen calls them (the callback is called by Razorpay, not a screen). (`atreya-docs/not-in-use.md`)
4. (Developer) How does the mobile app pay today, given its screens and Razorpay launcher are commented out? (PRD §13 Q4 and Q15; `Nadi-Tarangini-App:lib/route/router.dart:768`)
5. (Developer/security) Should the hard-coded email-service credential move to configuration and be replaced? (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:507`)
6. (Product owner) What does the Samvit Chakra checkout bridge do, and who uses it? (PAYMENTS-R12; `Nadi-Tarangini-Frontend:routes/web.php:813`)
7. (Product owner) Which roles may buy a plan or start a trial? No role check was seen in the routes file. (`Ashoka-World-Backend:routes/api.php:1415`)
8. (Owner) Fill environments.md: hosts, refs, and Razorpay test or live mode per environment. (`atreya-docs/environments.md`)
9. (Product owner) Are the 30-day single trial and the plan ids (1 = free, 2 = "already active") the intended policy? (PAYMENTS-R08, R10; `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:236`)
10. (Product owner) Are refunds and GST correctness in scope? Refunds are recognised in the status order but no reversal of reports was seen in the payment controller. (PAYMENTS-R05; `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:979`)
11. (QA) Must payment messages be available in all seven required languages? (`references/qa-scope-rules.md`)

## 13. Document control

| Field | Value |
|---|---|
| Status | Draft |
| Date | 2026-11-03 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend 8dfbb37db7d71a400b3656bd50fbed6173908a24; Nadi-Tarangini-App 0b7deec6de2b0b8b4f05eab4be8c8430523829bf; Nadi-Tarangini-Frontend e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d |
