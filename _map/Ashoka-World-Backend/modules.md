# Module candidates: Ashoka-World-Backend

Raw grouping from scripts/cluster.sh at commit `8dfbb37db7d71a400b3656bd50fbed6173908a24`. Modules are decided in `atreya-docs/modules.yaml`.

| Controller | Routes | URI prefixes | Middleware | Models | Views |
|---|---|---|---|---|---|
| MedicalReportSaveController | 61 | getDietDataTest (1), nadiDataAnalysis (1), reception-api/report (10), report (38), updateYogaPlannerPublic (1), v2/report (9), zipFileNadiAnalysis (1) | api, auth.token, reception.authentication | AllCountryNames, AllPrakrutiTypes, CalendarEvent, DoctorMedicineInventory, Ingredient, Languages, LocalityInfo, MajorSymptomData, MedicalReport, MedicalReportDiet, MedicalReportImageMarker, MedicalReportPrescription, MedicalReportSymptomDetail, MedicineCompany, MedicineNames, MedicineQuantity, MedicineTiming, MedicineType, MedicineWithConsume, MultichoiceFieldList, MultichoiceOptions, NTApplicationVersion, NadiReport, OtherReportData, PgDeviceList, PgDeviceMapping, PrakrutiWiseDiet, ResourceNameMaster, SymptomCategory, SymptomsDropdownItem, UserPersonalInfo, UserReport, UserSelectedCountry, YogaReportData |  |
| CoachDashboardController | 44 | nadi-pariksha-admin (30), nadi-pariksha-admin/auth (1), nadi-pariksha-admin/coach-user-details (1), nadi-pariksha-admin/doctor (3), nadi-pariksha-coach (1), nadi-pariksha-coach-login (1), nadi-pariksha-coach/user-details (1), nadi-pariksha-login-validation (1), nadi_pariksha (2), nadi_pariksha/getNadiReportForCoach (1), nadi_pariksha/getUserPrakritiAnswers (1), nadi_pariksha/getUserSurveyAnswersWithQuestions (1) | nadiPariksha.adminDashboardAuthentication | NPAnalysisDataModel, NPPrakritiAnswers, NPSurveyQuestion, NPUserModel, NPUserSurveyAnswer, NpAdminDashboardFeatures, NpAdminUser, NpCoupon, NpDoctorsDetails, NpLanguage, NpNotifyMe, NpPaymentDetails, NpPrakritiQuestion, NpPricingMaster, NpUserActivity | nadi-pariksha |
| PatientDetailsController | 43 | accessUserWisePatientList (1), fetchPatientNames (1), getAllCountries (2), getAssociationsCount (1), getLanguage (1), getLimitedActivePatients (1), infinitePatientList (1), nt-jiva (3), patient (20), patientList (1), reception-api (4), reception-api/patient (5), searchPatientUsingName (1), v2/patient (1) | api, auth.token, reception.authentication | BannersData, CalendarEvent, DoctorFormDetail, HrvResult, Languages, LocalityInfo, MedicalReport, MedicalReportDiet, MedicalReportFileUpload, MedicalReportPrescription, MedicalReportSymptomDetail, NadiReport, NakshatraResult, OtherReportData, PatientQuestionAnswer, Symptoms, SymptomsDropdownItem, UserPersonalInfo, UserReport |  |
| AppointmentController | 27 | appointment (13), editApproveRejectAppointment (1), getApproveRejectList (1), loadNewAppointment (1), markOnImage (1), reception-api/appointment (10) | api, auth.token, reception.authentication | CalendarEvent, Languages, LocalityInfo, MedicalReport, MedicalReportImageMarker, UserPersonalInfo |  |
| DoctorController | 27 | ashokaDashboard (1), editProfile (1), fetchUserInfo (1), getAllCountriesName (1), getCountryWiseStates (1), getDisallowedReports (1), getDocumentTypes (2), getExperienceList (2), getFormLanguages (2), getLanguages (2), getMaritialList (2), getProfessionType (1), getReleaseDetails (1), getUpiDetails (1), getUserWiseAllowedReports (1), storeDisallowedReports (1), updateApplicationLanguages (1), updateUpiDetails (1), updateWelcomeTour (1), userAllowedReports (1), v2 (2) | api, atreyaDashboard.authentication, auth.token | AllCountryNames, CountryWiseStates, Languages, MasterContents, PgDeviceMapping, ProfessionType, ResourceNameMaster, Subscription, Transaction, UserNadiCaptureType, UserPersonalInfo |  |
| CustomizeDetailsController | 26 | GetReorderFeatures (1), addNewSymptoms (1), addnewDetails (1), custom (1), custom-data (1), getAnswerTypes (1), getCustomizeTab (1), getFormList (1), getSymptomInfo (1), medicalForm (7), medicalFormList (1), reportManagement (5), saveNadiKeywords (1), selectManualNadiKeywords (1), updateFormDetails (1), updateReorder (1) | api, auth.token | CommonData, CustomizeTab, DoctorFormDetail, DoctorMultichoiceOption, MedicalFormDetail, MedicalFormList, MultichoiceFieldList, MultichoiceOptions, ResourceNameMaster, SymptomCategory, Symptoms, SymptomsDropdownItem, UserNadiCaptureType, UserPersonalInfo |  |
| DeviceManagementController | 26 | ashokaDashboard/device (25), ashokaDashboard/summary (1) | atreyaDashboard.authentication | MedicalReport, PgDeviceList, PgDeviceMapping, UserPersonalInfo |  |
| DoctorsManagementController | 23 | ashokaDashboard (7), ashokaDashboard/doctor (16) | atreyaDashboard.authentication | LocalityInfo, MedicalReport, PgDeviceList, PgDeviceMapping, PgOrderDetail, PgOrderDispatch, PgOrderIdGenerate, PgPlanDetail, UserNadiCaptureType, UserPersonalInfo |  |
| ReportsWebController | 23 | arogyaDarshika (1), careServicesReport (1), checkReportStatus (1), dietReport (1), getReportWiseLanguages (1), medicalVisitReport (1), medicalVisitReportV2 (1), nadiSwasthyaReport (1), nadiTaranginiReport (1), nadiTaranginiReportV3 (1), ntRecommendationReport (1), onePagerNadiTaranginiReport (1), patanjaliReport (1), postFetchNadiInfo (1), postPatanjaliReport (1), prescriptionReport (1), rutucharyaReport (1), spaReport (1), swasthyaDarshikaReport (1), swasthyaDarshikaReportV2 (1), weeklyDietReport (1), yogaPlannerReport (1), yogaReport (1) | api, auth.token | ArogyaDarshikaSavedData, Languages, LocalityInfo, MasterContents, MedicalReport, MedicalReportPrescription, NadiReport, OtherReportData, PgDeviceMapping, ResourceNameMaster, UserNadiCaptureType, UserPersonalInfo | concents, errors, reports |
| NadiParikshaController | 21 | nadi-pariksha-admin (2), nadi-report/pdf (1), nadi_pariksha (17), web-nadi-report/pdf (1) | NadiParikshaPublic, nadiPariksha.adminDashboardAuthentication, nadiPariksha.authentication | NPAnalysisDataModel, NPPrakritiAnswers, NPUserModel, NpLanguage, NpPrakritiQuestion, PrakritiAnswers | nadi-pariksha |
| ExternalUserController | 20 | external (1), external/nadi (3), external/patient (2), external/report (3), nt-capture/analyze (1), nt-capture/internal (5), nt-capture/patient (2), nt-capture/report (3) | api | AllCountryNames, AllPrakrutiTypes, LocalityInfo, MedicalReport, MedicalReportSymptomDetail, PgDeviceMapping, UserNadiCaptureType, UserPersonalInfo, UserReport, YogaReportData |  |
| MedicineController | 20 | medicalInventory (20) | api, auth.token | DoctorMedicineInventory, MedicineCompany, MedicineNames, MedicineQuantity, MedicineQuantityTypeCategory, MedicineType |  |
| AshokaSalesController | 18 | ashokaDashboard/report (2), ashokaDashboard/sales (13), ashokaDashboard/summary (3) | atreyaDashboard.authentication | AshokaSalesRequest, AshokaShipmentTracking, AshokaSubSalesRequest, AshokaUsersMaster, PgDeviceList, PgDeviceMapping, UserPersonalInfo |  |
| AuthController | 17 | deleteUserAccount (1), editFcmToken (1), flush-cache (1), forgotPassword (1), getCurrencyTypes (2), getUserCurrentSummary (1), getUserCustomizeSummary (1), getUserSummary (1), login (1), loginOtpBasedUser (1), logout (1), profile (1), v2 (2), v2/client (1), validateCorporateCode (1) | api, auth.token, client.authentication | ApiEndpoints, CorporateInfo, Languages, LocalityInfo, MedicalReport, PgDeviceMapping, ProfessionType, ProjectVariable, Subscription, Transaction, UserNadiCaptureType, UserPersonalInfo |  |
| UserManagementController | 14 | nt-admin/access-management (13), public (1) | api, auth.token |  |  |
| AshokaShipmentManagementController | 13 | ashokaDashboard/shipment (13) | atreyaDashboard.authentication | AshokaSalesRequest, AshokaShipmentTracking, PgDeviceList |  |
| AshokaUserManangementController | 13 | ashokaDashboard (13) | atreyaDashboard.authentication | AllCountryNames, AshokaRolesMaster, AshokaUsersMaster, UserNadiCaptureType, UserPersonalInfo |  |
| getAllTuryaaController | 12 | turyaa (9), turyaa/v2 (3) | turyaa.authentication | AnalysisData, GetTuryaaPrakrutiQuestion, PrakritiAnswers, PrakritiAnswersDescriptions, QuestionAnswers, TuryaaUserModel |  |
| AshokaSubscriptionManagementController | 11 | ashokaDashboard (1), ashokaDashboard/subscription (5), ashokaDashboard/subscriptions (5) | atreyaDashboard.authentication | ApiEndpoints, PgDeviceMapping, ResourceNameMaster, Subscription, SubscriptionStatus, SubscriptionTypes, SubscriptionTypesMaster, Transaction, UserNadiCaptureType, UserPersonalInfo |  |
| NPUserController | 11 | nadi_pariksha (10), rate-us (1) | NadiParikshaPublic, nadiPariksha.authentication | NPAnalysisDataModel, NPPrakritiAnswers, NPUserModel, NPUserSurveyAnswer, NPVisitParameter, NPVisitParameterData, NpLanguage, NpMasterContent, NpNotifyMe, NpPaymentDetails, NpPricingMaster, NpUserActivity |  |
| QuestionsController | 11 | turyaa (4), turyaa/v2 (7) | turyaa.authentication | AnalysisData, QuestionAnswers, Questions, TuryaaUserModel, VikrutiFeedbackQuestion |  |
| ResearchDasbhoardController | 11 | research (2), research-dashboard (5), research-dashboard-pulse-data (2), research-dashboard-pulse-view (2) | api, auth.token | MedicalReport, MedicalReportSymptomDetail, NadiReport, UserPersonalInfo | research_dashboard_vata |
| PublicFunctionsController | 10 | appVersion (2), ashokaDashboard (1), checkGeoIPValidity (1), external-capture (1), getAddressUsingPincode (1), getAppLanguages (1), getUserDetailsUsingMobileNumber (1), updateLanguageJson (1), v2 (1) | api, atreyaDashboard.authentication, auth.token | AppVersions, CommonData, LocalityInfo, MasterContents, PostalCode, UserPersonalInfo |  |
| WellnessReportController | 10 | turyaa/coach (10) | turyaa.authentication | AnalysisData, DailyQuestions, DietData, PrakritiAnswersDescriptions, TuryaaUserModel, UserStages, WellnessReport, WellnessTracking |  |
| NotificationController | 9 | notification (9) | api, auth.token | AllNotificationsInfo, NotificationTopic, UserNotificationsInfo, UserPersonalInfo |  |
| PrakrutiController | 9 | prakruti (5), reception-api/prakruti (4) | api, auth.token, reception.authentication | AllPrakrutiTypes, PatientPrakruti, Symptoms, SymptomsDropdownItem, UserPersonalInfo |  |
| SubscriptionController | 9 | getSinglePlan (1), subscriptions (8) | api, auth.token | ApiEndpoints, Feature, LocalityInfo, Subscription, Transaction, UserNadiCaptureType, UserPersonalInfo | email |
| AshokaStoresController | 8 | ashokaDashboard/stores (8) | atreyaDashboard.authentication | AshokaStoresAssetsComponent, AshokaStoresAssetsMaster, AshokaUsersMaster |  |
| ClinicController | 8 | addNewClinic (1), deleteClinic (1), fetchClinicInfo (1), fetchSingleClinicInfo (1), getAllUserClinics (1), getUserDefaultClinicDetails (1), markClinicAsDefault (1), updateClinic (1) | api, auth.token | CountryWiseStates, LocalityInfo, UserPersonalInfo |  |
| ENACHController | 8 | eMandate (8) |  | AshokaRolesMaster, AshokaUsersMaster, EnachCustomers, EnachDebitLog, EnachMandate |  |
| MedicalInventoryController | 8 | fetchLastVisitPrescription (1), medicalInventory (7) | api, auth.token | DoctorMedicineInventory, MedicalReport, MedicineCompany, MedicineNames, MedicineQuantity, MedicineTiming, MedicineType, MedicineWithConsume, SymptomsDropdownItem, UserPersonalInfo |  |
| NadiController | 8 | turyaa (7), turyaa/v2 (1) | turyaa.authentication | AnalysisData, DietData, GeneralDescription, PrakritiAnswers, QuestionAnswers, TuryaaUserModel |  |
| OtpSmsController | 8 | nt-jiva (2), otp (6) | api | UserPersonalInfo |  |
| ReceptionManagementController | 8 | getAllFeatures (1), reception (4), reception/manage (3) | api, auth.token | Feature, UserPersonalInfo |  |
| IngredientController | 7 | medicalInventory (7) | api, auth.token | DoctorMedicineInventory, Ingredient, MedicineQuantity, MedicineType |  |
| NpAppVersionController | 7 | nadi_pariksha (7) | NadiParikshaPublic, nadiPariksha.authentication | NPUserModel, NpAppVersion, NpDoctorsDetails, NpExternalServiceLogs |  |
| NtTransactionController | 7 | calculatePlanPrice (1), createNtOrder (1), payment-invoices (1), planStatus (1), test-generate-invoice (1), verifyTransaction (1), webhook/razorpay (1) | api, auth.token | LocalityInfo, MasterContents, NtCoupons, Transaction, UserNadiCaptureType, UserPersonalInfo |  |
| SignUpController | 7 | getCurrencyType (2), getSalutationTypes (2), signup (1), signupV2 (1), v2 (1) | api | CountryWiseStates, CurrencyType, CustomizeTab, DoctorFormDetail, DoctorMedicineInventory, DoctorMultichoiceOption, Ingredient, Languages, LocalityInfo, MedicalFormDetail, MultichoiceFieldList, MultichoiceOptions, ProjectVariable, SalutationTypes, UserNadiCaptureType, UserPersonalInfo |  |
| UserAnalyticsController | 7 | ashokaDashboard (5), ashokaDashboard/doctor (2) | atreyaDashboard.authentication | MedicalReport, UserPersonalInfo |  |
| AshokaAuthController | 6 | ashokaDashboard (2), ashokaDashboard/appVersion (2), ashokaDashboard/device (2) | atreyaDashboard.authentication | AppVersions, AshokaRolesMaster, AshokaUsersMaster, PgDeviceList |  |
| CoachController | 6 | turyaa (3), turyaa/coach (3) | turyaa.authentication | AnalysisData, DailyQuestions, PrakritiAnswers, QuestionAnswers, Questions, TuryaaUserModel, UserStages, WellnessTracking |  |
| DailyQuestionsController | 6 | turyaa (6) | turyaa.authentication | AnalysisData, DailyQuestions, DietData, GeneralDescription, PrakritiAnswers, QuestionAnswers, TuryaaUserModel, VikrutiDescription |  |
| DietManagementController | 6 | client/turyaa (1), turyaa (5) | api, client.authentication, turyaa.authentication | AnalysisData, DietData, MedicalReport, MedicalReportSymptomDetail, PrakritiAnswers, QuestionAnswers, TuryaaUserModel, UserDietChoice, UserPersonalInfo |  |
| NPPaymentController | 6 | nadi_pariksha (6) | NadiParikshaPublic, nadiPariksha.authentication | NPAnalysisDataModel, NPUserModel, NpCoupon, NpPaymentDetails, NpPricingMaster |  |
| NadiAnalysisController | 6 | v1 (2), v1/reports (3), v1/vikruti (1) | auth.token | AllPrakrutiTypes |  |
| ReportManagementController | 6 | ashokaDashboard/dailyCron (1), ashokaDashboard/report (5) | atreyaDashboard.authentication | AshokaSalesRequest, AshokaUsersMaster, MedicalReport, UserPersonalInfo |  |
| WellnessController | 6 | turyaa (6) | turyaa.authentication | WellnessTracking |  |
| AshokaQuotationController | 5 | ashokaDashboard/sales (5) | atreyaDashboard.authentication | AshokaCustomers, AshokaQuotation |  |
| CheckUserExistOrNotController | 5 | checkMobileNumber (1), checkUsername (1), checkpatientcode (1), checkusernameormobileno (1), getdetailsbymobileno (1) | api, auth.token | UserPersonalInfo |  |
| CompanyController | 5 | medicalInventory (5) | api, auth.token | MedicineCompany |  |
| NpFirebaseNotificationController | 5 | nadi_pariksha/firebase (5) |  | NPUserModel |  |
| PudiController | 5 | medicalInventory (5) | api, auth.token | DoctorMedicineInventory, Ingredient |  |
| RecipeCategoryController | 5 | researchDashboard (5) | research.authentication | CategoryValue, RecipeCategory, StatesNames |  |
| orgPatientManagementController | 5 | client (1), client/corporate (1), org (1), org/expert (2) | api, client.authentication, corporate.authentication | CorporateInfo, LocalityInfo, PatientPrakruti, Symptoms, SymptomsDropdownItem, UserPersonalInfo |  |
| AccountManagementController | 4 | client (4) | api, client.authentication | ArogyaDarshikaSavedData, BannersData, NadiReport, UserPersonalInfo, UserReport |  |
| AniruddhaRuleListController | 4 | researchDashboard (4) | research.authentication | AniruddhaRuleList |  |
| AshokaCorporateManagementController | 4 | ashokaDashboard/corporate (4) | atreyaDashboard.authentication | CorporateInfo, CorporatePayments, MedicalReport, PgDeviceMapping, UserPersonalInfo |  |
| AshokaCustomersController | 4 | ashokaDashboard/sales (4) | atreyaDashboard.authentication | AshokaCustomers |  |
| AshokaPaymentOrderController | 4 | ashokaDashboard/sales (4) | atreyaDashboard.authentication | AshokaPaymentOrder |  |
| AshokaStatusMasterController | 4 | ashokaDashboard/status (4) | atreyaDashboard.authentication | AshokaStatusMaster |  |
| AskQuestionController | 4 | client (4) | api, client.authentication | PatientQuestionAnswer, UserPersonalInfo |  |
| BadminFunctionsController | 4 | checkValidDateTest (1), getPhpInfo (1), guna (2) | api | MedicalReport, UserPersonalInfo |  |
| CategoryValueController | 4 | researchDashboard (4) | research.authentication | CategoryValue, RecipeCategory |  |
| CommonJsonController | 4 | researchDashboard (4) | research.authentication | CommonJson |  |
| DataManagementController | 4 | currentUserAccessibleUsers (1), currentUserAccessibleUsersWithLocations (1), nt-admin/data-management (2) | api, auth.token |  |  |
| DayNamesJsonController | 4 | researchDashboard (4) | research.authentication | DaynamesJson |  |
| ExerciseCategoryController | 4 | researchDashboard (4) | research.authentication | ExerciseCategory |  |
| ExerciseTagsController | 4 | researchDashboard (4) | research.authentication | ExerciseCategory, ExerciseTags |  |
| FeaturesController | 4 | nt-admin/access-management (3), report (1) | api, auth.token | MasterContents, MedicalReport, UserPersonalInfo |  |
| JsonArrayRuleListController | 4 | researchDashboard (4) | research.authentication | JsonArrayRuleslist |  |
| LinkDeviceContoller | 4 | getLinkDevice (1), linkDeviceInHouseV2 (1), planDetails (1), validateDeviceWithSerialNo (1) | api, auth.token | PgDeviceList, PgDeviceMapping, PgOrderDetail, PgOrderDispatch, PgOrderIdGenerate, PgPlanDetail, UserNadiCaptureType, UserPersonalInfo |  |
| MealsCategoryController | 4 | researchDashboard (4) | research.authentication | MealsCategory |  |
| MusicLibraryController | 4 | researchDashboard (4) | research.authentication | MusicLibrary, MusicTags |  |
| MusicTagsController | 4 | researchDashboard (4) | research.authentication | MusicTags |  |
| NadiParikshaOTPSmsController | 4 | nadi_pariksha/otp (2), nadi_pariksha/v2 (2) | NadiParikshaPublic | NPUserModel, NpLanguage, NpOTPattemptMaster |  |
| NadiReportGrantController | 4 | ashokaDashboard/subscription (4) | atreyaDashboard.authentication | NadiManualReportGrant, UserNadiCaptureType, UserPersonalInfo |  |
| NpPublicController | 4 | nadi_pariksha (4) | NadiParikshaPublic | NPAnalysisDataModel, NPUserModel |  |
| NtCouponsController | 4 | ashokaDashboard/summary (4) |  | NtCoupons |  |
| RecipePreferenceJsonController | 4 | researchDashboard (4) | research.authentication | RecipePreferenceJson |  |
| StatesNamesController | 4 | researchDashboard (4) | research.authentication | StatesNames |  |
| TuryaaOTPSmsController | 4 | turyaa/otp (4) |  | TuryaaUserModel |  |
| UserDetailsController | 4 | guna (4) | api | UserPersonalInfo |  |
| YogaCategoryController | 4 | researchDashboard (4) | research.authentication | YogaCategory |  |
| YogaJsonController | 4 | researchDashboard (4) | research.authentication | YogaCategory, YogaJson |  |
| orgExpertsController | 4 | org/expert (4) | corporate.authentication | CorporateInfo, CustomizeTab, LocalityInfo, UserPersonalInfo |  |
| orgFranchiseController | 4 | org/franchise (4) | corporate.authentication | CorporateInfo |  |
| prakrutiManagementController | 4 | v1 (1), v1/prakruti (3) | auth.token | AllPrakrutiTypes, Symptoms, SymptomsDropdownItem |  |
| DietAndRecipesManagementController | 3 | v1/diet (3) | auth.token | AllPrakrutiTypes, MedicalReportSymptomDetail, MultichoiceOptions, PrakrutiWiseDiet |  |
| EditProfileController | 3 | client (3) | api, client.authentication | MedicalReport, UserPersonalInfo |  |
| FirebaseController | 3 | sendToMultipleTopics (1), sendToSingleClient (1), sendToSingleTopic (1) |  |  |  |
| HelpController | 3 | getHelpVideos (1), getNtFaq (1), getNtHelpVideos (1) | api, auth.token |  |  |
| NadiReportController | 3 | nadi (3) | api, auth.token | MedicalReport, MedicalReportSymptomDetail, MultichoiceFieldList, MultichoiceOptions, NadiAveragePulseData, NadiReport, PrakrutiWiseDiet, ProjectVariable |  |
| NpPaymentControllerV2 | 3 | nadi_pariksha (3) | NadiParikshaPublic, nadiPariksha.authentication | NPAnalysisDataModel, NPUserModel, NpPaymentDetails, NpPricingMaster |  |
| S3BucketController | 3 | getDataUsingIp (1), sampleEncrypt (1), testUploadS3 (1) |  |  |  |
| VisitManagementController | 3 | client (3) | api, client.authentication | MedicalReport, MedicalReportDiet, MedicalReportPrescription, MedicalReportSymptomDetail, ResourceNameMaster, UserReport |  |
| AllPrakrutiTypesController | 2 | getallroles (1), patientweeklydiet (1) | api, auth.token | AllPrakrutiTypes, UserRole |  |
| AshokaAccessManagementController | 2 | ashokaDashboard/accessManagement (2) | atreyaDashboard.authentication | AshokaDashboardModulesMaster, AshokaRolesMaster |  |
| AshokaRolesController | 2 | ashokaDashboard (2) | atreyaDashboard.authentication | AshokaRolesMaster |  |
| CronController | 2 | cron (2) | api | CalendarEvent, UserPersonalInfo |  |
| DataConsentController | 2 | client (2) | api, client.authentication | UserPersonalInfo |  |
| DinacharyaController | 2 | getDinacharyaRutucharya (1), getGermanyRutucharya (1) | api, auth.token |  |  |
| FaqDataController | 2 | turyaa (2) | turyaa.authentication | FaqData |  |
| KnowledgeDataController | 2 | turyaa (2) |  | KnowledgeData |  |
| NpSurveyQuestionController | 2 | nadi_pariksha (2) | NadiParikshaPublic, nadiPariksha.authentication | NPSurveyQuestion, NPUserModel, NPUserSurveyAnswer, NpLanguage |  |
| ProfileInfoController | 2 | profile-info (2) | api, auth.token | LocalityInfo, UserPersonalInfo |  |
| ReorderFeaturesController | 2 | doctor (2) | api, auth.token | DoctorFormDetail, MedicalFormList |  |
| SwaggerController | 2 | api-docs (2) |  |  | swagger |
| UserStatsController | 2 | getAccountData (1), getUserStatsData (1) | api, auth.token | Languages, LocalityInfo, NadiReport, PgDeviceMapping, Subscription, Transaction, UserNadiCaptureType, UserPersonalInfo |  |
| WelcomeTourController | 2 | welcome-tour (2) | api, auth.token | UserPersonalInfo |  |
| orgAnalyticsController | 2 | org/analytics (2) | corporate.authentication | CorporateInfo, MedicalReport, UserPersonalInfo |  |
| orgAuthController | 2 | org (2) |  | CorporateInfo |  |
| AdminManagementController | 1 | add-self-admin (1) | api, auth.token |  |  |
| AshokaDepartmentsController | 1 | ashokaDashboard (1) | atreyaDashboard.authentication | AshokaDepartmentsMaster |  |
| AuthenticateController | 1 | researchDashboard (1) |  | ResearchUsers |  |
| AyurvedaStaticController | 1 | nadi_pariksha (1) | NadiParikshaPublic, nadiPariksha.authentication | NPUserModel, NpLanguage |  |
| ExternalCaptureController | 1 | external-capture (1) | api, auth.token | MedicalReport, OtherReportData |  |
| FirebaseNotificationController | 1 | turyaa (1) | turyaa.authentication |  |  |
| GenerateSwasthyaLambda | 1 | generateLambda (1) | api, auth.token |  |  |
| GunaLocalityInfoController | 1 | guna (1) | api | LocalityInfo |  |
| MedicineContorller | 1 | getmedicineprescription (1) | api, auth.token | MedicalReport, MedicalReportPrescription |  |
| NPnadiController | 1 | nadi_pariksha (1) | NadiParikshaPublic, nadiPariksha.authentication | NPAnalysisDataModel, NPPrakritiAnswers, NPUserModel, NpOtherReportData, PrakritiAnswers |  |
| NpCohortManagement | 1 | nadi_pariksha (1) | NadiParikshaPublic, nadiPariksha.authentication | NPUserModel |  |
| NpGoogleCronController | 1 | nadi_pariksha (1) |  | NPAnalysisDataModel, NPUserModel |  |
| PdfGeneratorController | 1 | generatepdf (1) | api |  |  |
| SpaReportController | 1 | newReport (1) | api | Languages, LocalityInfo, MedicalReport, NadiReport, SpaReportSummary, SpaReportTherapy, UserPersonalInfo, UserReport |  |
| UpdatePasswordController | 1 | updatepassword (1) | api, auth.token | UserPersonalInfo |  |
| orgSignUpController | 1 | org (1) |  | CorporateInfo, CustomizeTab, LocalityInfo, UserPersonalInfo |  |
| NadiFileController | 0 |  |  |  |  |
| SmsController | 0 |  |  |  |  |

Closures / routes without a controller: GET /, GET auth/google/redirect, GET pdf, GET spa, GET user, GET yoga
