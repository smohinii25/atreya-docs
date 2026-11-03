# Fact pack: nadi-flow (Nadi assessment & visit flow (prakruti, vikruti, nadi capture, diet, prescription, fees))

Generated 2026-11-03 by scripts/module-facts.sh. Product nt, critical true. Every line below is from code or a human-owned doc; cite the source given.

Commits: Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`, Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`, Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d`

## Backend routes (62)

### POST external-capture/addReportData
- controller: ExternalCaptureController@addReportData (found) · route: `Ashoka-World-Backend:routes/api.php:1409` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:29`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:37`); 400 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:49`); 400 "Invalid report data" (`Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:57`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:91`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/External/ExternalCaptureController.php:100`)

### POST generateLambda
- controller: GenerateSwasthyaLambda@generateLambda (found) · route: `Ashoka-World-Backend:routes/api.php:922` · middleware: api, auth.token
- called by: no screen in this workspace

### POST getDietDataTest
- controller: MedicalReportSaveController@getDietDataStateWise (found) · route: `Ashoka-World-Backend:routes/api.php:728` · middleware: none
- called by: no screen in this workspace

### POST getmedicineprescription
- controller: MedicineContorller@getMedicinePrescribed (found) · route: `Ashoka-World-Backend:routes/api.php:999` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 404 "No record found with the provided medical_id and doctor_id." (`Ashoka-World-Backend:app/Http/Controllers/MedicineContorller.php:33`)

### POST nadi/baselineCalculation
- controller: NadiReportController@baselineCalculation (found) · route: `Ashoka-World-Backend:routes/api.php:1255` · middleware: api, auth.token
- called by: no screen in this workspace

### POST nadi/report
- controller: NadiReportController@nadiReportDefinition (found) · route: `Ashoka-World-Backend:routes/api.php:1256` · middleware: api, auth.token
- called by: no screen in this workspace
- validation: `language_code`: required (`Ashoka-World-Backend:app/Http/Controllers/NadiReportController.php:803`); `state`: required|string (`Ashoka-World-Backend:app/Http/Controllers/NadiReportController.php:804`)

### POST nadi/reportInfo
- controller: NadiReportController@nadiReportInfo (found) · route: `Ashoka-World-Backend:routes/api.php:1254` · middleware: api, auth.token
- called by: no screen in this workspace
- validation: `doctor_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/NadiReportController.php:76`); `language_code`: required (`Ashoka-World-Backend:app/Http/Controllers/NadiReportController.php:77`); `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/NadiReportController.php:78`)

### POST nadiDataAnalysis
- controller: MedicalReportSaveController@nadiDataAnalysis (found) · route: `Ashoka-World-Backend:routes/api.php:964` · middleware: api, auth.token
- called by: Nadi-Tarangini-App uploadNadiData (LiveNadiScreen1); Nadi-Tarangini-Frontend LiveNadiController@saveUsbNadiData (live_nadi.medical_assessment, medical_assessment.medical_assesment); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@saveUsbNadiDataV3
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3267`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3271`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3275`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3283`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3287`); 400 "File required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3291`); 400 "Only txt or zip file is allowed" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3296`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3317`)

### POST prakruti/fetchPrakrutiQuestions
- controller: PrakrutiController@fetchPrakrutiQuestions (found) · route: `Ashoka-World-Backend:routes/api.php:1227` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getPrakrutiQuestions (PatientScreen, VisitReportListScreen); Nadi-Tarangini-Frontend PrakrutiQuestionsController@getPrakrutiDataOnList (appointment.appointment_list, live_nadi.medical_assessment, patient.add-member, patient.patientlist); Nadi-Tarangini-Frontend PrakrutiQuestionsController@index (errors.expiredMedicalId)
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:38`)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:31`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:34`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:71`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:134`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:141`)

### POST prakruti/fetchPrakrutiQuestionsNtLite
- controller: PrakrutiController@fetchPrakrutiQuestionsNtLite (found) · route: `Ashoka-World-Backend:routes/api.php:1229` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend PrakrutiQuestionsController@getPrakrutiDataForNewPatient (auth.nt-lite.nt_lite_dashboard)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:153`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:201`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:208`)

### POST prakruti/getAllPrakrutiTypes
- controller: PrakrutiController@getAllPrakrutiTypes (found) · route: `Ashoka-World-Backend:routes/api.php:1235` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getPrakrutiType (FillPrakrutiScreen); Nadi-Tarangini-Frontend PrakrutiQuestionsController@getPrakrutiDataForNewPatient (auth.nt-lite.nt_lite_dashboard); Nadi-Tarangini-Frontend PrakrutiQuestionsController@getPrakrutiDataOnList (appointment.appointment_list, live_nadi.medical_assessment, patient.add-member, patient.patientlist); Nadi-Tarangini-Frontend PrakrutiQuestionsController@index (errors.expiredMedicalId)
- errors: 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:753`)

### POST prakruti/saveManualPrakruti
- controller: PrakrutiController@saveManualPrakruti (found) · route: `Ashoka-World-Backend:routes/api.php:1238` · middleware: api, auth.token
- called by: Nadi-Tarangini-App saveManualPrakruti (FillPrakrutiScreen); Nadi-Tarangini-Frontend PrakrutiQuestionsController@savePrakrutiData (appointment.appointment_list, doctor_dashboard.dashboard, live_nadi.medical_assessment, patient.add-member)
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:777`)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:765`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:769`); 400 "Manual Prakruti required" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:773`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:855`); 400 "Invalid manual prakruti" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:858`); 400 "Prakruti already submitted" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:867`); ? "Prakruti saved successfully" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:887`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:893`)

### POST prakruti/savePrakrutiQuestions
- controller: PrakrutiController@savePrakrutiQuestions (found) · route: `Ashoka-World-Backend:routes/api.php:1232` · middleware: api, auth.token
- called by: Nadi-Tarangini-App savePrakrutiQuestions (FillPrakrutiScreen); Nadi-Tarangini-Frontend PrakrutiQuestionsController@savePrakrutiData (appointment.appointment_list, doctor_dashboard.dashboard, live_nadi.medical_assessment, patient.add-member)
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:389`)
- errors: 400 "Symptom is required" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:373`); 400 "Invalid symptom data" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:377`); 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:381`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:385`); 400 "Invalid symptom data" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:418`); 400 "Invalid symptom data" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:423`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:444`); 400 "Prakruti already submitted" (`Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:451`)

### POST report/addMedicineForPrescriptionNewV3
- controller: MedicalReportSaveController@addMedicineForPrescriptionNewV3 (found) · route: `Ashoka-World-Backend:routes/api.php:1176` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5133`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5134`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5135`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5136`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5137`); 400 "Medicine type is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5138`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5145`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5158`)

### POST report/deleteMedicineFromPrescriptionNewV3
- controller: MedicalReportSaveController@deleteMedicineFromPrescriptionNewV3 (found) · route: `Ashoka-World-Backend:routes/api.php:1177` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5343`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5344`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5345`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5346`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5347`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5352`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5366`); 400 "Prescription id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5377`)

### POST report/deleteSinglePrescription
- controller: MedicalReportSaveController@deleteSinglePrescription (found) · route: `Ashoka-World-Backend:routes/api.php:1188` · middleware: api, auth.token
- called by: Nadi-Tarangini-App deleteSinglePrescription; Nadi-Tarangini-Frontend PrescriptionController@deleteMedicine (auth.nt-lite.nt_lite_patient_report)
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10255`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10259`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10263`); 400 "Medicine/herb prescription id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10267`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10271`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10276`); 400 "Invalid medicine/herb prescription id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10280`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10286`)

### POST report/fetchManualNadiKeywords
- controller: MedicalReportSaveController@fetchManualNadiKeywords (found) · route: `Ashoka-World-Backend:routes/api.php:1157` · middleware: api, auth.token
- called by: Nadi-Tarangini-App fetchManualNadiKeywords; Nadi-Tarangini-Frontend LiveNadiController@liveNadi (errors.expiredMedicalId, live_nadi.medical_assessment); Nadi-Tarangini-Frontend ManualNadiKeywordsController@index (errors.expiredMedicalId); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment)
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:776`); `medical_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:777`)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:764`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:768`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:772`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:818`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:830`); 404 "Data not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:899`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:909`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:916`)

### POST report/fetchMarkOnImage
- controller: MedicalReportSaveController@fetchMarkOnImage (found) · route: `Ashoka-World-Backend:routes/api.php:1170` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10613`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10617`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10621`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10625`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10629`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10643`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10654`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10683`)

### POST report/fetchMarkOnImageUrl
- controller: MedicalReportSaveController@fetchMarkOnImageUrl (found) · route: `Ashoka-World-Backend:routes/api.php:1171` · middleware: api, auth.token
- called by: Nadi-Tarangini-App fetchMarkOnImage; Nadi-Tarangini-Frontend LiveNadiController@liveNadi (errors.expiredMedicalId, live_nadi.medical_assessment); Nadi-Tarangini-Frontend MarkOnImageController@index (errors.expiredMedicalId); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10833`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10837`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10841`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10845`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10849`); 400 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10863`); 400 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10874`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10900`)

### POST report/fetchNewVisitInformation
- controller: MedicalReportSaveController@newVisitInfo (found) · route: `Ashoka-World-Backend:routes/api.php:1192` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend VikrutiController@index (errors.expiredMedicalId, errors.limited_access)
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:984`); `medical_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:985`)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:972`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:976`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:980`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1027`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1043`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1153`)

### POST report/fetchSingleMedicinePrescription
- controller: MedicalReportSaveController@fetchSingleMedicinePrescription (found) · route: `Ashoka-World-Backend:routes/api.php:1189` · middleware: api, auth.token
- called by: Nadi-Tarangini-App fetchSingleMedicinePrescription (EditMedicinePrescription); Nadi-Tarangini-Frontend PrescriptionController@editMedicine (auth.nt-lite.nt_lite_patient_report, live_nadi.medical_assessment, medical_assessment.medical_assesment)
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10368`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10376`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10384`); 400 "Medicine/herb prescription id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10392`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10400`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10408`); 400 "Invalid medicine/herb prescription id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10416`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10427`)

### POST report/generateWeeklyDiet
- controller: MedicalReportSaveController@generateWeeklyDiet (found) · route: `Ashoka-World-Backend:routes/api.php:1210` · middleware: api, auth.token
- called by: Nadi-Tarangini-App generateWeeklyDiet
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12370`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12378`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12386`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12394`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12402`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12420`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12434`); 404 "Input data is required and must be an array" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12444`)

### POST report/generateYogaPlanner
- controller: MedicalReportSaveController@generateYogaPlanner (found) · route: `Ashoka-World-Backend:routes/api.php:1217` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12934`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12942`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12950`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12958`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12966`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12984`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12998`); 404 "Input data is required and must be an array" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13009`)

### POST report/getCurrentVisitInputForYogaPlanner
- controller: MedicalReportSaveController@getInputForYogaPlanner (found) · route: `Ashoka-World-Backend:routes/api.php:1215` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getCurrentVisitInputForYogaPlanner
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12804`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12812`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12820`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12828`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12836`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12854`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12868`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12907`)

### POST report/getDietAndLifestyle
- controller: MedicalReportSaveController@getDietAndLifestyle (found) · route: `Ashoka-World-Backend:routes/api.php:1196` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getDietData; Nadi-Tarangini-Frontend DietController@index (errors.expiredMedicalId); Nadi-Tarangini-Frontend LiveNadiController@liveNadi (errors.expiredMedicalId, live_nadi.medical_assessment); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1781`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1787`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1791`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1795`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1799`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1825`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1839`); 404 "Nadi not taken for this medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1843`)

### POST report/getLastPrescription
- controller: MedicalReportSaveController@getLastPrescription (found) · route: `Ashoka-World-Backend:routes/api.php:1179` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5483`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5487`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5490`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5493`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5496`); 404 "Invalid medical report" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5511`); 200 "No previous prescription found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5531`); 200 "Last prescribed medicine fetched successfully" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5539`)

### POST report/getMedicineFromPrescriptionNewV3
- controller: MedicalReportSaveController@getMedicineFromPrescriptionNewV3 (found) · route: `Ashoka-World-Backend:routes/api.php:1178` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5413`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5416`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5419`); 404 "No medicines found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5427`); 200 "All prescription medicines fetched successfully" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5463`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5470`)

### POST report/getNewMedicalId
- controller: MedicalReportSaveController@getNewMedicalId (found) · route: `Ashoka-World-Backend:routes/api.php:1154` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@ensureMedicalIdLocked; Nadi-Tarangini-Frontend PatientListController@fetchNewMedicalIdV2 (appointment.appointment_list, doctor_dashboard.dashboard, patient.add-member, patient.patientlist); Nadi-Tarangini-Frontend VikrutiController@index (errors.expiredMedicalId, errors.limited_access)
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:105`); `clinic_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:106`); `application_version_id`: required|integer (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:107`)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:90`); 400 "Clinic id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:94`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:98`); 400 "Application version id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:102`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:162`); 404 "Clinic not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:170`); 404 "Invalid application version id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:176`); 500 "Failed to create medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:249`)

### POST report/getPudiIngredient
- controller: MedicalReportSaveController@getPudiIngredient (found) · route: `Ashoka-World-Backend:routes/api.php:1202` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend LiveNadiController@liveNadi (errors.expiredMedicalId, live_nadi.medical_assessment); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment); Nadi-Tarangini-Frontend PrescriptionController@index (errors.expiredMedicalId)
- validation: `doctor_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2683`)

### POST report/getStrotas
- controller: MedicalReportSaveController@getStrotas (found) · route: `Ashoka-World-Backend:routes/api.php:1201` · middleware: api, auth.token
- called by: no screen in this workspace
- validation: `doctor_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2536`)

### POST report/getVikrutiWiseDietAndLifestyle
- controller: MedicalReportSaveController@getVikrutiWiseDietAndLifestyle (found) · route: `Ashoka-World-Backend:routes/api.php:1198` · middleware: api, auth.token
- called by: no screen in this workspace
- validation: `language_code`: in:1,2,3,4,5,6,7,8,9,10 (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2056`)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1991`); 400 "Language code is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1994`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1997`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2001`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2014`); 400 "Vikruti is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2019`); 400 "Invalid vikruti type" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2038`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2196`)

### POST report/newVisitQues
- controller: MedicalReportSaveController@saveNewVisitQues (found) · route: `Ashoka-World-Backend:routes/api.php:1193` · middleware: api, auth.token
- called by: no screen in this workspace
- validation: `medical_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1635`); `form_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1636`); `symptom_id`: required (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1637`); `symptom_value`: required|string (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1638`); `x_values`: required (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1639`); `y_values`: required (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1640`); `manual_nadi`: required (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1641`)

### POST report/saveCategoryWiseVikrutiQuestions
- controller: MedicalReportSaveController@saveCategoryWiseVikrutiQuestions (found) · route: `Ashoka-World-Backend:routes/api.php:1161` · middleware: api, auth.token
- called by: Nadi-Tarangini-App saveQuestionsTabData; Nadi-Tarangini-Frontend VikrutiController@saveCategoryWiseVikrutiData (live_nadi.medical_assessment, medical_assessment.medical_assesment)
- errors: 400 "Invalid symptom data" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10971`); 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10975`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10979`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10983`); 400 "Symptom Category id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10987`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10991`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10995`); 400 "Invalid Symptom Category id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10999`)

### POST report/saveDietAndLifestyle
- controller: MedicalReportSaveController@saveDietAndLifestyle (found) · route: `Ashoka-World-Backend:routes/api.php:1195` · middleware: api, auth.token
- called by: Nadi-Tarangini-App saveDietAndLifestyle; Nadi-Tarangini-Frontend DietController@saveDietData
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2733`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2737`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2741`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2745`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2749`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2764`); ? "Diet data stored successfully" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2778`); 404 "Diet data is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2786`)

### POST report/saveDietAndLifestyleManually
- controller: MedicalReportSaveController@saveDietAndLifestyleMaually (found) · route: `Ashoka-World-Backend:routes/api.php:1199` · middleware: api, auth.token
- called by: Nadi-Tarangini-App saveDietAndLifestyleManually; Nadi-Tarangini-Frontend DietController@saveVikrutiWiseDietData
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2925`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2929`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2933`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2937`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2941`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2956`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2967`); 400 "Nadi already taken for this visit" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2971`)

### POST report/saveManualNadi
- controller: MedicalReportSaveController@saveManualNadi (found) · route: `Ashoka-World-Backend:routes/api.php:1164` · middleware: api, auth.token
- called by: Nadi-Tarangini-App saveManualNadiKeywords; Nadi-Tarangini-Frontend ManualNadiKeywordsController@saveKeywordsData (live_nadi.medical_assessment)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:562`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:566`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:570`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:574`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:578`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:592`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:603`); 400 "Data not saved. Invalid manual nadi" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:627`)

### POST report/saveMarkOnImage
- controller: MedicalReportSaveController@saveMarkOnImage (found) · route: `Ashoka-World-Backend:routes/api.php:1167` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:654`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:658`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:662`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:666`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:670`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:684`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:695`); 409 "Nadi already taken for this visit" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:700`)

### POST report/saveMarkOnImageUrl
- controller: MedicalReportSaveController@saveMarkOnImageUrl (found) · route: `Ashoka-World-Backend:routes/api.php:1168` · middleware: api, auth.token
- called by: Nadi-Tarangini-App saveMarkOnImage; Nadi-Tarangini-Frontend MarkOnImageController@saveMarkOnImageData (live_nadi.medical_assessment)
- validation: `mark_on_image`: image|mimes:jpeg,png,jpg (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10767`)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10704`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10708`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10712`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10716`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10720`); 400 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10734`); 400 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10745`); 400 "Image shouldn" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:10763`)

### POST report/savePrescriptionData
- controller: MedicalReportSaveController@savePreScription (found) · route: `Ashoka-World-Backend:routes/api.php:1174` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4572`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4575`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4579`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4583`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4587`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4601`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4606`); 400 "Invalid prescription data" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4611`)

### POST report/savePrescriptionDataV2
- controller: MedicalReportSaveController@savePrescriptionNew (found) · route: `Ashoka-World-Backend:routes/api.php:1175` · middleware: api, auth.token
- called by: Nadi-Tarangini-App savePrescription; Nadi-Tarangini-Frontend FeeDetailsController@savePrescriptionDataOnSaveFees; Nadi-Tarangini-Frontend PrescriptionController@savePrescriptionData (live_nadi.medical_assessment)
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5562`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5565`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5569`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5573`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5577`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5582`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5594`); 400 "Invalid prescription data" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:5600`)

### POST report/saveRecommendations
- controller: MedicalReportSaveController@saveRecommendations (found) · route: `Ashoka-World-Backend:routes/api.php:1206` · middleware: api, auth.token
- called by: Nadi-Tarangini-App saveRecommendations; Nadi-Tarangini-Frontend PrescriptionController@saveRecommendationData (medical_assessment.medical_assesment)
- errors: 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12284`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12292`); 400 "Invalid medical report" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12304`); 400 "Invalid recommendations" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12314`); 400 "Invalid type" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12332`); ? "Recommendations saved successfully" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12345`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12354`)

### POST report/saveSinglePrescription
- controller: MedicalReportSaveController@saveSinglePrescription (found) · route: `Ashoka-World-Backend:routes/api.php:1182` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6293`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6296`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6300`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6304`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6308`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6313`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6326`); 400 "Invalid prescription data" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:6332`)

### POST report/saveSinglePrescriptionV2
- controller: MedicalReportSaveController@saveSinglePrescriptionV2 (found) · route: `Ashoka-World-Backend:routes/api.php:1183` · middleware: api, auth.token
- called by: Nadi-Tarangini-App saveSinglePrescription (AddMedicinePrescription); Nadi-Tarangini-Frontend PrescriptionController@savePrescriptionDataV2 (live_nadi.medical_assessment, medical_assessment.medical_assesment)
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7058`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7061`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7065`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7069`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7073`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7078`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7092`); 400 "Invalid prescription data" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7098`)

### POST report/saveSinglePrescriptionV3
- controller: MedicalReportSaveController@saveSinglePrescriptionV3 (found) · route: `Ashoka-World-Backend:routes/api.php:1184` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend PrescriptionController@savePrescriptionDataV3 (auth.nt-lite.nt_lite_patient_report)
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7930`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7935`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7940`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7945`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7950`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7957`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7971`); 400 "Invalid prescription data" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:7977`)

### POST report/saveVikrutiQuestions
- controller: MedicalReportSaveController@saveVikrutiQuestions (found) · route: `Ashoka-World-Backend:routes/api.php:1160` · middleware: api, auth.token
- called by: Nadi-Tarangini-App savePatientDetails (MainAssessmentScreen); Nadi-Tarangini-Frontend VikrutiController@saveVikrutiData; Nadi-Tarangini-Frontend VikrutiController@saveVikrutiDataV2 (appointment.appointment_list, live_nadi.medical_assessment)
- errors: 400 "Symptom is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:281`); 400 "Invalid symptom data" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:285`); 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:289`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:293`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:297`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:301`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:305`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:319`)

### POST report/updateSinglePrescription
- controller: MedicalReportSaveController@updateSinglePrescription (found) · route: `Ashoka-World-Backend:routes/api.php:1186` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8317`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8321`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8325`); 400 "Medicine/herb prescription id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8329`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8333`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8338`); 400 "Invalid medicine/herb prescription id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8342`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8348`)

### POST report/updateSinglePrescriptionV2
- controller: MedicalReportSaveController@updateSinglePrescriptionV2 (found) · route: `Ashoka-World-Backend:routes/api.php:1187` · middleware: api, auth.token
- called by: Nadi-Tarangini-App updateSinglePrescription (EditMedicinePrescription); Nadi-Tarangini-Frontend PrescriptionController@updatePrescriptionDataV2 (medical_assessment.medical_assesment)
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9329`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9333`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9337`); 400 "Medicine/herb prescription id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9341`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9345`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9350`); 400 "Invalid medicine/herb prescription id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9354`); 400 "Invalid medicine/herb prescription id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:9367`)

### POST report/updateSinglePrescriptionV3
- controller: MedicalReportSaveController@updateSinglePrescriptionV3 (found) · route: `Ashoka-World-Backend:routes/api.php:1185` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend PrescriptionController@updatePrescriptionDataV3 (auth.nt-lite.nt_lite_patient_report)
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8112`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8117`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8122`); 400 "Medicine/herb prescription id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8127`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8132`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8137`); 400 "Invalid medicine/herb prescription id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8142`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:8149`)

### POST report/updateWeeklyDiet
- controller: MedicalReportSaveController@updateWeeklyDiet (found) · route: `Ashoka-World-Backend:routes/api.php:1212` · middleware: api, auth.token
- called by: Nadi-Tarangini-App updateWeeklyDiet
- errors: 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12715`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12723`); 400 "Weekly diet must be an array with at least 7 items" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12733`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12745`); 400 "No weekly diet found for the given medical ID" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12759`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12780`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12789`)

### POST report/updateYogaPlanner
- controller: MedicalReportSaveController@updateYogaPlanner (found) · route: `Ashoka-World-Backend:routes/api.php:1219` · middleware: api, auth.token
- called by: Nadi-Tarangini-App updateYogaPlanner
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13071`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13079`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13087`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13095`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13103`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13121`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13135`); 400 "Yoga planner data must be an array" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13148`)

### POST report/visitWiseAllowedReports
- controller: MedicalReportSaveController@visitWiseAllowedReports (found) · route: `Ashoka-World-Backend:routes/api.php:1205` · middleware: api, auth.token
- called by: Nadi-Tarangini-App deleteReportForDoctor (ReportScreen); Nadi-Tarangini-Frontend AdminDashboardController@viewAllReport (admin.all_report_view, admin.user_previous_visits); Nadi-Tarangini-Frontend NtLiteDashboardController@getVisitReports; Nadi-Tarangini-Frontend NtLiteLiveNadiController@fetchAllowedReportsData; Nadi-Tarangini-Frontend ReportController@viewAllReportV2 (allReportView, patient.previousVisits)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12088`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12092`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12096`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12110`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12255`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12266`)

### POST updateYogaPlannerPublic
- controller: MedicalReportSaveController@updateYogaPlannerPublic (found) · route: `Ashoka-World-Backend:routes/api.php:779` · middleware: api
- called by: no screen in this workspace
- errors: 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13284`); 400 "Yoga planner data must be an array" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13294`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13395`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:13403`)

### POST v2/report/fetchNewVisitCategoryWiseQuestions
- controller: MedicalReportSaveController@fetchNewVisitCategoryWiseQuestions (found) · route: `Ashoka-World-Backend:routes/api.php:1665` · middleware: auth.token
- called by: Nadi-Tarangini-App fetchNewVisitCategoryWiseQuestions (FillPrakrutiScreen); Nadi-Tarangini-Frontend LiveNadiController@liveNadi (errors.expiredMedicalId, live_nadi.medical_assessment); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@getAllowedCaseStudySections; Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11766`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11770`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11774`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11780`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11803`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11966`)

### POST v2/report/fetchNewVisitInformation
- controller: MedicalReportSaveController@newVisitInfoV2 (found) · route: `Ashoka-World-Backend:routes/api.php:1653` · middleware: auth.token
- called by: Nadi-Tarangini-App getSymptomsList (FillPrakrutiScreen); Nadi-Tarangini-Frontend LiveNadiController@liveNadi (errors.expiredMedicalId, live_nadi.medical_assessment); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@ensureMedicalIdLocked; Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment); Nadi-Tarangini-Frontend VikrutiController@getVikrutiData (appointment.appointment_list, live_nadi.medical_assessment)
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1178`); `medical_id`: nullable|numeric (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1179`)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1170`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1174`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1221`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1245`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1394`)

### POST v2/report/getCurrentVisitInfo
- controller: MedicalReportSaveController@getCurrentVisitInfo (found) · route: `Ashoka-World-Backend:routes/api.php:1659` · middleware: auth.token
- called by: Nadi-Tarangini-App fetchCurrentVisitInfo (MainAssessmentScreen); Nadi-Tarangini-Frontend DietController@saveDietAndLifestyleNew (live_nadi.medical_assessment); Nadi-Tarangini-Frontend LiveNadiController@liveNadi (errors.expiredMedicalId, live_nadi.medical_assessment); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment); Nadi-Tarangini-Frontend NtLiteLiveNadiController@fetchCurrentVisitInfo; Nadi-Tarangini-Frontend PreviousVisitsController@resumeVisit (patient.patientlist)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11246`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11250`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11254`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11258`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11262`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11277`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11287`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11415`)

### POST v2/report/getCurrentVisitInputForDiet
- controller: MedicalReportSaveController@getCurrentVisitInputForDiet (found) · route: `Ashoka-World-Backend:routes/api.php:1657` · middleware: auth.token
- called by: Nadi-Tarangini-App getCurrentVisitInputForDiet (MainAssessmentScreen); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11439`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11447`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11455`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11463`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11471`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11489`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11503`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11637`)

### POST v2/report/getLastVisitInformation
- controller: MedicalReportSaveController@getLastVisitInformation (found) · route: `Ashoka-World-Backend:routes/api.php:1661` · middleware: auth.token
- called by: Nadi-Tarangini-App getLastVisitInformation (PatientScreen); Nadi-Tarangini-Frontend AdminDashboardController@fetchUserLastVisitInformation (admin.user_patient_list); Nadi-Tarangini-Frontend PatientListController@getLastVisitInformation (patient.patientlist)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11660`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11664`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11668`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11683`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11741`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11752`)

### POST v2/report/getLastVisitMandatoryQuesitons
- controller: MedicalReportSaveController@getLastVisitMandatoryQuesitons (found) · route: `Ashoka-World-Backend:routes/api.php:1663` · middleware: auth.token
- called by: Nadi-Tarangini-App getLastVisitMendaotryData (FillPrakrutiScreen, MainAssessmentScreen); Nadi-Tarangini-Frontend PatientListController@getLastVisitQuestions (appointment.appointment_list)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11977`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11981`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:11985`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12000`); 400 "Last nadi visit not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12019`); 400 "Last nadi visit not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12052`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12067`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:12076`)

### POST v2/report/getNewMedicalId
- controller: MedicalReportSaveController@getNewMedicalIdV2 (found) · route: `Ashoka-World-Backend:routes/api.php:1651` · middleware: auth.token
- called by: Nadi-Tarangini-App getMedicalId (MainAssessmentScreen); Nadi-Tarangini-Frontend PatientListController@fetchNewMedicalIdV2NtLite
- validation: `patient_id`: required (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1425`); `application_version_id`: required|integer (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1426`)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1409`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1413`); 400 "Application version id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1417`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1421`); 404 "Patient not found" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1477`); 404 "Invalid application version id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1501`); 500 "Failed to create medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1580`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:1587`)

### POST v2/report/getVikrutiWiseDietAndLifestyle
- controller: MedicalReportSaveController@getVikrutiWiseDietAndLifestyleV2 (found) · route: `Ashoka-World-Backend:routes/api.php:1654` · middleware: auth.token
- called by: Nadi-Tarangini-App savegetVikrutiWiseDiet; Nadi-Tarangini-Frontend DietController@getVikrutiWiseDietV2 (live_nadi.medical_assessment, medical_assessment.medical_assesment); Nadi-Tarangini-Frontend LiveNadiController@liveNadi (errors.expiredMedicalId, live_nadi.medical_assessment); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2209`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2213`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2217`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2221`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2225`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2240`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2252`); 400 "Nadi already taken for this visit" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:2256`)

### POST v2/report/saveDietAndLifestyleManually
- controller: MedicalReportSaveController@saveDietAndLifestyleMauallyV2 (found) · route: `Ashoka-World-Backend:routes/api.php:1655` · middleware: auth.token
- called by: no screen in this workspace
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3075`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3079`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3083`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3087`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3091`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3106`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3117`); 404 "Diet data is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3122`)

### POST zipFileNadiAnalysis
- controller: MedicalReportSaveController@zipFileNadiAnalysis (found) · route: `Ashoka-World-Backend:routes/api.php:966` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4056`); 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4060`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4064`); 400 "Clinic id is required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4068`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4072`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4076`); 400 "File required" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4080`); 400 "Only zip file is allowed" (`Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:4085`)

## Backend routes no screen calls

`POST external-capture/addReportData`, `POST generateLambda`, `POST getDietDataTest`, `POST getmedicineprescription`, `POST nadi/baselineCalculation`, `POST nadi/report`, `POST nadi/reportInfo`, `POST report/addMedicineForPrescriptionNewV3`, `POST report/deleteMedicineFromPrescriptionNewV3`, `POST report/fetchMarkOnImage`, `POST report/generateYogaPlanner`, `POST report/getLastPrescription`, `POST report/getMedicineFromPrescriptionNewV3`, `POST report/getStrotas`, `POST report/getVikrutiWiseDietAndLifestyle`, `POST report/newVisitQues`, `POST report/saveMarkOnImage`, `POST report/savePrescriptionData`, `POST report/saveSinglePrescription`, `POST report/updateSinglePrescription`, `POST updateYogaPlannerPublic`, `POST v2/report/saveDietAndLifestyleManually`, `POST zipFileNadiAnalysis`

## Web routes (53)

- Nadi-Tarangini-Frontend `POST addNewPrescriptionIngredient` → PrescriptionController@addNewPrescriptionIngredient · `Nadi-Tarangini-Frontend:routes/web.php:535` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `DELETE deleteMedicine/{medicalPrescriptionId}` → PrescriptionController@deleteMedicine · `Nadi-Tarangini-Frontend:routes/web.php:537` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET diet` → DietController@skipDiet · `Nadi-Tarangini-Frontend:routes/web.php:510` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET diet-lifestyle` → DietController@index · `Nadi-Tarangini-Frontend:routes/web.php:508` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST editMedicine/{medicalPrescriptionId}` → PrescriptionController@editMedicine · `Nadi-Tarangini-Frontend:routes/web.php:539` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET fee-details` → FeeDetailsController@index · `Nadi-Tarangini-Frontend:routes/web.php:543` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST fee-details/report-wise-languages` → FeeDetailsController@getReportWiseLanguages · `Nadi-Tarangini-Frontend:routes/web.php:545` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST fetchMarkOnImageData` → MarkOnImageController@fetchMarkOnImageData · `Nadi-Tarangini-Frontend:routes/web.php:492` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getManualNadiQuestions` → LiveNadiController@getManualNadiQuestions · `Nadi-Tarangini-Frontend:routes/web.php:412` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getMedicineNamesRespectToType` → PrescriptionController@getMedicineNamesRespectToType · `Nadi-Tarangini-Frontend:routes/web.php:523` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getPrakrutiData` → PrakrutiQuestionsController@getPrakrutiDataOnList · `Nadi-Tarangini-Frontend:routes/web.php:468` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getPrakrutiDataForNewPatient` → PrakrutiQuestionsController@getPrakrutiDataForNewPatient · `Nadi-Tarangini-Frontend:routes/web.php:469` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getVikrutiData` → VikrutiController@getVikrutiData · `Nadi-Tarangini-Frontend:routes/web.php:410` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getVikrutiWiseDiet` → DietController@getVikrutiWiseDietV2 · `Nadi-Tarangini-Frontend:routes/web.php:513` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET medical-assessment` → LiveNadiController@liveNadi · `Nadi-Tarangini-Frontend:routes/web.php:497` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET medical-assessment-v3` → MedicalAssessmentV3Controller@liveNadiV3 · `Nadi-Tarangini-Frontend:routes/web.php:554` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST medical-assessment-v3/diet/current` → MedicalAssessmentV3Controller@getCurrentVisitInputForDietV3 · `Nadi-Tarangini-Frontend:routes/web.php:559` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST medical-assessment-v3/diet/generate` → MedicalAssessmentV3Controller@generateWeeklyDietV3 · `Nadi-Tarangini-Frontend:routes/web.php:560` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST medical-assessment-v3/diet/update` → MedicalAssessmentV3Controller@updateWeeklyDietV3 · `Nadi-Tarangini-Frontend:routes/web.php:561` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST medical-assessment-v3/set-state` → MedicalAssessmentV3Controller@setMedicalAssessmentV3State · `Nadi-Tarangini-Frontend:routes/web.php:558` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST medical-assessment-v3/yoga/current` → MedicalAssessmentV3Controller@getCurrentVisitInputForYogaV3 · `Nadi-Tarangini-Frontend:routes/web.php:563` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST medical-assessment-v3/yoga/update` → MedicalAssessmentV3Controller@updateWeeklyYogaV3 · `Nadi-Tarangini-Frontend:routes/web.php:564` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET nadi-image` → MarkOnImageController@index · `Nadi-Tarangini-Frontend:routes/web.php:488` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET nadi-keywords` → ManualNadiKeywordsController@index · `Nadi-Tarangini-Frontend:routes/web.php:484` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET prakruti` → PrakrutiQuestionsController@index · `Nadi-Tarangini-Frontend:routes/web.php:466` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET prescription` → PrescriptionController@index · `Nadi-Tarangini-Frontend:routes/web.php:521` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST previousVisitsSymptomDetails` → VikrutiController@getSymptomHistory · `Nadi-Tarangini-Frontend:routes/web.php:414` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveCategoryWiseVikrutiData` → VikrutiController@saveCategoryWiseVikrutiData · `Nadi-Tarangini-Frontend:routes/web.php:482` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveDietAndLifestyle` → DietController@saveDietData · `Nadi-Tarangini-Frontend:routes/web.php:519` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveDietAndLifestyleNew` → DietController@saveDietAndLifestyleNew · `Nadi-Tarangini-Frontend:routes/web.php:517` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveDummyUsbNadiData` → LiveNadiController@saveDummyUsbNadiData · `Nadi-Tarangini-Frontend:routes/web.php:502` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveFeesData` → FeeDetailsController@saveFeesData · `Nadi-Tarangini-Frontend:routes/web.php:547` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveFeesDataAfterDiet` → DietController@saveFeesDataAfterDiet · `Nadi-Tarangini-Frontend:routes/web.php:551` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveFeesDataWithNA` → FeeDetailsController@saveFeesDataWithNA · `Nadi-Tarangini-Frontend:routes/web.php:549` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveKeywordsData` → ManualNadiKeywordsController@saveKeywordsData · `Nadi-Tarangini-Frontend:routes/web.php:486` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveMarkOnImageData` → MarkOnImageController@saveMarkOnImageData · `Nadi-Tarangini-Frontend:routes/web.php:490` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST savePrakrutiData` → PrakrutiQuestionsController@savePrakrutiData · `Nadi-Tarangini-Frontend:routes/web.php:475` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST savePrescriptionData` → PrescriptionController@savePrescriptionData · `Nadi-Tarangini-Frontend:routes/web.php:525` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST savePrescriptionDataV2` → PrescriptionController@savePrescriptionDataV2 · `Nadi-Tarangini-Frontend:routes/web.php:527` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST savePrescriptionDataV3` → PrescriptionController@savePrescriptionDataV3 · `Nadi-Tarangini-Frontend:routes/web.php:529` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveRecommendationData` → PrescriptionController@saveRecommendationData · `Nadi-Tarangini-Frontend:routes/web.php:541` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveUsbNadiData` → LiveNadiController@saveUsbNadiData · `Nadi-Tarangini-Frontend:routes/web.php:501` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveUsbNadiDataV3` → MedicalAssessmentV3Controller@saveUsbNadiDataV3 · `Nadi-Tarangini-Frontend:routes/web.php:567` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveVikrutiDataV2` → VikrutiController@saveVikrutiDataV2 · `Nadi-Tarangini-Frontend:routes/web.php:480` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveVirutiWiseDietAndLifestyle` → DietController@saveVikrutiWiseDietData · `Nadi-Tarangini-Frontend:routes/web.php:515` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST updateCurrentNadiTaranginiDevice` → LiveNadiController@updateCurrentNadiTaranginiDevice · `Nadi-Tarangini-Frontend:routes/web.php:742` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST updateCurrentNadiTaranginiDeviceV3` → MedicalAssessmentV3Controller@updateCurrentNadiTaranginiDeviceV3 · `Nadi-Tarangini-Frontend:routes/web.php:569` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST updateNadiCaptureType` → LiveNadiController@updateNadiCaptureType · `Nadi-Tarangini-Frontend:routes/web.php:499` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST updateNadiCaptureTypeV3` → MedicalAssessmentV3Controller@updateNadiCaptureTypeV3 · `Nadi-Tarangini-Frontend:routes/web.php:571` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST updatePrescriptionDataV2` → PrescriptionController@updatePrescriptionDataV2 · `Nadi-Tarangini-Frontend:routes/web.php:531` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST updatePrescriptionDataV3` → PrescriptionController@updatePrescriptionDataV3 · `Nadi-Tarangini-Frontend:routes/web.php:533` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST updateSessionNadiCaptureType` → MedicalAssessmentV3Controller@updateSessionNadiCaptureType · `Nadi-Tarangini-Frontend:routes/web.php:556` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET vikruti` → VikrutiController@index · `Nadi-Tarangini-Frontend:routes/web.php:477` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode

## Screens (7)

- Nadi-Tarangini-App **FillPrakrutiScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/nadi_flow_new/view/fill_prakruti_screen.dart` · route /fillPrakrutiScreen · goes to /assessmentScreen, /patientScreen
- Nadi-Tarangini-App **MainAssessmentScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/nadi_flow_new/view/main_assessment_screen.dart` · route /assessmentScreen
- Nadi-Tarangini-Frontend **errors.expiredMedicalId** `Nadi-Tarangini-Frontend:resources/views/errors/expiredMedicalId.blade.php` · route GET diet, GET diet-lifestyle, GET error, GET fee-details, GET medical-assessment, GET nadi-image, GET nadi-keywords, GET prakruti, GET prescription, GET vikruti · rendered by DietController@index, DietController@skipDiet, FeeDetailsController@index, LiveNadiController@liveNadi, ManualNadiKeywordsController@index, MarkOnImageController@index, PrakrutiQuestionsController@index, PrescriptionController@index, UnauthorizedController@error, VikrutiController@index · goes to /patientlist
- Nadi-Tarangini-Frontend **errors.expiredMedicalIdV3** `Nadi-Tarangini-Frontend:resources/views/errors/expiredMedicalIdV3.blade.php` · route GET medical-assessment-v3 · rendered by MedicalAssessmentV3Controller@liveNadiV3 · goes to /patientlist
- Nadi-Tarangini-Frontend **errors.limited_access** `Nadi-Tarangini-Frontend:resources/views/errors/limited_access.blade.php` · route GET vikruti · rendered by VikrutiController@index
- Nadi-Tarangini-Frontend **live_nadi.medical_assessment** `Nadi-Tarangini-Frontend:resources/views/live_nadi/medical_assessment.blade.php` · route GET medical-assessment · rendered by LiveNadiController@liveNadi
- Nadi-Tarangini-Frontend **medical_assessment.medical_assesment** `Nadi-Tarangini-Frontend:resources/views/medical_assessment/medical_assesment.blade.php` · route GET medical-assessment-v3 · rendered by MedicalAssessmentV3Controller@liveNadiV3

## API calls (192)

| Client | Caller | Call | Route | Status | Source |
|---|---|---|---|---|---|
| Nadi-Tarangini-App | deleteReportForDoctor | POST `/report/visitWiseAllowedReports` | POST report/visitWiseAllowedReports | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1907` |
| Nadi-Tarangini-App | deleteSinglePrescription | POST `/report/deleteSinglePrescription` | POST report/deleteSinglePrescription | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1990` |
| Nadi-Tarangini-App | fetchCurrentVisitInfo | POST `/v2/report/getCurrentVisitInfo` | POST v2/report/getCurrentVisitInfo | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1521` |
| Nadi-Tarangini-App | fetchManualNadiKeywords | POST `/report/fetchManualNadiKeywords` | POST report/fetchManualNadiKeywords | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1573` |
| Nadi-Tarangini-App | fetchMarkOnImage | POST `/report/fetchMarkOnImageUrl` | POST report/fetchMarkOnImageUrl | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1599` |
| Nadi-Tarangini-App | fetchNewVisitCategoryWiseQuestions | POST `/v2/report/fetchNewVisitCategoryWiseQuestions` | POST v2/report/fetchNewVisitCategoryWiseQuestions | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1586` |
| Nadi-Tarangini-App | fetchPreviousPrescriptions | POST `/medicalInventory/fetchPreviousPrescriptions` | POST medicalInventory/fetchPreviousPrescriptions | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1977` |
| Nadi-Tarangini-App | fetchPreviousVisitPrescriptions | POST `/medicalInventory/fetchLastVisitPrescriptions` | POST medicalInventory/fetchLastVisitPrescriptions | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1964` |
| Nadi-Tarangini-App | fetchReportLanguages | POST `/getReportWiseLanguages` | POST getReportWiseLanguages | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1215` |
| Nadi-Tarangini-App | fetchSingleMedicinePrescription | POST `/report/fetchSingleMedicinePrescription` | POST report/fetchSingleMedicinePrescription | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2004` |
| Nadi-Tarangini-App | generateWeeklyDiet | POST `/report/generateWeeklyDiet` | POST report/generateWeeklyDiet | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2342` |
| Nadi-Tarangini-App | getCurrentVisitInputForDiet | POST `/v2/report/getCurrentVisitInputForDiet` | POST v2/report/getCurrentVisitInputForDiet | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2291` |
| Nadi-Tarangini-App | getCurrentVisitInputForYogaPlanner | POST `/report/getCurrentVisitInputForYogaPlanner` | POST report/getCurrentVisitInputForYogaPlanner | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2415` |
| Nadi-Tarangini-App | getDietData | POST `/report/getDietAndLifestyle` | POST report/getDietAndLifestyle | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1366` |
| Nadi-Tarangini-App | getLastVisitInformation | POST `/v2/report/getLastVisitInformation` | POST v2/report/getLastVisitInformation | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2090` |
| Nadi-Tarangini-App | getLastVisitMendaotryData | POST `/v2/report/getLastVisitMandatoryQuesitons` | POST v2/report/getLastVisitMandatoryQuesitons | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1392` |
| Nadi-Tarangini-App | getMedicalId | POST `/v2/report/getNewMedicalId` | POST v2/report/getNewMedicalId | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:869` |
| Nadi-Tarangini-App | getMedicineTimings | POST `/medicalInventory/getMedicineTiming` | POST medicalInventory/getMedicineTiming | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1415` |
| Nadi-Tarangini-App | getMedicineWithComsume | POST `/medicalInventory/getMedicineWithComsume` | POST medicalInventory/getMedicineWithComsume | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1424` |
| Nadi-Tarangini-App | getPrakrutiQuestions | POST `/prakruti/fetchPrakrutiQuestions` | POST prakruti/fetchPrakrutiQuestions | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:583` |
| Nadi-Tarangini-App | getPrakrutiType | POST `/prakruti/getAllPrakrutiTypes` | POST prakruti/getAllPrakrutiTypes | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:599` |
| Nadi-Tarangini-App | getSymptomsList | POST `/v2/report/fetchNewVisitInformation` | POST v2/report/fetchNewVisitInformation | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:838` |
| Nadi-Tarangini-App | saveDietAndLifestyle | POST `/report/saveDietAndLifestyle` | POST report/saveDietAndLifestyle | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1433` |
| Nadi-Tarangini-App | saveDietAndLifestyleManually | POST `/report/saveDietAndLifestyleManually` | POST report/saveDietAndLifestyleManually | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1445` |
| Nadi-Tarangini-App | saveFeesDetails | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1481` |
| Nadi-Tarangini-App | saveManualNadiKeywords | POST `/report/saveManualNadi` | POST report/saveManualNadi | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1612` |
| Nadi-Tarangini-App | saveManualPrakruti | POST `/prakruti/saveManualPrakruti` | POST prakruti/saveManualPrakruti | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:627` |
| Nadi-Tarangini-App | saveMarkOnImage | POST `/report/saveMarkOnImageUrl` | POST report/saveMarkOnImageUrl | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1628` |
| Nadi-Tarangini-App | savePatientDetails | POST `/report/saveVikrutiQuestions` | POST report/saveVikrutiQuestions | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1270` |
| Nadi-Tarangini-App | savePrakrutiQuestions | POST `/prakruti/savePrakrutiQuestions` | POST prakruti/savePrakrutiQuestions | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:640` |
| Nadi-Tarangini-App | savePrescription | POST `/report/savePrescriptionDataV2` | POST report/savePrescriptionDataV2 | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1457` |
| Nadi-Tarangini-App | saveQuestionsTabData | POST `/report/saveCategoryWiseVikrutiQuestions` | POST report/saveCategoryWiseVikrutiQuestions | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1469` |
| Nadi-Tarangini-App | saveRecommendations | POST `/report/saveRecommendations` | POST report/saveRecommendations | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2056` |
| Nadi-Tarangini-App | saveSinglePrescription | POST `/report/saveSinglePrescriptionV2` | POST report/saveSinglePrescriptionV2 | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1952` |
| Nadi-Tarangini-App | savegetVikrutiWiseDiet | POST `/v2/report/getVikrutiWiseDietAndLifestyle` | POST v2/report/getVikrutiWiseDietAndLifestyle | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1352` |
| Nadi-Tarangini-App | updateSinglePrescription | POST `/report/updateSinglePrescriptionV2` | POST report/updateSinglePrescriptionV2 | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2018` |
| Nadi-Tarangini-App | updateWeeklyDiet | POST `/report/updateWeeklyDiet` | POST report/updateWeeklyDiet | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2354` |
| Nadi-Tarangini-App | updateYogaPlanner | POST `/report/updateYogaPlanner` | POST report/updateYogaPlanner | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2441` |
| Nadi-Tarangini-App | uploadNadiData | ? `/nadiDataAnalysis` | POST nadiDataAnalysis | matched | `Nadi-Tarangini-App:lib/common_files/api_services/http_api_service.dart:172` |
| Nadi-Tarangini-Frontend | AdminDashboardController@fetchUserLastVisitInformation | POST `/v2/report/getLastVisitInformation` | POST v2/report/getLastVisitInformation | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:855` |
| Nadi-Tarangini-Frontend | AdminDashboardController@viewAllReport | POST `/report/visitWiseAllowedReports` | POST report/visitWiseAllowedReports | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:710` |
| Nadi-Tarangini-Frontend | DietController@getVikrutiWiseDietV2 | POST `/v2/report/getVikrutiWiseDietAndLifestyle` | POST v2/report/getVikrutiWiseDietAndLifestyle | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:330` |
| Nadi-Tarangini-Frontend | DietController@index | POST `/report/getDietAndLifestyle` | POST report/getDietAndLifestyle | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:32` |
| Nadi-Tarangini-Frontend | DietController@saveDietAndLifestyleNew | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:643` |
| Nadi-Tarangini-Frontend | DietController@saveDietAndLifestyleNew | POST `/v2/report/getCurrentVisitInfo` | POST v2/report/getCurrentVisitInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:559` |
| Nadi-Tarangini-Frontend | DietController@saveDietData | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:128` |
| Nadi-Tarangini-Frontend | DietController@saveDietData | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:141` |
| Nadi-Tarangini-Frontend | DietController@saveDietData | POST `/report/saveDietAndLifestyle` | POST report/saveDietAndLifestyle | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:116` |
| Nadi-Tarangini-Frontend | DietController@saveFeesDataAfterDiet | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:269` |
| Nadi-Tarangini-Frontend | DietController@saveFeesDataAfterDiet | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:226` |
| Nadi-Tarangini-Frontend | DietController@saveFeesDataAfterDiet | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:239` |
| Nadi-Tarangini-Frontend | DietController@saveVikrutiWiseDietData | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:477` |
| Nadi-Tarangini-Frontend | DietController@saveVikrutiWiseDietData | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:490` |
| Nadi-Tarangini-Frontend | DietController@saveVikrutiWiseDietData | POST `/report/saveDietAndLifestyleManually` | POST report/saveDietAndLifestyleManually | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:462` |
| Nadi-Tarangini-Frontend | FeeDetailsController@getReportWiseLanguages | POST `/getReportWiseLanguages` | POST getReportWiseLanguages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:129` |
| Nadi-Tarangini-Frontend | FeeDetailsController@index | POST `/fetchUserInfo` | POST fetchUserInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:89` |
| Nadi-Tarangini-Frontend | FeeDetailsController@index | POST `/getLanguages` | POST getLanguages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:98` |
| Nadi-Tarangini-Frontend | FeeDetailsController@index | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:78` |
| Nadi-Tarangini-Frontend | FeeDetailsController@saveFeesData | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:255` |
| Nadi-Tarangini-Frontend | FeeDetailsController@saveFeesData | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:230` |
| Nadi-Tarangini-Frontend | FeeDetailsController@saveFeesDataWithNA | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:398` |
| Nadi-Tarangini-Frontend | FeeDetailsController@saveFeesDataWithNA | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:346` |
| Nadi-Tarangini-Frontend | FeeDetailsController@savePrescriptionDataOnSaveFees | POST `/report/savePrescriptionDataV2` | POST report/savePrescriptionDataV2 | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:480` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/appointment/dateWiseAppointment` | POST appointment/dateWiseAppointment | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:310` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | ? `/arogyaDarshika` | GET arogyaDarshika | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:412` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/fetchUserInfo` | POST fetchUserInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:357` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/getLanguages` | POST getLanguages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:366` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/getLinkDevice` | POST getLinkDevice | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:47` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:420` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:292` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/medicalInventory/fetchLastVisitPrescriptions` | POST medicalInventory/fetchLastVisitPrescriptions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:536` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/medicalInventory/fetchPreviousPrescriptions` | POST medicalInventory/fetchPreviousPrescriptions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:520` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | GET `/medicalInventory/getAllIngredient` | GET medicalInventory/getAllIngredient | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:551` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | GET `/medicalInventory/getAllMedicine` | GET medicalInventory/getAllMedicine | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:234` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | GET `/medicalInventory/getAllPudi` | GET medicalInventory/getAllPudi | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:577` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | GET `/medicalInventory/getAllQuantity` | GET medicalInventory/getAllQuantity | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:252` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/medicalInventory/getMedicineTiming` | POST medicalInventory/getMedicineTiming | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:266` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/medicalInventory/getMedicineWithComsume` | POST medicalInventory/getMedicineWithComsume | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:273` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/medicalInventory/prescriptionInfo` | POST medicalInventory/prescriptionInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:217` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | ? `/nadiTaranginiReport` | GET nadiTaranginiReport | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:407` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:345` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/report/fetchManualNadiKeywords` | POST report/fetchManualNadiKeywords | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:138` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/report/fetchMarkOnImageUrl` | POST report/fetchMarkOnImageUrl | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:382` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/report/getDietAndLifestyle` | POST report/getDietAndLifestyle | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:159` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/report/getPudiIngredient` | POST report/getPudiIngredient | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:227` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/v2/report/fetchNewVisitCategoryWiseQuestions` | POST v2/report/fetchNewVisitCategoryWiseQuestions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:199` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/v2/report/fetchNewVisitInformation` | POST v2/report/fetchNewVisitInformation | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:103` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/v2/report/getCurrentVisitInfo` | POST v2/report/getCurrentVisitInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:180` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/v2/report/getVikrutiWiseDietAndLifestyle` | POST v2/report/getVikrutiWiseDietAndLifestyle | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:442` |
| Nadi-Tarangini-Frontend | LiveNadiController@saveUsbNadiData | POST `/nadiDataAnalysis` | POST nadiDataAnalysis | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:790` |
| Nadi-Tarangini-Frontend | ManualNadiKeywordsController@index | POST `/report/fetchManualNadiKeywords` | POST report/fetchManualNadiKeywords | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/ManualNadiKeywordsController.php:32` |
| Nadi-Tarangini-Frontend | ManualNadiKeywordsController@saveKeywordsData | POST `/report/saveManualNadi` | POST report/saveManualNadi | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/ManualNadiKeywordsController.php:79` |
| Nadi-Tarangini-Frontend | MarkOnImageController@index | POST `/report/fetchMarkOnImageUrl` | POST report/fetchMarkOnImageUrl | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MarkOnImageController.php:35` |
| Nadi-Tarangini-Frontend | MarkOnImageController@saveMarkOnImageData | POST `/report/saveMarkOnImageUrl` | POST report/saveMarkOnImageUrl | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MarkOnImageController.php:106` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@ensureMedicalIdLocked | POST `/report/getNewMedicalId` | POST report/getNewMedicalId | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:327` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@ensureMedicalIdLocked | POST `/v2/report/fetchNewVisitInformation` | POST v2/report/fetchNewVisitInformation | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:303` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@getAllowedCaseStudySections | POST `/v2/report/fetchNewVisitCategoryWiseQuestions` | POST v2/report/fetchNewVisitCategoryWiseQuestions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:124` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/appointment/dateWiseAppointment` | POST appointment/dateWiseAppointment | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1052` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/fetchUserInfo` | POST fetchUserInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1095` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:732` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/getLanguages` | POST getLanguages | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1104` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/getLinkDevice` | POST getLinkDevice | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:479` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1333` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1034` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/medicalInventory/fetchLastVisitPrescriptions` | POST medicalInventory/fetchLastVisitPrescriptions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1207` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/medicalInventory/fetchPreviousPrescriptions` | POST medicalInventory/fetchPreviousPrescriptions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1192` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | GET `/medicalInventory/getAllIngredient` | GET medicalInventory/getAllIngredient | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1222` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | GET `/medicalInventory/getAllMedicine` | GET medicalInventory/getAllMedicine | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:808` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | GET `/medicalInventory/getAllPudi` | GET medicalInventory/getAllPudi | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1248` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | GET `/medicalInventory/getAllQuantity` | GET medicalInventory/getAllQuantity | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:812` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/medicalInventory/getAllSupplimentMedicineTypes` | POST medicalInventory/getAllSupplimentMedicineTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1321` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/medicalInventory/getMedicineTiming` | POST medicalInventory/getMedicineTiming | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:816` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/medicalInventory/getMedicineWithComsume` | POST medicalInventory/getMedicineWithComsume | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:822` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/medicalInventory/prescriptionInfo` | POST medicalInventory/prescriptionInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:795` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1083` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/report/fetchManualNadiKeywords` | POST report/fetchManualNadiKeywords | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:617` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/report/fetchMarkOnImageUrl` | POST report/fetchMarkOnImageUrl | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1115` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/report/getDietAndLifestyle` | POST report/getDietAndLifestyle | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1161` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/report/getPudiIngredient` | POST report/getPudiIngredient | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:802` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/report/getTypeWiseFeatureDetails` | POST report/getTypeWiseFeatureDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1261` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/v2/report/fetchNewVisitCategoryWiseQuestions` | POST v2/report/fetchNewVisitCategoryWiseQuestions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:756` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/v2/report/fetchNewVisitInformation` | POST v2/report/fetchNewVisitInformation | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:572` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/v2/report/getCurrentVisitInfo` | POST v2/report/getCurrentVisitInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:659` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/v2/report/getCurrentVisitInputForDiet` | POST v2/report/getCurrentVisitInputForDiet | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:686` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/v2/report/getVikrutiWiseDietAndLifestyle` | POST v2/report/getVikrutiWiseDietAndLifestyle | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1151` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@saveUsbNadiDataV3 | POST `/nadiDataAnalysis` | POST nadiDataAnalysis | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1852` |
| Nadi-Tarangini-Frontend | NtLiteDashboardController@getVisitReports | POST `/report/visitWiseAllowedReports` | POST report/visitWiseAllowedReports | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteDashboardController.php:393` |
| Nadi-Tarangini-Frontend | NtLiteLiveNadiController@fetchAllowedReportsData | POST `/report/visitWiseAllowedReports` | POST report/visitWiseAllowedReports | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteLiveNadiController.php:171` |
| Nadi-Tarangini-Frontend | NtLiteLiveNadiController@fetchCurrentVisitInfo | POST `/v2/report/getCurrentVisitInfo` | POST v2/report/getCurrentVisitInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteLiveNadiController.php:421` |
| Nadi-Tarangini-Frontend | PatientListController@fetchNewMedicalIdV2 | POST `/report/getNewMedicalId` | POST report/getNewMedicalId | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:166` |
| Nadi-Tarangini-Frontend | PatientListController@fetchNewMedicalIdV2NtLite | POST `/v2/report/getNewMedicalId` | POST v2/report/getNewMedicalId | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:220` |
| Nadi-Tarangini-Frontend | PatientListController@getLastVisitInformation | POST `/v2/report/getLastVisitInformation` | POST v2/report/getLastVisitInformation | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:661` |
| Nadi-Tarangini-Frontend | PatientListController@getLastVisitQuestions | POST `/v2/report/getLastVisitMandatoryQuesitons` | POST v2/report/getLastVisitMandatoryQuesitons | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:626` |
| Nadi-Tarangini-Frontend | PrakrutiQuestionsController@getPrakrutiDataForNewPatient | POST `/prakruti/fetchPrakrutiQuestionsNtLite` | POST prakruti/fetchPrakrutiQuestionsNtLite | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrakrutiQuestionsController.php:317` |
| Nadi-Tarangini-Frontend | PrakrutiQuestionsController@getPrakrutiDataForNewPatient | POST `/prakruti/getAllPrakrutiTypes` | POST prakruti/getAllPrakrutiTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrakrutiQuestionsController.php:302` |
| Nadi-Tarangini-Frontend | PrakrutiQuestionsController@getPrakrutiDataOnList | POST `/prakruti/fetchPrakrutiQuestions` | POST prakruti/fetchPrakrutiQuestions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrakrutiQuestionsController.php:255` |
| Nadi-Tarangini-Frontend | PrakrutiQuestionsController@getPrakrutiDataOnList | POST `/prakruti/getAllPrakrutiTypes` | POST prakruti/getAllPrakrutiTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrakrutiQuestionsController.php:227` |
| Nadi-Tarangini-Frontend | PrakrutiQuestionsController@index | POST `/appointment/dateWiseAppointment` | POST appointment/dateWiseAppointment | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrakrutiQuestionsController.php:55` |
| Nadi-Tarangini-Frontend | PrakrutiQuestionsController@index | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrakrutiQuestionsController.php:37` |
| Nadi-Tarangini-Frontend | PrakrutiQuestionsController@index | POST `/prakruti/fetchPrakrutiQuestions` | POST prakruti/fetchPrakrutiQuestions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrakrutiQuestionsController.php:104` |
| Nadi-Tarangini-Frontend | PrakrutiQuestionsController@index | POST `/prakruti/getAllPrakrutiTypes` | POST prakruti/getAllPrakrutiTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrakrutiQuestionsController.php:86` |
| Nadi-Tarangini-Frontend | PrakrutiQuestionsController@savePrakrutiData | ? `/prakruti/saveManualPrakruti` | POST prakruti/saveManualPrakruti | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrakrutiQuestionsController.php:138` |
| Nadi-Tarangini-Frontend | PrakrutiQuestionsController@savePrakrutiData | ? `/prakruti/savePrakrutiQuestions` | POST prakruti/savePrakrutiQuestions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrakrutiQuestionsController.php:138` |
| Nadi-Tarangini-Frontend | PrescriptionController@addNewPrescriptionIngredient | POST `/medicalInventory/addNewPrescriptionIngredient` | POST medicalInventory/addNewPrescriptionIngredient | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:637` |
| Nadi-Tarangini-Frontend | PrescriptionController@addNewPrescriptionIngredient | GET `/medicalInventory/getAllIngredient` | GET medicalInventory/getAllIngredient | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:683` |
| Nadi-Tarangini-Frontend | PrescriptionController@deleteMedicine | POST `/report/deleteSinglePrescription` | POST report/deleteSinglePrescription | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:116` |
| Nadi-Tarangini-Frontend | PrescriptionController@editMedicine | POST `/report/fetchSingleMedicinePrescription` | POST report/fetchSingleMedicinePrescription | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:141` |
| Nadi-Tarangini-Frontend | PrescriptionController@getMedicineNamesRespectToType | POST `/medicalInventory/getMedicineNamesRespectToType` | POST medicalInventory/getMedicineNamesRespectToType | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:609` |
| Nadi-Tarangini-Frontend | PrescriptionController@index | GET `/medicalInventory/getAllMedicine` | GET medicalInventory/getAllMedicine | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:54` |
| Nadi-Tarangini-Frontend | PrescriptionController@index | GET `/medicalInventory/getAllQuantity` | GET medicalInventory/getAllQuantity | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:72` |
| Nadi-Tarangini-Frontend | PrescriptionController@index | POST `/medicalInventory/getMedicineTiming` | POST medicalInventory/getMedicineTiming | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:86` |
| Nadi-Tarangini-Frontend | PrescriptionController@index | POST `/medicalInventory/getMedicineWithComsume` | POST medicalInventory/getMedicineWithComsume | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:93` |
| Nadi-Tarangini-Frontend | PrescriptionController@index | POST `/medicalInventory/prescriptionInfo` | POST medicalInventory/prescriptionInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:37` |
| Nadi-Tarangini-Frontend | PrescriptionController@index | POST `/report/getPudiIngredient` | POST report/getPudiIngredient | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:47` |
| Nadi-Tarangini-Frontend | PrescriptionController@savePrescriptionData | POST `/report/savePrescriptionDataV2` | POST report/savePrescriptionDataV2 | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:250` |
| Nadi-Tarangini-Frontend | PrescriptionController@savePrescriptionDataV2 | POST `/report/saveSinglePrescriptionV2` | POST report/saveSinglePrescriptionV2 | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:325` |
| Nadi-Tarangini-Frontend | PrescriptionController@savePrescriptionDataV3 | POST `/report/saveSinglePrescriptionV3` | POST report/saveSinglePrescriptionV3 | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:385` |
| Nadi-Tarangini-Frontend | PrescriptionController@saveRecommendationData | POST `/report/saveRecommendations` | POST report/saveRecommendations | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:759` |
| Nadi-Tarangini-Frontend | PrescriptionController@updatePrescriptionDataV2 | POST `/report/updateSinglePrescriptionV2` | POST report/updateSinglePrescriptionV2 | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:445` |
| Nadi-Tarangini-Frontend | PrescriptionController@updatePrescriptionDataV3 | POST `/report/updateSinglePrescriptionV3` | POST report/updateSinglePrescriptionV3 | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrescriptionController.php:506` |
| Nadi-Tarangini-Frontend | PreviousVisitsController@resumeVisit | POST `/v2/report/getCurrentVisitInfo` | POST v2/report/getCurrentVisitInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:231` |
| Nadi-Tarangini-Frontend | ReportController@viewAllReportV2 | POST `/report/visitWiseAllowedReports` | POST report/visitWiseAllowedReports | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/ReportController.php:116` |
| Nadi-Tarangini-Frontend | VikrutiController@getSymptomHistory | POST `/patient/previousVisitsDetails` | POST patient/previousVisitsDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/VikrutiController.php:186` |
| Nadi-Tarangini-Frontend | VikrutiController@getVikrutiData | POST `/v2/report/fetchNewVisitInformation` | POST v2/report/fetchNewVisitInformation | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/VikrutiController.php:136` |
| Nadi-Tarangini-Frontend | VikrutiController@index | POST `/report/fetchNewVisitInformation` | POST report/fetchNewVisitInformation | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/VikrutiController.php:73` |
| Nadi-Tarangini-Frontend | VikrutiController@index | POST `/report/getNewMedicalId` | POST report/getNewMedicalId | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/VikrutiController.php:38` |
| Nadi-Tarangini-Frontend | VikrutiController@saveCategoryWiseVikrutiData | POST `/report/saveCategoryWiseVikrutiQuestions` | POST report/saveCategoryWiseVikrutiQuestions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/VikrutiController.php:404` |
| Nadi-Tarangini-Frontend | VikrutiController@saveVikrutiData | POST `/report/saveVikrutiQuestions` | POST report/saveVikrutiQuestions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/VikrutiController.php:339` |
| Nadi-Tarangini-Frontend | VikrutiController@saveVikrutiDataV2 | POST `/report/saveVikrutiQuestions` | POST report/saveVikrutiQuestions | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/VikrutiController.php:285` |

## Tables (38)

- `all_country_names` (models: AllCountryNames): country_code, postal_code_lengths, postal_code_type
- `all_prakruti_types` (models: AllPrakrutiTypes): columns not in migrations
- `calendar_events` (models: CalendarEvent): clinic_id, consultation_type, reception_id
- `doctor_medicine_inventory` (models: DoctorMedicineInventory): is_active
- `doctor_multichoice_options` (models: DoctorMultichoiceOption): columns not in migrations
- `ingredients_list` (models: Ingredient): columns not in migrations
- `languages` (models: Languages): columns not in migrations
- `locality_info` (models: LocalityInfo): is_default, timezone
- `major_symptom_data` (models: MajorSymptomData): gender, symptom_category_tag
- `medical_report` (models: MedicalReport): city, country, external_visit_id, field_id_1, ip_address, mark_on_image_url, panchakarma_recom, reception_id, recommendations, state, try_count, user_nadi_capture_type, yoga_recom
- `medical_report_diet` (models: MedicalReportDiet): create_date, diet, doctor_id, id, is_active, last_modified_on, medical_id, patient_id, vikruti_type
- `medical_report_image_markers` (models: MedicalReportImageMarker): columns not in migrations
- `medical_report_prescription` (models: MedicalReportPrescription): is_active, other_details, total_quantity
- `medical_report_symptom_details_1` (models: MedicalReportSymptomDetail): symptom_value
- `medicine_company` (models: MedicineCompany): is_active
- `medicine_names` (models: MedicineNames): create_date, created_by, id, is_active, last_modified_on, medicine_name, medicine_type
- `medicine_timing` (models: MedicineTiming): create_date, id, is_active, last_modified_on, order_by, timing_label
- `medicine_type` (models: MedicineType): is_active, type
- `medicine_with_consume` (models: MedicineWithConsume): consume_label, create_date, created_by, id, is_active, last_modified_on
- `multichoice_field_list` (models: MultichoiceFieldList): columns not in migrations
- `multichoice_options` (models: MultichoiceOptions): lang_kannda
- `nadi_average_pulse_data` (models: NadiAveragePulseData): lang_kannada
- `nadi_report` (models: NadiReport): columns not in migrations
- `nt_application_version` (models: NTApplicationVersion): columns not in migrations
- `other_report_data` (models: OtherReportData): create_date, id, is_active, last_modified_on, medical_id, report_data, sub_title, title
- `patient_prakruti` (models: PatientPrakruti): columns not in migrations
- `pg_device_list` (models: PgDeviceList): created_by, device_type, is_linkable, is_usable, serial_no, status, track_status
- `pg_device_mapping` (models: PgDeviceMapping): columns not in migrations
- `prakruti_wise_diet` (models: PrakrutiWiseDiet): columns not in migrations
- `project_variables` (models: ProjectVariable): columns not in migrations
- `resource_name_master` (models: ResourceNameMaster): endpoint, is_default, no_of_pages, order_by, title
- `symptom_category` (models: SymptomCategory): is_active
- `symptoms` (models: Symptoms): is_active
- `symptoms_dropdown_item` (models: SymptomsDropdownItem): columns not in migrations
- `user_personal_info` (models: UserPersonalInfo): allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken
- `user_report` (models: UserReport): symptom_prediction
- `user_selected_countries` (models: UserSelectedCountry): columns not in migrations
- `yoga_report_data` (models: YogaReportData): columns not in migrations

## External systems

- AWS Lambda / API Gateway (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3557,3798,3799`
- S3 (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/MedicalReportSaveController.php:3534,3639,3682`, `Ashoka-World-Backend:app/Http/Controllers/PrakrutiController.php:121,188,221`
- S3 (Nadi-Tarangini-Frontend): `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:842,843`

## Environment matrix (verbatim from atreya-docs/environments.md)

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

## Languages

Required: English, Marathi, Hindi, Czech, German, Spanish, Italian (source: references/qa-scope-rules.md).
Language files in code: Nadi-Tarangini-Frontend:resources/lang/en/auth.php, Nadi-Tarangini-Frontend:resources/lang/en/pagination.php, Nadi-Tarangini-Frontend:resources/lang/en/passwords.php, Nadi-Tarangini-Frontend:resources/lang/en/validation.php, Nadi-Tarangini-Frontend:resources/lang/en_patient.json
