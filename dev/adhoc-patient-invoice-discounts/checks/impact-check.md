# Checks: adhoc-patient-invoice-discounts

Date: 2026-11-03. Status of impact.md: Draft.

## Mechanical checks

Output of `impact-check.sh` after the doc-checker fixes (second run; the first run also passed, 26 of 26):

```
PASS  impact-facts.json is schema atreya.impact/2
PASS  script facts untouched (facts_sha256)
PASS  analysis merged
PASS  review status Draft (json)
PASS  check-doc.sh passes impact.md
PASS  status Draft (impact.md)
PASS  impact.md counts and overall risk match the JSON
PASS  impact.md §3 lists exactly the JSON's modules
PASS  impact.md §9 lists exactly the JSON's risks
PASS  impact.md §10 lists exactly the JSON's QA scenarios
PASS  impact.md §11 lists exactly the JSON's open questions and assumptions
PASS  impact-report.html counts and overall risk match the JSON
PASS  impact-report.html has exactly the JSON's modules
PASS  impact-report.html has exactly the JSON's risks
PASS  impact-report.html has exactly the JSON's QA scenarios
PASS  impact-report.html has exactly the JSON's open questions
PASS  impact-report.html has exactly the JSON's assumptions
PASS  status Draft (impact-report.html)
PASS  exactly 2 script elements (data + app)
PASS  app script is the template's, unchanged
PASS  stylesheet is the template's, unchanged
PASS  embedded map data is valid JSON
PASS  CSP blocks every external request
PASS  no external URL (src/href/action/url()/@import)
PASS  no injected tags or inline event handlers
PASS  no key-like strings (json, md, html)

impact-check: PASS (/Users/atreyainnovationspvtltd/Mohini/atreya-ai/atreya-docs/dev/adhoc-patient-invoice-discounts)
```

check-doc.sh warnings: none.

## Doc-checker

One pass by the doc-checker agent, in a fresh context, on the first rendered draft. It was interrupted once by a usage limit and resumed. The findings below are the checker's; the "Fix" column was added by the analyst. The doc-checker was not re-run after the fixes.

Checked against commits Ashoka-World-Backend 8dfbb37, Nadi-Tarangini-App 0b7deec, Nadi-Tarangini-Frontend e8a9742.

**Summary: 46 claims · 34 verified · 6 mismatch · 4 not provable · 0 secret risk**

Not checked by the doc-checker (stopped early): the Fee-Info call sites in the report services (GenerateAarogyaDarshika:3827, NadiTaranginiV3:3240, GenerateReportResponseJson:3746, GenerateSwasthyaData:3240), PatientDetailsController:2073-2074 (nt-jiva), `api_repository.dart:1479-1481`, whether MONEY-02 really did not fire, and the indirect-module paths (spot-checked only).

### Mismatch

| # | Claim | What the code shows | Fix |
|---|---|---|---|
| 1 | Saving fees checks only login; any logged-in user could discount another doctor's visit (current, RA-03) | `saveFees` calls `patientDetails($client_id, $doctorId)`, which restricts the patient to the caller's allowed doctor ids (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2529-2533`, `Ashoka-World-Backend:app/Services/PatientDetails.php:15-25`). No role check and the commented-out visit doctor filter are true. | Reworded the statement and RA-03 ("any user allowed to see that doctor's patients, whatever their role"); added both cites; Q8 updated. |
| 2 | Amount owed computed in "at least nine places" | Eight places found; handlePatientLogin subtracts at `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1233`. | Changed to eight; cite changed to `AuthController.php:1233`; action updated. |
| 3 | Only one role-4 path saves fees as 0 | Four role-4 diet-save paths call `patient/saveFees` with no fees or zeros (`Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:124-147`, `:473-496`, `:611-628`, `:674-691`). Re-checked by the analyst: the role-4 conditions are at lines 124 and 473. | Rewritten in the summary, the nadi-flow note, step 2, data consistency, QA-11 and Q7, with all four cites. |
| 4 | saveFees stores 0 for any missing fee field | True only for fee_charged and fee_paid; consultation and therapy fees are kept when missing (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2985-2991`). | Data-consistency text corrected; cite added. |
| 5 | Web dashboard cites `dashboard.blade.php:31,37` | Those lines are inside a Blade comment; the live lines are 127 and 142. | Cite changed to `dashboard.blade.php:127,142`. |
| 6 | Fees forwarded by name from four web paths | Three web methods forward by name; the other call sites send nothing or zeros. | Summary and step 2 reworded ("three web methods and the app ... four role-4 diet-save calls send no fees or zeros"). |

### Not provable

| # | Claim | Why | Fix |
|---|---|---|---|
| 1 | Payment is collected outside the system; fee_paid is the only patient payment record (Verified) | The cite shows only the notification payload; other payment models were not traced. | Split: payload claim stays Verified (`AppointmentController.php:2091-2096`); the outside-collection claim is now Inferred and points to Q5. |
| 2 | "UPI, QR or cash" in step 4 | No source for cash. | "Cash" removed; step 4 evidence lowered to Inferred. |
| 3 | The payment notification is where payment collection starts | The notification is the next-appointment notification sent by saveFees. | appointments why_affected reworded. |
| 4 | RA-02 Critical under FAIL-01 | Payment happens outside the system, so no money movement is in the system. | RA-02 changed to FAIL-02 (High); new open question Q13 (Owner) asks whether FAIL-01 should apply. RA-01 (MONEY-02, Critical) still sets the overall level; its evidence lowered from Verified to Inferred because treating medical_report as a money table is a judgement. |

### Evidence class notes from the checker

- The ashoka-admin note (Inferred, no fee field reads) is correct.
- The enach entry (Not affected) is acceptable.
- Q1-Q12 are fair. Q7 and Q8 were extended as suggested.

### Secret risk

None found in impact.md.

## Doc-checker, second pass (decisions update)

After the user asked Claude to resolve the open questions from the code, 13 open questions were reduced to 7. Code answers were added to §1 as facts, and product calls were added as assumptions A3-A10, each labelled as a decision for the PO to confirm. A narrow doc-checker pass then checked only the new claims.

**Summary: 13 claims · 11 verified · 1 mismatch (wording) · 1 not provable · 0 secret risk**

| Finding | Fix |
|---|---|
| Mismatch: "for College users ... fees are saved as 0". Only the path at `DietController.php:611-628` sends explicit zeros; the path at `:124-147` sends no amounts. | Reworded: some paths send zeros, others send no amounts and the backend stores 0 for missing values. Added the backend citation `PatientDetailsController.php:2959-2960`. |
| Not provable: "no patient payment table". Checked against the model fillable lists only; the migrations and the JSON column `transactions.invoice_data` were not checked. | Kept as Inferred, with the scope stated in the text. Citations moved to the fillable lines (`Transaction.php:12-26`, `PgOrderDetail.php:24-35`, `AshokaPaymentOrder.php:15-29`, `CorporatePayments.php:31-44`). |

Verified: role id 4 = College, id 5 = Receptionist, id 6 = Pharmacy, id 7 = Admin; Assistant and Billing roles exist; no later migration reassigns id 4; feature permissions are stored in `allowed_functions.allowed_features` and the feature list is `master_contents` type `nt_hardcoded_features`; the visit report shows FEE CHARGED, FEE PAID and FEE REMAINING. None of A3-A10 states something the code contradicts. The checker was not re-run after these two fixes. Mechanical checks were re-run: PASS, 0 warnings.
