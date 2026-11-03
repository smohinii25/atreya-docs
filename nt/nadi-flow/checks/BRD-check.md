# Doc check: atreya-docs/nt/nadi-flow/BRD.md (pass 1, doc-checker agent report in substance)

Checked 2026-11-03 against commits backend 8dfbb37, app 0b7deec, frontend e8a9742.
Summary: about 48 claims · 41 verified · 4 mismatch (3 minor, 1 nuance) · 3 not provable · 0 secret risk

## Mismatch
1. Rule 8: MedicalReportSaveController.php:2256 is in a read (`getVikrutiWiseDietAndLifestyleV2`); only :2971 is a save (manual diet). Rule should say reading Vikruti-wise diet and saving manual diet are refused.
2. Rule 4: :319 (saveVikrutiQuestions) also requires nadi_consent=1, :1043 is a fetch, the save path's own valid-visit check is :330, and :335 returns 409 when the Nadi is already taken.
3. Rule 2: Prakruti refusal applies only when `patient_prakruti` is non-empty and does not contain "NA" (PrakrutiController.php:447, :863); not absolute.
4. Rule 14: the 403 country check exists (:3437) but GeoCheckService allows '*' by default and a comment at :3434 says "always allowed for now"; effectively unreachable by default.

## Not provable
1. Patient row: allowed_share_report is read at FeeDetailsController.php:83, in `index` (fee form), not on save.
2. §5 mobile coverage rests on facts.md callers beyond fill_prakruti_screen.dart.
3. §1 says both clients cover R01-R17 incl. fees; fee saving belongs to another module (Q4).

## Secret risk
None.
