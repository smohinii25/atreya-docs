# Not in use

Status: **Draft** · 2026-10-26. Each item is **Confirmed** (a human said so) or **Needs confirmation** (found by a script).

## Confirmed

| Feature | Where | Status | Note |
|---|---|---|---|
| Receptionist | Backend routes `reception/*`, `reception-api/*`; Frontend `ReceptionistController` routes | Confirmed | Not used on web or mobile. |
| Research dashboard | Backend `research*` routes; Frontend `ResearchDashboardController` routes | Confirmed | Production only links to another website. |

## Candidates (Needs confirmation)

### Ashoka-World-Backend: backend routes in no module (18)

- `/`: `GET /`: Needs confirmation
- `auth`: `GET auth/google/redirect`: Needs confirmation
- `checkValidDateTest`: `POST checkValidDateTest`: Needs confirmation
- `getDataUsingIp`: `POST getDataUsingIp`: Needs confirmation
- `getPhpInfo`: `GET getPhpInfo`: Needs confirmation
- `guna`: `POST guna/assingDeviceDetails`, `POST guna/getBadminDoctorInfo`, `POST guna/getPatientList`, `POST guna/getSingleClinicData`, `POST guna/getSingleUserData`, `POST guna/getUserByUsername`, `POST guna/updateUserDetails`: Needs confirmation
- `pdf`: `GET pdf`: Needs confirmation
- `sampleEncrypt`: `POST sampleEncrypt`: Needs confirmation
- `spa`: `GET spa`: Needs confirmation
- `testUploadS3`: `POST testUploadS3`: Needs confirmation
- `user`: `GET user`: Needs confirmation
- `yoga`: `GET yoga`: Needs confirmation

### Ashoka-World-Backend: shadowed duplicate routes (an earlier definition is overridden)

- `POST generate-pdf` at `routes/api.php:1433`: Needs confirmation
- `POST nadi-pariksha-admin/make-report-free` at `routes/web.php:100`: Needs confirmation
- `GET nadi-report/pdf/{userId}` at `routes/web.php:25`: Needs confirmation
- `GET nadi_pariksha/testrenderNadiReportPdf` at `routes/api.php:1851`: Needs confirmation
- `GET web-nadi-report/pdf/{userId}` at `routes/web.php:26`: Needs confirmation

### Ashoka-World-Backend: 47 commented-out route lines in routes/*.php

Needs confirmation whether these features were removed.

### Nadi-Tarangini-Frontend: 26 commented-out route lines in routes/*.php

Needs confirmation whether these features were removed.

### Nadi-Tarangini-App: screen classes with no GoRoute

- AddPatientFromAppointmentScreen (`lib/doctor_dashboard/patient/view/add_patient/add_patient_from_appointment_screen.dart`): Needs confirmation
- AllReportScreen (`lib/patient_module/view/all_report_screen.dart`): Needs confirmation
- ComingSoonPage (`lib/patient_module/view/comming_soon_page.dart`): Needs confirmation
- ContactScreen (`lib/patient_module/view/contact_screen.dart`): Needs confirmation
- GeoRestrictedScreen (`lib/doctor_dashboard/dashboard/view/geo_restricted_screen.dart`): Needs confirmation
- LoginWithOtpScreen (`lib/common_files/Login/view/login_with_otp.dart`): Needs confirmation
- LoginWithUsernameScreen (`lib/common_files/Login/view/login_with_username_screen.dart`): Needs confirmation
- MyDevicesScreen (`lib/doctor_dashboard/my_account/view/my_device_screen.dart`): Needs confirmation

More candidates (routes no screen calls) are added by /atreya:link-apis.

<!-- link-apis:start -->
### Backend routes no NT screen calls (from /atreya:link-apis)

Needs confirmation: a route may still be used by a client outside this workspace.

- **auth** (6 of 25): `GET checkusernameormobileno`, `GET getdetailsbymobileno`, `POST login`, `POST logout`, `POST signup`, `POST validateCorporateCode`
- **dashboard** (1 of 7): `POST getUserStatsData`
- **patients** (14 of 32): `GET checkpatientcode`, `POST getLanguage`, `POST patient/add-new-symptom`, `POST patient/clinicDetails`, `POST patient/deletePatientQuery`, `POST patient/getTopicsList`, `POST patient/patientAppointmentInfo`, `POST patient/patientPreviousVisit`, `POST patient/patientPreviousVisit-2`, `POST patient/patientProgress`, `POST patient/remainingFees`, `POST patient/showPatientQueries`, `POST patient/updatePatientQueries`, `POST patientList`
- **appointments** (8 of 19): `POST appointment/fetchDoctorInfo`, `POST cron/get-appointmest-using-ids`, `POST cron/get-date-wise-appointment`, `POST editApproveRejectAppointment`, `POST getApproveRejectList`, `POST loadNewAppointment`, `POST markOnImage`, `PUT appointment/markAppointmentDone`
- **nadi-flow** (23 of 62): `POST external-capture/addReportData`, `POST generateLambda`, `POST getDietDataTest`, `POST getmedicineprescription`, `POST nadi/baselineCalculation`, `POST nadi/report`, `POST nadi/reportInfo`, `POST report/addMedicineForPrescriptionNewV3`, `POST report/deleteMedicineFromPrescriptionNewV3`, `POST report/fetchMarkOnImage`, `POST report/generateYogaPlanner`, `POST report/getLastPrescription`, `POST report/getMedicineFromPrescriptionNewV3`, `POST report/getStrotas`, `POST report/getVikrutiWiseDietAndLifestyle`, `POST report/newVisitQues`, `POST report/saveMarkOnImage`, `POST report/savePrescriptionData`, `POST report/saveSinglePrescription`, `POST report/updateSinglePrescription`, `POST updateYogaPlannerPublic`, `POST v2/report/saveDietAndLifestyleManually`, `POST zipFileNadiAnalysis`
- **reports** (14 of 28): `GET checkReportStatus`, `GET generatepdf`, `GET nadiSwasthyaReport`, `GET ntRecommendationReport`, `GET onePagerNadiTaranginiReport`, `GET patanjaliReport`, `GET rutucharyaReport`, `GET swasthyaDarshikaReportV2`, `GET weeklyDietReport`, `GET yogaPlannerReport`, `POST generate-pdf`, `POST newReport`, `POST postFetchNadiInfo`, `POST postPatanjaliReport`
- **medical-inventory** (7 of 45): `GET medicalInventory/getAllMedicineNamesWithTypes`, `GET medicalInventory/medicineTypes`, `GET medicalInventory/supplementMedicineTypes`, `POST fetchLastVisitPrescription`, `POST medicalInventory/deleteMedicineType`, `POST medicalInventory/getPudiList`, `POST medicalInventory/updateMedicineType`
- **customization** (7 of 28): `GET custom/getCustomizePrakrutiQuestions`, `POST addNewSymptoms`, `POST doctor/doctorFormDetails`, `POST getCustomizeTab`, `POST medicalForm/getDoctorQuestions`, `POST updateFormDetails`, `PUT doctor/updateDoctorInformation`
- **payments** (3 of 16): `POST getSinglePlan`, `POST test-generate-invoice`, `POST webhook/razorpay/nadi`
- **enach** (8 of 8): `GET eMandate/getAllSalesUser`, `GET eMandate/getEnachCustomers`, `GET eMandate/getScheduleDebitDetails`, `POST eMandate/enachRegistration`, `POST eMandate/handleResponse`, `POST eMandate/scheduleDebit`, `POST eMandate/verifyMandate`, `POST eMandate/verifyTransaction`
- **my-account** (11 of 43): `GET getDisallowedReports`, `GET profile`, `GET userAllowedReports`, `GET v2/getDoctorData`, `POST editProfile`, `POST fetchClinicInfo`, `POST planDetails`, `POST profile-info/showUserInformation`, `POST storeDisallowedReports`, `POST updateApplicationLanguages`, `PUT profile-info/updateUserInformation`
- **notifications** (9 of 12): `POST notification/addNewNotification`, `POST notification/fetchAllNotificationTopicList`, `POST notification/fetchSingleNotification`, `POST notification/markasUnreadNotification`, `POST notification/sendToSingleTopic`, `POST notification/sendToSingleUser`, `POST sendToMultipleTopics`, `POST sendToSingleClient`, `POST sendToSingleTopic`
- **nt-admin** (1 of 23): `GET currentUserAccessibleUsers`
- **patient-portal** (4 of 17): `POST client/askQuery`, `POST client/deleteQuery`, `POST client/fetchAskedQueriesList`, `POST client/updateQuery`
- **corporate** (17 of 18): `POST client/corporate/addNewPatientForCorporate`, `POST org/analytics/getDashboardAnalysis`, `POST org/analytics/getFranchiseAnalytics`, `POST org/expert/addNewPatientForCorporate`, `POST org/expert/createExpert`, `POST org/expert/deleteExperts`, `POST org/expert/generateAddPatientUrl`, `POST org/expert/getExperts`, `POST org/expert/getFranchiseWiseDoctors`, `POST org/franchise/addNewFranchise`, `POST org/franchise/getAllFranchises`, `POST org/franchise/getSingleFranchise`, `POST org/franchise/updateNewFranchise`, `POST org/getDetailsUsingAddPatientUrl`, `POST org/orgLogin`, `POST org/orgSignUp`, `POST org/sendEmailOtp`
- **platform** (8 of 16): `GET api-docs/developer`, `GET api-docs/public`, `POST appVersion/updateAppVersionDetails`, `POST external-capture/generateS3UploadUrl`, `POST flush-cache`, `POST getallroles`, `POST patientweeklydiet`, `POST updateLanguageJson`
<!-- link-apis:end -->
