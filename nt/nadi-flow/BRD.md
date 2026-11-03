---
module: "nadi-flow"
doc: "BRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Nadi assessment & visit flow: Business Requirements Document

Terms such as Nadi, Prakruti and Vikruti are used as product names; their meanings are TO CONFIRM (`atreya-docs/glossary.md`). Technical evidence is in the Source columns; the detailed requirements are in `atreya-docs/nt/nadi-flow/PRD.md`.

## 1. Purpose & overview

This part of the product lets a doctor run a patient's visit from start to finish: open the visit, record the patient's Prakruti and Vikruti answers, capture Nadi readings (from a device, by keywords, or by marking an image), build diet, lifestyle and yoga plans, prescribe medicines and herbs, add recommendations, and record the fees at the end. It is available on the web application and, for part of the flow, on the mobile app; fee saving is reached from this flow but belongs to another module (NADI-FLOW-R01 to R17; `atreya-docs/_map/_modules/nadi-flow/facts.md`). Source: PRD §1.

## 2. Business objectives

TO CONFIRM. No ticket was given and the code does not state objectives. See §12 question 1.

## 3. Stakeholders & user roles

| Role | How the code shows it | Source |
|---|---|---|
| Doctor / clinician running a visit | The assessment pages need a signed-in user and a selected patient; there is no role check in the routes | NADI-FLOW-R16; `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:62`; `Nadi-Tarangini-Frontend:routes/web.php:497` |
| Patient | A patient is the subject of the visit; reports can be shared with the patient (a "share with patient" setting is read when the fee form is shown) | NADI-FLOW-R16; `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:83` |
| Admin | Admin pages call the "reports allowed for a visit" and "last visit information" functions | NADI-FLOW-R15; `Ashoka-World-Backend:routes/api.php:1205` |

Which roles are permitted is TO CONFIRM (§12 question 2).

## 4. Scope

### In scope
- Opening a visit for a patient (NADI-FLOW-R01).
- Prakruti questions, answers and manual Prakruti choice (R02 to R04).
- Vikruti questions, last-visit information and saving answers (R05, R06).
- Nadi capture: device data upload, manual keywords, marks on a nadi image (R07 to R09).
- Diet and lifestyle, weekly diet plan, yoga plan (R10 to R12).
- Prescription of medicines and herbs, and recommendations (R13, R14).
- List of reports allowed for a visit (R15).
- Fee details at the end of the visit (R16).
- Messages shown when a visit is no longer available (R17).

### Out of scope
- Features that exist in the system but that no screen in the workspace uses are not presented as live: 23 background functions (for example external report capture, report generation on a cloud service, older prescription versions, an older mark-on-image version, public yoga-plan update). They are questions in §12 (PRD §6.4, §13 question 1; `atreya-docs/_map/_modules/nadi-flow/facts.md`).
- Patient list, appointments, fee storage, medicine inventory and language lists, which this flow calls but which belong to other modules (PRD §6.3, §13 question 2).
- The same 23 functions are listed under nadi-flow in `atreya-docs/not-in-use.md` ("no screen calls"; status Needs confirmation).

## 5. Current business process (as-is)

1. The doctor selects a patient and opens a new visit; the system creates a visit number (R01).
2. If the patient's Prakruti has not been recorded, the doctor answers the Prakruti questions or picks a Prakruti manually (R02 to R04).
3. The doctor answers the Vikruti and symptom questions for the visit, optionally looking at the last visit's information (R05, R06).
4. The doctor captures the Nadi: by uploading device data, by choosing keywords, or by marking an image (R07 to R09).
5. The doctor reviews or adjusts diet, lifestyle and yoga plans (R10 to R12).
6. The doctor prescribes medicines or herbs and adds recommendations (R13, R14).
7. The doctor records the fees and may share reports with the patient and set the next appointment (R16).
8. If the visit is no longer available at any step, the web application shows a message and sends the doctor back to the patient list (R17).
The mobile app covers (per the fact pack's caller list, not individually re-verified in App code) Prakruti, parts of the assessment, diet, yoga, prescription, recommendations and report listing; the web application covers the whole flow in two versions (PRD §3).
Source: PRD §3; `Nadi-Tarangini-Frontend:routes/web.php:497`; `Nadi-Tarangini-Frontend:routes/web.php:554`; `Nadi-Tarangini-App:lib/doctor_dashboard/nadi_flow_new/view/fill_prakruti_screen.dart`.

## 6. Business rules

| # | Rule | Source |
|---|---|---|
| 1 | A visit cannot be opened without a user, a patient and an application version; the application version must be a known one. | NADI-FLOW-R01 (v2 route); `Ashoka-World-Backend:routes/api.php:1651`; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1417`; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1501` |
| 2 | A patient's Prakruti can be submitted only once; a second attempt is refused when a Prakruti is already stored (a stored value containing "NA" does not block it; see §12 question 5). | NADI-FLOW-R03, R04; `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:451`; `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:867` |
| 3 | A manual Prakruti must be provided and must be a valid type. | NADI-FLOW-R04; `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:773`; `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:858` |
| 4 | Vikruti answers can be saved only for an existing patient (who must have given Nadi consent) and a valid visit, and are refused when the Nadi was already taken for the visit. | NADI-FLOW-R06; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:319`; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:330`; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:335` |
| 5 | Nadi data uploaded from a device must be a text or zip file. | NADI-FLOW-R07; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3296` |
| 6 | A mark-on-image upload must be a jpeg, png or jpg picture, and must not exceed 5 MB. | NADI-FLOW-R09; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10767`; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10763` |
| 7 | Diet and lifestyle cannot be read for a visit where the Nadi has not been taken. | NADI-FLOW-R10; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1843` |
| 8 | Reading the Vikruti-wise diet (v2 version only), and saving a manual diet, are refused when the Nadi was already taken for that visit. | NADI-FLOW-R10; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2256`; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2971` |
| 9 | A weekly diet plan must contain at least 7 items, and a plan must already exist to be updated. | NADI-FLOW-R11; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12733`; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12759` |
| 10 | Prescription lines must have valid prescription data, a valid client and a valid visit; editing or deleting a line needs its prescription id. | NADI-FLOW-R13; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5600`; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9341` |
| 11 | Recommendations must be valid and of a valid type. | NADI-FLOW-R14; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12314`; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12332` |
| 12 | Fees cannot be saved without a current patient and visit in the web session. | NADI-FLOW-R16; `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:185` |
| 13 | Almost every operation needs the user, patient and visit to be given; otherwise it is refused with a plain message. | NADI-FLOW-R01 to R15; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2733`; `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:31` |
| 14 | Nadi capture is refused when the clinic is not found; the code also has a refusal for a country that is not allowed, but by default every country is allowed (TO CONFIRM). | NADI-FLOW-R07; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3437`; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3385` |

## 7. Business requirements

| ID | Requirement | Source |
|---|---|---|
| BR-01 | A doctor can open a visit for a patient, which creates a visit number used by all later steps. | NADI-FLOW-R01; `Ashoka-World-Backend:routes/api.php:1154` |
| BR-02 | A doctor can see the Prakruti questions and the list of Prakruti types for a patient. | NADI-FLOW-R02; `Ashoka-World-Backend:routes/api.php:1227` |
| BR-03 | A doctor can record a patient's Prakruti by answering the questions or by choosing it manually, once per patient. | NADI-FLOW-R03, R04; `Ashoka-World-Backend:routes/api.php:1232`; `Ashoka-World-Backend:routes/api.php:1238` |
| BR-04 | A doctor can see the Vikruti and symptom questions for a visit, together with the last visit's information. | NADI-FLOW-R05; `Ashoka-World-Backend:routes/api.php:1653`; `Ashoka-World-Backend:routes/api.php:1661` |
| BR-05 | A doctor can save the patient's Vikruti and symptom answers for the visit, including by symptom category. | NADI-FLOW-R06; `Ashoka-World-Backend:routes/api.php:1160` |
| BR-06 | A doctor can capture the Nadi by uploading data from the Nadi device. | NADI-FLOW-R07; `Ashoka-World-Backend:routes/api.php:964` |
| BR-07 | A doctor can record the Nadi by choosing keywords. | NADI-FLOW-R08; `Ashoka-World-Backend:routes/api.php:1157` |
| BR-08 | A doctor can mark points on a Nadi image and save it. | NADI-FLOW-R09; `Ashoka-World-Backend:routes/api.php:1168` |
| BR-09 | A doctor can view and save diet and lifestyle advice for a visit, including advice by Vikruti. | NADI-FLOW-R10; `Ashoka-World-Backend:routes/api.php:1196` |
| BR-10 | A doctor can generate and update a weekly diet plan. | NADI-FLOW-R11; `Ashoka-World-Backend:routes/api.php:1210` |
| BR-11 | A doctor can see and update a yoga plan for a visit. | NADI-FLOW-R12; `Ashoka-World-Backend:routes/api.php:1215`; `Ashoka-World-Backend:routes/api.php:1219` |
| BR-12 | A doctor can prescribe medicines and herbs: add, view, edit and delete prescription lines, and save the prescription. | NADI-FLOW-R13; `Ashoka-World-Backend:routes/api.php:1175`; `Ashoka-World-Backend:routes/api.php:1183`; `Ashoka-World-Backend:routes/api.php:1187`; `Ashoka-World-Backend:routes/api.php:1188`; `Ashoka-World-Backend:routes/api.php:1189` |
| BR-13 | A doctor can save recommendations for a visit. | NADI-FLOW-R14; `Ashoka-World-Backend:routes/api.php:1206` |
| BR-14 | Staff can see which reports are allowed for a given visit. | NADI-FLOW-R15; `Ashoka-World-Backend:routes/api.php:1205` |
| BR-15 | A doctor can record the visit's fees, remarks, next appointment and which reports are shared with the patient. | NADI-FLOW-R16; `Nadi-Tarangini-Frontend:routes/web.php:547` |
| BR-16 | If a visit is no longer available, the web application tells the doctor and returns them to the patient list. | NADI-FLOW-R17; `Nadi-Tarangini-Frontend:resources/views/errors/expiredMedicalId.blade.php:21` |

## 8. Availability by environment

Copied from `atreya-docs/environments.md`: for Backend, Mobile App and Web Frontend, the reference, host, feature flags and integration mode of dev, staging and production are all TO FILL. Availability by environment is therefore unknown. The staging comparison is waiting for these entries (`atreya-docs/nt/nadi-flow/staging-delta.md`).

## 9. Dependencies & external systems

| Dependency | Plain description | Source |
|---|---|---|
| Cloud function service (AWS Lambda / API Gateway) | Used by the backend in the Nadi data handling code; purpose TO CONFIRM | PRD §12; `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3557` |
| Cloud file storage (S3) | Web addresses of stored files appear in the backend and web code; purpose TO CONFIRM | PRD §12; `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:121`; `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:842` |
| Patient, appointment, fee, medicine inventory and language functions of other modules | The visit flow reads and writes through them (for example fee storage) | PRD §6.3; `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:78` |
| Nadi Tarangini device | Data from the device is uploaded; the web app remembers which device is in use | NADI-FLOW-R07; `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1893` |

## 10. Assumptions & constraints

- The web flow requires a signed-in user (`Nadi-Tarangini-Frontend:routes/web.php:497`).
- The flow depends on a current patient and visit being selected; otherwise the doctor is returned to the patient list (R17).
- Two versions of the web assessment exist side by side (`Nadi-Tarangini-Frontend:routes/web.php:497`, `Nadi-Tarangini-Frontend:routes/web.php:554`).
- Required languages are English, Marathi, Hindi, Czech, German, Spanish and Italian, but only English language files exist in the web code (`references/qa-scope-rules.md`; PRD §9).
- Other assumptions are in §12.

## 11. Success measures (TO CONFIRM)

1. How many visits should be completed from opening to fees, and in what time? (product owner)
2. What share of visits should include a Nadi capture, a diet plan and a prescription? (product owner)
3. Which error or abandonment rate is acceptable, for example visits that expire before fees are saved? (product owner)

## 12. Needs confirmation

1. (product owner) What are the business objectives of this flow (section 2)?
2. (product owner) Which roles may run assessments, prescribe and record fees (doctor, assistant, admin)? PRD §13 Q4.
3. (product owner) Which of the 23 background functions are live or legacy? PRD §13 Q1, Q15.
4. (product owner) Which module owns fee saving, patient lists and the App screens used by this flow, and should they be in this BRD? PRD §13 Q2.
5. (product owner) Can a patient's Prakruti be changed after it is submitted (code allows a re-submit when the stored value contains "NA"), and by whom? PRD §13 Q13.
6. (product owner / dev) Which prescription versions (older, current, newer) are the ones to support? PRD §13 Q10.
7. (product owner / QA) Which languages must this flow support and where are the translations? PRD §13 Q7.
8. (product owner / dev) Are the two openly reachable functions (diet test data and public yoga-plan update) intended to be public? PRD §13 Q8.
9. (dev) What do the cloud function and cloud storage uses do in this flow? PRD §13 Q9.
10. (product owner / DevOps) Please fill `environments.md` so availability and staging differences can be stated. PRD §13 Q6.
11. (product owner / dev) What makes a visit "expire", and what causes the "limited access" page? PRD §13 Q11.
12. (product owner / dev) The country restriction on Nadi capture is allowed for all countries by default; is it meant to be used?
13. (product owner) Some refusals (for example "Diet data is required") are reported as "not found" to the app; is this the intended behaviour? PRD §13 Q14.

## 13. Document control

| Field | Value |
|---|---|
| Status | Draft |
| Date | 2026-11-03 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`; Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`; Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d` |
