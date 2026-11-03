# Doc check: atreya-docs/nt/nadi-flow/PRD.md (pass 2, doc-checker agent report in substance)

Checked 2026-11-03 against commits Ashoka-World-Backend 8dfbb37, Nadi-Tarangini-App 0b7deec, Nadi-Tarangini-Frontend e8a9742.
Summary: about 120 claims checked · about 112 verified · 2 mismatch · 4 not provable · 0 secret risk

Pass-1 findings (nadiDataAnalysis CheckReportBalance middleware, saveFeesData integer 401, fee-details language filter) confirmed fixed.

## Mismatch
1. §8 row and §13 Q12: the message "Image shouldn" is the full text `"Image shouldn't be greater than 5 MB"`, HTTP 400, code NT_1757 (Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10763). Q12 can be dropped.
2. §9: the eu-only language filter applies in `getReportWiseLanguages` (FeeDetailsController.php:150), not on `GET fee-details`, which passes `getLanguages` unfiltered (line 101).

## Not provable
1. App callers (uploadNadiData, getCurrentVisitInputForYogaPlanner, generateWeeklyDiet, saveRecommendations, ...) not individually confirmed in api_repository.dart (caveat already in §3/§13 Q1).
2. §3 journey step order not shown by cited code.
3. §5 "rendered by their controllers" for fee_details, diet, prescription, vikruti pages lacks view citations.
4. R16 field list cited at FeeDetailsController.php:195; fields are at 192-208, share ids/file at 210-230.

## Secret risk
None.

## Notes
`DietController@saveDietAndLifestyleNew` also calls saveDietAndLifestyle / saveDietAndLifestyleManually (DietController.php:607-609); not in §6.1 callers.
