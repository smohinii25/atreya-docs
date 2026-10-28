# Screens: Nadi-Tarangini-Frontend (blade)

Built from commit `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d` by scripts/screens.sh.

screens: 328 · partials: 91 · rendered_by_controller: 134 · reachable_by_route: 133 · js_calls: 312 · js_calls_credited: 232 · js_calls_unresolved: 108

| View | Rendered by | Routes | Links to |
|---|---|---|---|
| `add_self_admin` | DashboardController@addSelfAdmin | `GET add-self-admin` |  |
| `admin.admin_dashboard` | AdminDashboardController@index | `GET admin/dashboard` |  |
| `admin.all_report_view` | AdminDashboardController@viewAllReport | `POST admin/report/viewAllReport` | GET admin/patient-list/{id}/previous-visits/{patientId}, GET admin/user-and-teams |
| `admin.create_user` | AdminDashboardController@createUser | `GET admin/create-user` | GET admin/user-and-teams |
| `admin.data_management` | AdminDashboardController@dataManagement | `GET admin/data-management/{id}` | GET admin/user-and-teams |
| `admin.edit_profile` | AdminDashboardController@editProfile | `GET admin/edit-profile/{id}` | GET admin/user-and-teams |
| `admin.payment_invoices` | AdminDashboardController@paymentInvoices | `GET admin/payment-invoices` | GET admin/getPlanDetails, GET admin/payment-invoices/list |
| `admin.plan_details` | AdminDashboardController@getPlanDetails | `GET admin/getPlanDetails` | GET admin/payment-invoices, POST admin/apply-coupon, POST admin/create-order, POST admin/verifyTransaction |
| `admin.update_password` | AdminDashboardController@updatePassword | `GET admin/update-password/{id}` | GET admin/user-and-teams |
| `admin.user_and_teams` | AdminDashboardController@userAndTeams | `GET admin/user-and-teams` | GET admin/create-user, GET admin/customize-report-user-wise/{id}, GET admin/data-management/{id}, GET admin/edit-profile/{id}, GET admin/get-user-wise-customize-question/{id}, GET admin/patient-list/{id}, GET admin/permissions/{id}, GET admin/update-password/{id} |
| `admin.user_patient_list` | AdminDashboardController@userPatientList | `GET admin/patient-list/{id}` | GET admin/user-and-teams |
| `admin.user_permissions` | AdminDashboardController@editPermissions | `GET admin/permissions/{id}` | GET admin/user-and-teams |
| `admin.user_previous_visits` | AdminDashboardController@userPreviousVisits | `GET admin/patient-list/{id}/previous-visits/{patientId}` | GET admin/patient-list/{id}, GET admin/user-and-teams, POST admin/report/viewAllReport, POST admin/report/viewVisitReport |
| `admin.visit_report_view` | AdminDashboardController@viewVisitReport | `POST admin/report/viewVisitReport` | GET admin/patient-list/{id}/previous-visits/{patientId}, GET admin/user-and-teams |
| `allReportView` | ReportController@viewAllReportV2 | `POST report/viewAllReport` | GET patientlist, GET previousVisits/{id} |
| `appointment.add-appointment` | AppointmentController@addAppointment | `GET add-appointment` | GET add-patient, GET appointment-list |
| `appointment.add_patient_for_appointment` | AppointmentController@addPatientForAppointment | `GET add-patient` | GET add-appointment, GET appointment-list |
| `appointment.appointment_history` | AppointmentController@appointmentHistory | `GET appointment-history` | GET appointment-list |
| `appointment.appointment_list` | AppointmentController@appointmentList | `GET appointment-list` | GET add-appointment, GET appointment-history, GET edit-appointment/{appointmentId}, GET view-appointment/{appointmentId} |
| `appointment.deleted_tab` |  |  |  |
| `appointment.done_tab` |  |  |  |
| `appointment.edit_appointment` | AppointmentController@editAppointment | `GET edit-appointment/{appointmentId}` | GET appointment-list |
| `appointment.missed_tab` |  |  |  |
| `appointment.tabs` |  |  |  |
| `appointment.view_appointment` | AppointmentController@viewAppointment | `GET view-appointment/{appointmentId}` | GET appointment-list |
| `appointment.visited_tab` |  |  |  |
| `auth.admin_signUp` | NewSignUpController@adminSignUp | `GET sign-up-admin` |  |
| `auth.college_signUp` | NewSignUpController@collegeSignUp | `GET sign-up-college` |  |
| `auth.forgot_password` | forgotPasswordController@forgotPassword | `GET forgotPassword` | GET login |
| `auth.login` | loginController@login | `GET login` | /images/nt_v2/common/drop-down.svg, GET forgotPassword, GET signup |
| `auth.nt-lite.nt_lite_add_patient_view` |  |  |  |
| `auth.nt-lite.nt_lite_dashboard` | NtLiteDashboardController@index | `GET nt-lite/dashboard` | GET dashboard, GET nt-lite/getPlanStatus |
| `auth.nt-lite.nt_lite_edit_payment` | NtLiteDashboardController@editPayment | `GET nt-lite/edit-payment` | /updatePaymentDetails, GET nt-lite/settings |
| `auth.nt-lite.nt_lite_live_nadi` | NtLiteLiveNadiController@index | `GET nt-lite/live-nadi` | /, GET dashboard, GET nt-lite/dashboard |
| `auth.nt-lite.nt_lite_patient_report` | NtLiteLiveNadiController@index | `GET nt-lite/live-nadi` | GET dashboard, GET nt-lite/dashboard, POST nt-lite/getVisitReports |
| `auth.nt-lite.nt_lite_payment_view` |  |  | GET nt-lite/edit-payment |
| `auth.nt-lite.nt_lite_previous_visits` | NtLiteDashboardController@previousVisits | `GET nt-lite/previousVisits/{id}` | GET dashboard, GET nt-lite/getPlanStatus, POST nt-lite/getVisitPrescription, POST nt-lite/getVisitReports |
| `auth.nt-lite.nt_lite_settings` | NtLiteDashboardController@settings | `GET nt-lite/settings` |  |
| `auth.nt-lite.nt_lite_signup_form` |  |  | GET login |
| `auth.nt-lite.nt_lite_success_modal` |  |  |  |
| `auth.nt-lite.nt_lite_verify_modal` |  |  |  |
| `auth.nt_lite_signup` | NtLiteSignUpController@showSignUp | `GET nt-lite/sign-up` |  |
| `auth.signup` | NewSignUpController@doctorSignUp | `GET sign-up` |  |
| `auth.signup-content.admin_sign_up_component` |  |  | GET login |
| `auth.signup-content.college_sign_up_component` |  |  | GET login |
| `auth.signup-content.new_sign_up_component` |  |  | GET login |
| `auth.tabs` | NewSignUpController@signup | `GET signup` | GET sign-up, GET sign-up-admin |
| `corporate-patient-module.dashboard` | PatientDashboardManagementController@corporatePatientDashboard | `GET corporate/patientDashboard` |  |
| `customize.add_question` | AdminCustomizeController@index, CustomizeController@index | `GET admin/add-question` | GET admin/customize-question |
| `customize.add_question_v2` | AdminCustomizeController@customizeQuestion | `GET admin/customize-question` |  |
| `customize.customize` | CustomizeController@customize | `GET customize` |  |
| `customize.customize_questionnaire` |  |  | GET admin/add-question, GET admin/user-and-teams |
| `customize.customize_report` | AdminCustomizeController@customizeReport | `GET admin/customize-report` | GET admin/user-and-teams |
| `customize.customize_tabs` |  |  | GET customize |
| `customize.report_single_modal` |  |  |  |
| `customize.user_wise_customize_questionnaire` | AdminCustomizeController@getUserWiseCustomizeQuestion | `GET admin/get-user-wise-customize-question/{id}` | GET admin/customize-question, GET admin/user-and-teams |
| `customize.user_wise_customize_report` | AdminCustomizeController@getCustomizeReportUserWise | `GET admin/customize-report-user-wise/{id}` | GET admin/user-and-teams |
| `design-form.add_form_details` | DesignFormController@addFormDetails | `GET design-form/add` | GET design-form/edit-details |
| `design-form.customize_tab_form` | DesignFormController@customizeTabForm | `GET design-form/customize-tab` |  |
| `design-form.edit_form` | DesignFormController@editForm | `GET design-form/edit` |  |
| `design-form.edit_form_details` | DesignFormController@editFormDetails | `GET design-form/edit-details` | GET design-form/edit-details |
| `design-form.reorder_form` | DesignFormController@reorderForm | `GET design-form/reorder` |  |
| `design-form.select_keywords` | DesignFormController@selectKeywords | `GET design-form/keywords` |  |
| `doctor_dashboard.appointment_card` |  |  |  |
| `doctor_dashboard.banner` |  |  |  |
| `doctor_dashboard.blogs` |  |  |  |
| `doctor_dashboard.calendar` |  |  |  |
| `doctor_dashboard.dashboard` | DashboardController@index | `GET dashboard` | GET add-appointment, GET add-member, GET appointment-list, GET edit-member/{id}, GET patientlist, GET previousVisits/{id}, POST getUserCurrentSummary, POST getUserCustomizeSummary |
| `doctor_dashboard.doctor_details` |  |  |  |
| `doctor_dashboard.feature_buttons` |  |  | GET add-member, GET patientlist |
| `doctor_dashboard.referral_card` |  |  |  |
| `doctor_dashboard.sama_nirama_stats` |  |  |  |
| `doctor_dashboard.total_count` |  |  |  |
| `doctor_dashboard.vikruti_stats` |  |  |  |
| `errors.400` | UnauthorizedController@error400 | `GET error-400` |  |
| `errors.401` | UnauthorizedController@error401 | `GET error-401` |  |
| `errors.403` | UnauthorizedController@error403 | `GET error-403` |  |
| `errors.404` | DashboardController@invoice, UnauthorizedController@error404 | `GET error-404`, `GET invoice/{invoiceId}` |  |
| `errors.405` |  |  |  |
| `errors.410` | AddMemberController@index | `GET add-member` |  |
| `errors.500` | UnauthorizedController@error500 | `GET error-500` |  |
| `errors.503` | UnauthorizedController@error503 | `GET error-503` |  |
| `errors.504` | UnauthorizedController@error504 | `GET error-504` |  |
| `errors.expiredMedicalId` | DietController@index, DietController@skipDiet, FeeDetailsController@index, LiveNadiController@liveNadi, ManualNadiKeywordsController@index, MarkOnImageController@index, PrakrutiQuestionsController@index, PrescriptionController@index, UnauthorizedController@error, VikrutiController@index | `GET diet`, `GET diet-lifestyle`, `GET error`, `GET fee-details`, `GET medical-assessment`, `GET nadi-image`, `GET nadi-keywords`, `GET prakruti`, `GET prescription`, `GET vikruti` | /patientlist |
| `errors.expiredMedicalIdV3` | MedicalAssessmentV3Controller@liveNadiV3 | `GET medical-assessment-v3` | /patientlist |
| `errors.footer` |  |  |  |
| `errors.limited_access` | VikrutiController@index | `GET vikruti` |  |
| `errors.regionRestricted` | UnauthorizedController@regionRestricted | `GET region-restricted` | POST logout |
| `external.external_assessment` | ExternalNadiController@externalAssessment | `GET nt-capture` |  |
| `external.input_validation` | ExternalNadiController@externalAssessment | `GET nt-capture` |  |
| `external.naditabs.assess_nadi_tab` |  |  |  |
| `external.naditabs.assess_nadi_tab_bluetooth` |  |  |  |
| `external.non_external_user` | ExternalNadiController@externalAssessment | `GET nt-capture` |  |
| `external.unauthorized` | ExternalNadiController@externalAssessment | `GET nt-capture` |  |
| `help.help` | HelpController@helpCenter | `GET help-center` |  |
| `live-nadi-bluetooth-not-supported-page` |  |  |  |
| `live-nadi-bluetooth-section` |  |  |  |
| `live-nadi-nt-linker-section` |  |  |  |
| `live-nadi-usb-section` |  |  |  |
| `live_nadi.assess_nadi_tab` |  |  |  |
| `live_nadi.assess_nadi_tab_bluetooth` |  |  |  |
| `live_nadi.assess_nav_bar` |  |  |  |
| `live_nadi.current_medical_details_card` |  |  |  |
| `live_nadi.current_patient_details_card` |  |  |  |
| `live_nadi.manual_nadi_tab` |  |  |  |
| `live_nadi.medical_assessment` | LiveNadiController@liveNadi | `GET medical-assessment` |  |
| `live_nadi.prakruti_details_card` |  |  |  |
| `medical_assessment.assess_nadi_tab` |  |  |  |
| `medical_assessment.assess_nadi_tab_bluetooth` |  |  |  |
| `medical_assessment.care_services` |  |  |  |
| `medical_assessment.case_study` |  |  |  |
| `medical_assessment.diet.diet_planner` |  |  | POST medical-assessment-v3/diet/current, POST medical-assessment-v3/diet/generate, POST medical-assessment-v3/diet/update |
| `medical_assessment.manual_nadi_tab` |  |  |  |
| `medical_assessment.medical_assesment` | MedicalAssessmentV3Controller@liveNadiV3 | `GET medical-assessment-v3` |  |
| `medical_assessment.nadi_tab` |  |  |  |
| `medical_assessment.prescription_tab` |  |  |  |
| `medical_assessment.tabs` |  |  |  |
| `medical_assessment.yoga.yoga_planner` |  |  | /images/yoga/calories-burn.svg, /images/yoga/dumbbell.svg, /images/yoga/exercise.svg, /images/yoga/session.svg, /images/yoga/yoga.svg, POST medical-assessment-v3/diet/generate, POST medical-assessment-v3/yoga/current, POST medical-assessment-v3/yoga/update |
| `medical_inventory.company` | CompanyController@company | `GET company` | GET edit-company/{id} |
| `medical_inventory.edit_company` | CompanyController@editCompany | `GET edit-company/{id}` | GET inventory |
| `medical_inventory.edit_ingredient` | IngredientsController@editIngredient | `GET edit-ingredient/{ingredientId}` | GET inventory |
| `medical_inventory.edit_medicine` | MedicineController@editMedicine | `GET edit-medicine/{medicineId}` | GET inventory |
| `medical_inventory.edit_pudi` | PudiController@editPudi | `GET edit-pudi/{pudiId}` | GET inventory |
| `medical_inventory.edit_supplement` | MedicineController@editSupplement | `GET edit-supplement/{medicineId}` | GET inventory |
| `medical_inventory.ingredients` | IngredientsController@ingredient | `GET ingredient` | GET edit-ingredient/{ingredientId} |
| `medical_inventory.medical-inventory` | InventoryController@inventory | `GET inventory` |  |
| `medical_inventory.medicine` | MedicineController@medicine | `GET medicine` | POST editMedicine/{medicalPrescriptionId} |
| `medical_inventory.medicine-type` | MedicineTypeController@medicineType | `GET medicine-type` |  |
| `medical_inventory.pudi` | PudiController@pudi | `GET pudi` | GET edit-pudi/{pudiId} |
| `medical_inventory.supplement` |  |  | GET edit-supplement/{medicineId} |
| `medical_inventory.tabs` |  |  |  |
| `my_account.addClinicDetails` | AddClinicDetailsController@addClinicDetails | `GET add-clinic` | GET clinic, GET profile |
| `my_account.billing_details` |  |  |  |
| `my_account.change_password` | ChangePasswordController@changePassword | `GET change-password` |  |
| `my_account.clinicList` | ClinicListController@clinicList | `GET clinic` | GET add-clinic, GET profile |
| `my_account.editClinicDetails` | EditClinicDetailsController@editClinicDetails | `GET edit-clinic/{id}` | GET clinic, GET profile |
| `my_account.edit_payment` | EditDoctorDetailsController@editPaymentDetails | `GET edit-payment` | GET profile |
| `my_account.edit_profile` | EditDoctorDetailsController@editDoctorProfile | `GET editprofile` | GET profile |
| `my_account.kyc_assess_nav_bar` |  |  |  |
| `my_account.my_account_tab` |  |  | GET editprofile |
| `my_account.my_devices_tab` |  |  |  |
| `my_account.myaccount` | EditDoctorDetailsController@editDoctorDetails | `GET profile` | GET clinic |
| `my_account.payment` |  |  |  |
| `my_account.payment_view` |  |  | GET edit-payment |
| `my_account.tabs` |  |  |  |
| `my_account.update_kyc` | DashboardController@updateKycDetails | `GET update_kyc` |  |
| `nadi_flow.consent_disclaimer_modal` |  |  |  |
| `nadi_flow.nadi_flow_prakruti_modal` |  |  |  |
| `nadi_flow.patient_details.patient_details_modal` |  |  |  |
| `nadi_flow.patient_details.patient_details_tab` |  |  |  |
| `nadi_flow.patient_details.symptoms_history_tab` |  |  |  |
| `nadi_flow.schedule_modal` |  |  |  |
| `notifications.notification` | NotificationController@notifications | `GET notifications` |  |
| `patient-module.ask_queries` | PatientDashboardController@askQueries | `GET patient/ask-queries` |  |
| `patient-module.daily_diet_lifestyle` | PatientDashboardController@dailyDietLifestyle | `GET patient/daily-diet-lifestyle/{parameterName}` |  |
| `patient-module.dashboard-content.banners` |  |  |  |
| `patient-module.dashboard-content.diet_data` |  |  | GET patient/daily-diet-lifestyle/{parameterName} |
| `patient-module.dashboard-content.nearest_center` |  |  |  |
| `patient-module.dashboard-content.patient_details` |  |  |  |
| `patient-module.dashboard-content.prakruti` |  |  |  |
| `patient-module.dashboard-content.prakruti_data` |  |  |  |
| `patient-module.dashboard-content.recommendation_card` |  |  |  |
| `patient-module.dashboard-content.tab_content` |  |  |  |
| `patient-module.dashboard-content.tabs.buttons.diet_btn` |  |  |  |
| `patient-module.dashboard-content.tabs.buttons.exercise_btn` |  |  |  |
| `patient-module.dashboard-content.tabs.buttons.music_btn` |  |  |  |
| `patient-module.dashboard-content.tabs.buttons.yoga_btn` |  |  |  |
| `patient-module.dashboard-content.tabs.diet` |  |  |  |
| `patient-module.dashboard-content.tabs.exercise` |  |  |  |
| `patient-module.dashboard-content.tabs.music` |  |  |  |
| `patient-module.dashboard-content.tabs.sleep_schedule` |  |  |  |
| `patient-module.dashboard-content.tabs.water_intake` |  |  |  |
| `patient-module.dashboard-content.tabs.yoga` |  |  |  |
| `patient-module.dashboard-content.vikruti_data` |  |  | GET patient/visits |
| `patient-module.data_consent` | PatientDashboardController@dataConsent | `GET patient/data-consent` |  |
| `patient-module.edit_profile` | PatientDashboardController@editProfile | `GET patient/edit` |  |
| `patient-module.patientAllReportsView` | PatientDashboardController@patientViewAllReports | `POST patient/report/viewAllReports` | GET patient/visits |
| `patient-module.patientArogyaDarshikaView` | PatientDashboardController@patientViewArogyaDarshika |  | GET patient/visits |
| `patient-module.patientSwasthyaDarshikaView` | PatientDashboardController@patientViewSwasthyaDarshika | `POST patient/report/viewSwasthyaDarshika` | GET patient/visits |
| `patient-module.patientVisitReportView` | PatientDashboardController@patientViewVisitReport | `POST patient/report/viewVisitReport` | GET patient/visits |
| `patient-module.patient_dashboard` | PatientDashboardController@index | `GET patient/dashboard` |  |
| `patient-module.request_appointment` | RequestAppointmentController@requestAppointment | `GET patient/request-appointment` |  |
| `patient-module.visit_history` | PatientVisitController@visitHistory | `GET patient/visits` |  |
| `patient.add-member` | AddMemberController@index | `GET add-member` | GET patientlist |
| `patient.add-member-tab` |  |  |  |
| `patient.anonymous-tab` |  |  |  |
| `patient.book-appointment-fields` |  |  |  |
| `patient.edit_member` | EditMemberController@index | `GET edit-member/{id}` | GET patientlist |
| `patient.patientlist` | PatientListController@index | `GET patientlist` | GET add-member |
| `patient.previousVisits` | PreviousVisitsController@index | `GET previousVisits/{id}` | GET patientlist |
| `patient.tabs` |  |  |  |
| `patient.view_member` | ViewMemberController@index | `GET view-member/{id}` | /edit-member/, GET patientlist |
| `payments.samvit_checkout` |  |  | /sc-checkout/callback |
| `payments.samvit_checkout_error` |  |  |  |
| `receptionist.add-receptionist` | ReceptionistController@addReception | `GET add-reception` | GET reception |
| `receptionist.edit-receptionist` | ReceptionistController@editReception | `GET edit-reception/{id}` | GET reception |
| `receptionist.set-permission` | ReceptionistController@setPermission | `GET set-permission` | GET reception |
| `receptionist.view-receptionist` | ReceptionistController@index | `GET reception` | GET add-reception, GET edit-reception/{id}, GET set-permission |
| `researchDashboardPages.aniruddhaList` | ResearchDashboardController@getAllAniruddhaRule | `GET researchDashboard/aniruddhaList` | POST add-aniruddha-rule, POST edit-aniruddha-rule |
| `researchDashboardPages.commonJson` | ResearchDashboardController@getAllCommonJsonData | `GET researchDashboard/commonJson` |  |
| `researchDashboardPages.criteriaList` | ResearchDashboardController@getAllRules | `GET researchDashboard/criteriaList` | POST add-rule, POST edit-rule |
| `researchDashboardPages.dayNames` | ResearchDashboardController@getAllDayNames | `GET researchDashboard/dayNames` |  |
| `researchDashboardPages.exerciseCategory` | ResearchDashboardController@getAllExerciseCategory | `GET researchDashboard/exerciseCategory` |  |
| `researchDashboardPages.exerciseData` | ResearchDashboardController@getAllExerciseData | `GET researchDashboard/exerciseData` |  |
| `researchDashboardPages.login` | ResearchDashboardController@researchLogin, ResearchDashboardController@researchLogout | `GET researchDashboard/researchLogout`, `GET researchLogin`, `POST researchDashboard/researchLogout` | POST checkResearchLogin |
| `researchDashboardPages.mealsCategory` | ResearchDashboardController@getAllMealsCategory | `GET researchDashboard/mealsCategory` |  |
| `researchDashboardPages.musicData` | ResearchDashboardController@getAllMusicData | `GET researchDashboard/musicData` |  |
| `researchDashboardPages.musicTags` | ResearchDashboardController@getAllMusicTags | `GET researchDashboard/musicTags` |  |
| `researchDashboardPages.recipeCategory` | ResearchDashboardController@addNewRecipeCategory, ResearchDashboardController@getAllRecipeCategory | `GET researchDashboard/recipeCategory`, `POST researchDashboard/addNewRecipeCategory` |  |
| `researchDashboardPages.recipePreference` | ResearchDashboardController@getAllRecipePreferenceJsonData | `GET researchDashboard/recipePreference` |  |
| `researchDashboardPages.recipeTags` | ResearchDashboardController@recipeTags | `GET researchDashboard/recipeTags` |  |
| `researchDashboardPages.statesNames` | ResearchDashboardController@statesNames | `GET researchDashboard/statesNames` |  |
| `researchDashboardPages.tagging` | ResearchDashboardController@getTagging | `GET researchDashboard/getTagging` |  |
| `researchDashboardPages.yogaCategory` | ResearchDashboardController@getAllYogaCategory | `GET researchDashboard/yogaCategory` |  |
| `researchDashboardPages.yogaData` | ResearchDashboardController@getAllYogaData, ResearchDashboardController@updateYogaJsonData | `GET researchDashboard/yogaData`, `POST researchDashboard/updateYogaJsonData` |  |
| `research_dashboard.college_dashboard` | HelpController@collegeDashboard | `GET nt-map`, `GET research-dashboard/college-dashboard` | GET dashboard, GET research-dashboard/nadi-analysis-1, GET research-dashboard/nadi-analysis-2, GET research-dashboard/nadi-tarangini-map |
| `research_dashboard.home_page` | HelpController@homePage | `GET research-dashboard/research-dashboard-home` | GET research-dashboard/college-dashboard, GET research-dashboard/nadi-analysis-1, GET research-dashboard/nadi-analysis-2, GET research-dashboard/nadi-tarangini-map |
| `research_dashboard.nadi_analysis_1` | HelpController@nadiAnalysis1 | `GET research-dashboard/nadi-analysis-1` | GET research-dashboard/college-dashboard, POST research-dashboard/download-nadi-file-data, POST research-dashboard/fetch-patient-visits, POST research-dashboard/get-labels-using-medicalid, POST research-dashboard/get-ten-seconds-nadidata |
| `research_dashboard.nadi_analysis_2` | HelpController@nadiAnalysis2 | `GET research-dashboard/nadi-analysis-2` | GET research-dashboard/college-dashboard, POST research-dashboard/get-nadi-analysis-2 |
| `research_dashboard.nt_map` | HelpController@nadiTaranginiMap | `GET research-dashboard/nadi-tarangini-map`, `GET research-dashboard/reports` | GET research-dashboard/college-dashboard |
| `research_dashboard.researchTestDiet` | ResearchDashboardController@researchTestDiet | `GET research-diet` |  |
| `research_dashboard.research_dashboard_layout` |  |  |  |
| `research_dashboard.research_dashboard_main_layout` |  |  |  |
| `research_dashboard.research_dashboard_nav_layout` |  |  | GET research-dashboard/college-dashboard |
| `research_dashboard.research_dashboard_sidebar` |  |  |  |
| `rutucharya.download_rutucharya` | DownloadRutucharyaController@index | `GET downloadRutucharya` |  |
| `subscription.checkout` | DashboardController@checkout | `GET checkout` | /, GET checkout, GET subscription |
| `subscription_plans` | DashboardController@getSubscriptionData | `GET subscription` |  |
| `unauthorized` |  |  |  |
| `vendor.pagination.bootstrap-4` |  |  |  |
| `vendor.pagination.default` |  |  |  |
| `vendor.pagination.semantic-ui` |  |  |  |
| `vendor.pagination.simple-bootstrap-4` |  |  |  |
| `vendor.pagination.simple-default` |  |  |  |
| `vendor.pagination.simple-tailwind` |  |  |  |
| `vendor.pagination.tailwind` |  |  |  |
| `visitReportView` | ReportController@viewVisitReport | `POST report/viewVisitReport` | GET patientlist, GET previousVisits/{id} |

Partials (layouts, components, modals, emails): 91
