# Doc check: atreya-docs/nt/nadi-flow/BRD.md (pass 2, doc-checker agent report in substance)

Checked 2026-11-03 against commits backend 8dfbb37, app 0b7deec, frontend e8a9742.
Summary: about 50 claims · 46 verified · 3 mismatch (minor) · 2 not provable · 0 secret risk

Pass-1 items (rules 2, 4, 14, share-with-patient citation, mobile wording) confirmed fixed; rule 8 partly.

## Mismatch
1. Rule 8: the "Nadi already taken" refusal on reading Vikruti-wise diet holds only for the v2 route (api.php:1654, MedicalReportSaveController.php:2256); v1 (api.php:1198) has no such check. Manual-diet save (:2971) correct.
2. BR-12 cites api.php:1175 (save only); add/view/delete/edit routes are at api.php:1176-1189.
3. Rule 1 cites v2 lines (1417, 1501) while BR-01 cites v1 route 1154; name both versions.

## Not provable
1. BR-04 "together with last visit's information": route 1653 only looks up the previous medical id; getLastVisitInformation (api.php:1661) not cited.
2. Mobile coverage (honestly caveated, not verified in App code).

## Secret risk
None.
