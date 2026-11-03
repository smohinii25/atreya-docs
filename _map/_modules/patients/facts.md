# Fact pack: patients (Patients)

Generated 2026-11-03 by scripts/module-facts.sh. Product nt, critical false. Every line below is from code or a human-owned doc; cite the source given.

Commits: Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`, Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`, Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d`

## Backend routes (32)

### POST accessUserWisePatientList
- controller: PatientDetailsController@accessUserWisePatientList (found) · route: `Ashoka-World-Backend:routes/api.php:933` · middleware: api, auth.token
- called by: Nadi-Tarangini-App accessUserWisePatientList (AddAppointmentScreen); Nadi-Tarangini-Frontend AppointmentController@getAccessUserWisePatientList (appointment.add-appointment)
- errors: 400 "Invalid user id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4662`); ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4693`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4702`)

### GET checkpatientcode
- controller: CheckUserExistOrNotController@checkPatientCode (found) · route: `Ashoka-World-Backend:routes/api.php:996` · middleware: api, auth.token
- called by: no screen in this workspace
- validation: `patient_code`: required|string (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:88`); `doctor_id`: required|integer (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:89`)

### POST fetchPatientNames
- controller: PatientDetailsController@fetchPatientNames (found) · route: `Ashoka-World-Backend:routes/api.php:931` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getPatientList (AddAppointmentScreen); Nadi-Tarangini-Frontend AppointmentController@addAppointment (appointment.add-appointment)
- errors: ? "Success" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4638`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4647`)

### GET getAllCountries
- controller: PatientDetailsController@getAllCountries (found) · route: `Ashoka-World-Backend:routes/api.php:766` · middleware: api
- called by: Nadi-Tarangini-App fetchCountryList (AddClinicScreen, AddPatientFromAppointmentScreen, AddPatientScreen, EditClinicScreen)
- errors: 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:627`)

### POST getAllCountries
- controller: PatientDetailsController@getAllCountries (found) · route: `Ashoka-World-Backend:routes/api.php:766` · middleware: api
- called by: Nadi-Tarangini-Frontend AddClinicDetailsController@addClinicDetails (my_account.addClinicDetails); Nadi-Tarangini-Frontend AddMemberController@index (errors.410, patient.add-member); Nadi-Tarangini-Frontend AdminDashboardController@createUser (admin.create_user); Nadi-Tarangini-Frontend AdminDashboardController@editProfile (admin.edit_profile); Nadi-Tarangini-Frontend AppointmentController@addPatientForAppointment (appointment.add_patient_for_appointment); Nadi-Tarangini-Frontend DashboardController@addSelfAdmin (add_self_admin); Nadi-Tarangini-Frontend DashboardController@updateKycDetails (my_account.update_kyc); Nadi-Tarangini-Frontend EditClinicDetailsController@editClinicDetails (my_account.editClinicDetails); Nadi-Tarangini-Frontend EditDoctorDetailsController@editDoctorDetails (my_account.myaccount); Nadi-Tarangini-Frontend EditDoctorDetailsController@editDoctorProfile (my_account.edit_profile); Nadi-Tarangini-Frontend EditMemberController@index (patient.edit_member); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment); Nadi-Tarangini-Frontend NewSignUpController@adminSignUp (auth.admin_signUp); Nadi-Tarangini-Frontend NewSignUpController@collegeSignUp (auth.college_signUp); Nadi-Tarangini-Frontend NewSignUpController@doctorSignUp (auth.signup); Nadi-Tarangini-Frontend NtLiteDashboardController@index (auth.nt-lite.nt_lite_dashboard); Nadi-Tarangini-Frontend NtLiteDashboardController@previousVisits (auth.nt-lite.nt_lite_previous_visits); Nadi-Tarangini-Frontend NtLiteSignUpController@showSignUp (auth.nt_lite_signup); Nadi-Tarangini-Frontend PatientDashboardController@editProfile (patient-module.edit_profile); Nadi-Tarangini-Frontend ReceptionistController@addReception (receptionist.add-receptionist); Nadi-Tarangini-Frontend ReceptionistController@editReception (receptionist.edit-receptionist); Nadi-Tarangini-Frontend loginController@login (auth.login)
- errors: 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:627`)

### POST getAssociationsCount
- controller: PatientDetailsController@getAssociationsCount (found) · route: `Ashoka-World-Backend:routes/api.php:935` · middleware: api, auth.token
- called by: Nadi-Tarangini-Frontend DashboardController@index (doctor_dashboard.dashboard)
- errors: 401 "Unauthorized" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5166`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5197`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5211`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5219`)

### POST getLanguage
- controller: PatientDetailsController@fetchLanguageCode (found) · route: `Ashoka-World-Backend:routes/api.php:1423` · middleware: api
- called by: no screen in this workspace

### POST getLimitedActivePatients
- controller: PatientDetailsController@getLimitedActivePatients (found) · route: `Ashoka-World-Backend:routes/api.php:928` · middleware: api, auth.token
- called by: Nadi-Tarangini-App dashboardPatientList (DashboardScreen); Nadi-Tarangini-Frontend DashboardController@index (doctor_dashboard.dashboard)
- errors: 400 "User id is not provided." (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4019`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4300`)

### POST infinitePatientList
- controller: PatientDetailsController@infinitePatientList (found) · route: `Ashoka-World-Backend:routes/api.php:927` · middleware: api, auth.token
- called by: Nadi-Tarangini-App fetchPatientList (PatientScreen, VisitReportListScreen); Nadi-Tarangini-Frontend AddMemberController@saveAnonymousData (patient.add-member); Nadi-Tarangini-Frontend AddMemberController@saveMemberData (appointment.add_patient_for_appointment, auth.nt-lite.nt_lite_dashboard, auth.nt-lite.nt_lite_previous_visits, patient.add-member); Nadi-Tarangini-Frontend AdminDashboardController@fetchUserPatientList (admin.user_patient_list); Nadi-Tarangini-Frontend AdminDashboardController@userPatientList (admin.user_patient_list); Nadi-Tarangini-Frontend AdminDashboardController@userPreviousVisits (admin.user_previous_visits); Nadi-Tarangini-Frontend DietController@saveFeesDataAfterDiet; Nadi-Tarangini-Frontend EditMemberController@updatetMemberData (patient.edit_member); Nadi-Tarangini-Frontend FeeDetailsController@saveFeesData; Nadi-Tarangini-Frontend FeeDetailsController@saveFeesDataWithNA; Nadi-Tarangini-Frontend LiveNadiController@liveNadi (errors.expiredMedicalId, live_nadi.medical_assessment); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment); Nadi-Tarangini-Frontend NtLiteDashboardController@callPatientList; Nadi-Tarangini-Frontend NtLiteDashboardController@index (auth.nt-lite.nt_lite_dashboard); Nadi-Tarangini-Frontend NtLiteDashboardController@previousVisits (auth.nt-lite.nt_lite_previous_visits); Nadi-Tarangini-Frontend NtLiteLiveNadiController@resolvePatient; Nadi-Tarangini-Frontend PatientListController@callPatientList (patient.patientlist); Nadi-Tarangini-Frontend PatientListController@deletePatient (patient.patientlist, patient.view_member); Nadi-Tarangini-Frontend PatientListController@getPatientListData; Nadi-Tarangini-Frontend PatientListController@index (patient.patientlist); Nadi-Tarangini-Frontend PrakrutiQuestionsController@index (errors.expiredMedicalId); Nadi-Tarangini-Frontend PreviousVisitsController@index (patient.previousVisits)
- errors: 400 "User id is not provided." (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3725`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4007`)

### POST patient/add-new-symptom
- controller: PatientDetailsController@addNewSymptom (found) · route: `Ashoka-World-Backend:routes/api.php:1134` · middleware: api, auth.token
- called by: no screen in this workspace

### POST patient/addAnonymousClient
- controller: PatientDetailsController@addAnonymousClient (found) · route: `Ashoka-World-Backend:routes/api.php:1122` · middleware: api, auth.token
- called by: Nadi-Tarangini-App submitAnonymousPatient (AddPatientScreen); Nadi-Tarangini-Frontend AddMemberController@saveAnonymousData (patient.add-member)
- validation: `age`: nullable (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:669`); `dateofbirth`: nullable|date_format:Y-m-d|before_or_equal:today (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:670`); `nadi_consent`: required|integer|in:0,1 (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:671`); `report_consent`: required|integer|in:0,1 (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:672`); `share_report_consent`: required|integer|in:0,1 (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:673`)
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:658`); 400 "Client code is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:661`); 400 "Gender is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:664`); ? "Invalid email format" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:723`); 400 "Invalid date of birth" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:740`); 400 "Date of birth must be between 1 and 100 years old" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:743`); 400 "Invalid age" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:750`); 400 "Date of birth or age is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:754`)

### POST patient/addClient
- controller: PatientDetailsController@addNewClient (found) · route: `Ashoka-World-Backend:routes/api.php:1145` · middleware: api, auth.token
- called by: Nadi-Tarangini-App submitPatientDetails (AddPatientFromAppointmentScreen, AddPatientScreen, EditPatientScreen); Nadi-Tarangini-Frontend AddMemberController@saveMemberData (appointment.add_patient_for_appointment, auth.nt-lite.nt_lite_dashboard, auth.nt-lite.nt_lite_previous_visits, patient.add-member)
- validation: `firstname`: required|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:83`); `middlename`: nullable|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:84`); `lastname`: required|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:85`); `gender`: required|in:M,F,D,N (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:86`); `nadi_consent`: required|regex:/^[01]$/ (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:87`); `report_consent`: required|regex:/^[01]$/ (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:88`); `share_report_consent`: required|regex:/^[01]$/ (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:89`); `dateofbirth`: nullable|date_format:Y-m-d|before_or_equal:today (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:90`); `age`: nullable (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:91`); `profile_picture`: image|mimes:jpeg,png,jpg (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:397`)
- errors: ? "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:104`); ? "Date of birth cannot be a future date" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:134`); ? "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:169`); 400 "Invalid phone number format" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:182`); 400 "Invalid date of birth" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:198`); 400 "Date of birth must be between 1 and 100 years old" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:206`); 400 "Invalid age" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:218`); 400 "Date of birth or age is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:227`)

### POST patient/clinicDetails
- controller: PatientDetailsController@loadClinic (found) · route: `Ashoka-World-Backend:routes/api.php:1136` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 404 "doctor_id field is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3126`); 404 "Clinic data not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3160`)

### POST patient/deletePatient
- controller: PatientDetailsController@deletePatient (found) · route: `Ashoka-World-Backend:routes/api.php:1120` · middleware: api, auth.token
- called by: Nadi-Tarangini-App deletePatient (PatientScreen); Nadi-Tarangini-Frontend PatientListController@deletePatient (patient.patientlist, patient.view_member)
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4744`)
- errors: 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4778`); 200 "Patient deleted successfully" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4789`); 404 "Patient not found or not deleted" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4792`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4798`)

### POST patient/deletePatientQuery
- controller: PatientDetailsController@deletePatientQuery (found) · route: `Ashoka-World-Backend:routes/api.php:1140` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "Query id is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3314`); 400 "Enter valid query id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3318`); 400 "Enter valid query id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3328`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3334`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3340`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3347`)

### POST patient/deleteReport
- controller: PatientDetailsController@deleteVisitReport (found) · route: `Ashoka-World-Backend:routes/api.php:1118` · middleware: api, auth.token
- called by: Nadi-Tarangini-App deleteReportForDoctor (ReportScreen); Nadi-Tarangini-Frontend PreviousVisitsController@deleteReport
- errors: 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4966`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4969`); 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4973`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4977`); 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4987`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4998`); 200 "Report deleted successfully" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5007`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5013`)

### POST patient/getBannerList
- controller: PatientDetailsController@getBannerList (found) · route: `Ashoka-World-Backend:routes/api.php:1143` · middleware: api, auth.token
- called by: Nadi-Tarangini-App getBannerList; Nadi-Tarangini-Frontend DashboardController@index (doctor_dashboard.dashboard)
- errors: 404 "Banner and referal list not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3436`); ? "Get banners and referal list" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3443`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3454`)

### POST patient/getClientDetails
- controller: PatientDetailsController@getClientDetails (found) · route: `Ashoka-World-Backend:routes/api.php:1126` · middleware: api, auth.token
- called by: Nadi-Tarangini-App fetchPatientDetails (PatientScreen, ViewPatientScreen, VisitReportListScreen); Nadi-Tarangini-App fetchPatientDetailsAndNavigate (EditPatientScreen); Nadi-Tarangini-Frontend DietController@saveDietData; Nadi-Tarangini-Frontend DietController@saveFeesDataAfterDiet; Nadi-Tarangini-Frontend DietController@saveVikrutiWiseDietData; Nadi-Tarangini-Frontend EditMemberController@index (patient.edit_member); Nadi-Tarangini-Frontend FeeDetailsController@index (errors.expiredMedicalId); Nadi-Tarangini-Frontend LiveNadiController@liveNadi (errors.expiredMedicalId, live_nadi.medical_assessment); Nadi-Tarangini-Frontend MedicalAssessmentV3Controller@liveNadiV3 (errors.expiredMedicalIdV3, medical_assessment.medical_assesment); Nadi-Tarangini-Frontend ViewMemberController@index (patient.view_member)
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:896`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:899`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:902`); 404 "Client not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:924`); ? "Get client details" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:997`); 404 "Details not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1009`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1017`)

### POST patient/getTopicsList
- controller: PatientDetailsController@getTopicsList (found) · route: `Ashoka-World-Backend:routes/api.php:1144` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3484`)

### POST patient/patientAppointmentInfo
- controller: PatientDetailsController@patientAppointmentInfo (found) · route: `Ashoka-World-Backend:routes/api.php:1142` · middleware: api, auth.token
- called by: no screen in this workspace
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3365`)
- errors: ? "Appointment not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3395`)

### POST patient/patientPreviousVisit
- controller: PatientDetailsController@patientPreviousVisit (found) · route: `Ashoka-World-Backend:routes/api.php:1114` · middleware: api, auth.token
- called by: no screen in this workspace
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1601`)
- errors: 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1635`); 404 "Visit list not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1740`); 200 "Get visit list" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1742`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1747`)

### POST patient/patientPreviousVisit-2
- controller: PatientDetailsController@patientPreviousVisit2 (found) · route: `Ashoka-World-Backend:routes/api.php:1128` · middleware: api, auth.token
- called by: no screen in this workspace
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1530`)
- errors: ? "Data not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1577`)

### POST patient/patientProgress
- controller: PatientDetailsController@patientProgress (found) · route: `Ashoka-World-Backend:routes/api.php:1146` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "Patient id is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4812`); 400 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4815`); ? "Patient medical data fetched successfully" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4849`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4877`)

### POST patient/previousVisitsDetails
- controller: PatientDetailsController@previousVisitsDetails (found) · route: `Ashoka-World-Backend:routes/api.php:1116` · middleware: api, auth.token
- called by: Nadi-Tarangini-App fetchSymptomHistory; Nadi-Tarangini-Frontend VikrutiController@getSymptomHistory (appointment.appointment_list, live_nadi.medical_assessment)
- validation: `patient_id`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5021`)
- errors: 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5056`); 404 "Visit list not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5144`); 200 "Success" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5146`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:5152`)

### POST patient/remainingFees
- controller: PatientDetailsController@remainingFees (found) · route: `Ashoka-World-Backend:routes/api.php:1130` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is not provided" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2399`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2402`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2405`); 404 "Client not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2416`); 404 "Fees data not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2426`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2445`)

### POST patient/saveFees
- controller: PatientDetailsController@saveFees (found) · route: `Ashoka-World-Backend:routes/api.php:1131` · middleware: api, auth.token
- called by: Nadi-Tarangini-App saveFeesDetails (MainAssessmentScreen); Nadi-Tarangini-Frontend DietController@saveDietAndLifestyleNew (live_nadi.medical_assessment); Nadi-Tarangini-Frontend DietController@saveDietData; Nadi-Tarangini-Frontend DietController@saveFeesDataAfterDiet; Nadi-Tarangini-Frontend DietController@saveVikrutiWiseDietData; Nadi-Tarangini-Frontend FeeDetailsController@saveFeesData; Nadi-Tarangini-Frontend FeeDetailsController@saveFeesDataWithNA
- validation: `fee_charged`: nullable|integer (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2475`); `fee_paid`: nullable|integer (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2476`); `consultation_fees`: nullable|integer (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2477`); `therapy_fees`: nullable|integer (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2478`); `doctor_remarks`: required (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2479`); `yoga_recom`: nullable (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2480`); `panchakarma_recom`: nullable (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2481`); `share_report_ids`: nullable|array (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2483`); `share_report_ids.*`: in:1,2,3,4,7,8,9 (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2484`); `file_to_upload`: nullable (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2485`); `file_description`: nullable (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2486`); `next_appointment_date`: nullable|date_format:Y-m-d|after_or_equal:tomorrow (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2487`); `starttime`: nullable|date_format:H:i (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2488`); `endtime`: nullable|date_format:H:i|after:starttime (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2489`)
- errors: 400 "Medical id is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2459`); 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2462`); 400 "Invalid medical id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2466`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2469`); ? "Invalid end time format" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2508`); 404 "Enter valid medical id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2527`); 404 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2532`); 400 "Next appointment date is mandatory" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2543`)

### POST patient/showPatientQueries
- controller: PatientDetailsController@showPatientQueries (found) · route: `Ashoka-World-Backend:routes/api.php:1137` · middleware: api, auth.token
- called by: no screen in this workspace
- validation: `status`: required|regex:/^[01]$/ (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3184`)
- errors: 400 "User id is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3181`); ? "Invalid status" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3187`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3239`)

### POST patient/updateClient
- controller: PatientDetailsController@updateClient (found) · route: `Ashoka-World-Backend:routes/api.php:1123` · middleware: api, auth.token
- called by: Nadi-Tarangini-App updatePatientDetails (AddPatientFromAppointmentScreen, AddPatientScreen, EditPatientScreen); Nadi-Tarangini-Frontend EditMemberController@updatetMemberData (patient.edit_member)
- validation: `firstname`: required|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1057`); `middlename`: nullable|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1058`); `lastname`: required|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1059`); `gender`: required|in:M,F,D,N (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1060`); `age`: nullable (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1061`); `dateofbirth`: nullable|date_format:Y-m-d|before_or_equal:today (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1062`); `profile_picture`: nullable|image|mimes:jpeg,png,jpg (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1063`); `profile_picture`: nullable|image|mimes:jpeg,png,jpg (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1290`)
- errors: 400 "Client id is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1030`); 400 "Invalid client id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1034`); 404 "Client not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1046`); 404 "Anonymous patient cannot be edited" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1054`); ? "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1077`); ? "Phone number is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1103`); ? "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1139`); ? "Invalid phone number format" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1149`)

### POST patient/updatePatientQueries
- controller: PatientDetailsController@updateQueries (found) · route: `Ashoka-World-Backend:routes/api.php:1138` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "Query id is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3254`); 400 "Answer is required" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3257`); 400 "Enter valid query id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3261`); 400 "Enter valid query id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3269`); 200 "Answer updated successfully" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3289`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3295`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3302`)

### POST patientList
- controller: PatientDetailsController@getPatientList (found) · route: `Ashoka-World-Backend:routes/api.php:926` · middleware: api, auth.token
- called by: no screen in this workspace
- errors: 400 "User id is not provided." (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3496`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:3712`)

### POST searchPatientUsingName
- controller: PatientDetailsController@searchPatientUsingName (found) · route: `Ashoka-World-Backend:routes/api.php:929` · middleware: api, auth.token
- called by: Nadi-Tarangini-App searchPatients (PatientScreen); Nadi-Tarangini-Frontend AdminDashboardController@searchUserPatientList (admin.user_patient_list); Nadi-Tarangini-Frontend NtLiteDashboardController@searchPatients (auth.nt-lite.nt_lite_dashboard); Nadi-Tarangini-Frontend PatientListController@searchPatients (patient.patientlist)
- errors: 400 "User id is not provided." (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4311`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:4603`)

### POST v2/patient/patientPreviousVisit
- controller: PatientDetailsController@patientPreviousVisitV2 (found) · route: `Ashoka-World-Backend:routes/api.php:1647` · middleware: auth.token
- called by: Nadi-Tarangini-App getPreviousVisitsforDoctor (PatientScreen, VisitReportListScreen); Nadi-Tarangini-Frontend AdminDashboardController@userPreviousVisits (admin.user_previous_visits); Nadi-Tarangini-Frontend NtLiteDashboardController@previousVisits (auth.nt-lite.nt_lite_previous_visits); Nadi-Tarangini-Frontend PreviousVisitsController@index (patient.previousVisits)
- validation: `patient_id`: required (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1758`)
- errors: 404 "Invalid patient id" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1792`); 404 "Visit list not found" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:1999`); 200 "Get visit list" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2001`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:2006`)

## Backend routes no screen calls

`GET checkpatientcode`, `POST getLanguage`, `POST patient/add-new-symptom`, `POST patient/clinicDetails`, `POST patient/deletePatientQuery`, `POST patient/getTopicsList`, `POST patient/patientAppointmentInfo`, `POST patient/patientPreviousVisit`, `POST patient/patientPreviousVisit-2`, `POST patient/patientProgress`, `POST patient/remainingFees`, `POST patient/showPatientQueries`, `POST patient/updatePatientQueries`, `POST patientList`

## Web routes (22)

- Nadi-Tarangini-Frontend `GET add-member` → AddMemberController@index · `Nadi-Tarangini-Frontend:routes/web.php:434` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST callPatientList` → PatientListController@callPatientList · `Nadi-Tarangini-Frontend:routes/web.php:403` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `DELETE deletePatient/{id}` → PatientListController@deletePatient · `Nadi-Tarangini-Frontend:routes/web.php:430` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `DELETE deleteReport/{medicalId}/{patientId}` → PreviousVisitsController@deleteReport · `Nadi-Tarangini-Frontend:routes/web.php:432` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET edit-member/{id}` → EditMemberController@index · `Nadi-Tarangini-Frontend:routes/web.php:440` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getLastVisitInformation` → PatientListController@getLastVisitInformation · `Nadi-Tarangini-Frontend:routes/web.php:473` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getLastVisitMandatoryQuesitons` → PatientListController@getLastVisitQuestions · `Nadi-Tarangini-Frontend:routes/web.php:472` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getLastVisitQuestions` → PatientListController@getLastVisitQuestions · `Nadi-Tarangini-Frontend:routes/web.php:471` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getMedicalId` → PatientListController@fetchNewMedicalIdV2 · `Nadi-Tarangini-Frontend:routes/web.php:460` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST getMedicalIdntlite` → PatientListController@fetchNewMedicalIdV2NtLite · `Nadi-Tarangini-Frontend:routes/web.php:462` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET getPatient` → PatientListController@getPatientListData · `Nadi-Tarangini-Frontend:routes/web.php:419` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET patientlist` → PatientListController@index · `Nadi-Tarangini-Frontend:routes/web.php:402` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET previousVisits/{id}` → PreviousVisitsController@index · `Nadi-Tarangini-Frontend:routes/web.php:425` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST resumeVisit` → PreviousVisitsController@resumeVisit · `Nadi-Tarangini-Frontend:routes/web.php:426` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveAnonymousData` → AddMemberController@saveAnonymousData · `Nadi-Tarangini-Frontend:routes/web.php:438` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST saveMemberData` → AddMemberController@saveMemberData · `Nadi-Tarangini-Frontend:routes/web.php:436` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST scheduledAppointments` → PatientListController@scheduledAppointments · `Nadi-Tarangini-Frontend:routes/web.php:639` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET search-patients` → PatientListController@searchPatients · `Nadi-Tarangini-Frontend:routes/web.php:404` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST setCurrentVisitSession` → PreviousVisitsController@setCurrentVisitSession · `Nadi-Tarangini-Frontend:routes/web.php:427` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST storePatient` → PatientListController@storePatient · `Nadi-Tarangini-Frontend:routes/web.php:407` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `POST updatetMemberData` → EditMemberController@updatetMemberData · `Nadi-Tarangini-Frontend:routes/web.php:442` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET view-member/{id}` → ViewMemberController@index · `Nadi-Tarangini-Frontend:routes/web.php:444` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode

## Screens (11)

- Nadi-Tarangini-App **AddPatientFromAppointmentScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/add_patient/add_patient_from_appointment_screen.dart` · goes to /addAppointmentScreen
- Nadi-Tarangini-App **AddPatientScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/add_patient/add_patient_screen.dart` · route /addPatientScreen · goes to /addAppointmentScreen, /dashboardScreen, /patientScreen
- Nadi-Tarangini-App **EditPatientScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/edit_patient/edit_patient_screen.dart` · route /editPatientScreen
- Nadi-Tarangini-App **PatientScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/patient_list/patient_screen.dart` · route /patientScreen · goes to /addPatientScreen, /assessmentScreen, /editPatientScreen, /fillPrakrutiScreen, /reportScreen, /viewPatientScreen
- Nadi-Tarangini-App **ViewPatientScreen** `Nadi-Tarangini-App:lib/doctor_dashboard/patient/view/view_patient/view_patient_screen.dart` · route /viewPatientScreen
- Nadi-Tarangini-Frontend **errors.410** `Nadi-Tarangini-Frontend:resources/views/errors/410.blade.php` · route GET add-member · rendered by AddMemberController@index
- Nadi-Tarangini-Frontend **patient.add-member** `Nadi-Tarangini-Frontend:resources/views/patient/add-member.blade.php` · route GET add-member · rendered by AddMemberController@index · goes to GET patientlist
- Nadi-Tarangini-Frontend **patient.edit_member** `Nadi-Tarangini-Frontend:resources/views/patient/edit_member.blade.php` · route GET edit-member/{id} · rendered by EditMemberController@index · goes to GET patientlist
- Nadi-Tarangini-Frontend **patient.patientlist** `Nadi-Tarangini-Frontend:resources/views/patient/patientlist.blade.php` · route GET patientlist · rendered by PatientListController@index · goes to GET add-member
- Nadi-Tarangini-Frontend **patient.previousVisits** `Nadi-Tarangini-Frontend:resources/views/patient/previousVisits.blade.php` · route GET previousVisits/{id} · rendered by PreviousVisitsController@index · goes to GET patientlist
- Nadi-Tarangini-Frontend **patient.view_member** `Nadi-Tarangini-Frontend:resources/views/patient/view_member.blade.php` · route GET view-member/{id} · rendered by ViewMemberController@index · goes to /edit-member/, GET patientlist

## API calls (122)

| Client | Caller | Call | Route | Status | Source |
|---|---|---|---|---|---|
| Nadi-Tarangini-App | accessUserWisePatientList | POST `/accessUserWisePatientList` | POST accessUserWisePatientList | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2405` |
| Nadi-Tarangini-App | dashboardPatientList | POST `/getLimitedActivePatients` | POST getLimitedActivePatients | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:563` |
| Nadi-Tarangini-App | deletePatient | POST `/patient/deletePatient` | POST patient/deletePatient | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:328` |
| Nadi-Tarangini-App | deleteReportForDoctor | POST `/patient/deleteReport` | POST patient/deleteReport | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1893` |
| Nadi-Tarangini-App | fetchCountryList | GET `/getAllCountries` | GET getAllCountries | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:202` |
| Nadi-Tarangini-App | fetchPatientDetails | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1296` |
| Nadi-Tarangini-App | fetchPatientDetailsAndNavigate | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:113` |
| Nadi-Tarangini-App | fetchPatientList | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:287` |
| Nadi-Tarangini-App | fetchSymptomHistory | POST `/patient/previousVisitsDetails` | POST patient/previousVisitsDetails | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1282` |
| Nadi-Tarangini-App | getBannerList | POST `/patient/getBannerList` | POST patient/getBannerList | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:554` |
| Nadi-Tarangini-App | getLastVisitInformation | POST `/v2/report/getLastVisitInformation` | POST v2/report/getLastVisitInformation | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2090` |
| Nadi-Tarangini-App | getPatientList | POST `/fetchPatientNames` | POST fetchPatientNames | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1772` |
| Nadi-Tarangini-App | getPrakrutiQuestions | POST `/prakruti/fetchPrakrutiQuestions` | POST prakruti/fetchPrakrutiQuestions | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:583` |
| Nadi-Tarangini-App | getPreviousVisitsforDoctor | POST `/v2/patient/patientPreviousVisit` | POST v2/patient/patientPreviousVisit | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1883` |
| Nadi-Tarangini-App | saveFeesDetails | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1481` |
| Nadi-Tarangini-App | searchPatients | POST `/searchPatientUsingName` | POST searchPatientUsingName | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:306` |
| Nadi-Tarangini-App | submitAnonymousPatient | POST `/patient/addAnonymousClient` | POST patient/addAnonymousClient | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:87` |
| Nadi-Tarangini-App | submitPatientDetails | POST `/patient/addClient` | POST patient/addClient | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:166` |
| Nadi-Tarangini-App | updatePatientDetails | POST `/patient/updateClient` | POST patient/updateClient | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:254` |
| Nadi-Tarangini-Frontend | AddClinicDetailsController@addClinicDetails | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AddClinicDetailsController.php:27` |
| Nadi-Tarangini-Frontend | AddMemberController@index | POST `/custom-data/getContentTypesWiseData` | POST custom-data/getContentTypesWiseData | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:72` |
| Nadi-Tarangini-Frontend | AddMemberController@index | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:41` |
| Nadi-Tarangini-Frontend | AddMemberController@index | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:51` |
| Nadi-Tarangini-Frontend | AddMemberController@saveAnonymousData | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:356` |
| Nadi-Tarangini-Frontend | AddMemberController@saveAnonymousData | POST `/patient/addAnonymousClient` | POST patient/addAnonymousClient | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:336` |
| Nadi-Tarangini-Frontend | AddMemberController@saveMemberData | POST `/appointment/addAppointment` | POST appointment/addAppointment | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:231` |
| Nadi-Tarangini-Frontend | AddMemberController@saveMemberData | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:200` |
| Nadi-Tarangini-Frontend | AddMemberController@saveMemberData | POST `/patient/addClient` | POST patient/addClient | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AddMemberController.php:150` |
| Nadi-Tarangini-Frontend | AdminDashboardController@createUser | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1205` |
| Nadi-Tarangini-Frontend | AdminDashboardController@editProfile | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:916` |
| Nadi-Tarangini-Frontend | AdminDashboardController@fetchUserPatientList | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:476` |
| Nadi-Tarangini-Frontend | AdminDashboardController@searchUserPatientList | POST `/searchPatientUsingName` | POST searchPatientUsingName | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:519` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPatientList | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:358` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPreviousVisits | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:568` |
| Nadi-Tarangini-Frontend | AdminDashboardController@userPreviousVisits | POST `/v2/patient/patientPreviousVisit` | POST v2/patient/patientPreviousVisit | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:600` |
| Nadi-Tarangini-Frontend | AppointmentController@addAppointment | POST `/fetchPatientNames` | POST fetchPatientNames | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AppointmentController.php:58` |
| Nadi-Tarangini-Frontend | AppointmentController@addPatientForAppointment | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AppointmentController.php:850` |
| Nadi-Tarangini-Frontend | AppointmentController@getAccessUserWisePatientList | POST `/accessUserWisePatientList` | POST accessUserWisePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AppointmentController.php:166` |
| Nadi-Tarangini-Frontend | DashboardController@addSelfAdmin | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1288` |
| Nadi-Tarangini-Frontend | DashboardController@index | POST `/getAssociationsCount` | POST getAssociationsCount | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:177` |
| Nadi-Tarangini-Frontend | DashboardController@index | POST `/getLimitedActivePatients` | POST getLimitedActivePatients | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:86` |
| Nadi-Tarangini-Frontend | DashboardController@index | POST `/patient/getBannerList` | POST patient/getBannerList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:56` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:714` |
| Nadi-Tarangini-Frontend | DietController@saveDietAndLifestyleNew | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:643` |
| Nadi-Tarangini-Frontend | DietController@saveDietData | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:128` |
| Nadi-Tarangini-Frontend | DietController@saveDietData | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:141` |
| Nadi-Tarangini-Frontend | DietController@saveFeesDataAfterDiet | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:269` |
| Nadi-Tarangini-Frontend | DietController@saveFeesDataAfterDiet | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:226` |
| Nadi-Tarangini-Frontend | DietController@saveFeesDataAfterDiet | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:239` |
| Nadi-Tarangini-Frontend | DietController@saveVikrutiWiseDietData | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:477` |
| Nadi-Tarangini-Frontend | DietController@saveVikrutiWiseDietData | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DietController.php:490` |
| Nadi-Tarangini-Frontend | EditClinicDetailsController@editClinicDetails | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditClinicDetailsController.php:28` |
| Nadi-Tarangini-Frontend | EditDoctorDetailsController@editDoctorDetails | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditDoctorDetailsController.php:52` |
| Nadi-Tarangini-Frontend | EditDoctorDetailsController@editDoctorProfile | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditDoctorDetailsController.php:246` |
| Nadi-Tarangini-Frontend | EditMemberController@index | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditMemberController.php:47` |
| Nadi-Tarangini-Frontend | EditMemberController@index | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditMemberController.php:68` |
| Nadi-Tarangini-Frontend | EditMemberController@index | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditMemberController.php:23` |
| Nadi-Tarangini-Frontend | EditMemberController@updatetMemberData | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditMemberController.php:158` |
| Nadi-Tarangini-Frontend | EditMemberController@updatetMemberData | POST `/patient/updateClient` | POST patient/updateClient | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditMemberController.php:121` |
| Nadi-Tarangini-Frontend | FeeDetailsController@index | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:78` |
| Nadi-Tarangini-Frontend | FeeDetailsController@saveFeesData | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:255` |
| Nadi-Tarangini-Frontend | FeeDetailsController@saveFeesData | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:230` |
| Nadi-Tarangini-Frontend | FeeDetailsController@saveFeesDataWithNA | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:398` |
| Nadi-Tarangini-Frontend | FeeDetailsController@saveFeesDataWithNA | POST `/patient/saveFees` | POST patient/saveFees | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/FeeDetailsController.php:346` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:292` |
| Nadi-Tarangini-Frontend | LiveNadiController@liveNadi | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/LiveNadiController.php:345` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:732` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1034` |
| Nadi-Tarangini-Frontend | MedicalAssessmentV3Controller@liveNadiV3 | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/MedicalAssessmentV3Controller.php:1083` |
| Nadi-Tarangini-Frontend | NewSignUpController@adminSignUp | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:333` |
| Nadi-Tarangini-Frontend | NewSignUpController@collegeSignUp | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:149` |
| Nadi-Tarangini-Frontend | NewSignUpController@doctorSignUp | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:29` |
| Nadi-Tarangini-Frontend | NtLiteDashboardController@callPatientList | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteDashboardController.php:119` |
| Nadi-Tarangini-Frontend | NtLiteDashboardController@index | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteDashboardController.php:90` |
| Nadi-Tarangini-Frontend | NtLiteDashboardController@index | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteDashboardController.php:43` |
| Nadi-Tarangini-Frontend | NtLiteDashboardController@previousVisits | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteDashboardController.php:285` |
| Nadi-Tarangini-Frontend | NtLiteDashboardController@previousVisits | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteDashboardController.php:239` |
| Nadi-Tarangini-Frontend | NtLiteDashboardController@previousVisits | POST `/v2/patient/patientPreviousVisit` | POST v2/patient/patientPreviousVisit | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteDashboardController.php:264` |
| Nadi-Tarangini-Frontend | NtLiteDashboardController@searchPatients | POST `/searchPatientUsingName` | POST searchPatientUsingName | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteDashboardController.php:171` |
| Nadi-Tarangini-Frontend | NtLiteLiveNadiController@resolvePatient | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteLiveNadiController.php:387` |
| Nadi-Tarangini-Frontend | NtLiteSignUpController@showSignUp | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:38` |
| Nadi-Tarangini-Frontend | PatientDashboardController@editProfile | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientDashboardController.php:154` |
| Nadi-Tarangini-Frontend | PatientListController@callPatientList | POST `/appointment/dateWiseAppointment` | POST appointment/dateWiseAppointment | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:324` |
| Nadi-Tarangini-Frontend | PatientListController@callPatientList | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:308` |
| Nadi-Tarangini-Frontend | PatientListController@deletePatient | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:375` |
| Nadi-Tarangini-Frontend | PatientListController@deletePatient | POST `/patient/deletePatient` | POST patient/deletePatient | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:366` |
| Nadi-Tarangini-Frontend | PatientListController@fetchNewMedicalIdV2 | POST `/report/getNewMedicalId` | POST report/getNewMedicalId | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:166` |
| Nadi-Tarangini-Frontend | PatientListController@fetchNewMedicalIdV2NtLite | POST `/v2/report/getNewMedicalId` | POST v2/report/getNewMedicalId | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:220` |
| Nadi-Tarangini-Frontend | PatientListController@getLastVisitInformation | POST `/v2/report/getLastVisitInformation` | POST v2/report/getLastVisitInformation | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:661` |
| Nadi-Tarangini-Frontend | PatientListController@getLastVisitQuestions | POST `/v2/report/getLastVisitMandatoryQuesitons` | POST v2/report/getLastVisitMandatoryQuesitons | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:626` |
| Nadi-Tarangini-Frontend | PatientListController@getPatientListData | POST `/appointment/dateWiseAppointment` | POST appointment/dateWiseAppointment | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:492` |
| Nadi-Tarangini-Frontend | PatientListController@getPatientListData | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:484` |
| Nadi-Tarangini-Frontend | PatientListController@index | POST `/appointment/dateWiseAppointment` | POST appointment/dateWiseAppointment | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:51` |
| Nadi-Tarangini-Frontend | PatientListController@index | POST `/getAllUserClinics` | POST getAllUserClinics | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:98` |
| Nadi-Tarangini-Frontend | PatientListController@index | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:79` |
| Nadi-Tarangini-Frontend | PatientListController@index | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:41` |
| Nadi-Tarangini-Frontend | PatientListController@scheduledAppointments | POST `/appointment/dateWisePatientAppointment` | POST appointment/dateWisePatientAppointment | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:442` |
| Nadi-Tarangini-Frontend | PatientListController@searchPatients | POST `/appointment/dateWiseAppointment` | POST appointment/dateWiseAppointment | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:560` |
| Nadi-Tarangini-Frontend | PatientListController@searchPatients | POST `/searchPatientUsingName` | POST searchPatientUsingName | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PatientListController.php:543` |
| Nadi-Tarangini-Frontend | PrakrutiQuestionsController@index | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PrakrutiQuestionsController.php:37` |
| Nadi-Tarangini-Frontend | PreviousVisitsController@deleteReport | POST `/patient/deleteReport` | POST patient/deleteReport | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:160` |
| Nadi-Tarangini-Frontend | PreviousVisitsController@index | POST `/appointment/dateWiseAppointment` | POST appointment/dateWiseAppointment | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:53` |
| Nadi-Tarangini-Frontend | PreviousVisitsController@index | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:119` |
| Nadi-Tarangini-Frontend | PreviousVisitsController@index | POST `/infinitePatientList` | POST infinitePatientList | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:35` |
| Nadi-Tarangini-Frontend | PreviousVisitsController@index | POST `/v2/patient/patientPreviousVisit` | POST v2/patient/patientPreviousVisit | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:83` |
| Nadi-Tarangini-Frontend | PreviousVisitsController@resumeVisit | POST `/v2/report/getCurrentVisitInfo` | POST v2/report/getCurrentVisitInfo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/PreviousVisitsController.php:231` |
| Nadi-Tarangini-Frontend | ReceptionistController@addReception | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/ReceptionistController.php:79` |
| Nadi-Tarangini-Frontend | ReceptionistController@editReception | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/ReceptionistController.php:144` |
| Nadi-Tarangini-Frontend | ViewMemberController@index | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/ViewMemberController.php:48` |
| Nadi-Tarangini-Frontend | ViewMemberController@index | POST `/patient/getClientDetails` | POST patient/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/ViewMemberController.php:21` |
| Nadi-Tarangini-Frontend | VikrutiController@getSymptomHistory | POST `/patient/previousVisitsDetails` | POST patient/previousVisitsDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/VikrutiController.php:186` |
| Nadi-Tarangini-Frontend | loginController@login | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:30` |

## Tables (16)

- `banners_data` (models: BannersData): accessibility, mobile_url
- `calendar_events` (models: CalendarEvent): clinic_id, consultation_type, reception_id
- `doctor_form_details` (models: DoctorFormDetail): columns not in migrations
- `languages` (models: Languages): columns not in migrations
- `locality_info` (models: LocalityInfo): is_default, timezone
- `medical_report` (models: MedicalReport): city, country, external_visit_id, field_id_1, ip_address, mark_on_image_url, panchakarma_recom, reception_id, recommendations, state, try_count, user_nadi_capture_type, yoga_recom
- `medical_report_diet` (models: MedicalReportDiet): create_date, diet, doctor_id, id, is_active, last_modified_on, medical_id, patient_id, vikruti_type
- `medical_report_file_upload` (models: MedicalReportFileUpload): columns not in migrations
- `medical_report_prescription` (models: MedicalReportPrescription): is_active, other_details, total_quantity
- `medical_report_symptom_details_1` (models: MedicalReportSymptomDetail): symptom_value
- `nadi_report` (models: NadiReport): columns not in migrations
- `notification_topics` (models: NotificationTopic): columns not in migrations
- `other_report_data` (models: OtherReportData): create_date, id, is_active, last_modified_on, medical_id, report_data, sub_title, title
- `patient_question_answer` (models: PatientQuestionAnswer): delete_by_doctor, delete_by_patient, is_active
- `symptoms` (models: Symptoms): is_active
- `user_personal_info` (models: UserPersonalInfo): allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken

## External systems

- Firebase (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:576,838,3011`
- S3 (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/PatientDetailsController.php:381,412,422`

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
