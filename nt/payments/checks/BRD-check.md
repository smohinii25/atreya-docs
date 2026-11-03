# Doc check: atreya-docs/nt/payments/BRD.md (pass 1, doc-checker agent a92da28b72f0be522)
Summary: about 62 claims · 52 verified · 4 mismatch · 6 not provable · 0 secret risk

## Mismatch
1. Section 5 step 5 and BR-10 rely on Razorpay's callback while section 4 and Needs-confirmation item 3 list the same callback as out of scope / not in use (NtTransactionController.php:923-932; not-in-use.md:71).
2. BR-04: only verifyTransaction calls Razorpay; the webhook path credits after an HMAC check only (NtTransactionController.php:357-358 vs 942-946, 1007-1010).
3. Rule 10 / BR-08: duplicate-order check only compares the first transaction for the user and plan (SubscriptionController.php:402-412).
4. Rule 2: coupon date check runs only when both valid_from and valid_until are set (NtTransactionController.php:1157-1164).

## Not provable
1. Item 4 cites "PAYMENTS-R01 note"; the note is in PRD sections 1, 3, 13 Q4/Q15.
2. Sections 2, 4: objectives/scope not code claims (correctly TO CONFIRM).
3. Item 7: absence claim about roles; reword "not seen in the routes file".
4. Item 10: "no reversal of reports was seen"; reword to "not seen in NtTransactionController".
5. Section 10: English-only language files; cite folder listing.
6. Section 9: email send is at SubscriptionController.php:285 as well as WhatsApp at 274.

## Secret risk
None in the BRD.

## Verified
Rules 1, 3 to 9; BR-01, 02, 05, 06, 07, 09; section 9 dependencies; out of scope; environments all TO FILL; PAYMENTS-R IDs exist in the PRD.
