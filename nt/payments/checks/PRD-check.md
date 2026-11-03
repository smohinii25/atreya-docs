# Doc check: atreya-docs/nt/payments/PRD.md (pass 1, doc-checker agent a1d1d79a98cc67878)
Checked 2026-11-03 against Ashoka-World-Backend 8dfbb37d, Nadi-Tarangini-App 0b7deec6, Nadi-Tarangini-Frontend e8a9742b.
Summary: about 150 claims · about 138 verified · 6 mismatch · 6 not provable · 0 secret risk
(Checker could not read the Samvit Chakra bridge controller: blocked by the guard hook.)

## Mismatch
1. Lines 18, 182-184, 53, 213: the three App screens (PricingPlanScreen, CheckOutScreen, InvoicePdfScreen) have class declarations and router.dart routes (lib/route/router.dart:768-795) commented out; they are dead code, not live screens. Sources: pricing_plan_screen.dart:16, checkout_screen.dart:25, invoice_screen.dart:13.
2. R04 (line 91): any validation failure returns only 400 NT_1865 "Invalid transaction verification request"; "Signature required" is never returned (NtTransactionController.php:270-276, message defined at 267).
3. R09 (line 142): "You already have an active subscription for this plan." is returned when a transaction for this user and plan has the same order_id (duplicate order), not when a subscription is active (SubscriptionController.php:402-412).
4. R10 (line 151): checkSubscriptionStatus takes no plan_id input; it tests the user's stored plan_id against 2 (SubscriptionController.php:1018-1029).
5. Section 8 (line 235): HTTP for "IGST amount cannot be negative" is 400 (NtTransactionController.php:97-105).
6. R03 (line 78): plan_id_v2 is also required|string, "Plan ID is required" (NtTransactionController.php:49, 64).
Minor: section 8 month/report_count cite line 50 (report_count is line 51). R04 "captures" only when Razorpay status is "authorized" (line 386); 400 "Transaction not captured" branch (line 424) omitted.

## Not provable
1. Screen names in R07, R08, R10, R11 Screens lines (fact pack only); InvoicePdfScreen is commented out.
2. Section 3 mobile step 3: screens that fetch plan status (fact pack only).
3. Lines 16, 20, 21: "module is marked critical" (fact pack only).
4. Section 9: only English language files (qa-scope-rules.md not opened).
5. Section 7: columns from model attributes, migrations not checked (already Q10).
6. Line 17: caller counts rest on fact pack (acceptable).

## Secret risk
None in the doc. Hardcoded ZeptoMail Authorization header exists at SubscriptionController.php:507; the doc writes [REDACTED].

## Verified (sample)
Routes and middleware; R02, R03, R04 (success path credits within same DB transaction), R05, R06, R07, R08, R09 (no Razorpay call, payment_status true from client-sent order_id/amount), R10, R11, R13; frontend callers; App api_repository calls; launch_payment.dart fully commented out; external integrations in section 12.
