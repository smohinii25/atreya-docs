# Doc check: atreya-docs/nt/payments/BRD.md (pass 2, doc-checker agent a51b6f52876cffd4d)
Summary: about 75 claims · about 72 verified · 0 hard mismatches · 3 not provable or overstated · 0 secret risk

## Not provable
1. BR-06: "blocked from new readings, patients and appointments" - line 1254 only computes the flags. Web enforcement is in Nadi-Tarangini-Frontend:app/Http/Middleware/CheckAuthToken.php:18-22; readings are blocked by CheckReportBalance on nadiDataAnalysis (api.php:964); app enforcement not shown.
2. Rule 8: same gap as 1.
3. BR-08: "give access to the Samvit Chakra learning site" - code only posts a student registration (SubscriptionController.php:450-470); reword to "register".

## Secret risk
None.

## Verified
Rules 1 to 10, BR-01 to BR-10 (other than above), sections 3, 5, 9, environments, out of scope, PAYMENTS IDs match the PRD.
