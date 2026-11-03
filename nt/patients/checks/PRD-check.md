# Doc check: atreya-docs/nt/patients/PRD.md (pass 1, agent a1c4d294e53216cc9)
Summary: about 150 claims · about 140 verified · 4 mismatch · 6 not provable · 0 secret risk
(Saved by the caller from the doc-checker's returned report; condensed.)

## Mismatch
1. Sec 2: delete-patient UPDATE filters only id and role_id '2'; the allowed-doctor-ids, is_active and delete_by_doctor checks are in an earlier SELECT (PatientDetailsController.php:4769-4785). -> Fixed in PRD.
2. R09: deleteReport is a soft delete (delete_by_doctor=1 on medical_report, doctor_id = caller) (PatientDetailsController.php:4980-5007). -> Fixed.
3. R12: "20 other web controllers" is 20 caller methods in 13 controllers. -> Fixed.
4. R02 and Q6: citation text truncated (:740, :723). -> Fixed.

## Not provable
1. "All patient routes carry auth.token": same methods also registered under reception-api with reception.authentication. -> Wording narrowed; added to section 13 (Q11).
2. R01 omits mobile_no/country_code requirement (PatientDetailsController.php:95-101). -> Added to section 13 (Q12).
3. R05 "paged"/dashboard purpose: paging logic not checked. -> Left as stated by route name; not cited (open).
4. R10 file upload / yoga/panchakarma storage behaviour not cited. -> Open.
5. Descriptive purposes for search, pick-lists and association count lack behaviour citations. -> Open.
6. Mobile navigation and "Calls" purposes rest on the fact pack, Dart files not opened. -> Open.

## Secret risk
None found.
