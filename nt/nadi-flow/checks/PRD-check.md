# Doc check: atreya-docs/nt/nadi-flow/PRD.md (pass 1, doc-checker agent report, saved verbatim in substance)

Checked 2026-11-03 against commits Ashoka-World-Backend 8dfbb37, Nadi-Tarangini-App 0b7deec, Nadi-Tarangini-Frontend e8a9742.
Summary: about 120 claims checked (§1-§5, R01-R17, §6.4, §9, §12, and spot checks of §6, §7 and §8) · 111 verified · 3 mismatch · 6 not provable · 0 secret risk

Scope: §1-§7 and §9-§15 read in full. §8 spot-checked (addReportData, getmedicineprescription, nadi/report, nadi/reportInfo, fetchManualNadiKeywords, nadiDataAnalysis, zipFileNadiAnalysis). facts.json not read. Caller names in §6.1 sampled only.

## Mismatch
1. §9 and R16: "Fee-details language list is filtered to ids 1, 2, 3" is conditional: `filterLanguagesBySiteType` returns the full list unless `currentSiteType() === 'eu'` (Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:49-57).
2. §6.1 `nadiDataAnalysis` auth is "api, auth.token", but the route also carries `->middleware(CheckReportBalance::class)` (Ashoka-World-Backend:routes/api.php:964). §2's "51 of 62" ignores this.
3. R16: `saveFeesData` does `return 401;` (integer body, not an HTTP status); it reads `v2_current_patient_id` / `v2_current_medical_id` while `GET fee-details` reads `current_patient_id` / `current_medical_id` (FeeDetailsController.php:172-186, :62-69).
Minor: R01 cites MedicalAssessmentV3Controller.php:271 as source, but the getNewMedicalId call is at line 327.

## Not provable
1. §3: MainAssessmentScreen calls "medical id, current visit info, current visit input for diet, save vikruti" cited only as "callers in §6" (facts.md); cite dart file and line.
2. §6.1/§6.4: the 23 "no screen" rows rest on facts.md; a full no-caller proof needs a search of Frontend controllers and App StringsConst (already in §13 Q1).
3. R16: App `patient/saveFees` URL comes from `StringsConst().saveFeesDetailsUrl` (strings_const.dart:180); api_repository.dart:1481 does not show the route.
4. §12: S3 lines in PrakrutiController.php 121/188/221 and LiveNadiController.php 842-843 are hard-coded S3 URLs, not SDK/API calls.
5. §7: per-table key fields only partly verified (medical_report confirmed; other 20 tables not); label as excerpt from fact pack.
6. R07: device/capture-type function names match; bodies at MedicalAssessmentV3Controller.php:1893-1913 not opened for session writes.

## Secret risk
None.

## Verified (sample)
Route counts and middleware split (51/9/1/1), 53 web rows and their lines, 23 no-screen rows, error messages/codes/lines for R01-R15, R16/R17 fee and expired-view facts, §8 spot checks, §9 language_code and Http::pool lines, App FillPrakruti navigation lines.
