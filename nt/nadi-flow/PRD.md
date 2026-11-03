---
module: "nadi-flow"
doc: "PRD"
status: "Draft"
date: "2026-11-03"
reviewer: "TBD"
commits:
  Ashoka-World-Backend: "8dfbb37db7d71a400b3656bd50fbed6173908a24"
  Nadi-Tarangini-App: "0b7deec6de2b0b8b4f05eab4be8c8430523829bf"
  Nadi-Tarangini-Frontend: "e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d"
---
# Nadi assessment & visit flow: Product Requirements Document

Terms Nadi, Prakruti, Vikruti and Pudi are used as names only; their meanings are TO CONFIRM in `atreya-docs/glossary.md`.

## 1. Overview

This module covers the clinical visit flow for a patient: opening a visit (medical id), answering Prakruti and Vikruti questions, capturing Nadi data (device upload, manual keywords, mark-on-image), producing diet, lifestyle and yoga plans, writing prescriptions and recommendations, and saving fees (`atreya-docs/_map/_modules/nadi-flow/facts.md`). It has 62 backend routes in `Ashoka-World-Backend:routes/api.php` (all POST), 53 web routes in `Nadi-Tarangini-Frontend:routes/web.php` and 7 screens (2 mobile, 5 web views) (`atreya-docs/_map/_modules/nadi-flow/facts.md`). Of the 62 backend routes, 23 are not called by any screen in this workspace (see §6 and §13). The web flow exists in two versions: `GET medical-assessment` (`Nadi-Tarangini-Frontend:routes/web.php:497`) and `GET medical-assessment-v3` (`Nadi-Tarangini-Frontend:routes/web.php:554`).

## 2. Users, roles & permissions

- 51 of the 62 backend routes use middleware `api, auth.token` (`nadiDataAnalysis` also carries `CheckReportBalance`, `Ashoka-World-Backend:routes/api.php:964`); 9 routes use `auth.token` only (the `v2/report/*` routes at `Ashoka-World-Backend:routes/api.php:1651`, `Ashoka-World-Backend:routes/api.php:1653`, `Ashoka-World-Backend:routes/api.php:1654`, `Ashoka-World-Backend:routes/api.php:1655`, `Ashoka-World-Backend:routes/api.php:1657`, `Ashoka-World-Backend:routes/api.php:1659`, `Ashoka-World-Backend:routes/api.php:1661`, `Ashoka-World-Backend:routes/api.php:1663`, `Ashoka-World-Backend:routes/api.php:1665`); `POST getDietDataTest` has no middleware (`Ashoka-World-Backend:routes/api.php:728`) and `POST updateYogaPlannerPublic` has only `api` (`Ashoka-World-Backend:routes/api.php:779`). No route in this module is public with a documented purpose (see §13).
- All 53 web routes use `check_auth_token, fetch_notifications, ensure_normal_dashboard_mode` (`Nadi-Tarangini-Frontend:routes/web.php:410`, `Nadi-Tarangini-Frontend:routes/web.php:466`, `Nadi-Tarangini-Frontend:routes/web.php:497`, `Nadi-Tarangini-Frontend:routes/web.php:554`, and all rows in §6).
- Backend handlers read the user id from the request and return 400 "User id is required" or "User id is not provided" when missing (e.g. `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:31`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2733`).
- Role names that may use each part are not in the fact pack: see §13 question 4.

## 3. User journeys

**Web (doctor), version 1** (`GET medical-assessment`, `Nadi-Tarangini-Frontend:routes/web.php:497`):
1. The view `live_nadi.medical_assessment` is rendered by `LiveNadiController@liveNadi`; if no current patient or visit is in session, the "expired medical id" view is shown, which links to `/patientlist` (`Nadi-Tarangini-Frontend:resources/views/errors/expiredMedicalId.blade.php:21`).
2. The page calls the backend for: manual nadi keywords, mark-on-image URL, new-visit questions, current visit info, diet and lifestyle, vikruti-wise diet, pudi ingredients (callers in §6: `LiveNadiController@liveNadi`).
3. The user saves Prakruti (`savePrakrutiData`), Vikruti (`saveVikrutiDataV2`, `saveCategoryWiseVikrutiData`), nadi keywords (`saveKeywordsData`), mark-on-image (`saveMarkOnImageData`), USB nadi data (`saveUsbNadiData`), prescription (`savePrescriptionData*`), diet (`saveDietAndLifestyle*`), then fees (`saveFeesData`) (`Nadi-Tarangini-Frontend:routes/web.php:475`, `Nadi-Tarangini-Frontend:routes/web.php:480`, `Nadi-Tarangini-Frontend:routes/web.php:482`, `Nadi-Tarangini-Frontend:routes/web.php:486`, `Nadi-Tarangini-Frontend:routes/web.php:490`, `Nadi-Tarangini-Frontend:routes/web.php:501`, `Nadi-Tarangini-Frontend:routes/web.php:525`, `Nadi-Tarangini-Frontend:routes/web.php:519`, `Nadi-Tarangini-Frontend:routes/web.php:547`).

**Web (doctor), version 3** (`GET medical-assessment-v3`, `Nadi-Tarangini-Frontend:routes/web.php:554`): `MedicalAssessmentV3Controller@liveNadiV3` renders `medical_assessment.medical_assesment`; the state of the active tab and section is kept by `POST medical-assessment-v3/set-state` (`Nadi-Tarangini-Frontend:routes/web.php:558`); diet and yoga planner are served by the `medical-assessment-v3/diet/*` and `medical-assessment-v3/yoga/*` routes (`Nadi-Tarangini-Frontend:routes/web.php:559-564`); USB nadi upload is `saveUsbNadiDataV3` (`Nadi-Tarangini-Frontend:routes/web.php:567`). Expired visit shows `errors.expiredMedicalIdV3` (`Nadi-Tarangini-Frontend:resources/views/errors/expiredMedicalIdV3.blade.php`).

**Mobile (App)**: `FillPrakrutiScreen` (`/fillPrakrutiScreen`) goes to `/assessmentScreen` (`MainAssessmentScreen`) and `/patientScreen` (`Nadi-Tarangini-App:lib/doctor_dashboard/nadi_flow_new/view/fill_prakruti_screen.dart:205`, `Nadi-Tarangini-App:lib/doctor_dashboard/nadi_flow_new/view/fill_prakruti_screen.dart:103`). `FillPrakrutiScreen` calls the Prakruti types, symptoms list, category-wise questions, last-visit mandatory data, save Prakruti and save manual Prakruti APIs; `MainAssessmentScreen` calls medical id, current visit info, current visit input for diet, and save vikruti (`savePatientDetails`) (callers per the fact pack, `atreya-docs/_map/_modules/nadi-flow/facts.md`; not individually re-verified in App code, see §13 question 1).

## 4. Functional requirements

### NADI-FLOW-R01: Open a visit by creating a medical id
`POST report/getNewMedicalId` creates a medical id for a patient and clinic; `POST v2/report/getNewMedicalId` does so for a patient and application version. Both fail with 400 when user id, patient id or application version id is missing, 404 when patient or application version is not found, and 500 "Failed to create medical id" when creation fails (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:90`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:98`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:102`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:162`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:176`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:249`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1409`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1413`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1417`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1477`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1501`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1580`).
**Acceptance criteria**
- Given `patient_id`, `clinic_id` and `application_version_id` (all required) when v1 is called then a medical id is created; missing clinic id returns 400 "Clinic id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:94`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:105-107`).
- Given an unknown application version id then the API returns 404 "Invalid application version id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:176`).
**Source**: `Ashoka-World-Backend:routes/api.php:1154`, `Ashoka-World-Backend:routes/api.php:1651`, `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:327`
**Screens**: MainAssessmentScreen (App), patient list pages (Web) · **API**: POST report/getNewMedicalId, POST v2/report/getNewMedicalId

### NADI-FLOW-R02: Fetch Prakruti questions and Prakruti types
`POST prakruti/fetchPrakrutiQuestions` returns the questions for a patient (`patient_id` required|numeric); `POST prakruti/fetchPrakrutiQuestionsNtLite` is the NT Lite variant; `POST prakruti/getAllPrakrutiTypes` lists the types (`Ashoka-World-Backend:routes/api.php:1227`, `Ashoka-World-Backend:routes/api.php:1229`, `Ashoka-World-Backend:routes/api.php:1235`).
**Acceptance criteria**
- Given no user id then 400 "User id is required"; no patient id then 400 "Patient id is required"; unknown patient then 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:31`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:34`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:71`).
- Given an unhandled failure then 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:134`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:753`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:38`
**Screens**: FillPrakrutiScreen, PatientScreen, VisitReportListScreen (App); patient list, appointment list, add-member, NT Lite dashboard (Web) · **API**: POST prakruti/fetchPrakrutiQuestions, fetchPrakrutiQuestionsNtLite, getAllPrakrutiTypes

### NADI-FLOW-R03: Save Prakruti answers
`POST prakruti/savePrakrutiQuestions` saves symptom answers for a patient (`Ashoka-World-Backend:routes/api.php:1232`).
**Acceptance criteria**
- Given no symptom then 400 "Symptom is required"; malformed symptom then 400 "Invalid symptom data"; missing patient id then 400 "Patient id is required"; unknown patient then 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:373`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:377`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:385`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:444`).
- Given Prakruti already exists for the patient then 400 "Prakruti already submitted" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:451`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:389`
**Screens**: FillPrakrutiScreen (App); live_nadi.medical_assessment, appointment list, doctor dashboard, add-member (Web, `PrakrutiQuestionsController@savePrakrutiData`) · **API**: POST prakruti/savePrakrutiQuestions

### NADI-FLOW-R04: Save a manually selected Prakruti
`POST prakruti/saveManualPrakruti` saves a Prakruti type chosen by the user (`Ashoka-World-Backend:routes/api.php:1238`).
**Acceptance criteria**
- Given no manual Prakruti then 400 "Manual Prakruti required"; invalid type then 400 "Invalid manual prakruti"; already saved then 400 "Prakruti already submitted"; success returns message "Prakruti saved successfully" (HTTP code not determined by the fact pack) (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:773`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:858`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:867`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:887`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:777`
**Screens**: FillPrakrutiScreen (App); same web pages as R03 · **API**: POST prakruti/saveManualPrakruti

### NADI-FLOW-R05: Fetch Vikruti and visit questions and prior-visit context
`POST report/fetchNewVisitInformation` (v1), `POST v2/report/fetchNewVisitInformation`, `POST v2/report/fetchNewVisitCategoryWiseQuestions`, `POST v2/report/getCurrentVisitInfo`, `POST v2/report/getLastVisitInformation` and `POST v2/report/getLastVisitMandatoryQuesitons` return the question set and the current or last visit data (`Ashoka-World-Backend:routes/api.php:1192`, `Ashoka-World-Backend:routes/api.php:1653`, `Ashoka-World-Backend:routes/api.php:1665`, `Ashoka-World-Backend:routes/api.php:1659`, `Ashoka-World-Backend:routes/api.php:1661`, `Ashoka-World-Backend:routes/api.php:1663`).
**Acceptance criteria**
- Given v1 `patient_id` and `medical_id` are required|numeric; v2 requires `patient_id` and allows `medical_id` nullable (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:984`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:985`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1178`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1179`).
- Given an unknown medical id then 404 "Enter valid medical id"; unknown patient then 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1043`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1027`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1245`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1221`).
- Given no earlier nadi visit then `getLastVisitMandatoryQuesitons` returns 400 "Last nadi visit not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12019`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11246`
**Screens**: MainAssessmentScreen, PatientScreen, FillPrakrutiScreen (App); live_nadi.medical_assessment, medical_assessment.medical_assesment, vikruti page, patient list, admin patient list (Web) · **API**: as listed

### NADI-FLOW-R06: Save Vikruti answers
`POST report/saveVikrutiQuestions` and `POST report/saveCategoryWiseVikrutiQuestions` save symptom answers for a visit (`Ashoka-World-Backend:routes/api.php:1160`, `Ashoka-World-Backend:routes/api.php:1161`).
**Acceptance criteria**
- Given no symptom then 400 "Symptom is required"; invalid symptom data then 400 "Invalid symptom data"; missing medical or patient id then 400; unknown patient then 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:281`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:285`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:293`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:297`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:319`).
- Given the category-wise route and no symptom category id then 400 "Symptom Category id is required"; unknown id then 400 "Invalid Symptom Category id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10987`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10999`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:281`
**Screens**: MainAssessmentScreen (App, `savePatientDetails`, `saveQuestionsTabData`); live_nadi.medical_assessment, appointment list (Web) · **API**: POST report/saveVikrutiQuestions, POST report/saveCategoryWiseVikrutiQuestions

### NADI-FLOW-R07: Upload Nadi device data
`POST nadiDataAnalysis` accepts a nadi data file for a patient visit (`Ashoka-World-Backend:routes/api.php:964`).
**Acceptance criteria**
- Given no file then 400 "File required"; extension other than txt or zip then 400 "Only txt or zip file is allowed"; unknown patient then 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3291`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3296`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3317`).
- Given user id, patient id or medical id is missing then 400 with the matching message (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3267`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3271`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3275`).
The device in use and capture type are kept per session by web routes `updateCurrentNadiTaranginiDevice`, `updateNadiCaptureType` (v1) and `updateCurrentNadiTaranginiDeviceV3`, `updateNadiCaptureTypeV3`, `updateSessionNadiCaptureType` (v3) (`Nadi-Tarangini-Frontend:routes/web.php:742`, `Nadi-Tarangini-Frontend:routes/web.php:499`, `Nadi-Tarangini-Frontend:routes/web.php:569`, `Nadi-Tarangini-Frontend:routes/web.php:571`, `Nadi-Tarangini-Frontend:routes/web.php:556`; `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1893-1913`). `POST zipFileNadiAnalysis` (zip only) has no screen caller (§13).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3267`
**Screens**: LiveNadiScreen1 (App, `uploadNadiData`); live_nadi.medical_assessment, medical_assessment.medical_assesment (Web) · **API**: POST nadiDataAnalysis

### NADI-FLOW-R08: Manual nadi keywords
`POST report/fetchManualNadiKeywords` returns keywords for a visit; `POST report/saveManualNadi` saves them (`Ashoka-World-Backend:routes/api.php:1157`, `Ashoka-World-Backend:routes/api.php:1164`).
**Acceptance criteria**
- Fetch: `patient_id` and `medical_id` required|numeric; no data then 404 "Data not found"; unknown medical id then 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:776`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:777`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:899`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:830`).
- Save: invalid manual nadi then 400 "Data not saved. Invalid manual nadi" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:627`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:562`
**Screens**: App (`fetchManualNadiKeywords`, `saveManualNadiKeywords`); `GET nadi-keywords` via `ManualNadiKeywordsController`, live_nadi.medical_assessment (Web) · **API**: POST report/fetchManualNadiKeywords, POST report/saveManualNadi

### NADI-FLOW-R09: Mark on nadi image
`POST report/fetchMarkOnImageUrl` and `POST report/saveMarkOnImageUrl` read and save marks on the nadi image (`Ashoka-World-Backend:routes/api.php:1171`, `Ashoka-World-Backend:routes/api.php:1168`).
**Acceptance criteria**
- Save: `mark_on_image` must be an image of type jpeg, png or jpg (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10767`); missing ids return 400 with the matching message (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10704`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10708`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10712`).
- Fetch: unknown patient returns 400 "Patient not found", unknown medical id 400 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10863`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10874`).
The older `fetchMarkOnImage` and `saveMarkOnImage` routes have no screen caller (§13).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10704`
**Screens**: App (`fetchMarkOnImage`, `saveMarkOnImage`); `GET nadi-image` and live_nadi.medical_assessment (Web) · **API**: POST report/fetchMarkOnImageUrl, POST report/saveMarkOnImageUrl

### NADI-FLOW-R10: Diet and lifestyle (per visit and Vikruti-wise)
`POST report/getDietAndLifestyle`, `POST v2/report/getVikrutiWiseDietAndLifestyle`, `POST v2/report/getCurrentVisitInputForDiet`, `POST report/saveDietAndLifestyle` and `POST report/saveDietAndLifestyleManually` read and save diet and lifestyle for a visit (`Ashoka-World-Backend:routes/api.php:1196`, `Ashoka-World-Backend:routes/api.php:1654`, `Ashoka-World-Backend:routes/api.php:1657`, `Ashoka-World-Backend:routes/api.php:1195`, `Ashoka-World-Backend:routes/api.php:1199`).
**Acceptance criteria**
- Given nadi was not taken for the medical id then `getDietAndLifestyle` returns 404 "Nadi not taken for this medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1843`).
- Given nadi was already taken then Vikruti-wise and manual save return 400 "Nadi already taken for this visit" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2256`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2971`).
- Given no diet data then `saveDietAndLifestyle` returns 404 "Diet data is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2786`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1781`
**Screens**: App (`getDietData`, `saveDietAndLifestyle`, `saveDietAndLifestyleManually`, `getCurrentVisitInputForDiet`, `savegetVikrutiWiseDiet`); `GET diet-lifestyle`, `GET diet`, live_nadi.medical_assessment (Web) · **API**: as listed

### NADI-FLOW-R11: Weekly diet planner
`POST report/generateWeeklyDiet` generates and `POST report/updateWeeklyDiet` updates a weekly diet (`Ashoka-World-Backend:routes/api.php:1210`, `Ashoka-World-Backend:routes/api.php:1212`); the web V3 equivalents are `medical-assessment-v3/diet/current`, `/generate`, `/update` (`Nadi-Tarangini-Frontend:routes/web.php:559-561`).
**Acceptance criteria**
- Given no input data then generate returns 404 "Input data is required and must be an array" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12444`).
- Given a weekly diet with fewer than 7 items then update returns 400 "Weekly diet must be an array with at least 7 items"; none stored for the medical id then 400 "No weekly diet found for the given medical ID" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12733`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12759`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12370`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12715`
**Screens**: App (`generateWeeklyDiet`, `updateWeeklyDiet`); medical_assessment.medical_assesment (Web V3) · **API**: POST report/generateWeeklyDiet, POST report/updateWeeklyDiet

### NADI-FLOW-R12: Yoga planner
`POST report/getCurrentVisitInputForYogaPlanner` and `POST report/updateYogaPlanner` are called by the App; `POST report/generateYogaPlanner` and `POST updateYogaPlannerPublic` have no screen caller; web V3 uses `medical-assessment-v3/yoga/current` and `/update` (`Ashoka-World-Backend:routes/api.php:1215`, `Ashoka-World-Backend:routes/api.php:1219`, `Ashoka-World-Backend:routes/api.php:1217`, `Ashoka-World-Backend:routes/api.php:779`; `Nadi-Tarangini-Frontend:routes/web.php:563-564`).
**Acceptance criteria**
- Given yoga planner data that is not an array then update returns 400 "Yoga planner data must be an array" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13148`).
- Given missing or invalid ids then 400 or 404 with the matching message (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12804`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13071`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13121`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12804`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13071`
**Screens**: App (`getCurrentVisitInputForYogaPlanner`, `updateYogaPlanner`); medical_assessment.medical_assesment (Web V3) · **API**: as listed

### NADI-FLOW-R13: Prescription (medicines and herbs)
The user adds, edits, deletes and views single prescription lines and saves the visit prescription. Current callers: `report/savePrescriptionDataV2`, `report/saveSinglePrescriptionV2` and `V3`, `report/updateSinglePrescriptionV2` and `V3`, `report/fetchSingleMedicinePrescription`, `report/deleteSinglePrescription`, `report/getPudiIngredient` (`Ashoka-World-Backend:routes/api.php:1175`, `Ashoka-World-Backend:routes/api.php:1183`, `Ashoka-World-Backend:routes/api.php:1184`, `Ashoka-World-Backend:routes/api.php:1187`, `Ashoka-World-Backend:routes/api.php:1185`, `Ashoka-World-Backend:routes/api.php:1189`, `Ashoka-World-Backend:routes/api.php:1188`, `Ashoka-World-Backend:routes/api.php:1202`). V1 routes (`savePrescriptionData`, `saveSinglePrescription`, `updateSinglePrescription`) and the `...NewV3` add/delete/get routes, `getLastPrescription` and `getmedicineprescription` have no screen caller (§13).
**Acceptance criteria**
- Given `doctor_id` missing on `getPudiIngredient` then validation fails (required|numeric) (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2683`).
- Given prescription data that is invalid then save returns 400 "Invalid prescription data"; unknown client id returns 404 "Invalid client id"; unknown medical id returns 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5600`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5582`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5594`).
- Given update or delete without prescription id then 400 "Medicine/herb prescription id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9341`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10267`).
Web helper routes: `getMedicineNamesRespectToType`, `addNewPrescriptionIngredient`, `editMedicine/{id}`, `deleteMedicine/{id}` (`Nadi-Tarangini-Frontend:routes/web.php:523`, `Nadi-Tarangini-Frontend:routes/web.php:535`, `Nadi-Tarangini-Frontend:routes/web.php:539`, `Nadi-Tarangini-Frontend:routes/web.php:537`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5562`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7058`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7930`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9329`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8112`
**Screens**: AddMedicinePrescription, EditMedicinePrescription (App); `GET prescription`, live_nadi.medical_assessment, medical_assessment.medical_assesment, NT Lite patient report (Web) · **API**: as listed

### NADI-FLOW-R14: Save recommendations
`POST report/saveRecommendations` saves recommendations for a visit (`Ashoka-World-Backend:routes/api.php:1206`).
**Acceptance criteria**
- Given no medical id then 400 "Medical id is required"; invalid recommendations then 400 "Invalid recommendations"; invalid type then 400 "Invalid type"; success message "Recommendations saved successfully" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12284`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12314`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12332`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12345`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12284`
**Screens**: App (`saveRecommendations`); medical_assessment.medical_assesment (Web, `saveRecommendationData`, `Nadi-Tarangini-Frontend:routes/web.php:541`) · **API**: POST report/saveRecommendations

### NADI-FLOW-R15: List reports allowed for a visit
`POST report/visitWiseAllowedReports` returns the reports allowed for a visit (`Ashoka-World-Backend:routes/api.php:1205`).
**Acceptance criteria**
- Given no medical id then 400 "Medical id is required"; unknown medical id then 404 "Enter valid medical id"; success message "Success" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12092`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12110`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12255`).
**Source**: `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12088`
**Screens**: ReportScreen (App); admin all-report view, previous visits, NT Lite dashboard (Web) · **API**: POST report/visitWiseAllowedReports

### NADI-FLOW-R16: Fee details at the end of a visit
Web `GET fee-details` shows the fee form after reading patient (`patient/getClientDetails`), doctor (`fetchUserInfo`) and languages (`getLanguages`) from the backend; `POST saveFeesData`, `POST saveFeesDataWithNA` and `POST saveFeesDataAfterDiet` send fees to the backend `POST patient/saveFees` (a route outside the 62 listed for this module); `POST fee-details/report-wise-languages` calls `getReportWiseLanguages` (`Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:60-135`, `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:162-260`, `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:346`). The form posts `fee_charged`, `fee_paid`, `consultation_fees`, `therapy_fees`, `doctor_remarks`, `next_appointment_date`, `yoga_recommendations`, `panchakarma_recommendations` and optional share-report ids and file (`Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:192-230`). `FeeDetailsController@savePrescriptionDataOnSaveFees` also calls `report/savePrescriptionDataV2` (`Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:480`).
**Acceptance criteria**
- Given no current patient or visit in session then `GET fee-details` shows the expired-medical-id view and `saveFeesData` returns the integer 401 as its response body, using the session keys `v2_current_patient_id` and `v2_current_medical_id` (not an HTTP status; `GET fee-details` reads `current_patient_id` and `current_medical_id`) (`Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:68`, `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:185`).
- Given no `report_id` then `getReportWiseLanguages` returns 400 "Report id is required" (`Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:114`).
- Given the backend returns status code `NT_1806` then `saveFeesData` returns -1 (`Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:247`).
**Source**: `Nadi-Tarangini-Frontend:routes/web.php:543`, `Nadi-Tarangini-Frontend:routes/web.php:545`, `Nadi-Tarangini-Frontend:routes/web.php:547`, `Nadi-Tarangini-Frontend:routes/web.php:549`, `Nadi-Tarangini-Frontend:routes/web.php:551`
**Screens**: fee_details (Web); App calls `patient/saveFees` from `saveFeesDetails` (`Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1481`; URL from `saveFeesDetailsUrl` at `Nadi-Tarangini-App:lib/common_files/constants/strings_const.dart:180`) · **API**: POST patient/saveFees (owner module: see §13)

### NADI-FLOW-R17: Expired or limited-access visit pages
When the current patient or visit is not in session, the web flow shows `errors.expiredMedicalId` (v1 pages) or `errors.expiredMedicalIdV3` (v3), each linking to `/patientlist`; `errors.limited_access` is rendered by `VikrutiController@index` (`Nadi-Tarangini-Frontend:resources/views/errors/expiredMedicalId.blade.php:21`, `Nadi-Tarangini-Frontend:resources/views/errors/expiredMedicalIdV3.blade.php`, `Nadi-Tarangini-Frontend:resources/views/errors/limited_access.blade.php`).
**Acceptance criteria**
- Given `GET fee-details` with no patient or visit id in session then the expired view is returned (`Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:68`).
- Given the rule that makes limited_access appear is not in the fact pack then see §13 question 11.
**Source**: `Nadi-Tarangini-Frontend:resources/views/errors/limited_access.blade.php`
**Screens**: errors.expiredMedicalId, errors.expiredMedicalIdV3, errors.limited_access (Web) · **API**: none

## 5. Screens (web / mobile)

| Screen | Platform | File | Route / path | Purpose (provable) |
|---|---|---|---|---|
| FillPrakrutiScreen | App | `Nadi-Tarangini-App:lib/doctor_dashboard/nadi_flow_new/view/fill_prakruti_screen.dart` | /fillPrakrutiScreen | Calls Prakruti types, save Prakruti and manual Prakruti APIs; goes to /assessmentScreen and /patientScreen (`Nadi-Tarangini-App:lib/doctor_dashboard/nadi_flow_new/view/fill_prakruti_screen.dart`) |
| MainAssessmentScreen | App | `Nadi-Tarangini-App:lib/doctor_dashboard/nadi_flow_new/view/main_assessment_screen.dart` | /assessmentScreen | Calls medical id, current visit info, diet input, save vikruti APIs (§6) |
| errors.expiredMedicalId | Web | `Nadi-Tarangini-Frontend:resources/views/errors/expiredMedicalId.blade.php` | GET diet, diet-lifestyle, error, fee-details, medical-assessment, nadi-image, nadi-keywords, prakruti, prescription, vikruti | Shown when the visit is not available; goes to /patientlist (`Nadi-Tarangini-Frontend:resources/views/errors/expiredMedicalId.blade.php:21`) |
| errors.expiredMedicalIdV3 | Web | `Nadi-Tarangini-Frontend:resources/views/errors/expiredMedicalIdV3.blade.php` | GET medical-assessment-v3 | Same for v3; goes to /patientlist |
| errors.limited_access | Web | `Nadi-Tarangini-Frontend:resources/views/errors/limited_access.blade.php` | GET vikruti | Rendered by `VikrutiController@index` |
| live_nadi.medical_assessment | Web | `Nadi-Tarangini-Frontend:resources/views/live_nadi/medical_assessment.blade.php` | GET medical-assessment | Main assessment page (v1), rendered by `LiveNadiController@liveNadi` |
| medical_assessment.medical_assesment | Web | `Nadi-Tarangini-Frontend:resources/views/medical_assessment/medical_assesment.blade.php` | GET medical-assessment-v3 | Main assessment page (v3), rendered by `MedicalAssessmentV3Controller@liveNadiV3` |

Other pages named in the route lists (`diet`, `fee_details`, `prescription`, `vikruti`, `nadi-keywords`, `nadi-image`, `prakruti`) are rendered by their controllers but are not in the screen list of the fact pack. Screens named in the App call list but not in the 7 above (LiveNadiScreen1, AddMedicinePrescription, EditMedicinePrescription, PatientScreen, VisitReportListScreen, ReportScreen) belong to other module folders; see §13 question 2.

## 6. APIs

### 6.1 Backend routes (62), all in `Ashoka-World-Backend:routes/api.php` (route line in the last column)

| Method | Endpoint | Controller | Auth (middleware) | Called by · route source |
|---|---|---|---|---|
| POST | `external-capture/addReportData` | ExternalCaptureController@addReportData | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1409` |
| POST | `generateLambda` | GenerateSwasthyaLambda@generateLambda | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:922` |
| POST | `getDietDataTest` | MedicalReportSaveController@getDietDataStateWise | none | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:728` |
| POST | `getmedicineprescription` | MedicineContorller@getMedicinePrescribed | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:999` |
| POST | `nadi/baselineCalculation` | NadiReportController@baselineCalculation | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1255` |
| POST | `nadi/report` | NadiReportController@nadiReportDefinition | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1256` |
| POST | `nadi/reportInfo` | NadiReportController@nadiReportInfo | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1254` |
| POST | `nadiDataAnalysis` | MedicalReportSaveController@nadiDataAnalysis | api, auth.token, CheckReportBalance (`Ashoka-World-Backend:routes/api.php:964`) | App uploadNadiData; Frontend LiveNadiController@saveUsbNadiData; Frontend MedicalAssessmentV3Controller@saveUsbNadiDataV3 · `Ashoka-World-Backend:routes/api.php:964` |
| POST | `prakruti/fetchPrakrutiQuestions` | PrakrutiController@fetchPrakrutiQuestions | api, auth.token | App getPrakrutiQuestions; Frontend PrakrutiQuestionsController@getPrakrutiDataOnList; Frontend PrakrutiQuestionsController@index · `Ashoka-World-Backend:routes/api.php:1227` |
| POST | `prakruti/fetchPrakrutiQuestionsNtLite` | PrakrutiController@fetchPrakrutiQuestionsNtLite | api, auth.token | Frontend PrakrutiQuestionsController@getPrakrutiDataForNewPatient · `Ashoka-World-Backend:routes/api.php:1229` |
| POST | `prakruti/getAllPrakrutiTypes` | PrakrutiController@getAllPrakrutiTypes | api, auth.token | App getPrakrutiType; Frontend PrakrutiQuestionsController@getPrakrutiDataForNewPatient; Frontend PrakrutiQuestionsController@getPrakrutiDataOnList; Frontend PrakrutiQuestionsController@index · `Ashoka-World-Backend:routes/api.php:1235` |
| POST | `prakruti/saveManualPrakruti` | PrakrutiController@saveManualPrakruti | api, auth.token | App saveManualPrakruti; Frontend PrakrutiQuestionsController@savePrakrutiData · `Ashoka-World-Backend:routes/api.php:1238` |
| POST | `prakruti/savePrakrutiQuestions` | PrakrutiController@savePrakrutiQuestions | api, auth.token | App savePrakrutiQuestions; Frontend PrakrutiQuestionsController@savePrakrutiData · `Ashoka-World-Backend:routes/api.php:1232` |
| POST | `report/addMedicineForPrescriptionNewV3` | MedicalReportSaveController@addMedicineForPrescriptionNewV3 | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1176` |
| POST | `report/deleteMedicineFromPrescriptionNewV3` | MedicalReportSaveController@deleteMedicineFromPrescriptionNewV3 | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1177` |
| POST | `report/deleteSinglePrescription` | MedicalReportSaveController@deleteSinglePrescription | api, auth.token | App deleteSinglePrescription; Frontend PrescriptionController@deleteMedicine · `Ashoka-World-Backend:routes/api.php:1188` |
| POST | `report/fetchManualNadiKeywords` | MedicalReportSaveController@fetchManualNadiKeywords | api, auth.token | App fetchManualNadiKeywords; Frontend LiveNadiController@liveNadi; Frontend ManualNadiKeywordsController@index; Frontend MedicalAssessmentV3Controller@liveNadiV3 · `Ashoka-World-Backend:routes/api.php:1157` |
| POST | `report/fetchMarkOnImage` | MedicalReportSaveController@fetchMarkOnImage | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1170` |
| POST | `report/fetchMarkOnImageUrl` | MedicalReportSaveController@fetchMarkOnImageUrl | api, auth.token | App fetchMarkOnImage; Frontend LiveNadiController@liveNadi; Frontend MarkOnImageController@index; Frontend MedicalAssessmentV3Controller@liveNadiV3 · `Ashoka-World-Backend:routes/api.php:1171` |
| POST | `report/fetchNewVisitInformation` | MedicalReportSaveController@newVisitInfo | api, auth.token | Frontend VikrutiController@index · `Ashoka-World-Backend:routes/api.php:1192` |
| POST | `report/fetchSingleMedicinePrescription` | MedicalReportSaveController@fetchSingleMedicinePrescription | api, auth.token | App fetchSingleMedicinePrescription; Frontend PrescriptionController@editMedicine · `Ashoka-World-Backend:routes/api.php:1189` |
| POST | `report/generateWeeklyDiet` | MedicalReportSaveController@generateWeeklyDiet | api, auth.token | App generateWeeklyDiet · `Ashoka-World-Backend:routes/api.php:1210` |
| POST | `report/generateYogaPlanner` | MedicalReportSaveController@generateYogaPlanner | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1217` |
| POST | `report/getCurrentVisitInputForYogaPlanner` | MedicalReportSaveController@getInputForYogaPlanner | api, auth.token | App getCurrentVisitInputForYogaPlanner · `Ashoka-World-Backend:routes/api.php:1215` |
| POST | `report/getDietAndLifestyle` | MedicalReportSaveController@getDietAndLifestyle | api, auth.token | App getDietData; Frontend DietController@index; Frontend LiveNadiController@liveNadi; Frontend MedicalAssessmentV3Controller@liveNadiV3 · `Ashoka-World-Backend:routes/api.php:1196` |
| POST | `report/getLastPrescription` | MedicalReportSaveController@getLastPrescription | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1179` |
| POST | `report/getMedicineFromPrescriptionNewV3` | MedicalReportSaveController@getMedicineFromPrescriptionNewV3 | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1178` |
| POST | `report/getNewMedicalId` | MedicalReportSaveController@getNewMedicalId | api, auth.token | Frontend MedicalAssessmentV3Controller@ensureMedicalIdLocked; Frontend PatientListController@fetchNewMedicalIdV2; Frontend VikrutiController@index · `Ashoka-World-Backend:routes/api.php:1154` |
| POST | `report/getPudiIngredient` | MedicalReportSaveController@getPudiIngredient | api, auth.token | Frontend LiveNadiController@liveNadi; Frontend MedicalAssessmentV3Controller@liveNadiV3; Frontend PrescriptionController@index · `Ashoka-World-Backend:routes/api.php:1202` |
| POST | `report/getStrotas` | MedicalReportSaveController@getStrotas | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1201` |
| POST | `report/getVikrutiWiseDietAndLifestyle` | MedicalReportSaveController@getVikrutiWiseDietAndLifestyle | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1198` |
| POST | `report/newVisitQues` | MedicalReportSaveController@saveNewVisitQues | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1193` |
| POST | `report/saveCategoryWiseVikrutiQuestions` | MedicalReportSaveController@saveCategoryWiseVikrutiQuestions | api, auth.token | App saveQuestionsTabData; Frontend VikrutiController@saveCategoryWiseVikrutiData · `Ashoka-World-Backend:routes/api.php:1161` |
| POST | `report/saveDietAndLifestyle` | MedicalReportSaveController@saveDietAndLifestyle | api, auth.token | App saveDietAndLifestyle; Frontend DietController@saveDietData · `Ashoka-World-Backend:routes/api.php:1195` |
| POST | `report/saveDietAndLifestyleManually` | MedicalReportSaveController@saveDietAndLifestyleMaually | api, auth.token | App saveDietAndLifestyleManually; Frontend DietController@saveVikrutiWiseDietData · `Ashoka-World-Backend:routes/api.php:1199` |
| POST | `report/saveManualNadi` | MedicalReportSaveController@saveManualNadi | api, auth.token | App saveManualNadiKeywords; Frontend ManualNadiKeywordsController@saveKeywordsData · `Ashoka-World-Backend:routes/api.php:1164` |
| POST | `report/saveMarkOnImage` | MedicalReportSaveController@saveMarkOnImage | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1167` |
| POST | `report/saveMarkOnImageUrl` | MedicalReportSaveController@saveMarkOnImageUrl | api, auth.token | App saveMarkOnImage; Frontend MarkOnImageController@saveMarkOnImageData · `Ashoka-World-Backend:routes/api.php:1168` |
| POST | `report/savePrescriptionData` | MedicalReportSaveController@savePreScription | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1174` |
| POST | `report/savePrescriptionDataV2` | MedicalReportSaveController@savePrescriptionNew | api, auth.token | App savePrescription; Frontend FeeDetailsController@savePrescriptionDataOnSaveFees; Frontend PrescriptionController@savePrescriptionData · `Ashoka-World-Backend:routes/api.php:1175` |
| POST | `report/saveRecommendations` | MedicalReportSaveController@saveRecommendations | api, auth.token | App saveRecommendations; Frontend PrescriptionController@saveRecommendationData · `Ashoka-World-Backend:routes/api.php:1206` |
| POST | `report/saveSinglePrescription` | MedicalReportSaveController@saveSinglePrescription | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1182` |
| POST | `report/saveSinglePrescriptionV2` | MedicalReportSaveController@saveSinglePrescriptionV2 | api, auth.token | App saveSinglePrescription; Frontend PrescriptionController@savePrescriptionDataV2 · `Ashoka-World-Backend:routes/api.php:1183` |
| POST | `report/saveSinglePrescriptionV3` | MedicalReportSaveController@saveSinglePrescriptionV3 | api, auth.token | Frontend PrescriptionController@savePrescriptionDataV3 · `Ashoka-World-Backend:routes/api.php:1184` |
| POST | `report/saveVikrutiQuestions` | MedicalReportSaveController@saveVikrutiQuestions | api, auth.token | App savePatientDetails; Frontend VikrutiController@saveVikrutiData; Frontend VikrutiController@saveVikrutiDataV2 · `Ashoka-World-Backend:routes/api.php:1160` |
| POST | `report/updateSinglePrescription` | MedicalReportSaveController@updateSinglePrescription | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1186` |
| POST | `report/updateSinglePrescriptionV2` | MedicalReportSaveController@updateSinglePrescriptionV2 | api, auth.token | App updateSinglePrescription; Frontend PrescriptionController@updatePrescriptionDataV2 · `Ashoka-World-Backend:routes/api.php:1187` |
| POST | `report/updateSinglePrescriptionV3` | MedicalReportSaveController@updateSinglePrescriptionV3 | api, auth.token | Frontend PrescriptionController@updatePrescriptionDataV3 · `Ashoka-World-Backend:routes/api.php:1185` |
| POST | `report/updateWeeklyDiet` | MedicalReportSaveController@updateWeeklyDiet | api, auth.token | App updateWeeklyDiet · `Ashoka-World-Backend:routes/api.php:1212` |
| POST | `report/updateYogaPlanner` | MedicalReportSaveController@updateYogaPlanner | api, auth.token | App updateYogaPlanner · `Ashoka-World-Backend:routes/api.php:1219` |
| POST | `report/visitWiseAllowedReports` | MedicalReportSaveController@visitWiseAllowedReports | api, auth.token | App deleteReportForDoctor; Frontend AdminDashboardController@viewAllReport; Frontend NtLiteDashboardController@getVisitReports; Frontend NtLiteLiveNadiController@fetchAllowedReportsData; Frontend ReportController@viewAllReportV2 · `Ashoka-World-Backend:routes/api.php:1205` |
| POST | `updateYogaPlannerPublic` | MedicalReportSaveController@updateYogaPlannerPublic | api | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:779` |
| POST | `v2/report/fetchNewVisitCategoryWiseQuestions` | MedicalReportSaveController@fetchNewVisitCategoryWiseQuestions | auth.token | App fetchNewVisitCategoryWiseQuestions; Frontend LiveNadiController@liveNadi; Frontend MedicalAssessmentV3Controller@getAllowedCaseStudySections; Frontend MedicalAssessmentV3Controller@liveNadiV3 · `Ashoka-World-Backend:routes/api.php:1665` |
| POST | `v2/report/fetchNewVisitInformation` | MedicalReportSaveController@newVisitInfoV2 | auth.token | App getSymptomsList; Frontend LiveNadiController@liveNadi; Frontend MedicalAssessmentV3Controller@ensureMedicalIdLocked; Frontend MedicalAssessmentV3Controller@liveNadiV3; Frontend VikrutiController@getVikrutiData · `Ashoka-World-Backend:routes/api.php:1653` |
| POST | `v2/report/getCurrentVisitInfo` | MedicalReportSaveController@getCurrentVisitInfo | auth.token | App fetchCurrentVisitInfo; Frontend DietController@saveDietAndLifestyleNew; Frontend LiveNadiController@liveNadi; Frontend MedicalAssessmentV3Controller@liveNadiV3; Frontend NtLiteLiveNadiController@fetchCurrentVisitInfo; Frontend PreviousVisitsController@resumeVisit · `Ashoka-World-Backend:routes/api.php:1659` |
| POST | `v2/report/getCurrentVisitInputForDiet` | MedicalReportSaveController@getCurrentVisitInputForDiet | auth.token | App getCurrentVisitInputForDiet; Frontend MedicalAssessmentV3Controller@liveNadiV3 · `Ashoka-World-Backend:routes/api.php:1657` |
| POST | `v2/report/getLastVisitInformation` | MedicalReportSaveController@getLastVisitInformation | auth.token | App getLastVisitInformation; Frontend AdminDashboardController@fetchUserLastVisitInformation; Frontend PatientListController@getLastVisitInformation · `Ashoka-World-Backend:routes/api.php:1661` |
| POST | `v2/report/getLastVisitMandatoryQuesitons` | MedicalReportSaveController@getLastVisitMandatoryQuesitons | auth.token | App getLastVisitMendaotryData; Frontend PatientListController@getLastVisitQuestions · `Ashoka-World-Backend:routes/api.php:1663` |
| POST | `v2/report/getNewMedicalId` | MedicalReportSaveController@getNewMedicalIdV2 | auth.token | App getMedicalId; Frontend PatientListController@fetchNewMedicalIdV2NtLite · `Ashoka-World-Backend:routes/api.php:1651` |
| POST | `v2/report/getVikrutiWiseDietAndLifestyle` | MedicalReportSaveController@getVikrutiWiseDietAndLifestyleV2 | auth.token | App savegetVikrutiWiseDiet; Frontend DietController@getVikrutiWiseDietV2; Frontend LiveNadiController@liveNadi; Frontend MedicalAssessmentV3Controller@liveNadiV3 · `Ashoka-World-Backend:routes/api.php:1654` |
| POST | `v2/report/saveDietAndLifestyleManually` | MedicalReportSaveController@saveDietAndLifestyleMauallyV2 | auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:1655` |
| POST | `zipFileNadiAnalysis` | MedicalReportSaveController@zipFileNadiAnalysis | api, auth.token | no screen in this workspace · `Ashoka-World-Backend:routes/api.php:966` |

### 6.2 Web routes (53), all in `Nadi-Tarangini-Frontend:routes/web.php`

| Method | Endpoint | Controller | Auth (middleware) | Source |
|---|---|---|---|---|
| POST | `addNewPrescriptionIngredient` | PrescriptionController@addNewPrescriptionIngredient | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:535` |
| DELETE | `deleteMedicine/{medicalPrescriptionId}` | PrescriptionController@deleteMedicine | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:537` |
| GET | `diet` | DietController@skipDiet | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:510` |
| GET | `diet-lifestyle` | DietController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:508` |
| POST | `editMedicine/{medicalPrescriptionId}` | PrescriptionController@editMedicine | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:539` |
| GET | `fee-details` | FeeDetailsController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:543` |
| POST | `fee-details/report-wise-languages` | FeeDetailsController@getReportWiseLanguages | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:545` |
| POST | `fetchMarkOnImageData` | MarkOnImageController@fetchMarkOnImageData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:492` |
| POST | `getManualNadiQuestions` | LiveNadiController@getManualNadiQuestions | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:412` |
| POST | `getMedicineNamesRespectToType` | PrescriptionController@getMedicineNamesRespectToType | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:523` |
| POST | `getPrakrutiData` | PrakrutiQuestionsController@getPrakrutiDataOnList | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:468` |
| POST | `getPrakrutiDataForNewPatient` | PrakrutiQuestionsController@getPrakrutiDataForNewPatient | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:469` |
| POST | `getVikrutiData` | VikrutiController@getVikrutiData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:410` |
| POST | `getVikrutiWiseDiet` | DietController@getVikrutiWiseDietV2 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:513` |
| GET | `medical-assessment` | LiveNadiController@liveNadi | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:497` |
| GET | `medical-assessment-v3` | MedicalAssessmentV3Controller@liveNadiV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:554` |
| POST | `medical-assessment-v3/diet/current` | MedicalAssessmentV3Controller@getCurrentVisitInputForDietV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:559` |
| POST | `medical-assessment-v3/diet/generate` | MedicalAssessmentV3Controller@generateWeeklyDietV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:560` |
| POST | `medical-assessment-v3/diet/update` | MedicalAssessmentV3Controller@updateWeeklyDietV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:561` |
| POST | `medical-assessment-v3/set-state` | MedicalAssessmentV3Controller@setMedicalAssessmentV3State | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:558` |
| POST | `medical-assessment-v3/yoga/current` | MedicalAssessmentV3Controller@getCurrentVisitInputForYogaV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:563` |
| POST | `medical-assessment-v3/yoga/update` | MedicalAssessmentV3Controller@updateWeeklyYogaV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:564` |
| GET | `nadi-image` | MarkOnImageController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:488` |
| GET | `nadi-keywords` | ManualNadiKeywordsController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:484` |
| GET | `prakruti` | PrakrutiQuestionsController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:466` |
| GET | `prescription` | PrescriptionController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:521` |
| POST | `previousVisitsSymptomDetails` | VikrutiController@getSymptomHistory | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:414` |
| POST | `saveCategoryWiseVikrutiData` | VikrutiController@saveCategoryWiseVikrutiData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:482` |
| POST | `saveDietAndLifestyle` | DietController@saveDietData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:519` |
| POST | `saveDietAndLifestyleNew` | DietController@saveDietAndLifestyleNew | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:517` |
| POST | `saveDummyUsbNadiData` | LiveNadiController@saveDummyUsbNadiData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:502` |
| POST | `saveFeesData` | FeeDetailsController@saveFeesData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:547` |
| POST | `saveFeesDataAfterDiet` | DietController@saveFeesDataAfterDiet | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:551` |
| POST | `saveFeesDataWithNA` | FeeDetailsController@saveFeesDataWithNA | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:549` |
| POST | `saveKeywordsData` | ManualNadiKeywordsController@saveKeywordsData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:486` |
| POST | `saveMarkOnImageData` | MarkOnImageController@saveMarkOnImageData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:490` |
| POST | `savePrakrutiData` | PrakrutiQuestionsController@savePrakrutiData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:475` |
| POST | `savePrescriptionData` | PrescriptionController@savePrescriptionData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:525` |
| POST | `savePrescriptionDataV2` | PrescriptionController@savePrescriptionDataV2 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:527` |
| POST | `savePrescriptionDataV3` | PrescriptionController@savePrescriptionDataV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:529` |
| POST | `saveRecommendationData` | PrescriptionController@saveRecommendationData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:541` |
| POST | `saveUsbNadiData` | LiveNadiController@saveUsbNadiData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:501` |
| POST | `saveUsbNadiDataV3` | MedicalAssessmentV3Controller@saveUsbNadiDataV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:567` |
| POST | `saveVikrutiDataV2` | VikrutiController@saveVikrutiDataV2 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:480` |
| POST | `saveVirutiWiseDietAndLifestyle` | DietController@saveVikrutiWiseDietData | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:515` |
| POST | `updateCurrentNadiTaranginiDevice` | LiveNadiController@updateCurrentNadiTaranginiDevice | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:742` |
| POST | `updateCurrentNadiTaranginiDeviceV3` | MedicalAssessmentV3Controller@updateCurrentNadiTaranginiDeviceV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:569` |
| POST | `updateNadiCaptureType` | LiveNadiController@updateNadiCaptureType | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:499` |
| POST | `updateNadiCaptureTypeV3` | MedicalAssessmentV3Controller@updateNadiCaptureTypeV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:571` |
| POST | `updatePrescriptionDataV2` | PrescriptionController@updatePrescriptionDataV2 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:531` |
| POST | `updatePrescriptionDataV3` | PrescriptionController@updatePrescriptionDataV3 | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:533` |
| POST | `updateSessionNadiCaptureType` | MedicalAssessmentV3Controller@updateSessionNadiCaptureType | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:556` |
| GET | `vikruti` | VikrutiController@index | check_auth_token, fetch_notifications, ensure_normal_dashboard_mode | `Nadi-Tarangini-Frontend:routes/web.php:477` |

### 6.3 Backend routes called by this module's screens but not part of its 62

The fact pack lists these calls from module screens to routes owned by other modules; they are named here only so callers are traceable: `patient/saveFees` (7 calls), `patient/getClientDetails` (6), `infinitePatientList` (6), `medicalInventory/*` (getMedicineWithComsume, getMedicineTiming, prescriptionInfo, fetchPreviousPrescriptions, fetchLastVisitPrescriptions, getAllQuantity, getAllMedicine, getAllIngredient, getAllPudi, getMedicineNamesRespectToType, getAllSupplimentMedicineTypes, addNewPrescriptionIngredient), `getLanguages`, `fetchUserInfo`, `appointment/dateWiseAppointment`, `getReportWiseLanguages`, `getNtHelpVideos`, `getLinkDevice`, `patient/previousVisitsDetails`, `getAllCountries`, `arogyaDarshika` (`atreya-docs/_map/_modules/nadi-flow/facts.md`, "API calls" table, e.g. `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1481`, `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:78`).

### 6.4 Routes with no screen caller (23)

`external-capture/addReportData`, `generateLambda`, `getDietDataTest`, `getmedicineprescription`, `nadi/baselineCalculation`, `nadi/report`, `nadi/reportInfo`, `report/addMedicineForPrescriptionNewV3`, `report/deleteMedicineFromPrescriptionNewV3`, `report/fetchMarkOnImage`, `report/generateYogaPlanner`, `report/getLastPrescription`, `report/getMedicineFromPrescriptionNewV3`, `report/getStrotas`, `report/getVikrutiWiseDietAndLifestyle`, `report/newVisitQues`, `report/saveMarkOnImage`, `report/savePrescriptionData`, `report/saveSinglePrescription`, `report/updateSinglePrescription`, `updateYogaPlannerPublic`, `v2/report/saveDietAndLifestyleManually`, `zipFileNadiAnalysis` (all in the table of 6.1; `atreya-docs/_map/_modules/nadi-flow/facts.md` "Backend routes no screen calls"). Not described as live features; see §13 question 1.

## 7. Data model

Excerpt of key fields from migrations, per the fact pack (not a full schema) (`atreya-docs/_map/_modules/nadi-flow/facts.md`, "Tables"; migrations in `Ashoka-World-Backend:database/migrations`). Tables whose columns are not in migrations are listed in §13 question 3.

| Table (model) | Key fields from migrations |
|---|---|
| `all_country_names` (AllCountryNames) | country_code, postal_code_lengths, postal_code_type |
| `calendar_events` (CalendarEvent) | clinic_id, consultation_type, reception_id |
| `doctor_medicine_inventory` (DoctorMedicineInventory) | is_active |
| `locality_info` (LocalityInfo) | is_default, timezone |
| `major_symptom_data` (MajorSymptomData) | gender, symptom_category_tag |
| `medical_report` (MedicalReport) | city, country, external_visit_id, field_id_1, ip_address, mark_on_image_url, panchakarma_recom, reception_id, recommendations, state, try_count, user_nadi_capture_type, yoga_recom |
| `medical_report_diet` (MedicalReportDiet) | create_date, diet, doctor_id, id, is_active, last_modified_on, medical_id, patient_id, vikruti_type |
| `medical_report_prescription` (MedicalReportPrescription) | is_active, other_details, total_quantity |
| `medical_report_symptom_details_1` (MedicalReportSymptomDetail) | symptom_value |
| `medicine_company` (MedicineCompany) | is_active |
| `medicine_names` (MedicineNames) | create_date, created_by, id, is_active, last_modified_on, medicine_name, medicine_type |
| `medicine_timing` (MedicineTiming) | create_date, id, is_active, last_modified_on, order_by, timing_label |
| `medicine_type` (MedicineType) | is_active, type |
| `medicine_with_consume` (MedicineWithConsume) | consume_label, create_date, created_by, id, is_active, last_modified_on |
| `multichoice_options` (MultichoiceOptions) | lang_kannda |
| `nadi_average_pulse_data` (NadiAveragePulseData) | lang_kannada |
| `other_report_data` (OtherReportData) | create_date, id, is_active, last_modified_on, medical_id, report_data, sub_title, title |
| `pg_device_list` (PgDeviceList) | created_by, device_type, is_linkable, is_usable, serial_no, status, track_status |
| `resource_name_master` (ResourceNameMaster) | endpoint, is_default, no_of_pages, order_by, title |
| `symptom_category` (SymptomCategory) | is_active |
| `symptoms` (Symptoms) | is_active |
| `user_personal_info` (UserPersonalInfo) | allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken |
| `user_report` (UserReport) | symptom_prediction |

Tables with no columns found in migrations: `all_prakruti_types`, `doctor_multichoice_options`, `ingredients_list`, `languages`, `medical_report_image_markers`, `multichoice_field_list`, `nadi_report`, `nt_application_version`, `patient_prakruti`, `pg_device_mapping`, `prakruti_wise_diet`, `project_variables`, `symptoms_dropdown_item`, `user_selected_countries`, `yoga_report_data`.

## 8. Validations & error handling

Rows are taken from the fact pack: validation rules (`API | field | rule`, HTTP n/a) and error responses found in controllers (`API | error case | message | HTTP | source`). "not determined" means the fact pack could not read the HTTP code (see §13 question 5). Duplicate messages for the same API and HTTP code are shown once.

| API | Field / case | Rule or message | HTTP | Source |
|---|---|---|---|---|
| `external-capture/addReportData` | error case | "Success" | 200 | `Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:91` |
| `external-capture/addReportData` | error case | "Enter valid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:49` |
| `external-capture/addReportData` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:37` |
| `external-capture/addReportData` | error case | "Invalid report data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:57` |
| `external-capture/addReportData` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:29` |
| `external-capture/addReportData` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:100` |
| `getmedicineprescription` | error case | "No record found with the provided medical_id and doctor_id." | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicineContorller.php:33` |
| `nadi/report` | `language_code` | required | n/a | `Ashoka-World-Backend:app/Http/Controllers/NadiReportController.php:803` |
| `nadi/report` | `state` | required|string | n/a | `Ashoka-World-Backend:app/Http/Controllers/NadiReportController.php:804` |
| `nadi/reportInfo` | `doctor_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/NadiReportController.php:76` |
| `nadi/reportInfo` | `language_code` | required | n/a | `Ashoka-World-Backend:app/Http/Controllers/NadiReportController.php:77` |
| `nadi/reportInfo` | `patient_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/NadiReportController.php:78` |
| `nadiDataAnalysis` | error case | "Success" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4032` |
| `nadiDataAnalysis` | error case | "Enter valid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3454` |
| `nadiDataAnalysis` | error case | "File required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3291` |
| `nadiDataAnalysis` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3283` |
| `nadiDataAnalysis` | error case | "Invalid nadi data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3550` |
| `nadiDataAnalysis` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3287` |
| `nadiDataAnalysis` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3275` |
| `nadiDataAnalysis` | error case | "Only txt or zip file is allowed" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3296` |
| `nadiDataAnalysis` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3271` |
| `nadiDataAnalysis` | error case | "Required data is not available for this medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3476` |
| `nadiDataAnalysis` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3267` |
| `nadiDataAnalysis` | error case | "Nadi capture not allowed in this country" | 403 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3437` |
| `nadiDataAnalysis` | error case | "Clinic not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3385` |
| `nadiDataAnalysis` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3372` |
| `nadiDataAnalysis` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3317` |
| `nadiDataAnalysis` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4038` |
| `prakruti/fetchPrakrutiQuestions` | `patient_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:38` |
| `prakruti/fetchPrakrutiQuestions` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:34` |
| `prakruti/fetchPrakrutiQuestions` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:31` |
| `prakruti/fetchPrakrutiQuestions` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:71` |
| `prakruti/fetchPrakrutiQuestions` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:134` |
| `prakruti/fetchPrakrutiQuestionsNtLite` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:153` |
| `prakruti/fetchPrakrutiQuestionsNtLite` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:201` |
| `prakruti/getAllPrakrutiTypes` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:753` |
| `prakruti/saveManualPrakruti` | `patient_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:777` |
| `prakruti/saveManualPrakruti` | error case | "Prakruti saved successfully" | null | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:887` |
| `prakruti/saveManualPrakruti` | error case | "Invalid manual prakruti" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:858` |
| `prakruti/saveManualPrakruti` | error case | "Manual Prakruti required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:773` |
| `prakruti/saveManualPrakruti` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:769` |
| `prakruti/saveManualPrakruti` | error case | "Prakruti already submitted" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:867` |
| `prakruti/saveManualPrakruti` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:765` |
| `prakruti/saveManualPrakruti` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:855` |
| `prakruti/saveManualPrakruti` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:893` |
| `prakruti/savePrakrutiQuestions` | `patient_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:389` |
| `prakruti/savePrakrutiQuestions` | error case | "Prakruti saved successfully" | 200 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:709` |
| `prakruti/savePrakrutiQuestions` | error case | "Invalid symptom data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:377` |
| `prakruti/savePrakrutiQuestions` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:385` |
| `prakruti/savePrakrutiQuestions` | error case | "Prakruti already submitted" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:451` |
| `prakruti/savePrakrutiQuestions` | error case | "Prakruti not saved" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:511` |
| `prakruti/savePrakrutiQuestions` | error case | "Symptom is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:373` |
| `prakruti/savePrakrutiQuestions` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:381` |
| `prakruti/savePrakrutiQuestions` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:444` |
| `prakruti/savePrakrutiQuestions` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:715` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Medicine added to prescription successfully" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5322` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5134` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5137` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Invalid herb_name" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5198` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5136` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Invalid medicine type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5184` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5135` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Medicine already added for this prescription" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5279` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Medicine name is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5253` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Medicine type is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5138` |
| `report/addMedicineForPrescriptionNewV3` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5133` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5158` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5145` |
| `report/addMedicineForPrescriptionNewV3` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5325` |
| `report/deleteMedicineFromPrescriptionNewV3` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5344` |
| `report/deleteMedicineFromPrescriptionNewV3` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5347` |
| `report/deleteMedicineFromPrescriptionNewV3` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5346` |
| `report/deleteMedicineFromPrescriptionNewV3` | error case | "Invalid prescription id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5378` |
| `report/deleteMedicineFromPrescriptionNewV3` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5345` |
| `report/deleteMedicineFromPrescriptionNewV3` | error case | "Prescription id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5377` |
| `report/deleteMedicineFromPrescriptionNewV3` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5343` |
| `report/deleteMedicineFromPrescriptionNewV3` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5366` |
| `report/deleteMedicineFromPrescriptionNewV3` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5352` |
| `report/deleteMedicineFromPrescriptionNewV3` | error case | "Invalid prescription id for this medical record" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5386` |
| `report/deleteMedicineFromPrescriptionNewV3` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5402` |
| `report/deleteSinglePrescription` | error case | "Prescription deleted successfully" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10340` |
| `report/deleteSinglePrescription` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10259` |
| `report/deleteSinglePrescription` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10276` |
| `report/deleteSinglePrescription` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10271` |
| `report/deleteSinglePrescription` | error case | "Invalid medicine/herb prescription id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10280` |
| `report/deleteSinglePrescription` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10263` |
| `report/deleteSinglePrescription` | error case | "Medicine/herb prescription id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10267` |
| `report/deleteSinglePrescription` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10255` |
| `report/deleteSinglePrescription` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10299` |
| `report/deleteSinglePrescription` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10286` |
| `report/deleteSinglePrescription` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10348` |
| `report/fetchManualNadiKeywords` | `patient_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:776` |
| `report/fetchManualNadiKeywords` | `medical_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:777` |
| `report/fetchManualNadiKeywords` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:772` |
| `report/fetchManualNadiKeywords` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:768` |
| `report/fetchManualNadiKeywords` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:764` |
| `report/fetchManualNadiKeywords` | error case | "Data not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:899` |
| `report/fetchManualNadiKeywords` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:830` |
| `report/fetchManualNadiKeywords` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:818` |
| `report/fetchManualNadiKeywords` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:909` |
| `report/fetchMarkOnImage` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10683` |
| `report/fetchMarkOnImage` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10625` |
| `report/fetchMarkOnImage` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10629` |
| `report/fetchMarkOnImage` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10621` |
| `report/fetchMarkOnImage` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10617` |
| `report/fetchMarkOnImage` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10613` |
| `report/fetchMarkOnImage` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10654` |
| `report/fetchMarkOnImage` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10643` |
| `report/fetchMarkOnImage` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10690` |
| `report/fetchMarkOnImageUrl` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10900` |
| `report/fetchMarkOnImageUrl` | error case | "Enter valid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10874` |
| `report/fetchMarkOnImageUrl` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10845` |
| `report/fetchMarkOnImageUrl` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10849` |
| `report/fetchMarkOnImageUrl` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10841` |
| `report/fetchMarkOnImageUrl` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10837` |
| `report/fetchMarkOnImageUrl` | error case | "Patient not found" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10863` |
| `report/fetchMarkOnImageUrl` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10833` |
| `report/fetchMarkOnImageUrl` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10907` |
| `report/fetchNewVisitInformation` | `patient_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:984` |
| `report/fetchNewVisitInformation` | `medical_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:985` |
| `report/fetchNewVisitInformation` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:980` |
| `report/fetchNewVisitInformation` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:976` |
| `report/fetchNewVisitInformation` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:972` |
| `report/fetchNewVisitInformation` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1043` |
| `report/fetchNewVisitInformation` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1027` |
| `report/fetchNewVisitInformation` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1153` |
| `report/fetchSingleMedicinePrescription` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10514` |
| `report/fetchSingleMedicinePrescription` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10376` |
| `report/fetchSingleMedicinePrescription` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10408` |
| `report/fetchSingleMedicinePrescription` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10400` |
| `report/fetchSingleMedicinePrescription` | error case | "Invalid medicine/herb prescription id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10416` |
| `report/fetchSingleMedicinePrescription` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10384` |
| `report/fetchSingleMedicinePrescription` | error case | "Medicine/herb prescription id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10392` |
| `report/fetchSingleMedicinePrescription` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10368` |
| `report/fetchSingleMedicinePrescription` | error case | "Data not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10496` |
| `report/fetchSingleMedicinePrescription` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10445` |
| `report/fetchSingleMedicinePrescription` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10427` |
| `report/fetchSingleMedicinePrescription` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10544` |
| `report/generateWeeklyDiet` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12684` |
| `report/generateWeeklyDiet` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12402` |
| `report/generateWeeklyDiet` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12394` |
| `report/generateWeeklyDiet` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12386` |
| `report/generateWeeklyDiet` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12378` |
| `report/generateWeeklyDiet` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12370` |
| `report/generateWeeklyDiet` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12434` |
| `report/generateWeeklyDiet` | error case | "Input data is required and must be an array" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12444` |
| `report/generateWeeklyDiet` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12420` |
| `report/generateWeeklyDiet` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12699` |
| `report/generateWeeklyDiet` | error case | "Unable to generate diet. Please try again" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12691` |
| `report/generateYogaPlanner` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13045` |
| `report/generateYogaPlanner` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12966` |
| `report/generateYogaPlanner` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12958` |
| `report/generateYogaPlanner` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12950` |
| `report/generateYogaPlanner` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12942` |
| `report/generateYogaPlanner` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12934` |
| `report/generateYogaPlanner` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12998` |
| `report/generateYogaPlanner` | error case | "Input data is required and must be an array" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13009` |
| `report/generateYogaPlanner` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12984` |
| `report/generateYogaPlanner` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13038` |
| `report/getCurrentVisitInputForYogaPlanner` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12907` |
| `report/getCurrentVisitInputForYogaPlanner` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12836` |
| `report/getCurrentVisitInputForYogaPlanner` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12828` |
| `report/getCurrentVisitInputForYogaPlanner` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12820` |
| `report/getCurrentVisitInputForYogaPlanner` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12812` |
| `report/getCurrentVisitInputForYogaPlanner` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12804` |
| `report/getCurrentVisitInputForYogaPlanner` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12868` |
| `report/getCurrentVisitInputForYogaPlanner` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12854` |
| `report/getCurrentVisitInputForYogaPlanner` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12917` |
| `report/getDietAndLifestyle` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1795` |
| `report/getDietAndLifestyle` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1799` |
| `report/getDietAndLifestyle` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1787` |
| `report/getDietAndLifestyle` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1791` |
| `report/getDietAndLifestyle` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1781` |
| `report/getDietAndLifestyle` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1839` |
| `report/getDietAndLifestyle` | error case | "Nadi not taken for this medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1843` |
| `report/getDietAndLifestyle` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1825` |
| `report/getDietAndLifestyle` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1979` |
| `report/getLastPrescription` | error case | "Last prescribed medicine fetched successfully" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5539` |
| `report/getLastPrescription` | error case | "No previous prescription found" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5531` |
| `report/getLastPrescription` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5487` |
| `report/getLastPrescription` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5496` |
| `report/getLastPrescription` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5493` |
| `report/getLastPrescription` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5490` |
| `report/getLastPrescription` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5483` |
| `report/getLastPrescription` | error case | "Invalid medical report" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5511` |
| `report/getLastPrescription` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5546` |
| `report/getMedicineFromPrescriptionNewV3` | error case | "All prescription medicines fetched successfully" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5463` |
| `report/getMedicineFromPrescriptionNewV3` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5419` |
| `report/getMedicineFromPrescriptionNewV3` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5416` |
| `report/getMedicineFromPrescriptionNewV3` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5413` |
| `report/getMedicineFromPrescriptionNewV3` | error case | "No medicines found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5427` |
| `report/getMedicineFromPrescriptionNewV3` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5470` |
| `report/getNewMedicalId` | `patient_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:105` |
| `report/getNewMedicalId` | `clinic_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:106` |
| `report/getNewMedicalId` | `application_version_id` | required|integer | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:107` |
| `report/getNewMedicalId` | error case | "Application version id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:102` |
| `report/getNewMedicalId` | error case | "Clinic id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:94` |
| `report/getNewMedicalId` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:98` |
| `report/getNewMedicalId` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:90` |
| `report/getNewMedicalId` | error case | "Clinic not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:170` |
| `report/getNewMedicalId` | error case | "Invalid application version id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:176` |
| `report/getNewMedicalId` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:162` |
| `report/getNewMedicalId` | error case | "Failed to create medical id" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:249` |
| `report/getNewMedicalId` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:256` |
| `report/getPudiIngredient` | `doctor_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2683` |
| `report/getStrotas` | `doctor_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2536` |
| `report/getVikrutiWiseDietAndLifestyle` | `language_code` | in:1,2,3,4,5,6,7,8,9,10 | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2056` |
| `report/getVikrutiWiseDietAndLifestyle` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2001` |
| `report/getVikrutiWiseDietAndLifestyle` | error case | "Invalid vikruti type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2038` |
| `report/getVikrutiWiseDietAndLifestyle` | error case | "Language code is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1994` |
| `report/getVikrutiWiseDietAndLifestyle` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1997` |
| `report/getVikrutiWiseDietAndLifestyle` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1991` |
| `report/getVikrutiWiseDietAndLifestyle` | error case | "Vikruti is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2019` |
| `report/getVikrutiWiseDietAndLifestyle` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2014` |
| `report/getVikrutiWiseDietAndLifestyle` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2196` |
| `report/newVisitQues` | `medical_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1635` |
| `report/newVisitQues` | `form_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1636` |
| `report/newVisitQues` | `symptom_id` | required | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1637` |
| `report/newVisitQues` | `symptom_value` | required|string | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1638` |
| `report/newVisitQues` | `x_values` | required | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1639` |
| `report/newVisitQues` | `y_values` | required | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1640` |
| `report/newVisitQues` | `manual_nadi` | required | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1641` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Data saved" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11221` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Data not saved. Invalid symptom data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11215` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Invalid Symptom Category id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10999` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10991` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10995` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Invalid symptom data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10971` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10983` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10979` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Symptom Category id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10987` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10975` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11024` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Enter valid symptom category id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11035` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11013` |
| `report/saveCategoryWiseVikrutiQuestions` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11227` |
| `report/saveDietAndLifestyle` | error case | "Diet data stored successfully" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2778` |
| `report/saveDietAndLifestyle` | error case | "Donts key is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2797` |
| `report/saveDietAndLifestyle` | error case | "Dos key is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2793` |
| `report/saveDietAndLifestyle` | error case | "Field id is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2805` |
| `report/saveDietAndLifestyle` | error case | "Field name is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2801` |
| `report/saveDietAndLifestyle` | error case | "Invalid diet data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2789` |
| `report/saveDietAndLifestyle` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2745` |
| `report/saveDietAndLifestyle` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2749` |
| `report/saveDietAndLifestyle` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2741` |
| `report/saveDietAndLifestyle` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2737` |
| `report/saveDietAndLifestyle` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2733` |
| `report/saveDietAndLifestyle` | error case | "Diet data is required" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2786` |
| `report/saveDietAndLifestyle` | error case | "Invalid diet data" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2864` |
| `report/saveDietAndLifestyle` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2764` |
| `report/saveDietAndLifestyle` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2910` |
| `report/saveDietAndLifestyleManually` | error case | "Diet data stored successfully" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3054` |
| `report/saveDietAndLifestyleManually` | error case | "Donts key is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2987` |
| `report/saveDietAndLifestyleManually` | error case | "Dos key is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2983` |
| `report/saveDietAndLifestyleManually` | error case | "Field id is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2995` |
| `report/saveDietAndLifestyleManually` | error case | "Field name is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2991` |
| `report/saveDietAndLifestyleManually` | error case | "Invalid diet data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2979` |
| `report/saveDietAndLifestyleManually` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2937` |
| `report/saveDietAndLifestyleManually` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2941` |
| `report/saveDietAndLifestyleManually` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2933` |
| `report/saveDietAndLifestyleManually` | error case | "Nadi already taken for this visit" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2971` |
| `report/saveDietAndLifestyleManually` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2929` |
| `report/saveDietAndLifestyleManually` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2925` |
| `report/saveDietAndLifestyleManually` | error case | "Diet data is required" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2976` |
| `report/saveDietAndLifestyleManually` | error case | "Invalid diet data" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3040` |
| `report/saveDietAndLifestyleManually` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2956` |
| `report/saveDietAndLifestyleManually` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3061` |
| `report/saveManualNadi` | error case | "Manual nadi saved" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:631` |
| `report/saveManualNadi` | error case | "Data not saved. Invalid manual nadi" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:627` |
| `report/saveManualNadi` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:574` |
| `report/saveManualNadi` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:578` |
| `report/saveManualNadi` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:570` |
| `report/saveManualNadi` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:566` |
| `report/saveManualNadi` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:562` |
| `report/saveManualNadi` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:603` |
| `report/saveManualNadi` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:592` |
| `report/saveManualNadi` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:639` |
| `report/saveMarkOnImage` | error case | "Mark on image saved" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:745` |
| `report/saveMarkOnImage` | error case | "Both x and y values must be integers" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:715` |
| `report/saveMarkOnImage` | error case | "Data not saved. Invalid x and y values" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:738` |
| `report/saveMarkOnImage` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:666` |
| `report/saveMarkOnImage` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:670` |
| `report/saveMarkOnImage` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:662` |
| `report/saveMarkOnImage` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:658` |
| `report/saveMarkOnImage` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:654` |
| `report/saveMarkOnImage` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:695` |
| `report/saveMarkOnImage` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:684` |
| `report/saveMarkOnImage` | error case | "Nadi already taken for this visit" | 409 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:700` |
| `report/saveMarkOnImage` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:751` |
| `report/saveMarkOnImageUrl` | `mark_on_image` | image|mimes:jpeg,png,jpg | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10767` |
| `report/saveMarkOnImageUrl` | error case | "Image must be a type of: jpeg, png, jpg" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10770` |
| `report/saveMarkOnImageUrl` | error case | "Mark on image saved" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10803` |
| `report/saveMarkOnImageUrl` | error case | "Enter valid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10745` |
| `report/saveMarkOnImageUrl` | error case | "Failed to save mark on image" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10808` |
| `report/saveMarkOnImageUrl` | error case | "Image shouldn't be greater than 5 MB" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10763` |
| `report/saveMarkOnImageUrl` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10716` |
| `report/saveMarkOnImageUrl` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10720` |
| `report/saveMarkOnImageUrl` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10712` |
| `report/saveMarkOnImageUrl` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10708` |
| `report/saveMarkOnImageUrl` | error case | "Patient not found" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10734` |
| `report/saveMarkOnImageUrl` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10704` |
| `report/saveMarkOnImageUrl` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10821` |
| `report/savePrescriptionData` | error case | "Prescription saved successfully" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5110` |
| `report/savePrescriptionData` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4575` |
| `report/savePrescriptionData` | error case | "Duration_days is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4825` |
| `report/savePrescriptionData` | error case | "In_addition is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4852` |
| `report/savePrescriptionData` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4587` |
| `report/savePrescriptionData` | error case | "Invalid duration_days for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4723` |
| `report/savePrescriptionData` | error case | "Invalid in_addition for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4684` |
| `report/savePrescriptionData` | error case | "Invalid inventory_consume for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4733` |
| `report/savePrescriptionData` | error case | "Invalid inventory_consume for prescription no ." | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4950` |
| `report/savePrescriptionData` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4583` |
| `report/savePrescriptionData` | error case | "Invalid medicine type for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4642` |
| `report/savePrescriptionData` | error case | "Invalid medicine_company for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4891` |
| `report/savePrescriptionData` | error case | "Invalid medicine_name for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4881` |
| `report/savePrescriptionData` | error case | "Invalid prescription data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4611` |
| `report/savePrescriptionData` | error case | "Invalid pudi_name for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4664` |
| `report/savePrescriptionData` | error case | "Invalid pudi_values for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4674` |
| `report/savePrescriptionData` | error case | "Invalid quantity for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4694` |
| `report/savePrescriptionData` | error case | "Invalid quantity_type for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4704` |
| `report/savePrescriptionData` | error case | "Invalid timing for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4743` |
| `report/savePrescriptionData` | error case | "Invalid timing for prescription no ." | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4960` |
| `report/savePrescriptionData` | error case | "Inventory_consume is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4816` |
| `report/savePrescriptionData` | error case | "Inventory_consume is required for prescription no ." | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5035` |
| `report/savePrescriptionData` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4579` |
| `report/savePrescriptionData` | error case | "Medicine_company is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5080` |
| `report/savePrescriptionData` | error case | "Medicine_name is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5089` |
| `report/savePrescriptionData` | error case | "Medicine_type is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5098` |
| `report/savePrescriptionData` | error case | "Pudi_name is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4870` |
| `report/savePrescriptionData` | error case | "Pudi_values is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4861` |
| `report/savePrescriptionData` | error case | "Quantity is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4843` |
| `report/savePrescriptionData` | error case | "Quantity_type is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4834` |
| `report/savePrescriptionData` | error case | "Timing is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4807` |
| `report/savePrescriptionData` | error case | "Timing is required for prescription no ." | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5026` |
| `report/savePrescriptionData` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4572` |
| `report/savePrescriptionData` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4601` |
| `report/savePrescriptionData` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4606` |
| `report/savePrescriptionData` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5118` |
| `report/savePrescriptionDataV2` | error case | "Prescription saved successfully" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6271` |
| `report/savePrescriptionDataV2` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5565` |
| `report/savePrescriptionDataV2` | error case | "Duration_days is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5881` |
| `report/savePrescriptionDataV2` | error case | "Herb_name is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5918` |
| `report/savePrescriptionDataV2` | error case | "In_addition is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5908` |
| `report/savePrescriptionDataV2` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5577` |
| `report/savePrescriptionDataV2` | error case | "Invalid duration_days for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5777` |
| `report/savePrescriptionDataV2` | error case | "Invalid herb_name for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5701` |
| `report/savePrescriptionDataV2` | error case | "Invalid in_addition for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5730` |
| `report/savePrescriptionDataV2` | error case | "Invalid inventory_consume for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5789` |
| `report/savePrescriptionDataV2` | error case | "Invalid inventory_consume for prescription no ." | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6089` |
| `report/savePrescriptionDataV2` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5573` |
| `report/savePrescriptionDataV2` | error case | "Invalid medicine type for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5677` |
| `report/savePrescriptionDataV2` | error case | "Invalid medicine_company for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5944` |
| `report/savePrescriptionDataV2` | error case | "Invalid medicine_name for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5929` |
| `report/savePrescriptionDataV2` | error case | "Invalid prescription data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5600` |
| `report/savePrescriptionDataV2` | error case | "Invalid quantity for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5744` |
| `report/savePrescriptionDataV2` | error case | "Invalid quantity_type for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5755` |
| `report/savePrescriptionDataV2` | error case | "Invalid timing for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5799` |
| `report/savePrescriptionDataV2` | error case | "Invalid timing for prescription no ." | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6100` |
| `report/savePrescriptionDataV2` | error case | "Inventory_consume is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5872` |
| `report/savePrescriptionDataV2` | error case | "Inventory_consume is required for prescription no ." | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6178` |
| `report/savePrescriptionDataV2` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5569` |
| `report/savePrescriptionDataV2` | error case | "Medicine_company is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5952` |
| `report/savePrescriptionDataV2` | error case | "Medicine_name is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6224` |
| `report/savePrescriptionDataV2` | error case | "Medicine_type is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6233` |
| `report/savePrescriptionDataV2` | error case | "Prescription data exceeds the maximum limit of 20 entries" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5615` |
| `report/savePrescriptionDataV2` | error case | "Quantity is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5899` |
| `report/savePrescriptionDataV2` | error case | "Quantity_type is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5890` |
| `report/savePrescriptionDataV2` | error case | "Select unique medicines/herbs only" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5644` |
| `report/savePrescriptionDataV2` | error case | "Timing is required for prescription no " | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5863` |
| `report/savePrescriptionDataV2` | error case | "Timing is required for prescription no ." | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6169` |
| `report/savePrescriptionDataV2` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5562` |
| `report/savePrescriptionDataV2` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5594` |
| `report/savePrescriptionDataV2` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5582` |
| `report/savePrescriptionDataV2` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6279` |
| `report/saveRecommendations` | error case | "Recommendations saved successfully" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12345` |
| `report/saveRecommendations` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12292` |
| `report/saveRecommendations` | error case | "Invalid medical report" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12304` |
| `report/saveRecommendations` | error case | "Invalid recommendations" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12314` |
| `report/saveRecommendations` | error case | "Invalid type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12332` |
| `report/saveRecommendations` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12284` |
| `report/saveRecommendations` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12354` |
| `report/saveSinglePrescription` | error case | "Prescription saved successfully" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7037` |
| `report/saveSinglePrescription` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6296` |
| `report/saveSinglePrescription` | error case | "Duration_days is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6702` |
| `report/saveSinglePrescription` | error case | "Herb_name is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6739` |
| `report/saveSinglePrescription` | error case | "In_addition is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6729` |
| `report/saveSinglePrescription` | error case | "Insufficient stock" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6664` |
| `report/saveSinglePrescription` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6308` |
| `report/saveSinglePrescription` | error case | "Invalid duration_days" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6581` |
| `report/saveSinglePrescription` | error case | "Invalid herb_name" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6505` |
| `report/saveSinglePrescription` | error case | "Invalid in_addition" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6534` |
| `report/saveSinglePrescription` | error case | "Invalid inventory_consume" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6593` |
| `report/saveSinglePrescription` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6304` |
| `report/saveSinglePrescription` | error case | "Invalid medicine company" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6432` |
| `report/saveSinglePrescription` | error case | "Invalid medicine type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6388` |
| `report/saveSinglePrescription` | error case | "Invalid medicine_company" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6806` |
| `report/saveSinglePrescription` | error case | "Invalid medicine_name" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6750` |
| `report/saveSinglePrescription` | error case | "Invalid prescription data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6332` |
| `report/saveSinglePrescription` | error case | "Invalid quantity" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6548` |
| `report/saveSinglePrescription` | error case | "Invalid quantity_type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6416` |
| `report/saveSinglePrescription` | error case | "Invalid timing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6603` |
| `report/saveSinglePrescription` | error case | "Inventory_consume is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6693` |
| `report/saveSinglePrescription` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6300` |
| `report/saveSinglePrescription` | error case | "Medicine name already exists" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6408` |
| `report/saveSinglePrescription` | error case | "Medicine_name is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7018` |
| `report/saveSinglePrescription` | error case | "Medicine_type is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6368` |
| `report/saveSinglePrescription` | error case | "Quantity is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6720` |
| `report/saveSinglePrescription` | error case | "Quantity_type is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6377` |
| `report/saveSinglePrescription` | error case | "This medicine/pudi/supplement is already added in the prescription" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6354` |
| `report/saveSinglePrescription` | error case | "Timing is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6684` |
| `report/saveSinglePrescription` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6293` |
| `report/saveSinglePrescription` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6326` |
| `report/saveSinglePrescription` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6313` |
| `report/saveSinglePrescription` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7045` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid ingredient or ID mismatch" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7454` |
| `report/saveSinglePrescriptionV2` | error case | "Prescription saved successfully" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7906` |
| `report/saveSinglePrescriptionV2` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7061` |
| `report/saveSinglePrescriptionV2` | error case | "Company already exists" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7175` |
| `report/saveSinglePrescriptionV2` | error case | "Duration_days is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7136` |
| `report/saveSinglePrescriptionV2` | error case | "Herb_name is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7669` |
| `report/saveSinglePrescriptionV2` | error case | "Herbs name already exists." | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7391` |
| `report/saveSinglePrescriptionV2` | error case | "Ingredients required and must not be duplicated" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7403` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7073` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid consume_data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7145` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid duration_days" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7122` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid duration_days at index {$index}" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7577` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid herb_name" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7492` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7069` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid medicine company" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7275` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid medicine type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7221` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid medicine_name" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7680` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid prescription data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7098` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid quantity at index {$index}" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7559` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid quantity_type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7257` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid quantity_type at index {$index}" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7568` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid timing at index {$index}" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7550` |
| `report/saveSinglePrescriptionV2` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7065` |
| `report/saveSinglePrescriptionV2` | error case | "Medicine name already exists" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7242` |
| `report/saveSinglePrescriptionV2` | error case | "Medicine with consume already exists at index {$index}" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7595` |
| `report/saveSinglePrescriptionV2` | error case | "Medicine_name is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7887` |
| `report/saveSinglePrescriptionV2` | error case | "Medicine_type is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7196` |
| `report/saveSinglePrescriptionV2` | error case | "Quantity_type is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7208` |
| `report/saveSinglePrescriptionV2` | error case | "This medicine/pudi/supplement is already added in the prescription" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7161` |
| `report/saveSinglePrescriptionV2` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7058` |
| `report/saveSinglePrescriptionV2` | error case | "consume_data must be a non-empty array" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7538` |
| `report/saveSinglePrescriptionV2` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7092` |
| `report/saveSinglePrescriptionV2` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7078` |
| `report/saveSinglePrescriptionV2` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7914` |
| `report/saveSinglePrescriptionV3` | error case | "Prescription saved successfully" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8082` |
| `report/saveSinglePrescriptionV3` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7935` |
| `report/saveSinglePrescriptionV3` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7950` |
| `report/saveSinglePrescriptionV3` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7945` |
| `report/saveSinglePrescriptionV3` | error case | "Invalid medicine_id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7996` |
| `report/saveSinglePrescriptionV3` | error case | "Invalid prescription data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7977` |
| `report/saveSinglePrescriptionV3` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7940` |
| `report/saveSinglePrescriptionV3` | error case | "Medicine_name is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8016` |
| `report/saveSinglePrescriptionV3` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7930` |
| `report/saveSinglePrescriptionV3` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7971` |
| `report/saveSinglePrescriptionV3` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7957` |
| `report/saveSinglePrescriptionV3` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8094` |
| `report/saveVikrutiQuestions` | error case | "Data saved" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:534` |
| `report/saveVikrutiQuestions` | error case | "Data not saved. Invalid symptom data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:528` |
| `report/saveVikrutiQuestions` | error case | "Invalid height" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:442` |
| `report/saveVikrutiQuestions` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:301` |
| `report/saveVikrutiQuestions` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:305` |
| `report/saveVikrutiQuestions` | error case | "Invalid symptom data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:285` |
| `report/saveVikrutiQuestions` | error case | "Invalid weight" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:444` |
| `report/saveVikrutiQuestions` | error case | "Major symptoms is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:452` |
| `report/saveVikrutiQuestions` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:297` |
| `report/saveVikrutiQuestions` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:293` |
| `report/saveVikrutiQuestions` | error case | "Symptom is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:281` |
| `report/saveVikrutiQuestions` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:289` |
| `report/saveVikrutiQuestions` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:330` |
| `report/saveVikrutiQuestions` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:319` |
| `report/saveVikrutiQuestions` | error case | "Nadi already taken for this visit" | 409 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:335` |
| `report/saveVikrutiQuestions` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:540` |
| `report/updateSinglePrescription` | error case | "Prescription updated successfully" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9304` |
| `report/updateSinglePrescription` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8321` |
| `report/updateSinglePrescription` | error case | "Duration_days is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8852` |
| `report/updateSinglePrescription` | error case | "Herb_name is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8889` |
| `report/updateSinglePrescription` | error case | "In_addition is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8879` |
| `report/updateSinglePrescription` | error case | "Insufficient stock" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8759` |
| `report/updateSinglePrescription` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8338` |
| `report/updateSinglePrescription` | error case | "Invalid duration_days" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8636` |
| `report/updateSinglePrescription` | error case | "Invalid herb_name" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8560` |
| `report/updateSinglePrescription` | error case | "Invalid in_addition" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8589` |
| `report/updateSinglePrescription` | error case | "Invalid inventory_consume" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8648` |
| `report/updateSinglePrescription` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8333` |
| `report/updateSinglePrescription` | error case | "Invalid medicine company" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8487` |
| `report/updateSinglePrescription` | error case | "Invalid medicine type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8442` |
| `report/updateSinglePrescription` | error case | "Invalid medicine/herb prescription id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8342` |
| `report/updateSinglePrescription` | error case | "Invalid medicine_company" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8954` |
| `report/updateSinglePrescription` | error case | "Invalid medicine_name" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8900` |
| `report/updateSinglePrescription` | error case | "Invalid prescription data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8368` |
| `report/updateSinglePrescription` | error case | "Invalid quantity" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8603` |
| `report/updateSinglePrescription` | error case | "Invalid quantity_type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8471` |
| `report/updateSinglePrescription` | error case | "Invalid timing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8658` |
| `report/updateSinglePrescription` | error case | "Inventory_consume is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8843` |
| `report/updateSinglePrescription` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8325` |
| `report/updateSinglePrescription` | error case | "Medicine name already exists" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8463` |
| `report/updateSinglePrescription` | error case | "Medicine/herb prescription id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8329` |
| `report/updateSinglePrescription` | error case | "Medicine_name is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9285` |
| `report/updateSinglePrescription` | error case | "Medicine_type is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8422` |
| `report/updateSinglePrescription` | error case | "Quantity is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8870` |
| `report/updateSinglePrescription` | error case | "Quantity_type is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8431` |
| `report/updateSinglePrescription` | error case | "This medicine/pudi/supplement is already added in the prescription" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8408` |
| `report/updateSinglePrescription` | error case | "Timing is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8834` |
| `report/updateSinglePrescription` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8317` |
| `report/updateSinglePrescription` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8361` |
| `report/updateSinglePrescription` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8348` |
| `report/updateSinglePrescription` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9312` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid ingredient or ID mismatch" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9748` |
| `report/updateSinglePrescriptionV2` | error case | "Prescription updated successfully" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10230` |
| `report/updateSinglePrescriptionV2` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9333` |
| `report/updateSinglePrescriptionV2` | error case | "Company already exists" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9472` |
| `report/updateSinglePrescriptionV2` | error case | "Duration_days is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9431` |
| `report/updateSinglePrescriptionV2` | error case | "Herb_name is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9996` |
| `report/updateSinglePrescriptionV2` | error case | "Herbs name already exists." | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9685` |
| `report/updateSinglePrescriptionV2` | error case | "Ingredients required and must not be duplicated" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9697` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9350` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid consume_data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9440` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid duration_days" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9417` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid duration_days at index {$index}" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9909` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid herb_name" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9824` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9345` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid medicine company" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9570` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid medicine type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9517` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid medicine/herb prescription id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9354` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid medicine_name" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10007` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid prescription data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9394` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid quantity at index {$index}" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9891` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid quantity_type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9552` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid quantity_type at index {$index}" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9900` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid timing at index {$index}" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9882` |
| `report/updateSinglePrescriptionV2` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9337` |
| `report/updateSinglePrescriptionV2` | error case | "Medicine name already exists" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9537` |
| `report/updateSinglePrescriptionV2` | error case | "Medicine with consume already exists at index {$index}" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9927` |
| `report/updateSinglePrescriptionV2` | error case | "Medicine/herb prescription id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9341` |
| `report/updateSinglePrescriptionV2` | error case | "Medicine_name is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10211` |
| `report/updateSinglePrescriptionV2` | error case | "Medicine_type is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9492` |
| `report/updateSinglePrescriptionV2` | error case | "Pudi not found" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9780` |
| `report/updateSinglePrescriptionV2` | error case | "Quantity_type is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9504` |
| `report/updateSinglePrescriptionV2` | error case | "This medicine/pudi/supplement is already added in the prescription" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9458` |
| `report/updateSinglePrescriptionV2` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9329` |
| `report/updateSinglePrescriptionV2` | error case | "consume_data must be a non-empty array" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9870` |
| `report/updateSinglePrescriptionV2` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9387` |
| `report/updateSinglePrescriptionV2` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9374` |
| `report/updateSinglePrescriptionV2` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10238` |
| `report/updateSinglePrescriptionV3` | error case | "Prescription updated successfully" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8287` |
| `report/updateSinglePrescriptionV3` | error case | "Client id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8117` |
| `report/updateSinglePrescriptionV3` | error case | "Invalid client id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8137` |
| `report/updateSinglePrescriptionV3` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8132` |
| `report/updateSinglePrescriptionV3` | error case | "Invalid medicine/herb prescription id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8142` |
| `report/updateSinglePrescriptionV3` | error case | "Invalid medicine_id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8202` |
| `report/updateSinglePrescriptionV3` | error case | "Invalid prescription data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8183` |
| `report/updateSinglePrescriptionV3` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8122` |
| `report/updateSinglePrescriptionV3` | error case | "Medicine/herb prescription id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8127` |
| `report/updateSinglePrescriptionV3` | error case | "Medicine_name is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8222` |
| `report/updateSinglePrescriptionV3` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8112` |
| `report/updateSinglePrescriptionV3` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8163` |
| `report/updateSinglePrescriptionV3` | error case | "Invalid client id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8149` |
| `report/updateSinglePrescriptionV3` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8299` |
| `report/updateWeeklyDiet` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12780` |
| `report/updateWeeklyDiet` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12723` |
| `report/updateWeeklyDiet` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12715` |
| `report/updateWeeklyDiet` | error case | "No weekly diet found for the given medical ID" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12759` |
| `report/updateWeeklyDiet` | error case | "Weekly diet must be an array with at least 7 items" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12733` |
| `report/updateWeeklyDiet` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12789` |
| `report/updateYogaPlanner` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13251` |
| `report/updateYogaPlanner` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13103` |
| `report/updateYogaPlanner` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13095` |
| `report/updateYogaPlanner` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13087` |
| `report/updateYogaPlanner` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13079` |
| `report/updateYogaPlanner` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13071` |
| `report/updateYogaPlanner` | error case | "Yoga planner data must be an array" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13148` |
| `report/updateYogaPlanner` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13135` |
| `report/updateYogaPlanner` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13121` |
| `report/updateYogaPlanner` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13259` |
| `report/visitWiseAllowedReports` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12255` |
| `report/visitWiseAllowedReports` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12096` |
| `report/visitWiseAllowedReports` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12092` |
| `report/visitWiseAllowedReports` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12088` |
| `report/visitWiseAllowedReports` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12110` |
| `report/visitWiseAllowedReports` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12266` |
| `updateYogaPlannerPublic` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13395` |
| `updateYogaPlannerPublic` | error case | "Yoga planner data must be an array" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13294` |
| `updateYogaPlannerPublic` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13284` |
| `updateYogaPlannerPublic` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13403` |
| `v2/report/fetchNewVisitCategoryWiseQuestions` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11774` |
| `v2/report/fetchNewVisitCategoryWiseQuestions` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11770` |
| `v2/report/fetchNewVisitCategoryWiseQuestions` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11766` |
| `v2/report/fetchNewVisitCategoryWiseQuestions` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11803` |
| `v2/report/fetchNewVisitCategoryWiseQuestions` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11780` |
| `v2/report/fetchNewVisitCategoryWiseQuestions` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11966` |
| `v2/report/fetchNewVisitInformation` | `patient_id` | required|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1178` |
| `v2/report/fetchNewVisitInformation` | `medical_id` | nullable|numeric | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1179` |
| `v2/report/fetchNewVisitInformation` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1174` |
| `v2/report/fetchNewVisitInformation` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1170` |
| `v2/report/fetchNewVisitInformation` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1245` |
| `v2/report/fetchNewVisitInformation` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1221` |
| `v2/report/fetchNewVisitInformation` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1394` |
| `v2/report/getCurrentVisitInfo` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11415` |
| `v2/report/getCurrentVisitInfo` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11262` |
| `v2/report/getCurrentVisitInfo` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11258` |
| `v2/report/getCurrentVisitInfo` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11254` |
| `v2/report/getCurrentVisitInfo` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11250` |
| `v2/report/getCurrentVisitInfo` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11246` |
| `v2/report/getCurrentVisitInfo` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11287` |
| `v2/report/getCurrentVisitInfo` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11277` |
| `v2/report/getCurrentVisitInfo` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11424` |
| `v2/report/getCurrentVisitInputForDiet` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11637` |
| `v2/report/getCurrentVisitInputForDiet` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11471` |
| `v2/report/getCurrentVisitInputForDiet` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11463` |
| `v2/report/getCurrentVisitInputForDiet` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11455` |
| `v2/report/getCurrentVisitInputForDiet` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11447` |
| `v2/report/getCurrentVisitInputForDiet` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11439` |
| `v2/report/getCurrentVisitInputForDiet` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11503` |
| `v2/report/getCurrentVisitInputForDiet` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11489` |
| `v2/report/getCurrentVisitInputForDiet` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11647` |
| `v2/report/getLastVisitInformation` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11741` |
| `v2/report/getLastVisitInformation` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11668` |
| `v2/report/getLastVisitInformation` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11664` |
| `v2/report/getLastVisitInformation` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11660` |
| `v2/report/getLastVisitInformation` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11683` |
| `v2/report/getLastVisitInformation` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11752` |
| `v2/report/getLastVisitMandatoryQuesitons` | error case | "Success" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12067` |
| `v2/report/getLastVisitMandatoryQuesitons` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11985` |
| `v2/report/getLastVisitMandatoryQuesitons` | error case | "Last nadi visit not found" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12019` |
| `v2/report/getLastVisitMandatoryQuesitons` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11981` |
| `v2/report/getLastVisitMandatoryQuesitons` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11977` |
| `v2/report/getLastVisitMandatoryQuesitons` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12000` |
| `v2/report/getLastVisitMandatoryQuesitons` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12076` |
| `v2/report/getNewMedicalId` | `patient_id` | required | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1425` |
| `v2/report/getNewMedicalId` | `application_version_id` | required|integer | n/a | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1426` |
| `v2/report/getNewMedicalId` | error case | "Application version id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1417` |
| `v2/report/getNewMedicalId` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1421` |
| `v2/report/getNewMedicalId` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1413` |
| `v2/report/getNewMedicalId` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1409` |
| `v2/report/getNewMedicalId` | error case | "Invalid application version id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1501` |
| `v2/report/getNewMedicalId` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1477` |
| `v2/report/getNewMedicalId` | error case | "Failed to create medical id" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1580` |
| `v2/report/getNewMedicalId` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1587` |
| `v2/report/getVikrutiWiseDietAndLifestyle` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2221` |
| `v2/report/getVikrutiWiseDietAndLifestyle` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2225` |
| `v2/report/getVikrutiWiseDietAndLifestyle` | error case | "Invalid vikruti type" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2302` |
| `v2/report/getVikrutiWiseDietAndLifestyle` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2217` |
| `v2/report/getVikrutiWiseDietAndLifestyle` | error case | "Nadi already taken for this visit" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2256` |
| `v2/report/getVikrutiWiseDietAndLifestyle` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2213` |
| `v2/report/getVikrutiWiseDietAndLifestyle` | error case | "User id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2209` |
| `v2/report/getVikrutiWiseDietAndLifestyle` | error case | "Vikruti is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2284` |
| `v2/report/getVikrutiWiseDietAndLifestyle` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2240` |
| `v2/report/getVikrutiWiseDietAndLifestyle` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2475` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Diet data stored successfully" | null | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3200` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Donts key is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3133` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Dos key is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3129` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Field id is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3141` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Field name is missing" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3137` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Invalid diet data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3125` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3087` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3091` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3083` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3079` |
| `v2/report/saveDietAndLifestyleManually` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3075` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Diet data is required" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3122` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3117` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Invalid diet data" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3186` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Invalid patient id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3106` |
| `v2/report/saveDietAndLifestyleManually` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3207` |
| `zipFileNadiAnalysis` | error case | "Success" | 200 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4412` |
| `zipFileNadiAnalysis` | error case | "Clinic id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4068` |
| `zipFileNadiAnalysis` | error case | "Enter valid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4185` |
| `zipFileNadiAnalysis` | error case | "File required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4080` |
| `zipFileNadiAnalysis` | error case | "Invalid medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4072` |
| `zipFileNadiAnalysis` | error case | "Invalid nadi data" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4287` |
| `zipFileNadiAnalysis` | error case | "Invalid patient id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4076` |
| `zipFileNadiAnalysis` | error case | "Medical id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4064` |
| `zipFileNadiAnalysis` | error case | "Only zip file is allowed" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4085` |
| `zipFileNadiAnalysis` | error case | "Patient id is required" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4060` |
| `zipFileNadiAnalysis` | error case | "Required data is not available for this medical id" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4204` |
| `zipFileNadiAnalysis` | error case | "User id is not provided" | 400 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4056` |
| `zipFileNadiAnalysis` | error case | "Clinic not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4098` |
| `zipFileNadiAnalysis` | error case | "Enter valid medical id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4168` |
| `zipFileNadiAnalysis` | error case | "Invalid clinic id" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4089` |
| `zipFileNadiAnalysis` | error case | "Patient not found" | 404 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4114` |
| `zipFileNadiAnalysis` | error case | "Internal server error" | 500 | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4418` |

## 9. Non-functional

- **Security**: backend routes require `auth.token` except `getDietDataTest` (none) and `updateYogaPlannerPublic` (`api` only) (`Ashoka-World-Backend:routes/api.php:728`, `Ashoka-World-Backend:routes/api.php:779`); web routes require `check_auth_token` (§2). Web calls to the backend send `auth-token` and `user-id` headers from the session (`Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:78-83`). Nadi upload accepts only txt or zip files (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3296`); mark-on-image accepts jpeg, png, jpg (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10767`).
- **Languages**: required list is English, Marathi, Hindi, Czech, German, Spanish, Italian (`references/qa-scope-rules.md`). Language files found in code: `Nadi-Tarangini-Frontend:resources/lang/en/auth.php`, `en/pagination.php`, `en/passwords.php`, `en/validation.php` and `Nadi-Tarangini-Frontend:resources/lang/en_patient.json`; only English files are in code (`atreya-docs/_map/_modules/nadi-flow/facts.md`, "Languages"). The `getVikrutiWiseDietAndLifestyle` route accepts `language_code` in 1-10 (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2056`); `nadi/reportInfo` requires `language_code` (`Ashoka-World-Backend:app/Http/Controllers/NadiReportController.php:77`). The report-wise language list returned by `fee-details/report-wise-languages` is filtered to ids 1, 2, 3 only when the site type is `eu`; otherwise the full list is returned (`Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:55-57`). Mapping of ids to languages: see §13 question 7.
- **Performance**: the V3 web page loads several backend calls in parallel using `Http::pool` (`Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:474`, `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:790`). No timeouts or limits were read for this module.

## 10. Environment matrix

Copied verbatim from `atreya-docs/environments.md`; "TO FILL" is unfilled.

### Ashoka-World-Backend

| Env | Ref | Host | Feature flags | Integration mode |
|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL |

### Nadi-Tarangini-App

| Env | Ref | Build flavor | Host | Feature flags | Integration mode |
|---|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL | TO FILL |

### Nadi-Tarangini-Frontend

| Env | Ref | Host | Feature flags | Integration mode |
|---|---|---|---|---|
| dev | TO FILL | TO FILL | TO FILL | TO FILL |
| staging | TO FILL | TO FILL | TO FILL | TO FILL |
| production | TO FILL | TO FILL | TO FILL | TO FILL |

## 11. Staging delta

See [staging-delta.md](staging-delta.md). Status: all three repos are skipped, waiting for `environments.md` (staging and production refs are not filled in). No delta was computed (`atreya-docs/nt/nadi-flow/staging-delta.md`).

## 12. External integrations

| System | Where |
|---|---|
| AWS Lambda / API Gateway | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3557`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3798`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3799` |
| S3 (backend; hard-coded S3 URL strings, not SDK calls) | `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3534`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3639`, `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3682`; `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:121`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:188`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:221` |
| S3 (web frontend; hard-coded S3 URL strings) | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:842`, `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:843` |

(`atreya-docs/_map/_modules/nadi-flow/facts.md`, "External systems".) What each integration does is not stated in the fact pack: see §13 question 9.

## 13. Open questions

1. (PO, dev) 23 backend routes have no screen caller in this workspace (§6.4). Which are live (called by another client, a device or an external system) and which are legacy? Includes `external-capture/addReportData` and `updateYogaPlannerPublic`.
2. (PO) The module description includes "fees", but `patient/saveFees`, `patient/getClientDetails` and `infinitePatientList` are not among the module's 62 routes, and several App screens (LiveNadiScreen1, AddMedicinePrescription, EditMedicinePrescription, PatientScreen, VisitReportListScreen, ReportScreen) are not in its 7 screens. Which module owns them, and should this PRD cover them?
3. (dev) These tables have no columns in migrations: `all_prakruti_types`, `doctor_multichoice_options`, `ingredients_list`, `languages`, `medical_report_image_markers`, `multichoice_field_list`, `nadi_report`, `nt_application_version`, `patient_prakruti`, `pg_device_mapping`, `prakruti_wise_diet`, `project_variables`, `symptoms_dropdown_item`, `user_selected_countries`, `yoga_report_data`. Where are they created, and what are their key fields?
4. (PO) Which user roles may run the assessment, prescription, diet and fee steps? Routes only show `auth.token` and `check_auth_token`; no role check was read.
5. (dev) Success responses on several APIs show HTTP "not determined" (e.g. `prakruti/saveManualPrakruti`, `report/saveRecommendations`, `v2/report/getCurrentVisitInfo`). What HTTP code do they return?
6. (PO, DevOps) `environments.md` is all TO FILL for the three repos. Please provide refs, hosts, feature flags and integration modes so the staging delta can be computed.
7. (QA, PO) Required languages are English, Marathi, Hindi, Czech, German, Spanish, Italian, but code has only English language files in the web frontend. Which `language_code` values 1-10 map to which languages, and where are the other translations?
8. (dev, security) `POST getDietDataTest` has no middleware and `POST updateYogaPlannerPublic` has only `api`. Are they intentionally public, and are they still needed?
9. (dev) What do AWS Lambda / API Gateway and the S3 uses do in this flow (e.g. which report, which file)?
10. (dev) Prescription has V1, V2 and V3 variants for save, update and delete. Which are current? Is V1 (`savePrescriptionData`, `saveSinglePrescription`, `updateSinglePrescription`) retired? Is the `...NewV3` set (`addMedicineForPrescriptionNewV3`, `deleteMedicineFromPrescriptionNewV3`, `getMedicineFromPrescriptionNewV3`) meant for a future screen?
11. (dev, PO) What rule makes `errors.limited_access` appear on `GET vikruti`, and what makes a medical id "expired"?
12. (dev) Removed: the full message "Image shouldn't be greater than 5 MB" is in code (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10763`).
13. (PO) Prakruti can only be submitted once ("Prakruti already submitted"). Can it be edited or reset later, and by whom?
14. (PO) Several validation failures return 404 (e.g. "Diet data is required", "Input data is required and must be an array"). Is this the intended contract for clients?
15. (dev) `nadi/reportInfo`, `nadi/report`, `nadi/baselineCalculation`, `report/getStrotas`, `generateLambda` and `report/newVisitQues` have no screen caller. Who calls them, and what do they produce?

## 14. Diagrams

None yet: run /atreya:diagram nadi-flow.

## 15. Document control

| Field | Value |
|---|---|
| Status | Draft |
| Date | 2026-11-03 |
| Reviewer | TBD |
| Commits | Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`; Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`; Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d` |
