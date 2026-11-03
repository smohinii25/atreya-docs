# Fact pack: payments (Subscriptions & payments (Razorpay))

Generated 2026-11-03 by scripts/module-facts.sh. Product nt, critical true. Every line below is from code or a human-owned doc; cite the source given.

Commits: Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`, Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`, Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d`

## Backend routes (16)

### POST calculatePlanPrice
- controller: NtTransactionController@calculatePlanPrice (found) · route: `Ashoka-World-Backend:routes/api.php:1418` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@applyCoupon (admin.plan_details)
- errors: 400 "Plan id is required" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1111`); 400 "Invalid Plan ID" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1138`); 400 "Invalid coupon code" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1152`); 400 "Invalid coupon code" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1168`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1186`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1196`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1205`)

### POST createNtOrder
- controller: NtTransactionController@createNtOrder (found) · route: `Ashoka-World-Backend:routes/api.php:1415` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@createNtOrder (admin.plan_details)
- validation: `month`: required|integer (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:50`); `report_count`: required|integer (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:51`); `final_amount`: required|numeric|min:1 (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:52`); `coupon_code`: nullable|string|max:50 (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:53`); `gst_no`: nullable|string|max:50 (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:54`); `billing_state`: nullable|string|max:100 (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:55`); `tax_type`: nullable|in:CGST_SGST,IGST (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:56`); `taxable_amount`: nullable|numeric|min:0 (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:57`); `gst_rate`: nullable|numeric|min:0 (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:58`); `total_gst`: nullable|numeric|min:0 (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:59`); `cgst_amount`: nullable|numeric|min:0 (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:60`); `sgst_amount`: nullable|numeric|min:0 (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:61`); `igst_amount`: nullable|numeric|min:0 (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:62`)
- errors: ? "IGST amount cannot be negative" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:94`); 400 "Razorpay order creation failed" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:215`); ? "Order created successfully" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:231`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:245`)

### POST getSinglePlan
- controller: SubscriptionController@getSinglePlanDetails (found) · route: `Ashoka-World-Backend:routes/api.php:729` · middleware: none
- called by: no screen in this workspace
- errors: 400 "Plan id is required." (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:983`); 400 "Invalid Plan ID" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:992`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1005`)

### GET payment-invoices
- controller: NtTransactionController@getPaymentInvoices (found) · route: `Ashoka-World-Backend:routes/api.php:1417` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@fetchPaymentInvoices
- errors: 400 "User ID header is missing" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:769`); 200 "Payment invoices fetched successfully" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:884`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:897`)

### GET planStatus
- controller: NtTransactionController@getPlanStatus (found) · route: `Ashoka-World-Backend:routes/api.php:960` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getPlanStatus (AddAppointmentScreen, AppointmentScreen, DashboardScreen, PatientScreen); Nadi-Tarangini-Frontend ?@?; Nadi-Tarangini-Frontend AdminDashboardController@getPlanStatus; Nadi-Tarangini-Frontend DashboardController@getPlanStatus; Nadi-Tarangini-Frontend NtLiteDashboardController@getPlanStatus
- errors: 400 "User ID header is missing" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1224`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1259`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1277`)

### GET subscriptions/checkSubscriptionStatus
- controller: SubscriptionController@checkSubscriptionStatus (found) · route: `Ashoka-World-Backend:routes/api.php:1346` · middleware: api, auth.token
- called by: Nadi-Tarangini-App checkActiveSubscription
- errors: 200 "Plan already active" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1027`); 200 "Star account" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1033`); 200 "No active plan found" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1039`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1046`)

### GET subscriptions/getAllTransactions
- controller: SubscriptionController@getAllTransactions (found) · route: `Ashoka-World-Backend:routes/api.php:1345` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getTransactionHistory; Nadi-Tarangini-Frontend EditDoctorDetailsController@editDoctorDetails (my_account.myaccount); Nadi-Tarangini-Frontend EditDoctorDetailsController@editDoctorProfile (my_account.edit_profile)
- errors: 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:940`)

### GET subscriptions/getEndPoints
- controller: SubscriptionController@getEndPoints (found) · route: `Ashoka-World-Backend:routes/api.php:1341` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend ?@?; Nadi-Tarangini-Frontend DashboardController@freeTrial; Nadi-Tarangini-Frontend DashboardController@savePaymentData (subscription.checkout); Nadi-Tarangini-Frontend DashboardController@switchToDoctor (admin.admin_dashboard, admin.all_report_view, admin.create_user, admin.data_management); Nadi-Tarangini-Frontend loginController@checkLoginCredentials (auth.login); Nadi-Tarangini-Frontend loginController@getUserDetailsOtpBasedLogin (auth.login)
- errors: 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:59`)

### GET subscriptions/getPlans
- controller: SubscriptionController@getAllPlans (found) · route: `Ashoka-World-Backend:routes/api.php:1340` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getAllPlanInfo; Nadi-Tarangini-Frontend DashboardController@checkout (subscription.checkout); Nadi-Tarangini-Frontend DashboardController@freeTrial; Nadi-Tarangini-Frontend DashboardController@getSubscriptionData (subscription_plans); Nadi-Tarangini-Frontend DashboardController@savePaymentData (subscription.checkout)
- errors: 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:41`)

### POST subscriptions/getReportWisePlans
- controller: SubscriptionController@getReportWisePlans (found) · route: `Ashoka-World-Backend:routes/api.php:1348` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@getPlanDetails (admin.plan_details)
- errors: 404 "No subscription plans found" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1062`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:1077`)

### GET subscriptions/getUserPlan
- controller: SubscriptionController@getUserPlan (found) · route: `Ashoka-World-Backend:routes/api.php:1344` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getUserPlan; Nadi-Tarangini-Frontend ?@?; Nadi-Tarangini-Frontend DashboardController@index (doctor_dashboard.dashboard); Nadi-Tarangini-Frontend EditDoctorDetailsController@editDoctorProfile (my_account.edit_profile)
- errors: 400 "Plan not found" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:144`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:169`)

### POST subscriptions/purchasePlan
- controller: SubscriptionController@purchasePlan (found) · route: `Ashoka-World-Backend:routes/api.php:1343` · middleware: api, auth.token
- called by: Nadi-Tarangini-App purchasePlan; Nadi-Tarangini-Frontend DashboardController@savePaymentData (subscription.checkout)
- validation: `plan_id`: required|integer|exists:subscriptions,id (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:313`); `order_id`: required (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:314`); `amount`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:315`); `invoice_data`: required|array (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:316`); `currency`: required|string (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:317`); `plan_month`: required|string (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:318`)
- errors: ? "Plan month is required" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:329`); ? "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:355`); 400 "No trial for free plan." (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:365`); 400 "Invalid plan month" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:380`); 400 "Invalid currency. Available currencies: " (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:389`); 400 "You already have an active subscription for this plan." (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:410`); ? "Plan purchased successfully." (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:560`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:565`)

### POST subscriptions/startTrial
- controller: SubscriptionController@startTrial (found) · route: `Ashoka-World-Backend:routes/api.php:1342` · middleware: api, auth.token
- called by: Nadi-Tarangini-App startFreeTrial; Nadi-Tarangini-Frontend DashboardController@freeTrial
- errors: 400 "You have already used your trial." (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:220`); 400 "You already have an active subscription for this plan." (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:229`); 400 "Plan id is required." (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:234`); 400 "No trial for free plan." (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:236`); 400 "plan not found." (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:241`); ? "Trial started successfully." (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:298`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:303`)

### POST test-generate-invoice
- controller: NtTransactionController@testGenerateInvoice (found) · route: `Ashoka-World-Backend:routes/api.php:1419` · middleware: api, auth.token
- called by: no screen in this workspace
- validation: `transaction_id`: required|integer|exists:transactions,id (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:527`)
- errors: 403 "This API is only available in local or staging environment" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:522`); 500 "Invoice generation failed" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:579`)

### POST verifyTransaction
- controller: NtTransactionController@verifyTransaction (found) · route: `Ashoka-World-Backend:routes/api.php:1416` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend AdminDashboardController@verifyTransaction (admin.plan_details)
- validation: `razorpay_payment_id`: required|string (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:260`); `razorpay_order_id`: required|string (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:261`); `razorpay_signature`: required|string (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:262`)
- errors: ? "Signature required" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:267`); 400 "Invalid transaction verification request" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:274`); 400 "Transaction record not found" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:291`); ? "Transaction already verified" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:328`); 400 "Invalid transaction signature" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:353`); 400 "Unable to fetch transaction from Razorpay" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:367`); 400 "Order id mismatch" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:382`); 400 "Transaction capture failed" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:400`)

### POST webhook/razorpay/nadi
- controller: NtTransactionController@razorpayWebhook (found) · route: `Ashoka-World-Backend:routes/api.php:1934` · middleware: none
- called by: no screen in this workspace
- errors: 400 "Missing signature" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:939`); 400 "Invalid webhook signature" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:945`); 400 "Malformed payload" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:954`); 404 "Transaction not found" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:973`); 200 "Processed" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1030`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:1038`)

## Backend routes no screen calls

`POST getSinglePlan`, `POST test-generate-invoice`, `POST webhook/razorpay/nadi`

## Web routes (3)

- Nadi-Tarangini-Frontend `POST api/webhooks/razorpay/sc` → SamvitPaymentBridgeController@handleRazorpayWebhook · `Nadi-Tarangini-Frontend:routes/api.php:23`
- Nadi-Tarangini-Frontend `GET sc-checkout` → SamvitPaymentBridgeController@showCheckout · `Nadi-Tarangini-Frontend:routes/web.php:813`
- Nadi-Tarangini-Frontend `POST sc-checkout/callback` → SamvitPaymentBridgeController@processPaymentCallback · `Nadi-Tarangini-Frontend:routes/web.php:814`

## Screens (3)

- Nadi-Tarangini-App **CheckOutScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/checkout_screen.dart` · route /checkoutScreen
- Nadi-Tarangini-App **InvoicePdfScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/invoice_screen.dart` · route /invoiceScreen
- Nadi-Tarangini-App **PricingPlanScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/pricing_plan_screen.dart` · route /pricingPlanScreen

## API calls (33)

| Client | Caller | Call | Route | Status | Source |
|---|---|---|---|---|---|
| Nadi-Tarangini-App | checkActiveSubscription | GET `/subscriptions/checkSubscriptionStatus` | GET subscriptions/checkSubscriptionStatus | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1820` |
| Nadi-Tarangini-App | getAllPlanInfo | GET `/subscriptions/getPlans` | GET subscriptions/getPlans | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1838` |
| Nadi-Tarangini-App | getPlanStatus | GET `/planStatus` | GET planStatus | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2510` |
| Nadi-Tarangini-App | getTransactionHistory | GET `/subscriptions/getAllTransactions` | GET subscriptions/getAllTransactions | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1829` |
| Nadi-Tarangini-App | getUserPlan | GET `/subscriptions/getUserPlan` | GET subscriptions/getUserPlan | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1811` |
| Nadi-Tarangini-App | purchasePlan | POST `/subscriptions/purchasePlan` | POST subscriptions/purchasePlan | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1871` |
| Nadi-Tarangini-App | startFreeTrial | POST `/subscriptions/startTrial` | POST subscriptions/startTrial | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1847` |
| Nadi-Tarangini-Frontend | ?@? | GET `/planStatus` | GET planStatus | matched | `Nadi-Tarangini-Frontend:app/Http/Middleware/CheckAuthToken.php:218` |
| Nadi-Tarangini-Frontend | ?@? | GET `/subscriptions/getEndPoints` | GET subscriptions/getEndPoints | matched | `Nadi-Tarangini-Frontend:app/Services/SubscriptionService.php:37` |
| Nadi-Tarangini-Frontend | ?@? | GET `/subscriptions/getUserPlan` | GET subscriptions/getUserPlan | matched | `Nadi-Tarangini-Frontend:app/Services/SubscriptionService.php:25` |
| Nadi-Tarangini-Frontend | AdminDashboardController@applyCoupon | POST `/calculatePlanPrice` | POST calculatePlanPrice | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1650` |
| Nadi-Tarangini-Frontend | AdminDashboardController@createNtOrder | POST `/createNtOrder` | POST createNtOrder | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1699` |
| Nadi-Tarangini-Frontend | AdminDashboardController@fetchPaymentInvoices | GET `/payment-invoices` | GET payment-invoices | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1808` |
| Nadi-Tarangini-Frontend | AdminDashboardController@getPlanDetails | POST `/subscriptions/getReportWisePlans` | POST subscriptions/getReportWisePlans | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1619` |
| Nadi-Tarangini-Frontend | AdminDashboardController@getPlanStatus | GET `/planStatus` | GET planStatus | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1774` |
| Nadi-Tarangini-Frontend | AdminDashboardController@verifyTransaction | POST `/verifyTransaction` | POST verifyTransaction | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1727` |
| Nadi-Tarangini-Frontend | DashboardController@checkout | GET `/subscriptions/getPlans` | GET subscriptions/getPlans | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1128` |
| Nadi-Tarangini-Frontend | DashboardController@freeTrial | GET `/subscriptions/getEndPoints` | GET subscriptions/getEndPoints | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:586` |
| Nadi-Tarangini-Frontend | DashboardController@freeTrial | GET `/subscriptions/getPlans` | GET subscriptions/getPlans | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:593` |
| Nadi-Tarangini-Frontend | DashboardController@freeTrial | POST `/subscriptions/startTrial` | POST subscriptions/startTrial | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:573` |
| Nadi-Tarangini-Frontend | DashboardController@getPlanStatus | GET `/planStatus` | GET planStatus | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:552` |
| Nadi-Tarangini-Frontend | DashboardController@getSubscriptionData | GET `/subscriptions/getPlans` | GET subscriptions/getPlans | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:486` |
| Nadi-Tarangini-Frontend | DashboardController@index | GET `/subscriptions/getUserPlan` | GET subscriptions/getUserPlan | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:123` |
| Nadi-Tarangini-Frontend | DashboardController@savePaymentData | GET `/subscriptions/getEndPoints` | GET subscriptions/getEndPoints | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1210` |
| Nadi-Tarangini-Frontend | DashboardController@savePaymentData | GET `/subscriptions/getPlans` | GET subscriptions/getPlans | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1217` |
| Nadi-Tarangini-Frontend | DashboardController@savePaymentData | POST `/subscriptions/purchasePlan` | POST subscriptions/purchasePlan | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1191` |
| Nadi-Tarangini-Frontend | DashboardController@switchToDoctor | GET `/subscriptions/getEndPoints` | GET subscriptions/getEndPoints | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1545` |
| Nadi-Tarangini-Frontend | EditDoctorDetailsController@editDoctorDetails | GET `/subscriptions/getAllTransactions` | GET subscriptions/getAllTransactions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditDoctorDetailsController.php:123` |
| Nadi-Tarangini-Frontend | EditDoctorDetailsController@editDoctorProfile | GET `/subscriptions/getAllTransactions` | GET subscriptions/getAllTransactions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditDoctorDetailsController.php:332` |
| Nadi-Tarangini-Frontend | EditDoctorDetailsController@editDoctorProfile | GET `/subscriptions/getUserPlan` | GET subscriptions/getUserPlan | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditDoctorDetailsController.php:352` |
| Nadi-Tarangini-Frontend | NtLiteDashboardController@getPlanStatus | GET `/planStatus` | GET planStatus | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteDashboardController.php:549` |
| Nadi-Tarangini-Frontend | loginController@checkLoginCredentials | GET `/subscriptions/getEndPoints` | GET subscriptions/getEndPoints | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:255` |
| Nadi-Tarangini-Frontend | loginController@getUserDetailsOtpBasedLogin | GET `/subscriptions/getEndPoints` | GET subscriptions/getEndPoints | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:635` |

## Tables (8)

- `api_endpoints` (models: ApiEndpoints): create_date, id, is_active, is_public, is_public_reception, method, name, updated_date, url
- `locality_info` (models: LocalityInfo): is_default, timezone
- `master_contents` (models: MasterContents): content, create_date, id, is_active, last_modified_on, month_number, title, type, week_number
- `nt_coupons` (models: NtCoupons): coupon_code, created_at, discount, id, status, updated_at, user_id, valid_from, valid_until
- `subscriptions` (models: Subscription): api_rules, blocked_api_rules, create_date, duration, features, id, limits, name, price, status, updated_at
- `transactions` (models: Transaction): amount, comment, coupon_code, create_date, currency, expire_status, free_expire_date, id, invoice_data, is_trial, month, order_id, pay_gate_order_id, pay_gate_order_json, pay_gate_payment_id, pay_gate_payment_status, pay_gate_response_json, pay_gate_signature, pay_gate_webhook_json, payment_date, payment_status, plan_id, plan_id_v2, report_count, updated_at, user_id
- `user_nadi_capture_type` (models: UserNadiCaptureType): allowed_countries, avoid_device_selection_usb, can_change_capture_type, create_date, expiry_date, free_tier_enrolled, id, is_active, is_star_account, last_modified_on, nadi_capture_type, no_of_reports, plan_type, user_id
- `user_personal_info` (models: UserPersonalInfo): allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken

## External systems

- Razorpay (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:197,198,201`
- Razorpay (Nadi-Tarangini-App): `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/utils/launch_payment.dart:9,24,56`
- S3 (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/NtTransactionController.php:679`, `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:552`
- S3 (Nadi-Tarangini-App): `Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/billing_tab.dart:278`
- Samvit Chakra (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:450,452`
- ZeptoMail (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/SubscriptionController.php:512`

## Environment matrix (verbatim from atreya-docs/environments.md)

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

## Languages

Required: English, Marathi, Hindi, Czech, German, Spanish, Italian (source: references/qa-scope-rules.md).
Language files in code: Nadi-Tarangini-Frontend:resources/lang/en/auth.php, Nadi-Tarangini-Frontend:resources/lang/en/pagination.php, Nadi-Tarangini-Frontend:resources/lang/en/passwords.php, Nadi-Tarangini-Frontend:resources/lang/en/validation.php, Nadi-Tarangini-Frontend:resources/lang/en_patient.json
