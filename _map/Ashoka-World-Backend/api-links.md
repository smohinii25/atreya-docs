# API links: who calls Ashoka-World-Backend

Built from Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24` by scripts/link-apis.sh.

- Nadi-Tarangini-App: 181 calls, 175 matched, 0 with no matching route, 13 unresolved
- Nadi-Tarangini-Frontend: 726 calls, 717 matched, 4 with no matching route, 22 unresolved

**338 of 924 backend routes are called by a screen in this workspace.**

Modules marked *external callers* belong to other products or partner APIs whose clients are not in this workspace, so "not called" is expected there.

| Module | Product | Routes | Called | Not called | Note |
|---|---|---|---|---|---|
| auth | nt | 25 | 19 | 6 |  |
| dashboard | nt | 7 | 6 | 1 |  |
| patients | nt | 32 | 18 | 14 |  |
| appointments | nt | 19 | 11 | 8 |  |
| nadi-flow | nt | 62 | 39 | 23 |  |
| reports | nt | 28 | 14 | 14 |  |
| medical-inventory | nt | 45 | 38 | 7 |  |
| customization | nt | 28 | 21 | 7 |  |
| payments | nt | 16 | 13 | 3 |  |
| enach | nt | 8 | 0 | 8 |  |
| my-account | nt | 43 | 32 | 11 |  |
| notifications | nt | 12 | 3 | 9 |  |
| chatbot | nt | 0 | 0 | 0 |  |
| help | nt | 3 | 3 | 0 |  |
| nt-admin | nt | 23 | 22 | 1 |  |
| patient-portal | nt | 17 | 13 | 4 |  |
| corporate | nt | 18 | 1 | 17 |  |
| nt-lite | nt | 0 | 0 | 0 |  |
| external-api | nt | 33 | 3 | 30 | external callers |
| nt-jiva | nt | 5 | 0 | 5 | external callers |
| platform | nt | 16 | 8 | 8 |  |
| receptionist | nt | 41 | 6 | 35 | confirmed not in use |
| research-dashboard | nt | 73 | 67 | 6 | confirmed not in use |
| ashoka-admin | ashoka-admin | 167 | 0 | 167 | external callers |
| nadi-pariksha | nadi-pariksha | 111 | 0 | 111 | external callers |
| turyaa | turyaa | 74 | 1 | 73 | external callers |

## Routes no screen calls (NT modules, possibly unused)

### auth (6)

- `GET checkusernameormobileno`
- `GET getdetailsbymobileno`
- `POST login`
- `POST logout`
- `POST signup`
- `POST validateCorporateCode`

### dashboard (1)

- `POST getUserStatsData`

### patients (14)

- `GET checkpatientcode`
- `POST getLanguage`
- `POST patient/add-new-symptom`
- `POST patient/clinicDetails`
- `POST patient/deletePatientQuery`
- `POST patient/getTopicsList`
- `POST patient/patientAppointmentInfo`
- `POST patient/patientPreviousVisit`
- `POST patient/patientPreviousVisit-2`
- `POST patient/patientProgress`
- `POST patient/remainingFees`
- `POST patient/showPatientQueries`
- `POST patient/updatePatientQueries`
- `POST patientList`

### appointments (8)

- `POST appointment/fetchDoctorInfo`
- `POST cron/get-appointmest-using-ids`
- `POST cron/get-date-wise-appointment`
- `POST editApproveRejectAppointment`
- `POST getApproveRejectList`
- `POST loadNewAppointment`
- `POST markOnImage`
- `PUT appointment/markAppointmentDone`

### nadi-flow (23)

- `POST external-capture/addReportData`
- `POST generateLambda`
- `POST getDietDataTest`
- `POST getmedicineprescription`
- `POST nadi/baselineCalculation`
- `POST nadi/report`
- `POST nadi/reportInfo`
- `POST report/addMedicineForPrescriptionNewV3`
- `POST report/deleteMedicineFromPrescriptionNewV3`
- `POST report/fetchMarkOnImage`
- `POST report/generateYogaPlanner`
- `POST report/getLastPrescription`
- `POST report/getMedicineFromPrescriptionNewV3`
- `POST report/getStrotas`
- `POST report/getVikrutiWiseDietAndLifestyle`
- `POST report/newVisitQues`
- `POST report/saveMarkOnImage`
- `POST report/savePrescriptionData`
- `POST report/saveSinglePrescription`
- `POST report/updateSinglePrescription`
- `POST updateYogaPlannerPublic`
- `POST v2/report/saveDietAndLifestyleManually`
- `POST zipFileNadiAnalysis`

### reports (14)

- `GET checkReportStatus`
- `GET generatepdf`
- `GET nadiSwasthyaReport`
- `GET ntRecommendationReport`
- `GET onePagerNadiTaranginiReport`
- `GET patanjaliReport`
- `GET rutucharyaReport`
- `GET swasthyaDarshikaReportV2`
- `GET weeklyDietReport`
- `GET yogaPlannerReport`
- `POST generate-pdf`
- `POST newReport`
- `POST postFetchNadiInfo`
- `POST postPatanjaliReport`

### medical-inventory (7)

- `GET medicalInventory/getAllMedicineNamesWithTypes`
- `GET medicalInventory/medicineTypes`
- `GET medicalInventory/supplementMedicineTypes`
- `POST fetchLastVisitPrescription`
- `POST medicalInventory/deleteMedicineType`
- `POST medicalInventory/getPudiList`
- `POST medicalInventory/updateMedicineType`

### customization (7)

- `GET custom/getCustomizePrakrutiQuestions`
- `POST addNewSymptoms`
- `POST doctor/doctorFormDetails`
- `POST getCustomizeTab`
- `POST medicalForm/getDoctorQuestions`
- `POST updateFormDetails`
- `PUT doctor/updateDoctorInformation`

### payments (3)

- `POST getSinglePlan`
- `POST test-generate-invoice`
- `POST webhook/razorpay/nadi`

### enach (8)

- `GET eMandate/getAllSalesUser`
- `GET eMandate/getEnachCustomers`
- `GET eMandate/getScheduleDebitDetails`
- `POST eMandate/enachRegistration`
- `POST eMandate/handleResponse`
- `POST eMandate/scheduleDebit`
- `POST eMandate/verifyMandate`
- `POST eMandate/verifyTransaction`

### my-account (11)

- `GET getDisallowedReports`
- `GET profile`
- `GET userAllowedReports`
- `GET v2/getDoctorData`
- `POST editProfile`
- `POST fetchClinicInfo`
- `POST planDetails`
- `POST profile-info/showUserInformation`
- `POST storeDisallowedReports`
- `POST updateApplicationLanguages`
- `PUT profile-info/updateUserInformation`

### notifications (9)

- `POST notification/addNewNotification`
- `POST notification/fetchAllNotificationTopicList`
- `POST notification/fetchSingleNotification`
- `POST notification/markasUnreadNotification`
- `POST notification/sendToSingleTopic`
- `POST notification/sendToSingleUser`
- `POST sendToMultipleTopics`
- `POST sendToSingleClient`
- `POST sendToSingleTopic`

### nt-admin (1)

- `GET currentUserAccessibleUsers`

### patient-portal (4)

- `POST client/askQuery`
- `POST client/deleteQuery`
- `POST client/fetchAskedQueriesList`
- `POST client/updateQuery`

### corporate (17)

- `POST client/corporate/addNewPatientForCorporate`
- `POST org/analytics/getDashboardAnalysis`
- `POST org/analytics/getFranchiseAnalytics`
- `POST org/expert/addNewPatientForCorporate`
- `POST org/expert/createExpert`
- `POST org/expert/deleteExperts`
- `POST org/expert/generateAddPatientUrl`
- `POST org/expert/getExperts`
- `POST org/expert/getFranchiseWiseDoctors`
- `POST org/franchise/addNewFranchise`
- `POST org/franchise/getAllFranchises`
- `POST org/franchise/getSingleFranchise`
- `POST org/franchise/updateNewFranchise`
- `POST org/getDetailsUsingAddPatientUrl`
- `POST org/orgLogin`
- `POST org/orgSignUp`
- `POST org/sendEmailOtp`

### platform (8)

- `GET api-docs/developer`
- `GET api-docs/public`
- `POST appVersion/updateAppVersionDetails`
- `POST external-capture/generateS3UploadUrl`
- `POST flush-cache`
- `POST getallroles`
- `POST patientweeklydiet`
- `POST updateLanguageJson`

