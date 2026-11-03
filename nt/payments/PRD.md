---
module: "payments"
doc: "PRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Subscriptions & payments (Razorpay): Product Requirements Document

## 1. Overview

The module covers subscription plans, free trials, Razorpay payments, the report balance a paying user receives, invoices and transaction history. (`atreya-docs/_map/_modules/payments/facts.md`)
The backend exposes 16 routes for it, 13 of which are called by the web frontend or the mobile app. (`Ashoka-World-Backend:routes/api.php:1340`, `atreya-docs/_map/_modules/payments/facts.md`)
Three screens belong to it in the mobile app (pricing plan, checkout, invoice), but their class declarations and routes are commented out; see §13 Q15. (`Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/pricing_plan_screen.dart`, `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/checkout_screen.dart`, `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/invoice_screen.dart`)
The web frontend adds a "Samvit Chakra" checkout bridge with three routes of its own. (`Nadi-Tarangini-Frontend:routes/web.php:813`, `Nadi-Tarangini-Frontend:routes/web.php:814`, `Nadi-Tarangini-Frontend:routes/api.php:23`)
The module is marked critical. (`atreya-docs/_map/_modules/payments/facts.md`)
Three backend routes have no caller in this workspace: `POST getSinglePlan`, `POST test-generate-invoice`, `POST webhook/razorpay/nadi`; see §13. (`atreya-docs/_map/_modules/payments/facts.md`)

## 2. Users, roles & permissions

| Part | Who reaches it | Source |
|---|---|---|
| Plan, trial, order, verification, status, history and invoice routes | Callers presenting `auth.token` (middleware `api, auth.token`) | `Ashoka-World-Backend:routes/api.php:1340`, `Ashoka-World-Backend:routes/api.php:960`, `Ashoka-World-Backend:routes/api.php:1415` |
| `POST getSinglePlan` | No middleware (public) | `Ashoka-World-Backend:routes/api.php:729` |
| `POST webhook/razorpay/nadi` | No middleware (public); protected only by a signature check on the request body | `Ashoka-World-Backend:routes/api.php:1934`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:939` |

- Report credit and `planStatus` use the top-level user, even if a sub-user paid or asks; `getUserPlan`, `checkSubscriptionStatus`, `purchasePlan` and `startTrial` use the `user-id` header user directly. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1060`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1228`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:134`)
- The admin dashboard controller calls the order, verification, coupon and invoice routes, so the paid flow on web is reached from the admin dashboard. (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1650`, `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1699`)
- Which roles (doctor, clinic, reception, admin) may buy a plan is not stated in these files: see §13 Q9.

## 3. User journeys

**Web: buy report-wise plan (admin dashboard, `admin.plan_details`)**
1. Plan details are loaded with `POST subscriptions/getReportWisePlans`. (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1619`)
2. A coupon is applied through `POST calculatePlanPrice`, which returns the discounted amount. (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1650`)
3. An order is created with `POST createNtOrder`. (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1699`)
4. After payment, the result is confirmed with `POST verifyTransaction`. (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1727`)
5. The plan status is refreshed with `GET planStatus`. (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1774`)
6. Invoices are listed with `GET payment-invoices`. (`Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1808`)

**Web: legacy subscription checkout and free trial (`subscription.checkout`, `subscription_plans`)**
1. Plans are listed with `GET subscriptions/getPlans`. (`Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:486`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1128`)
2. The user starts a trial with `POST subscriptions/startTrial`, or after payment the frontend saves it with `POST subscriptions/purchasePlan`. (`Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:573`, `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1191`)

**Mobile app**
1. The app loads plans, the user's plan and plan status. (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1838`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1811`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2510`)
2. The user may start a free trial or call `purchasePlan`. (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1847`, `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1871`)
3. Plan status is fetched from the appointment, add-appointment, dashboard and patient screens. (`atreya-docs/_map/_modules/payments/facts.md`)
4. The app's Razorpay launch file contains only commented-out code; see §13 Q4. (`Nadi-Tarangini-App:lib/doctor_dashboard/subscription/utils/launch_payment.dart:9`)

**Samvit Chakra (separate site) checkout**: the frontend serves `GET sc-checkout`, receives `POST sc-checkout/callback` and a Razorpay webhook at `POST api/webhooks/razorpay/sc`. Their behaviour is not described here; see §13 Q7. (`Nadi-Tarangini-Frontend:routes/web.php:813`)

## 4. Functional requirements

### PAYMENTS-R01: List subscription plans
Active plans (`status = 1`) are returned by `GET subscriptions/getPlans`. `POST subscriptions/getReportWisePlans` returns the report-wise plan structure and answers 404 "No subscription plans found" when none exist. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:31`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1062`)
**Acceptance criteria**
- Given an authenticated caller, when `GET subscriptions/getPlans` is called, then rows of `subscriptions` with status 1 are returned. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:31`)
- Given no report-wise plans, when `getReportWisePlans` is called, then 404 "No subscription plans found". (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1062`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:31`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1062`
**Screens**: subscription_plans, admin.plan_details (Web) · **API**: GET subscriptions/getPlans, POST subscriptions/getReportWisePlans

### PAYMENTS-R02: Calculate plan price with a coupon
`POST calculatePlanPrice` finds the price of the given `plan_id` in the active `master_contents` row of type `subscription_plans_report_and_month_wise`. If a `coupon_code` is sent, it must exist with status 1 and, when both dates are set, fall inside `valid_from` and `valid_until`; the discount percent is capped at 100 and the amount is rounded to 2 decimals. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1115`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1152`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1175`)
**Acceptance criteria**
- Given no plan id, then 400 "Plan id is required". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1111`)
- Given a plan id absent from the plan content, then 400 "Invalid Plan ID". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1138`)
- Given an unknown, inactive or out-of-date coupon, then 400 "Invalid coupon code". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1152`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1168`)
- Given a valid coupon, then 200 "Success" with the discounted amount; without a coupon, the plan price. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1186`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1196`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1111`
**Screens**: admin.plan_details (Web) · **API**: POST calculatePlanPrice

### PAYMENTS-R03: Create a Razorpay order
`POST createNtOrder` validates `plan_id_v2`, `month`, `report_count`, `final_amount` (min 1) and optional coupon and GST fields, saves a `transactions` row, then creates a Razorpay order for the final amount in paise and stores the order id and JSON on the row. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:50`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:184`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:221`)
**Acceptance criteria**
- Given missing or non-numeric `month`, `report_count` or `final_amount`, or `final_amount` below 1, then the validation message is returned (codes NT_1882 to NT_1856). (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:64`)
- Given `tax_type` other than `CGST_SGST` or `IGST`, then "Invalid tax type". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:56`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:64`)
- Given a negative IGST amount, then "IGST amount cannot be negative". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:94`)
- Given Razorpay refuses the order, then 400 "Razorpay order creation failed". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:215`)
- Given success, then "Order created successfully". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:231`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:50`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:197`
**Screens**: admin.plan_details (Web) · **API**: POST createNtOrder

### PAYMENTS-R04: Verify a payment after checkout
`POST verifyTransaction` takes `razorpay_payment_id`, `razorpay_order_id` and `razorpay_signature`, finds the transaction, checks the signature, fetches the payment from Razorpay, compares order ids and captures. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:260`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:353`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:367`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:382`)
**Acceptance criteria**
- Given a missing signature or malformed request (any validation failure), then 400 "Invalid transaction verification request"; the per-field message "Signature required" is defined but not returned. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:267`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:274`)
- Given no matching transaction, then 400 "Transaction record not found". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:291`)
- Given the transaction is already verified, then "Transaction already verified" with payment_status CAPTURED. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:328`)
- Given a bad signature, a payment Razorpay cannot return, a different order id or a failed capture, then 400 "Invalid transaction signature", "Unable to fetch transaction from Razorpay", "Order id mismatch" or "Transaction capture failed". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:353`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:367`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:382`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:400`)
On success it stores the payment fields, sets `payment_status = 1` and `payment_date`, and credits the reports (R06) in the same database transaction. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:473`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:484`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:260`
**Screens**: admin.plan_details (Web) · **API**: POST verifyTransaction

### PAYMENTS-R05: Process Razorpay webhooks
`POST webhook/razorpay/nadi` is public and checks an HMAC-SHA256 of the raw body against `X-Razorpay-Signature`. It locks the transaction found by `pay_gate_order_id`, stores the webhook JSON and signature, and moves the payment status forward only in the order CREATED, AUTHORIZED/FAILED, CAPTURED, REFUNDED. On CAPTURED for a not-yet-credited transaction it sets `payment_status = 1` and credits reports (R06). (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:939`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:968`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:979`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1025`)
**Acceptance criteria**
- Given no signature or no configured secret, then 400 "Missing signature". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:939`)
- Given a signature mismatch, then 400 "Invalid webhook signature". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:945`)
- Given no payment entity or order id, then 400 "Malformed payload". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:954`)
- Given an unknown order id, then 404 "Transaction not found". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:973`)
- Given a CAPTURED event for an already credited transaction, then no second credit is made, and 200 "Processed" is returned. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1010`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1030`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:939`
**Screens**: none (server to server) · **API**: POST webhook/razorpay/nadi

### PAYMENTS-R06: Credit reports and extend expiry after a captured payment
For the top-level user, the number of reports bought is added to `user_nadi_capture_type.no_of_reports`, and the expiry becomes the existing expiry (if still in the future) or now, plus the bought months. Expiry null stays unlimited, and a report count of -1 means unlimited and is kept once set. The row is set active. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1052`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1067`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1072`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1078`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1084`)
**Acceptance criteria**
- Given an active capture row expiring in the future, when 3 months and N reports are credited, then expiry moves 3 months past the old expiry and reports increase by N. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1067`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1082`)
- Given no row exists, then one is created active. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1091`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1052`
**Screens**: none · **API**: POST webhook/razorpay/nadi, POST verifyTransaction

### PAYMENTS-R07: Report the plan status
`GET planStatus` returns whether the top-level user has a plan, a report balance and an expiry; `can_take_nadi`, `can_add_patient` and `can_add_appointment` are all true only when the plan is not expired and has reports left (or is unlimited). With no capture row it returns has_plan false and all permissions false. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1228`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1228`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1254`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1259`)
**Acceptance criteria**
- Given no `user-id` header, then 400 "User ID header is missing". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1224`)
- Given an expired plan or 0 reports, then `can_take_nadi` is false. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1254`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1224`
**Screens**: AddAppointmentScreen, AppointmentScreen, DashboardScreen, PatientScreen (App); admin, doctor and lite dashboards (Web) · **API**: GET planStatus

### PAYMENTS-R08: Start a free trial
`POST subscriptions/startTrial` starts a 30-day trial on a paid plan, once per user. It records a `transactions` row with `is_trial = 1`, sets the user's plan and expiry, and sends a WhatsApp template and an email. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:220`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:244`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:274`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:288`)
**Acceptance criteria**
- Given a user who already has a trial row, then 400 "You have already used your trial.". (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:220`)
- Given the user's current plan equals the requested plan, then 400 "You already have an active subscription for this plan.". (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:229`)
- Given no plan id, then 400 "Plan id is required."; given plan id 1, then 400 "No trial for free plan."; given an unknown plan, then 400 "plan not found.". (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:234`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:236`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:241`)
- Given success, then "Trial started successfully." with the trial expiry. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:298`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:220`
**Screens**: DashboardController freeTrial (Web) · **API**: POST subscriptions/startTrial

### PAYMENTS-R09: Purchase a plan (client-reported payment)
`POST subscriptions/purchasePlan` takes `plan_id`, `order_id`, `amount`, `invoice_data`, `currency` and `plan_month`, checks the month against the plan's price list and the currency, and then extends the user's plan expiry by the plan duration (from today, or from the current expiry when renewing the same plan). When the plan's features carry `is_samvitchakra`, the user is also registered on the Samvit Chakra site. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:313`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:380`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:431`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:450`)
**Acceptance criteria**
- Given plan id 1, then 400 "No trial for free plan.". (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:365`)
- Given a `plan_month` not in the price list, then 400 "Invalid plan month". (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:380`)
- Given an unsupported currency, then 400 "Invalid currency. Available currencies: ". (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:389`)
- Given a transaction for this user and plan with the same `order_id` (duplicate order), then 400 "You already have an active subscription for this plan.". (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:410`)
- Given success, then a `transactions` row is saved with `payment_status` true from the client-sent `order_id` and `amount` (no Razorpay call in this method), and "Plan purchased successfully." is returned. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:414`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:560`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:313`
**Screens**: subscription.checkout (Web) · **API**: POST subscriptions/purchasePlan

### PAYMENTS-R10: Show the user's current plan and subscription status
`GET subscriptions/getUserPlan` returns the user's plan (name, price, features, api rules, limits), the latest transaction for it, the expiry and the remaining days; 400 "Plan not found" if the plan is missing. `GET subscriptions/checkSubscriptionStatus` answers "Plan already active" for plan id 2, "Star account" for star accounts, else "No active plan found". `GET subscriptions/getEndPoints` returns all `api_endpoints` rows. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:129`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:144`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1027`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1033`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1039`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:46`)
**Acceptance criteria**
- Given a plan id that matches no plan, then 400 "Plan not found". (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:144`)
- Given the user's stored `plan_id` is 2, then 200 "Plan already active". (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1027`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:129`
**Screens**: DashboardController index, my_account.myaccount, my_account.edit_profile, auth.login (Web) · **API**: GET subscriptions/getUserPlan, GET subscriptions/checkSubscriptionStatus, GET subscriptions/getEndPoints

### PAYMENTS-R11: Transaction history and invoices
`GET subscriptions/getAllTransactions` returns the user's transactions split into `allTransactions` and `trialDetails` (trial rows). `GET payment-invoices` returns the payment invoices of the user, and 400 "User ID header is missing" when the header is absent. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:928`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:923`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:769`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:884`)
**Acceptance criteria**
- Given a user with a trial and a paid purchase, then the trial row is in `trialDetails` and the paid row in `allTransactions`. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:928`)
- Given no `user-id` header on `payment-invoices`, then 400 "User ID header is missing". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:769`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:918`
**Screens**: my_account.myaccount (Web); App InvoicePdfScreen is commented out (Q15) · **API**: GET subscriptions/getAllTransactions, GET payment-invoices

### PAYMENTS-R12: Samvit Chakra payment bridge (web frontend)
The frontend has `GET sc-checkout`, `POST sc-checkout/callback` and `POST api/webhooks/razorpay/sc`, all served by `SamvitPaymentBridgeController`. Their behaviour is not documented here; see §13 Q7. (`Nadi-Tarangini-Frontend:routes/web.php:813`, `Nadi-Tarangini-Frontend:routes/web.php:814`, `Nadi-Tarangini-Frontend:routes/api.php:23`)
**Acceptance criteria**
- To be written after §13 Q7 is answered.
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:813`
**Screens**: samvit_checkout (Web) · **API**: none in this workspace

### PAYMENTS-R13: Test invoice generation (local and staging only)
`POST test-generate-invoice` answers 403 "This API is only available in local or staging environment" outside those environments; the environment check runs before validation, which requires `transaction_id` to exist in `transactions`. No screen calls it. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:522`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:527`)
**Acceptance criteria**
- Given a production environment, then 403 "This API is only available in local or staging environment". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:522`)
- Given generation fails, then 500 "Invoice generation failed". (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:579`)
**Source**: `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:522`
**Screens**: none · **API**: POST test-generate-invoice

## 5. Screens (web / mobile)

| Screen | Platform | File | Route / path | Purpose (provable) |
|---|---|---|---|---|
| PricingPlanScreen (commented out in code, Q15) | App | `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/pricing_plan_screen.dart` | /pricingPlanScreen | Shows plans (file name; calls not traced here) |
| CheckOutScreen (commented out in code, Q15) | App | `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/checkout_screen.dart` | /checkoutScreen | Checkout (file name; calls not traced here) |
| InvoicePdfScreen (commented out in code, Q15) | App | `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/invoice_screen.dart` | /invoiceScreen | Invoice (file name; calls not traced here) |
| sc-checkout | Web | `Nadi-Tarangini-Frontend:routes/web.php:813` | GET sc-checkout | Samvit Chakra checkout bridge |
| Web pages admin.plan_details, subscription.checkout, subscription_plans | Web | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1619` | see §3 | Plan purchase pages named by the fact pack |

## 6. APIs

| Method | Endpoint | Controller | Auth (middleware) | Called by |
|---|---|---|---|---|
| POST | calculatePlanPrice | NtTransactionController@calculatePlanPrice | api, auth.token | Web AdminDashboardController@applyCoupon |
| POST | createNtOrder | NtTransactionController@createNtOrder | api, auth.token | Web AdminDashboardController@createNtOrder |
| POST | verifyTransaction | NtTransactionController@verifyTransaction | api, auth.token | Web AdminDashboardController@verifyTransaction |
| GET | payment-invoices | NtTransactionController@getPaymentInvoices | api, auth.token | Web AdminDashboardController@fetchPaymentInvoices |
| GET | planStatus | NtTransactionController@getPlanStatus | api, auth.token | App getPlanStatus; Web admin, doctor, lite dashboards, CheckAuthToken middleware |
| POST | test-generate-invoice | NtTransactionController@testGenerateInvoice | api, auth.token | no screen in this workspace |
| POST | webhook/razorpay/nadi | NtTransactionController@razorpayWebhook | none | no screen (Razorpay) |
| POST | getSinglePlan | SubscriptionController@getSinglePlanDetails | none | no screen in this workspace |
| GET | subscriptions/getPlans | SubscriptionController@getAllPlans | api, auth.token | App getAllPlanInfo; Web DashboardController |
| POST | subscriptions/getReportWisePlans | SubscriptionController@getReportWisePlans | api, auth.token | Web AdminDashboardController@getPlanDetails |
| GET | subscriptions/getUserPlan | SubscriptionController@getUserPlan | api, auth.token | App getUserPlan; Web DashboardController@index, EditDoctorDetailsController, SubscriptionService |
| GET | subscriptions/getEndPoints | SubscriptionController@getEndPoints | api, auth.token | Web login, DashboardController, SubscriptionService |
| GET | subscriptions/getAllTransactions | SubscriptionController@getAllTransactions | api, auth.token | App getTransactionHistory; Web EditDoctorDetailsController |
| GET | subscriptions/checkSubscriptionStatus | SubscriptionController@checkSubscriptionStatus | api, auth.token | App checkActiveSubscription |
| POST | subscriptions/purchasePlan | SubscriptionController@purchasePlan | api, auth.token | App purchasePlan; Web DashboardController@savePaymentData |
| POST | subscriptions/startTrial | SubscriptionController@startTrial | api, auth.token | App startFreeTrial; Web DashboardController@freeTrial |

Source for every row: `atreya-docs/_map/_modules/payments/facts.md` (Backend routes), routes at `Ashoka-World-Backend:routes/api.php:729`, `:960`, `:1340`.

## 7. Data model

Key fields, from the fact pack's table list (`atreya-docs/_map/_modules/payments/facts.md`). Columns not in migrations: see §13 Q10.

| Table | Key fields |
|---|---|
| `transactions` | user_id, plan_id, plan_id_v2, amount, currency, month, report_count, coupon_code, order_id, pay_gate_order_id, pay_gate_order_json, pay_gate_payment_id, pay_gate_payment_status, pay_gate_response_json, pay_gate_webhook_json, pay_gate_signature, payment_status, payment_date, invoice_data, is_trial, free_expire_date, expire_status, comment |
| `subscriptions` | name, price, duration, features, limits, api_rules, blocked_api_rules, status |
| `nt_coupons` | coupon_code, discount, status, valid_from, valid_until, user_id |
| `user_nadi_capture_type` | user_id, no_of_reports, expiry_date, is_active, is_star_account, free_tier_enrolled, plan_type, nadi_capture_type |
| `user_personal_info` | plan_id, plan_expire_date, (also many non-payment columns) |
| `master_contents` | type, content, is_active (plan content read by `calculatePlanPrice`) |
| `api_endpoints` | name, url, method, is_active, is_public |
| `locality_info` | is_default, timezone |

## 8. Validations & error handling

| API | Field / case | Rule or message | HTTP | Source |
|---|---|---|---|---|
| createNtOrder | plan_id_v2 | required, string | per code | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:49` |
| createNtOrder | month, report_count | required, integer | per code | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:50` |
| createNtOrder | final_amount | required, numeric, min 1 | per code | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:52` |
| createNtOrder | coupon_code, gst_no, billing_state | nullable string, max 50, 50, 100 | per code | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:53` |
| createNtOrder | tax_type | nullable, CGST_SGST or IGST | per code | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:56` |
| createNtOrder | tax and amount fields | nullable numeric, min 0 | per code | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:57` |
| createNtOrder | IGST negative | "IGST amount cannot be negative" | 400 | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:94` |
| createNtOrder | Razorpay fails | "Razorpay order creation failed" | 400 | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:215` |
| verifyTransaction | payment id, order id, signature | required string | per code | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:260` |
| verifyTransaction | bad request, no record, bad signature, fetch failed, order mismatch, capture failed | messages in R04 | 400 | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:274` |
| calculatePlanPrice | no plan, bad plan, bad coupon | messages in R02 | 400 | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1111` |
| purchasePlan | plan_id | required, integer, exists in subscriptions | per code | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:313` |
| purchasePlan | order_id | required | per code | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:314` |
| purchasePlan | amount | required, numeric | per code | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:315` |
| purchasePlan | invoice_data | required, array | per code | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:316` |
| purchasePlan | currency, plan_month | required, string | per code | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:317` |
| purchasePlan | free plan, bad month, bad currency, same plan active | messages in R09 | 400 | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:365` |
| startTrial | trial used, same plan, no id, free plan, no plan | messages in R08 | 400 | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:220` |
| test-generate-invoice | transaction_id | required, integer, exists in transactions | per code | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:527` |
| test-generate-invoice | production | 403 "This API is only available in local or staging environment" | 403 | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:522` |
| webhook/razorpay/nadi | signature, payload, transaction | messages in R05 | 400, 404 | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:939` |
| planStatus, payment-invoices | missing `user-id` header | "User ID header is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1224` |
| getSinglePlan | no id, unknown id | "Plan id is required." / "Invalid Plan ID" | 400 | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:983` |
| most routes | unhandled exception | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1005` |

## 9. Non-functional

- **Security**: user routes sit behind `api, auth.token`; the webhook and `getSinglePlan` have no middleware, and the webhook relies on an HMAC signature. (`Ashoka-World-Backend:routes/api.php:1934`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:945`)
- **Concurrency**: webhook and report credit lock the rows with `lockForUpdate` so two events do not credit twice. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:968`, `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1063`)
- **Secret risk (not copied)**: `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:507` contains an `Authorization` header value written directly in code for the ZeptoMail file upload. The value is [REDACTED]. See §13 Q8. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:507`)
- **Languages**: required list is English, Marathi, Hindi, Czech, German, Spanish, Italian. (`references/qa-scope-rules.md`) Language files found for the web frontend: only `resources/lang/en/*.php` and `en_patient.json`. (`Nadi-Tarangini-Frontend:resources/lang/en/auth.php`) Payment messages are English strings in the backend controllers. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:64`)
- **Performance**: no timeouts or limits are shown in the files read; none stated.

## 10. Environment matrix

Verbatim from `atreya-docs/environments.md`. All values are TO FILL.

### Ashoka-World-Backend
| Env | Ref | Host | Feature flags | Integration mode |
|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL |

### Nadi-Tarangini-App
| Env | Ref | Build flavor | Host | Feature flags | Integration mode |
|---|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |

### Nadi-Tarangini-Frontend
| Env | Ref | Host | Feature flags | Integration mode |
|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL |

Razorpay test or live mode per environment is therefore unknown; see §13 Q6. (`atreya-docs/environments.md`)

## 11. Staging delta

See `atreya-docs/nt/payments/staging-delta.md`. Status: waiting for environments.md for all three repos (staging and production refs are not filled in). No delta was computed. (`atreya-docs/nt/payments/staging-delta.md`)

## 12. External integrations

| System | Where | Source |
|---|---|---|
| Razorpay | Backend order creation and signature/webhook checks | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:197` |
| Razorpay | App launch file (commented out) | `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/utils/launch_payment.dart:9` |
| S3 | Backend invoice storage; App billing tab (file fully commented out) | `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:679`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:552`, `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/billing_tab.dart:278` |
| Samvit Chakra | Backend registers the student on plan purchase | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:450` |
| ZeptoMail | Backend uploads the invoice PDF for email | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:512` |
| WhatsApp template / email | Trial-started message | `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:274` |

## 13. Open questions

1. (PO) Are `POST getSinglePlan`, `POST test-generate-invoice` and `POST webhook/razorpay/nadi` live? No screen in this workspace calls them. (`atreya-docs/_map/_modules/payments/facts.md`)
2. (PO) `getSinglePlan` has no middleware. Is public access intended? (`Ashoka-World-Backend:routes/api.php:729`)
3. (Dev) Two paid flows exist: Razorpay order, verify and webhook (R03 to R05), and `purchasePlan` where the client reports `order_id` and `amount` (R09). Which is current? `purchasePlan` does not call Razorpay in the code read; it records the client-sent order id and amount with `payment_status` true, so payment is not independently checked there. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:414`)
4. (Dev) `launch_payment.dart` is fully commented out. How does the app pay today? (`Nadi-Tarangini-App:lib/doctor_dashboard/subscription/utils/launch_payment.dart:9`)
5. (Dev) A commented-out `creditReportsToUser` call remains at `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:440` while an active one is at `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:484`. Is the commented line dead code to be removed? (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:440`)
6. (Owner) Razorpay test or live mode, hosts and refs per environment: environments.md is TO FILL. (`atreya-docs/environments.md`)
7. (Dev/PO) What do the Samvit Chakra bridge routes do, and who may use them? Glossary meaning of "Samvit Chakra" is TO CONFIRM. (`Nadi-Tarangini-Frontend:routes/web.php:813`, `atreya-docs/glossary.md`)
8. (Dev/Security) A ZeptoMail `Authorization` value is written in code at `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:507` [REDACTED]. Should it move to configuration and be rotated? (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:507`)
9. (PO) Which roles may buy a plan, start a trial, or see invoices (doctor, clinic, reception, admin)? (`Ashoka-World-Backend:routes/api.php:1415`)
10. (Dev) Columns on `transactions`, `subscriptions` and others are listed from models in the fact pack; confirm against migrations. (`atreya-docs/_map/_modules/payments/facts.md`)
11. (PO) Plan id 1 is treated as the free plan and plan id 2 as "already active"; confirm what each plan id means and the expected prices. (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:236`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1027`)
12. (PO) Is the trial length (30 days) and one-trial-per-user rule the intended policy? (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:244`)
13. (PO) Is GST handling (CGST_SGST or IGST by billing state) correct and complete, and are refunds in scope? The webhook ranks REFUNDED but credit reversal was not seen. (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:979`)
14. (QA) Seven languages are required but only English files were found; are payment messages to be translated? (`references/qa-scope-rules.md`)
15. (Dev) The class declarations of PricingPlanScreen, CheckOutScreen and InvoicePdfScreen and their routes in router.dart are commented out. Which screens does the app use for plans, checkout and invoices today? (`Nadi-Tarangini-App:lib/route/router.dart:768`)
16. (Dev) Caller and screen names in R07, R10, R11, §3 mobile step 3 and §6 "Called by" come from the fact pack and were not traced to call sites (App plan-status screens, CheckAuthToken, SubscriptionService, my_account and auth.login pages). Please confirm. (`atreya-docs/_map/_modules/payments/facts.md`)

## 14. Diagrams

None yet: run /atreya:diagram payments.

## 15. Document control

| Field | Value |
|---|---|
| Status | Draft |
| Date | 2026-11-03 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend 8dfbb37db7d71a400b3656bd50fbed6173908a24; Nadi-Tarangini-App 0b7deec6de2b0b8b4f05eab4be8c8430523829bf; Nadi-Tarangini-Frontend e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d |
