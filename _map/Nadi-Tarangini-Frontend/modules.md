# Module candidates: Nadi-Tarangini-Frontend

Raw grouping from scripts/cluster.sh at commit `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d`. Modules are decided in `atreya-docs/modules.yaml`.

| Controller | Routes | URI prefixes | Middleware | Models | Views |
|---|---|---|---|---|---|
| ResearchDashboardController | 69 | add-aniruddha-rule (1), add-rule (1), checkResearchLogin (1), delete-rule (1), edit-aniruddha-rule (1), edit-rule (1), research-diet (1), researchDashboard (46), researchDashboard/delete-aniruddha-rule (1), researchDashboard/delete-rule (1), researchDashboard/deleteCommonJson (1), researchDashboard/deleteDayName (1), researchDashboard/deleteExerciseCategory (1), researchDashboard/deleteExerciseTag (1), researchDashboard/deleteMealCategory (1), researchDashboard/deleteMusicLibraryData (1), researchDashboard/deleteMusicTag (1), researchDashboard/deleteRecipeCategory (1), researchDashboard/deleteRecipePreference (1), researchDashboard/deleteRecipeTag (1), researchDashboard/deleteStateName (1), researchDashboard/deleteYogaCategory (1), researchDashboard/deleteYogaJson (1), researchLogin (1) | check_research_auth_token |  | researchDashboardPages, research_dashboard |
| AdminDashboardController | 31 | admin (19), admin/data-management (1), admin/edit-profile (1), admin/patient-list (5), admin/payment-invoices (1), admin/permissions (1), admin/report (2), admin/update-password (1) | nt_admin_authentication |  | admin |
| DashboardController | 30 | add-self-admin (2), admin (1), api (1), api/welcome-tour (1), checkout (1), dashboard (1), delete-account (1), freeTrial (1), get-all-clinic-list (1), get-default-clinic-details (1), get-languages-for-reports (1), getPlanStatus (1), getReleaseDetails (1), getUserCurrentSummary (1), getUserCustomizeSummary (1), getWelcomeTourSteps (1), invoice (1), linked-device (1), member-progress (1), member-report (1), queries (1), savePaymentData (1), subscription (1), switchToAdmin (1), update-report-language (1), updateTourData (1), update_kyc (1), welcome-tour (2) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications, nt_admin_authentication |  | add_self_admin, doctor_dashboard, errors, my_account, subscription, subscription_plans |
| AppointmentController | 15 | add-appointment (1), add-patient (1), appointment-history (1), appointment-list (1), currentUserAccessibleUsersWithLocations (1), deleteAppointment (1), edit-appointment (1), fetch-single-appointment (1), getAccessUserWisePatientList (1), saveNewPatientAppointment (1), saveVisitedPatientAppointment (1), store-appointment-id (1), updateAppointment (1), validateAppointment (1), view-appointment (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | appointment |
| HelpController | 15 | help (1), help-center (1), nt-map (1), research-dashboard (12) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | help, research_dashboard |
| AdminCustomizeController | 13 | admin (9), admin/customize-report-user-wise (1), admin/get-user-wise-category-wise-customize-questions (1), admin/get-user-wise-customize-question (1), admin/get-user-wise-report-pages (1) | nt_admin_authentication |  | customize |
| loginController | 13 | checkLoginCredintial (1), editFcmToken (1), get-all-roles (1), getUserDetailsOtpBasedLogin (1), login (1), logout (2), nt-lite (2), send-email-login-otp (1), send-login-otp (1), verify-email-login-otp (1), verify-login-otp (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | auth |
| PatientDashboardController | 12 | patient (8), patient/daily-diet-lifestyle (1), patient/report (3) | check_client_auth_token |  | patient-module |
| PatientListController | 12 | callPatientList (1), deletePatient (1), getLastVisitInformation (1), getLastVisitMandatoryQuesitons (1), getLastVisitQuestions (1), getMedicalId (1), getMedicalIdntlite (1), getPatient (1), patientlist (1), scheduledAppointments (1), search-patients (1), storePatient (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | patient |
| MedicalAssessmentV3Controller | 11 | medical-assessment-v3 (2), medical-assessment-v3/diet (3), medical-assessment-v3/yoga (2), saveUsbNadiDataV3 (1), updateCurrentNadiTaranginiDeviceV3 (1), updateNadiCaptureTypeV3 (1), updateSessionNadiCaptureType (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | errors, medical_assessment |
| PrescriptionController | 11 | addNewPrescriptionIngredient (1), deleteMedicine (1), editMedicine (1), getMedicineNamesRespectToType (1), prescription (1), savePrescriptionData (1), savePrescriptionDataV2 (1), savePrescriptionDataV3 (1), saveRecommendationData (1), updatePrescriptionDataV2 (1), updatePrescriptionDataV3 (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | errors |
| DesignFormController | 10 | design-form (10) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | design-form |
| UnauthorizedController | 10 | error (1), error-400 (1), error-401 (1), error-403 (1), error-404 (1), error-500 (1), error-503 (1), error-504 (1), region-restricted (1), unauthorized (1) |  |  | errors |
| NewSignUpController | 9 | checkDoctorMobileNo (1), checkDoctorUsername (1), checkValidationsLinkDevice (1), linkDeviceAfterValidation (1), sign-up (1), sign-up-admin (1), sign-up-college (1), signup (1), updateSignUpDetails (1) |  |  | auth |
| NtLiteDashboardController | 9 | nt-lite (8), nt-lite/previousVisits (1) | ensure_nt_lite_dashboard_mode, nt_lite_auth |  | auth |
| ReceptionistController | 9 | activeInactiveReception (1), add-reception (1), createReception (1), deleteReceptionist (1), edit-reception (1), reception (1), set-permission (1), updatePermission (1), updateReceptionist (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | receptionist |
| ReportController | 8 | arogya-darshika (1), nt-report (1), report (6) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | allReportView, visitReportView |
| DietController | 7 | diet (1), diet-lifestyle (1), getVikrutiWiseDiet (1), saveDietAndLifestyle (1), saveDietAndLifestyleNew (1), saveFeesDataAfterDiet (1), saveVirutiWiseDietAndLifestyle (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | errors |
| MedicineController | 7 | add-medicine (1), deleteMedicineinventory (1), edit-medicine (1), edit-supplement (1), getQuantity (1), medicine (1), updateMedicine (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | medical_inventory |
| EditDoctorDetailsController | 6 | edit-payment (1), editprofile (1), profile (1), updateKycDetails (1), updatePaymentDetails (1), updatetDoctorDetails (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | my_account |
| LiveNadiController | 6 | getManualNadiQuestions (1), medical-assessment (1), saveDummyUsbNadiData (1), saveUsbNadiData (1), updateCurrentNadiTaranginiDevice (1), updateNadiCaptureType (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | errors, live_nadi |
| CompanyController | 5 | addCompany (1), company (1), deleteCompany (1), edit-company (1), updateCompany (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | medical_inventory |
| IngredientsController | 5 | addIngredients (1), deleteIngredient (1), edit-ingredient (1), ingredient (1), updateIngredient (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | medical_inventory |
| PudiController | 5 | add-pudi (1), deletePudi (1), edit-pudi (1), pudi (1), update-pudi (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | medical_inventory |
| VikrutiController | 5 | getVikrutiData (1), previousVisitsSymptomDetails (1), saveCategoryWiseVikrutiData (1), saveVikrutiDataV2 (1), vikruti (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | errors |
| FeeDetailsController | 4 | fee-details (2), saveFeesData (1), saveFeesDataWithNA (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | errors |
| InventoryController | 4 | inventory (1), medicineuploadfile (1), supplementuploadfile (1), uploadfile (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | medical_inventory |
| NtLiteSignUpController | 4 | nt-lite (4) |  |  | auth |
| PrakrutiQuestionsController | 4 | getPrakrutiData (1), getPrakrutiDataForNewPatient (1), prakruti (1), savePrakrutiData (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | errors |
| PreviousVisitsController | 4 | deleteReport/{medicalId} (1), previousVisits (1), resumeVisit (1), setCurrentVisitSession (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | patient |
| AddMemberController | 3 | add-member (1), saveAnonymousData (1), saveMemberData (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | errors, patient |
| ClinicListController | 3 | clinic (1), deleteClinic (1), storeClinic (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | my_account |
| CustomizeController | 3 | admin (2), customize (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications, nt_admin_authentication |  | customize |
| MarkOnImageController | 3 | fetchMarkOnImageData (1), nadi-image (1), saveMarkOnImageData (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | errors |
| AddClinicDetailsController | 2 | add-clinic (1), saveClinicDetails (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | my_account |
| AddressDetailsController | 2 | address (2) |  |  |  |
| ChangePasswordController | 2 | change-password (1), updatePassword (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | my_account |
| EditClinicDetailsController | 2 | edit-clinic (1), updatedClinicDetails (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | my_account |
| EditMemberController | 2 | edit-member (1), updatetMemberData (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | patient |
| ExternalNadiController | 2 | analyzeExternalNadiData (1), nt-capture (1) |  |  | external |
| ManualNadiKeywordsController | 2 | nadi-keywords (1), saveKeywordsData (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | errors |
| MedicineTypeController | 2 | add-medicine-type (1), medicine-type (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | medical_inventory |
| NotificationController | 2 | notification (1), notifications (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | notifications |
| OtpVerificationController | 2 | send-verification-otp (1), verify-verification-otp (1) |  |  |  |
| PatientDashboardManagementController | 2 | corporate (2) | check_client_auth_token, corporate_patient_check_auth |  | corporate-patient-module |
| PatientVisitController | 2 | patient (1), patient/deletePatientReport (1) | check_client_auth_token |  | patient-module |
| forgotPasswordController | 2 | checkForgotPassword (1), forgotPassword (1) |  |  | auth |
| DownloadRutucharyaController | 1 | downloadRutucharya (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | rutucharya |
| MarkClinicDefaultController | 1 | makeDefaultClinic (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  |  |
| NtChatbotProxyController | 1 | nt-chatbot (1) |  |  |  |
| NtLiteLiveNadiController | 1 | nt-lite (1) | ensure_nt_lite_dashboard_mode, nt_lite_auth |  | auth |
| RequestAppointmentController | 1 | patient (1) | check_client_auth_token |  | patient-module |
| ViewMemberController | 1 | view-member (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  | patient |
| WebErrorReportController | 1 | web-error-report (1) | check_auth_token, ensure_normal_dashboard_mode, fetch_notifications |  |  |
| SignUpController | 0 |  |  |  |  |

Closures / routes without a controller: GET /, GET api/user, GET set-language/{lang}
