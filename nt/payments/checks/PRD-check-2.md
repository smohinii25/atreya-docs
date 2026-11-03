# Doc check: atreya-docs/nt/payments/PRD.md (pass 2, doc-checker agent aa5cbcf34647ef8fb)
Checked 2026-11-03 against the stamped commits.
Summary: about 150 claims · about 144 verified · 3 mismatch · 4 not provable · 0 secret risk values (2 lines flagged, both already redacted)

## Mismatch
1. R13 (line 171): the 403 comes from the environment check, which fires before validation; a non-existent transaction_id gets 400 with the first validation error (NtTransactionController.php:519-535). Only line 171 was misleading.
2. Line 31: "top-level user" applies only to creditReportsToUser and getPlanStatus (NtTransactionController.php:1060, 1228). getUserPlan, checkSubscriptionStatus, purchasePlan and startTrial use the header user-id (SubscriptionController.php:134, 1019-1031). Line 1057 is a comment.
3. Section 12: billing_tab.dart is fully commented out, including the S3 URL at line 278 (Nadi-Tarangini-App:lib/doctor_dashboard/subscription/view/billing_tab.dart:1, 278).

## Not provable
1. Section 3 mobile step 3: the four App screens calling plan status (fact pack only).
2. R07 Screens line: App and Web dashboards calling plan status.
3. Section 6 "Called by" column: CheckAuthToken, SubscriptionService, EditDoctorDetailsController, login callers (fact pack only).
4. R10/R11 Screens: my_account.myaccount, my_account.edit_profile, auth.login names (fact pack only).

## Secret risk
Lines 259 and 314 describe the hard-coded ZeptoMail Authorization header at SubscriptionController.php:507; value shown as [REDACTED]. Doc is clean.

## Verified
Routes and middleware; R02 to R11, R13 behaviours and messages; frontend and App callers named above; launch_payment.dart and the three screens commented out; environment sections are TO FILL / pointers.
