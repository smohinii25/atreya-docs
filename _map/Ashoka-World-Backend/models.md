# Models and tables: Ashoka-World-Backend

Built from commit `8dfbb37db7d71a400b3656bd50fbed6173908a24` by scripts/models.sh (static parse).

192 models, 192 tables (111 with migrations, 81 without: their columns are unknown from code), 1 table names inferred from class names.

## Models

| Model | Table | Relations | Source |
|---|---|---|---|
| AllCountryNames | `all_country_names` |  | `app/Models/AllCountryNames.php` |
| AllNotificationsInfo | `all_notifications_info` |  | `app/Models/AllNotificationsInfo.php` |
| AllPrakrutiTypes | `all_prakruti_types` |  | `app/Models/AllPrakrutiTypes.php` |
| AniruddhaRuleList | `aniruddha_rule_list` |  | `app/Models/AniruddhaRuleList.php` |
| ApiEndpoints | `api_endpoints` |  | `app/Models/ApiEndpoints.php` |
| AppVersions | `app_versions` |  | `app/Models/AppVersions.php` |
| ArogyaDarshikaData | `arogya_darshika_data` |  | `app/Models/ArogyaDarshikaData.php` |
| ArogyaDarshikaSavedData | `arogya_darshika_saved_data` |  | `app/Models/ArogyaDarshikaSavedData.php` |
| AshokaCustomers | `ashoka_customers` |  | `app/Models/AshokaCustomers.php` |
| AshokaDashboardModulesMaster | `ashoka_dashboard_modules_master` |  | `app/Models/AshokaDashboardModulesMaster.php` |
| AshokaDepartmentsMaster | `ashoka_departments_master` |  | `app/Models/AshokaDepartmentsMaster.php` |
| AshokaPaymentOrder | `ashoka_payment_orders` |  | `app/Models/AshokaPaymentOrder.php` |
| AshokaQuotation | `ashoka_quotation` |  | `app/Models/AshokaQuotation.php` |
| AshokaRolesMaster | `ashoka_roles_master` | department: belongsTo AshokaDepartmentsMaster | `app/Models/AshokaRolesMaster.php` |
| AshokaSalesRequest | `ashoka_sales_request` | ashokaSubSalesRequests: hasMany AshokaSubSalesRequest | `app/Models/AshokaSalesRequest.php` |
| AshokaShipmentTracking | `ashoka_shipment_tracking` |  | `app/Models/AshokaShipmentTracking.php` |
| AshokaStatusCategoryMaster | `ashoka_status_category_master` | statuses: hasMany AshokaStatusMaster | `app/Models/AshokaStatusCategoryMaster.php` |
| AshokaStatusMaster | `ashoka_status_master` | category: belongsTo AshokaStatusCategoryMaster | `app/Models/AshokaStatusMaster.php` |
| AshokaStoresAssetsComponent | `ashoka_stores_assets_component` | asset: belongsTo AshokaStoresAssetsMaster | `app/Models/AshokaStoresAssetsComponent.php` |
| AshokaStoresAssetsMaster | `ashoka_stores_assets_master` |  | `app/Models/AshokaStoresAssetsMaster.php` |
| AshokaSubSalesRequest | `ashoka_sub_sales_request` | ashokaSalesRequest: belongsTo AshokaSalesRequest | `app/Models/AshokaSubSalesRequest.php` |
| AshokaUsersMaster | `ashoka_users_master` | role: belongsTo AshokaRolesMaster | `app/Models/AshokaUsersMaster.php` |
| AssessmentCategory | `assessment_category` |  | `app/Models/AssessmentCategory.php` |
| BannersData | `banners_data` |  | `app/Models/BannersData.php` |
| CalendarCat | `calendar_cat` |  | `app/Models/CalendarCat.php` |
| CalendarEvent | `calendar_events` |  | `app/Models/CalendarEvent.php` |
| CalendarParam | `calendar_param` |  | `app/Models/CalendarParam.php` |
| CalendarUser | `calendar_users` |  | `app/Models/CalendarUser.php` |
| CampaignData | `campaign_data` |  | `app/Models/CampaignData.php` |
| CategoryValue | `category_value` |  | `app/Models/CategoryValue.php` |
| Cme | `cme` |  | `app/Models/Cme.php` |
| CollaborateWithUs | `collaborate_with_us` |  | `app/Models/CollaborateWithUs.php` |
| CommonData | `common_data` |  | `app/Models/CommonData.php` |
| CommonJson | `common_json` |  | `app/Models/CommonJson.php` |
| CorporateInfo | `corporate_info` |  | `app/Models/CorporateInfo.php` |
| CorporatePayments | `corporate_payments` |  | `app/Models/CorporatePayments.php` |
| CountryWiseStates | `country_wise_states` |  | `app/Models/CountryWiseStates.php` |
| CronStatus | `cron_status` |  | `app/Models/CronStatus.php` |
| CurrencyType | `currency_type` |  | `app/Models/CurrencyType.php` |
| CustomizeTab | `customize_tab` | children: hasMany CustomizeTab | `app/Models/CustomizeTab.php` |
| DaynamesJson | `daynames_json` |  | `app/Models/DaynamesJson.php` |
| DoctorFormDetail | `doctor_form_details` |  | `app/Models/DoctorFormDetail.php` |
| DoctorMedicineInventory | `doctor_medicine_inventory` | medicineCompany: belongsTo MedicineCompany; medicineQuantity: belongsTo MedicineQuantity; medicineType: belongsTo MedicineType | `app/Models/DoctorMedicineInventory.php` |
| DoctorMultichoiceOption | `doctor_multichoice_options` | multichoiceOption: belongsTo MultichoiceOptions | `app/Models/DoctorMultichoiceOption.php` |
| DoctorQualification | `doctor_qualification` |  | `app/Models/DoctorQualification.php` |
| DoctorType | `doctor_type` |  | `app/Models/DoctorType.php` |
| EnachCustomers | `enach_customers` |  | `app/Models/EnachCustomers.php` |
| EnachDebitLog | `enach_debit_logs` |  | `app/Models/EnachDebitLog.php` |
| EnachMandate | `enach_mandate` | customer: belongsTo EnachCustomers | `app/Models/EnachMandate.php` |
| ExerciseCategory | `exercise_category` |  | `app/Models/ExerciseCategory.php` |
| ExerciseTags | `exercise_tags` |  | `app/Models/ExerciseTags.php` |
| ExternalWebhookLogs | `external_webhook_logs` |  | `app/Models/External/ExternalWebhookLogs.php` |
| FaqData | `faqs` |  | `app/Models/FaqData.php` |
| Feature | `features` |  | `app/Models/Feature.php` |
| HrvResult | `hrv_result` |  | `app/Models/HrvResult.php` |
| Ingredient | `ingredients_list` |  | `app/Models/Ingredient.php` |
| InputValidationsMaster | `input_validations_master` |  | `app/Models/InputValidationsMaster.php` |
| JsonArrayRuleslist | `json_array_ruleslist` |  | `app/Models/JsonArrayRuleslist.php` |
| Languages | `languages` |  | `app/Models/Languages.php` |
| LocalityInfo | `locality_info` |  | `app/Models/LocalityInfo.php` |
| MajorSymptomData | `major_symptom_data` |  | `app/Models/MajorSymptomData.php` |
| MarkOnImage | `markonimage_list` |  | `app/Models/MarkOnImage.php` |
| MasterContents | `master_contents` |  | `app/Models/MasterContents.php` |
| MealsCategory | `meals_category` |  | `app/Models/MealsCategory.php` |
| MedicalFormDetail | `medical_form_details` |  | `app/Models/MedicalFormDetail.php` |
| MedicalFormList | `medical_form_list` |  | `app/Models/MedicalFormList.php` |
| MedicalReport | `medical_report` |  | `app/Models/MedicalReport.php` |
| MedicalReportDiet | `medical_report_diet` |  | `app/Models/MedicalReportDiet.php` |
| MedicalReportFileUpload | `medical_report_file_upload` |  | `app/Models/MedicalReportFileUpload.php` |
| MedicalReportImageMarker | `medical_report_image_markers` |  | `app/Models/MedicalReportImageMarker.php` |
| MedicalReportKeyMapping | `medical_report_key_mapping` |  | `app/Models/MedicalReportKeyMapping.php` |
| MedicalReportPrescription | `medical_report_prescription` |  | `app/Models/MedicalReportPrescription.php` |
| MedicalReportSymptomDetail | `medical_report_symptom_details_1` |  | `app/Models/MedicalReportSymptomDetail.php` |
| MedicineCompany | `medicine_company` |  | `app/Models/MedicineCompany.php` |
| MedicineNames | `medicine_names` |  | `app/Models/MedicineNames.php` |
| MedicineQuantity | `medicine_quantity` |  | `app/Models/MedicineQuantity.php` |
| MedicineQuantityTypeCategory | `medicine_quantity_type_category` |  | `app/Models/MedicineQuantityTypeCategory.php` |
| MedicineTiming | `medicine_timing` |  | `app/Models/MedicineTiming.php` |
| MedicineType | `medicine_type` |  | `app/Models/MedicineType.php` |
| MedicineWithConsume | `medicine_with_consume` |  | `app/Models/MedicineWithConsume.php` |
| MultichoiceFieldList | `multichoice_field_list` |  | `app/Models/MultichoiceFieldList.php` |
| MultichoiceOptions | `multichoice_options` |  | `app/Models/MultichoiceOptions.php` |
| MusicLibrary | `music_library` |  | `app/Models/MusicLibrary.php` |
| MusicTags | `music_tags` |  | `app/Models/MusicTags.php` |
| MyStatsData | `my_stats_data` |  | `app/Models/MyStatsData.php` |
| NTApplicationVersion | `nt_application_version` |  | `app/Models/NTApplicationVersion.php` |
| NadiAveragePulseData | `nadi_average_pulse_data` |  | `app/Models/NadiAveragePulseData.php` |
| NadiManualReportGrant | `nadi_manual_report_grants` |  | `app/Models/NadiManualReportGrant.php` |
| NPAnalysisDataModel | `np_analysis_data` |  | `app/Models/NadiParikshaModels/NPAnalysisDataModel.php` |
| NPPrakritiAnswers | `np_prakriti_answers` |  | `app/Models/NadiParikshaModels/NPPrakritiAnswers.php` |
| NPSurveyQuestion | `np_survey_questions` |  | `app/Models/NadiParikshaModels/NPSurveyQuestion.php` |
| NPUserModel | `np_users` |  | `app/Models/NadiParikshaModels/NPUserModel.php` |
| NPUserSurveyAnswer | `np_user_survey_answers` |  | `app/Models/NadiParikshaModels/NPUserSurveyAnswer.php` |
| NPVisitParameter | `np_visit_parameters` |  | `app/Models/NadiParikshaModels/NPVisitParameter.php` |
| NPVisitParameterData | `np_visit_parameter_data` |  | `app/Models/NadiParikshaModels/NPVisitParameterData.php` |
| NpAdminDashboardFeatures | `np_admin_dashboard_features` |  | `app/Models/NadiParikshaModels/NpAdminDashboardFeatures.php` |
| NpAdminRole | `np_admin_role` |  | `app/Models/NadiParikshaModels/NpAdminRole.php` |
| NpAdminUser | `np_admin_users` |  | `app/Models/NadiParikshaModels/NpAdminUser.php` |
| NpAppVersion | `np_app_version` |  | `app/Models/NadiParikshaModels/NpAppVersion.php` |
| NpCoupon | `np_coupons` |  | `app/Models/NadiParikshaModels/NpCoupon.php` |
| NpDoctorsDetails | `np_doctors_details` |  | `app/Models/NadiParikshaModels/NpDoctorsDetails.php` |
| NpExternalServiceLogs | `np_external_service_logs` |  | `app/Models/NadiParikshaModels/NpExternalServiceLogs.php` |
| NpLanguage | `np_languages` |  | `app/Models/NadiParikshaModels/NpLanguage.php` |
| NpMasterContent | `np_master_content` |  | `app/Models/NadiParikshaModels/NpMasterContent.php` |
| NpNotifyMe | `np_notify_me` |  | `app/Models/NadiParikshaModels/NpNotifyMe.php` |
| NpOTPattemptMaster | `np_otp_attempt_master` |  | `app/Models/NadiParikshaModels/NpOTPattemptMaster.php` |
| NpOtherReportData | `np_other_report_data` |  | `app/Models/NadiParikshaModels/NpOtherReportData.php` |
| NpPaymentDetails | `np_payment_details` |  | `app/Models/NadiParikshaModels/NpPaymentDetails.php` |
| NpPrakritiQuestion | `np_prakriti_questions` |  | `app/Models/NadiParikshaModels/NpPrakritiQuestion.php` |
| NpPricingMaster | `np_pricing_master` |  | `app/Models/NadiParikshaModels/NpPricingMaster.php` |
| NpUserActivity | `np_user_activity` |  | `app/Models/NadiParikshaModels/NpUserActivity.php` |
| NpUserApiLogs | `np_user_api_logs` |  | `app/Models/NadiParikshaModels/NpUserApiLogs.php` |
| NadiReport | `nadi_report` | medical: belongsTo MedicalReport | `app/Models/NadiReport.php` |
| NakshatraInput | `nakshtra_input` |  | `app/Models/NakshatraInput.php` |
| NakshatraResult | `nakshatra_result` | medical: belongsTo Medical | `app/Models/NakshatraResult.php` |
| NotificationTopic | `notification_topics` |  | `app/Models/NotificationTopic.php` |
| NtCoupons | `nt_coupons` |  | `app/Models/NtCoupons.php` |
| OtherReportData | `other_report_data` |  | `app/Models/OtherReportData.php` |
| PatientPrakruti | `patient_prakruti` |  | `app/Models/PatientPrakruti.php` |
| PatientProfession | `patient_profession` |  | `app/Models/PatientProfession.php` |
| PatientQuestionAnswer | `patient_question_answer` |  | `app/Models/PatientQuestionAnswer.php` |
| PaymentGatewayResponse | `payment_gateway_response` |  | `app/Models/PaymentGatewayResponse.php` |
| PgBuyerDetail | `pg_buyer_details` |  | `app/Models/PgBuyerDetail.php` |
| PgDeviceList | `pg_device_list` |  | `app/Models/PgDeviceList.php` |
| PgDeviceMapping | `pg_device_mapping` |  | `app/Models/PgDeviceMapping.php` |
| PgDeviceReturnDetail | `pg_device_return_details` |  | `app/Models/PgDeviceReturnDetail.php` |
| PgOrderDetail | `pg_order_details` |  | `app/Models/PgOrderDetail.php` |
| PgOrderDispatch | `pg_order_dispatch_table` |  | `app/Models/PgOrderDispatch.php` |
| PgOrderIdGenerate | `pg_order_id_generate` |  | `app/Models/PgOrderIdGenerate.php` |
| PgPlanDetail | `pg_plan_details` |  | `app/Models/PgPlanDetail.php` |
| PostalCode | `postal_codes` |  | `app/Models/PostalCode.php` |
| PrakrutiDescriptionV1 | `prakruti_description_v1` |  | `app/Models/PrakrutiDescriptionV1.php` |
| PrakrutiWiseDiet | `prakruti_wise_diet` |  | `app/Models/PrakrutiWiseDiet.php` |
| ProfessionType | `profession_type` |  | `app/Models/ProfessionType.php` |
| ProjectVariable | `project_variables` |  | `app/Models/ProjectVariable.php` |
| RecipeCategory | `recipe_category` |  | `app/Models/RecipeCategory.php` |
| RecipePreferenceJson | `recipe_preference_json` |  | `app/Models/RecipePreferenceJson.php` |
| ReferColleague | `refer_colleague` |  | `app/Models/ReferColleague.php` |
| RequestCallback | `request_callback` |  | `app/Models/RequestCallback.php` |
| ResearchUsers | `research_users` |  | `app/Models/ResearchUsers.php` |
| ResourceNameMaster | `resource_name_master` |  | `app/Models/ResourceNameMaster.php` |
| RituInput | `ritu_input` |  | `app/Models/RituInput.php` |
| RutucharyaPeriodsDates | `rutucharya_periods_dates` |  | `app/Models/RutucharyaPeriodsDates.php` |
| SalutationTypes | `salutation_types` |  | `app/Models/SalutationTypes.php` |
| SessionLog | `session_log` | role: belongsTo Role; user: belongsTo User | `app/Models/SessionLog.php` |
| ShortUrl | `shorturl` |  | `app/Models/ShortUrl.php` |
| SpaReportSummary | `spa_report_summary` |  | `app/Models/SpaReportSummary.php` |
| SpaReportTherapy | `spa_report_therapy` |  | `app/Models/SpaReportTherapy.php` |
| StatesNames | `states_names` |  | `app/Models/StatesNames.php` |
| Subscription | `subscriptions` |  | `app/Models/Subscription.php` |
| SubscriptionStatus | `subscription_status` |  | `app/Models/SubscriptionStatus.php` |
| SubscriptionTypes | `subscription_types` |  | `app/Models/SubscriptionTypes.php` |
| SubscriptionTypesMaster | `subscription_types_master` |  | `app/Models/SubscriptionTypesMaster.php` |
| SubscriptionWiseReports | `subscription_wise_reports` |  | `app/Models/SubscriptionWiseReports.php` |
| SwasthyaReportData | `swasthya_report_data` |  | `app/Models/SwasthyaReportData.php` |
| SymptomCategory | `symptom_category` | createdBy: belongsTo User | `app/Models/SymptomCategory.php` |
| Symptoms | `symptoms` | category: belongsTo SymptomCategory; dropdownItems: hasMany SymptomsDropdownItem | `app/Models/Symptoms.php` |
| SymptomsDropdownItem | `symptoms_dropdown_item` | symptom: belongsTo Symptoms | `app/Models/SymptomsDropdownItem.php` |
| Transaction | `transactions` |  | `app/Models/Transaction.php` |
| AnalysisData | `analysis_data` |  | `app/Models/TuryaaModels/AnalysisData.php` |
| DailyQuestions | `daily_questions` |  | `app/Models/TuryaaModels/DailyQuestions.php` |
| DietData | `diet_data` |  | `app/Models/TuryaaModels/DietData.php` |
| GeneralDescription | `general_description` |  | `app/Models/TuryaaModels/GeneralDescription.php` |
| GetTuryaaPrakrutiQuestion | `prakriti_questions` |  | `app/Models/TuryaaModels/GetTuryaaPrakrutiQuestion.php` |
| KnowledgeData | `knowledge_data` |  | `app/Models/TuryaaModels/KnowledgeData.php` |
| PrakritiAnswers | `prakriti_answers` |  | `app/Models/TuryaaModels/PrakritiAnswers.php` |
| PrakritiAnswersDescriptions | `prakriti_answer_descriptions` |  | `app/Models/TuryaaModels/PrakritiAnswersDescriptions.php` |
| QuestionAnswers | `question_answers` |  | `app/Models/TuryaaModels/QuestionAnswers.php` |
| QuestionCategories | `question_categories` |  | `app/Models/TuryaaModels/QuestionCategories.php` |
| QuestionTypes | `question_types` |  | `app/Models/TuryaaModels/QuestionTypes.php` |
| Questions | `questions` |  | `app/Models/TuryaaModels/Questions.php` |
| TuryaaUserModel | `users` |  | `app/Models/TuryaaModels/TuryaaUserModel.php` |
| UserDietChoice | `user_diet_choice` |  | `app/Models/TuryaaModels/UserDietChoice.php` |
| UserStages | `user_stages` |  | `app/Models/TuryaaModels/UserStages.php` |
| VikrutiDescription | `vikruti_description` |  | `app/Models/TuryaaModels/VikrutiDescription.php` |
| VikrutiFeedbackQuestion | `vikruti_feedback_questions` |  | `app/Models/TuryaaModels/VikrutiFeedbackQuestion.php` |
| WellnessReport | `wellness_report` |  | `app/Models/TuryaaModels/WellnessReport.php` |
| WellnessTracking | `wellness_tracking` |  | `app/Models/TuryaaModels/WellnessTracking.php` |
| User | `users` (inferred) |  | `app/Models/User.php` |
| UserApiKeyMapping | `user_api_key_mapping` | user: belongsTo User | `app/Models/UserApiKeyMapping.php` |
| UserNadiCaptureType | `user_nadi_capture_type` |  | `app/Models/UserNadiCaptureType.php` |
| UserNotificationsInfo | `user_notifications_info` |  | `app/Models/UserNotificationsInfo.php` |
| UserPersonalInfo | `user_personal_info` |  | `app/Models/UserPersonalInfo.php` |
| UserReport | `user_report` |  | `app/Models/UserReport.php` |
| UserReportDescription | `user_report_descriptions` |  | `app/Models/UserReportDescription.php` |
| UserRole | `user_role` | users: hasMany UserPersonalInfo | `app/Models/UserRole.php` |
| UserSelectedCountry | `user_selected_countries` |  | `app/Models/UserSelectedCountry.php` |
| UserVikrutiDescriptionV1 | `user_vikruti_descriptions_v1` |  | `app/Models/UserVikrutiDescriptionV1.php` |
| WhitelistedMobilenoTuryaa | `whitelisted_mobileno_turyaa` |  | `app/Models/WhitelistedMobilenoTuryaa.php` |
| YogaCategory | `yoga_category` |  | `app/Models/YogaCategory.php` |
| YogaJson | `yoga_json` |  | `app/Models/YogaJson.php` |
| YogaReportData | `yoga_report_data` |  | `app/Models/YogaReportData.php` |

## Tables

| Table | Models | Columns (from migrations) | Migrations |
|---|---|---|---|
| `all_country_names` | AllCountryNames | country_code, postal_code_lengths, postal_code_type | 2 |
| `all_notifications_info` | AllNotificationsInfo | routes | 1 |
| `all_prakruti_types` | AllPrakrutiTypes | unknown | 0 |
| `analysis_data` | AnalysisData | arogya_darshika_data, created_at, created_by, daily_data, feedback_rating_comment, goal, id, nadi_data, status, tongue_analysis_data, tongue_data, updated_at, updated_by, user_id, wds_input_json | 4 |
| `aniruddha_rule_list` | AniruddhaRuleList | unknown | 0 |
| `api_endpoints` | ApiEndpoints | create_date, id, is_active, is_public, is_public_reception, method, name, updated_date, url | 3 |
| `app_versions` | AppVersions | unknown | 0 |
| `arogya_darshika_data` | ArogyaDarshikaData | lang_kannda | 1 |
| `arogya_darshika_saved_data` | ArogyaDarshikaSavedData | lang_prakriti, lang_swasthya | 2 |
| `ashoka_customers` | AshokaCustomers | address, city, country, country_code, create_date, created_by, email, gst, id, is_quotation_send, last_modified_on, mobile_no, name, pincode, shipping_address, state, status, user_type | 3 |
| `ashoka_dashboard_modules_master` | AshokaDashboardModulesMaster | create_date, id, is_active, last_modified_on, module_name | 1 |
| `ashoka_departments_master` | AshokaDepartmentsMaster | create_date, department_name, id, is_active, last_modified_on | 1 |
| `ashoka_payment_orders` | AshokaPaymentOrder | amount, comment, created_at, created_by, currency_type, id, name, order_type, payment_date, status, track_status, updated_at, uploaded_files | 3 |
| `ashoka_quotation` | AshokaQuotation | create_date, created_by, currency_type, customer_id, file_name, id, last_modified_on, quotation_data, quotation_no, status, total_price | 3 |
| `ashoka_roles_master` | AshokaRolesMaster | access_tabs, create_date, department_id, id, is_active, last_modified_on, role_name | 2 |
| `ashoka_sales_request` | AshokaSalesRequest | actual_received_amount, address, bank, comment, country_code, create_date, currency_type, customer_name, device_dispatch_date, device_ids, dispatch_type, email, finance_payment_confirmation_status, gst_no, id, is_active, last_modified_on, mobile_no, payment_confirmation, payment_type, plan_type, quantity, received_amount, sale_amount, shipping_address, shipping_charges, status, track_status, user_id, user_type, want_seperate_invoice | 11 |
| `ashoka_shipment_tracking` | AshokaShipmentTracking | create_date, created_by, device_no, dispatch_link, id, invoice_details, invoice_link, invoice_no, is_active, last_modified_on, oc_create_date, oc_link, oc_no, quantity, request_id, status, total_paid, total_price, tracking_id | 5 |
| `ashoka_status_category_master` | AshokaStatusCategoryMaster | create_date, id, is_active, label, last_modified_on | 1 |
| `ashoka_status_master` | AshokaStatusMaster | category_id, create_date, id, is_active, label, last_modified_on | 1 |
| `ashoka_stores_assets_component` | AshokaStoresAssetsComponent | asset_id, assign_status, create_date, created_by, id, is_active, last_modified_on, serial_no, track_status | 2 |
| `ashoka_stores_assets_master` | AshokaStoresAssetsMaster | asset_name, create_date, created_by, id, is_active, last_modified_on | 2 |
| `ashoka_sub_sales_request` | AshokaSubSalesRequest | actual_sub_received_amount, is_amount_credited | 1 |
| `ashoka_users_master` | AshokaUsersMaster | assign_assets, auth_token, blood_group, country_code, create_date, email_id, employee_id, firstname, gender, id, is_active, last_modified_on, lastname, mobile_no, password, role_id, user_name | 4 |
| `assessment_category` | AssessmentCategory | unknown | 0 |
| `banners_data` | BannersData | accessibility, mobile_url | 1 |
| `calendar_cat` | CalendarCat | unknown | 0 |
| `calendar_events` | CalendarEvent | clinic_id, consultation_type, reception_id | 4 |
| `calendar_param` | CalendarParam | unknown | 0 |
| `calendar_users` | CalendarUser | unknown | 0 |
| `campaign_data` | CampaignData | unknown | 0 |
| `category_value` | CategoryValue | unknown | 0 |
| `cme` | Cme | unknown | 0 |
| `collaborate_with_us` | CollaborateWithUs | unknown | 0 |
| `common_data` | CommonData | created_at, data, id, label, updated_at | 1 |
| `common_json` | CommonJson | unknown | 0 |
| `corporate_info` | CorporateInfo | add_patient_url, city, corp_role_id, corporate_id, corporate_type, country, doctors_info, pincode, profile_image, state | 3 |
| `corporate_payments` | CorporatePayments | amount, corporate_id, create_date, created_by, id, invoice_info, invoice_url, last_modified_on, month, payment_date, payment_status, payment_type, status | 1 |
| `country_wise_states` | CountryWiseStates | timezone | 2 |
| `cron_status` | CronStatus | unknown | 0 |
| `currency_type` | CurrencyType | unknown | 0 |
| `customize_tab` | CustomizeTab | unknown | 0 |
| `daily_questions` | DailyQuestions | is_having_child, order, parent_condition_for_option | 2 |
| `daynames_json` | DaynamesJson | unknown | 0 |
| `diet_data` | DietData | created_at, diet_file, diet_json, id, ingredients_file, input_json, status, updated_at, user_id | 2 |
| `doctor_form_details` | DoctorFormDetail | unknown | 0 |
| `doctor_medicine_inventory` | DoctorMedicineInventory | is_active | 1 |
| `doctor_multichoice_options` | DoctorMultichoiceOption | unknown | 0 |
| `doctor_qualification` | DoctorQualification | unknown | 0 |
| `doctor_type` | DoctorType | unknown | 0 |
| `enach_customers` | EnachCustomers | country_code, create_date, created_by, email, full_name, id, is_active, last_modified_on, mobile | 2 |
| `enach_debit_logs` | EnachDebitLog | created_at, customer_id, gateway_message, gateway_txn_id, id, mandate_reg_no, scheduled_amount, scheduled_date, scheduling_request_json, scheduling_response_json, statusCode, statusMessage, txn_id, updated_at | 1 |
| `enach_mandate` | EnachMandate | BankTransactionID, account_number, alias_name, amount_type, bal_amt, cardNo, card_exp_month, card_exp_year, card_id, clnt_rqst_meta, create_date, customer_id, cvv_code, debit_end_date, debit_start_date, frequency, hash, id, input_pipe_data, last_modified_on, mandate_reg_no, mandate_status, max_amount, output_pipe_data, token, total_amount, tpsl_bank_cd, tpsl_txn_id, tpsl_txn_time, txn_amount, txn_err_msg, txn_id, txn_status, validation_input_json, validation_output_json, validation_status | 1 |
| `exercise_category` | ExerciseCategory | unknown | 0 |
| `exercise_tags` | ExerciseTags | unknown | 0 |
| `external_webhook_logs` | ExternalWebhookLogs | client_code, created_at, delivery_id, error_message, event_name, id, medical_id, patient_id, request_payload, response_payload, response_status, status, updated_at, user_id, visit_id, webhook_url | 1 |
| `faqs` | FaqData | unknown | 0 |
| `features` | Feature | create_date, id, is_having_child, name, parent_id, required_apis, updated_at | 2 |
| `general_description` | GeneralDescription | created_at, description, id, label, status, updated_at | 2 |
| `hrv_result` | HrvResult | unknown | 0 |
| `ingredients_list` | Ingredient | unknown | 0 |
| `input_validations_master` | InputValidationsMaster | create_date, id, is_active, label, last_modified_on, validation | 1 |
| `jobs` |  | attempts, available_at, created_at, id, payload, queue, reserved_at | 1 |
| `json_array_ruleslist` | JsonArrayRuleslist | unknown | 0 |
| `knowledge_data` | KnowledgeData | attachment, created, created_at, description, id, status, subtitle, title, updated_at | 1 |
| `languages` | Languages | unknown | 0 |
| `locality_info` | LocalityInfo | is_default, timezone | 2 |
| `major_symptom_data` | MajorSymptomData | gender, symptom_category_tag | 1 |
| `markonimage_list` | MarkOnImage | unknown | 0 |
| `master_contents` | MasterContents | content, create_date, id, is_active, last_modified_on, month_number, title, type, week_number | 2 |
| `meals_category` | MealsCategory | unknown | 0 |
| `medical_form_details` | MedicalFormDetail | unknown | 0 |
| `medical_form_list` | MedicalFormList | unknown | 0 |
| `medical_report` | MedicalReport | city, country, external_visit_id, field_id_1, ip_address, mark_on_image_url, panchakarma_recom, reception_id, recommendations, state, try_count, user_nadi_capture_type, yoga_recom | 10 |
| `medical_report_diet` | MedicalReportDiet | create_date, diet, doctor_id, id, is_active, last_modified_on, medical_id, patient_id, vikruti_type | 3 |
| `medical_report_file_upload` | MedicalReportFileUpload | unknown | 0 |
| `medical_report_image_markers` | MedicalReportImageMarker | unknown | 0 |
| `medical_report_key_mapping` | MedicalReportKeyMapping | unknown | 0 |
| `medical_report_prescription` | MedicalReportPrescription | is_active, other_details, total_quantity | 3 |
| `medical_report_symptom_details_1` | MedicalReportSymptomDetail | symptom_value | 1 |
| `medicine_company` | MedicineCompany | is_active | 1 |
| `medicine_names` | MedicineNames | create_date, created_by, id, is_active, last_modified_on, medicine_name, medicine_type | 1 |
| `medicine_quantity` | MedicineQuantity | category_type, is_active | 2 |
| `medicine_quantity_type_category` | MedicineQuantityTypeCategory | category, create_date, created_by, id, is_active, last_modified_on | 1 |
| `medicine_timing` | MedicineTiming | create_date, id, is_active, last_modified_on, order_by, timing_label | 2 |
| `medicine_type` | MedicineType | is_active, type | 2 |
| `medicine_with_consume` | MedicineWithConsume | consume_label, create_date, created_by, id, is_active, last_modified_on | 2 |
| `multichoice_field_list` | MultichoiceFieldList | unknown | 0 |
| `multichoice_options` | MultichoiceOptions | lang_kannda | 1 |
| `music_library` | MusicLibrary | unknown | 0 |
| `music_tags` | MusicTags | unknown | 0 |
| `my_stats_data` | MyStatsData | unknown | 0 |
| `nadi_average_pulse_data` | NadiAveragePulseData | lang_kannada | 2 |
| `nadi_manual_report_grants` | NadiManualReportGrant | action, comment, create_date, expiry_date, granted_by, id, last_modified_on, no_of_reports, plan_type, previous_expiry_date, previous_no_of_reports, requested_user_id, target_user_id | 2 |
| `nadi_report` | NadiReport | unknown | 0 |
| `nakshatra_result` | NakshatraResult | unknown | 0 |
| `nakshtra_input` | NakshatraInput | unknown | 0 |
| `notification_topics` | NotificationTopic | unknown | 0 |
| `np_admin_dashboard_features` | NpAdminDashboardFeatures | created_at, feature_name, id, parent_id, status, updated_at | 2 |
| `np_admin_role` | NpAdminRole | access_tabs, created_at, id, is_active, role_name, updated_at | 1 |
| `np_admin_users` | NpAdminUser | access_tabs, auth_token, created_at, created_by, email, id, name, role_id, status, updated_at, updated_by | 3 |
| `np_analysis_data` | NPAnalysisDataModel | arogya_darshika_data, created_at, created_by, daily_data, file_url, id, interactions, jiva_consent_status, jiva_created_at, location, nadi_data, nadi_status, nadi_taken_at, nt_device_id, payment_id, status, swasthya_data, updated_at, updated_by, user_id, wds_input_json | 8 |
| `np_app_version` | NpAppVersion | android_version_code, android_version_no, created_at, id, ios_build_no, ios_version_no, is_compulsory, updated_at | 1 |
| `np_coupons` | NpCoupon | coupon_code, created_at, discount, id, status, updated_at, valid_from, valid_until | 1 |
| `np_doctors_details` | NpDoctorsDetails | created_at, email, id, json_data, json_data_hi, json_data_mr, name, phone, status, updated_at | 2 |
| `np_external_service_logs` | NpExternalServiceLogs | created_at, id, identifier, provider, request_payload, response_payload, service_id, service_type, status, updated_at, webhook_payload | 1 |
| `np_languages` | NpLanguage | id, is_active, lang, lang_code | 1 |
| `np_master_content` | NpMasterContent | content, created_at, id, lang, status, type, updated_at | 1 |
| `np_notify_me` | NpNotifyMe | created_at, id, status, updated_at, user_id | 1 |
| `np_other_report_data` | NpOtherReportData | created_at, id, report_data, sub_title, title, updated_at, visit_id | 1 |
| `np_otp_attempt_master` | NpOTPattemptMaster | created_at, id, otp_attempts, timer, updated_at | 1 |
| `np_payment_details` | NpPaymentDetails | comment, coupon_code, created_at, gst_no, id, invoice_data, invoice_no, pay_gate_order_id, pay_gate_order_json, pay_gate_payment_id, pay_gate_payment_status, pay_gate_response_json, pay_gate_signature, pay_gate_webhook_json, price, product_id, status, txnid, updated_at, user_id | 4 |
| `np_prakriti_answers` | NPPrakritiAnswers | created_at, created_by, id, prakriti_json, prakruti, prakruti_mr, status, updated_at, updated_by, user_answers, user_id | 2 |
| `np_prakriti_questions` | NpPrakritiQuestion | created_at, created_by, id, mandatory, metadata, metadata_hi, metadata_mr, options, options_hi, options_mr, order, qtype, qtype_hi, qtype_mr, question, question_hi, question_mr, status, tags, updated_at, updated_by | 3 |
| `np_pricing_master` | NpPricingMaster | created_at, id, payment_url, price, product_name, status, updated_at | 1 |
| `np_survey_questions` | NPSurveyQuestion | created_at, id, input_type, options, options_mr, question, question_mr, question_tag, sort_order, updated_at, visibility_rule | 2 |
| `np_user_activity` | NpUserActivity | action, action_count, created_at, id, reference_id, resource_type, screen, updated_at, user_id | 1 |
| `np_user_api_logs` | NpUserApiLogs | created_at, data, end_point, id, priority, tag, updated_at, user_id | 1 |
| `np_user_survey_answers` | NPUserSurveyAnswer | answers, created_at, id, updated_at, user_id | 1 |
| `np_users` | NPUserModel | access, address_details, auth_token, birthday, city, coach_id, coin, country, country_code, created_at, current_level, device_information, device_type, email, gender, height, id, is_exists, lang, mobile, name, otp, otp_attempt_time, otp_attempts, password, pincode, state, terms_and_condition, updated_at, weight | 7 |
| `np_visit_parameter_data` | NPVisitParameterData | created_at, id, parameter_id, parameter_value, updated_at, visit_id | 1 |
| `np_visit_parameters` | NPVisitParameter | created_at, data_type, id, parameters_name, status, updated_at | 1 |
| `nt_application_version` | NTApplicationVersion | unknown | 0 |
| `nt_coupons` | NtCoupons | coupon_code, created_at, discount, id, status, updated_at, user_id, valid_from, valid_until | 1 |
| `other_report_data` | OtherReportData | create_date, id, is_active, last_modified_on, medical_id, report_data, sub_title, title | 3 |
| `patient_prakruti` | PatientPrakruti | unknown | 0 |
| `patient_profession` | PatientProfession | unknown | 0 |
| `patient_question_answer` | PatientQuestionAnswer | delete_by_doctor, delete_by_patient, is_active | 1 |
| `payment_gateway_response` | PaymentGatewayResponse | unknown | 0 |
| `pg_buyer_details` | PgBuyerDetail | unknown | 0 |
| `pg_device_list` | PgDeviceList | created_by, device_type, is_linkable, is_usable, serial_no, status, track_status | 7 |
| `pg_device_mapping` | PgDeviceMapping | unknown | 0 |
| `pg_device_return_details` | PgDeviceReturnDetail | unknown | 0 |
| `pg_order_details` | PgOrderDetail | unknown | 0 |
| `pg_order_dispatch_table` | PgOrderDispatch | unknown | 0 |
| `pg_order_id_generate` | PgOrderIdGenerate | unknown | 0 |
| `pg_plan_details` | PgPlanDetail | unknown | 0 |
| `postal_codes` | PostalCode | country_code, country_name, created_at, district, id, latitude, longitude, place_name, postal_code, state, state_code, sub_district, updated_at | 1 |
| `prakriti_answer_descriptions` | PrakritiAnswersDescriptions | prakruti_details | 2 |
| `prakriti_answers` | PrakritiAnswers | unknown | 0 |
| `prakriti_questions` | GetTuryaaPrakrutiQuestion | order | 1 |
| `prakruti_description_v1` | PrakrutiDescriptionV1 | unknown | 0 |
| `prakruti_wise_diet` | PrakrutiWiseDiet | unknown | 0 |
| `profession_type` | ProfessionType | create_date, id, is_active, profession_name, theme_code | 1 |
| `project_variables` | ProjectVariable | unknown | 0 |
| `question_answers` | QuestionAnswers | goal_answer | 1 |
| `question_categories` | QuestionCategories | unknown | 0 |
| `question_types` | QuestionTypes | unknown | 0 |
| `questions` | Questions | is_having_child, order | 1 |
| `recipe_category` | RecipeCategory | unknown | 0 |
| `recipe_preference_json` | RecipePreferenceJson | unknown | 0 |
| `refer_colleague` | ReferColleague | unknown | 0 |
| `request_callback` | RequestCallback | unknown | 0 |
| `research_users` | ResearchUsers | unknown | 0 |
| `resource_name_master` | ResourceNameMaster | endpoint, is_default, no_of_pages, order_by, title | 3 |
| `ritu_input` | RituInput | unknown | 0 |
| `rutucharya_periods_dates` | RutucharyaPeriodsDates | city, country, create_date, end_date, id, is_active, last_modified_on, rutu, rutu_id, rutucharya_label, start_date, state, year | 2 |
| `salutation_types` | SalutationTypes | unknown | 0 |
| `session_log` | SessionLog | unknown | 0 |
| `shorturl` | ShortUrl | unknown | 0 |
| `spa_report_summary` | SpaReportSummary | unknown | 0 |
| `spa_report_therapy` | SpaReportTherapy | unknown | 0 |
| `states_names` | StatesNames | unknown | 0 |
| `subscription_status` | SubscriptionStatus | unknown | 0 |
| `subscription_types` | SubscriptionTypes | is_active | 1 |
| `subscription_types_master` | SubscriptionTypesMaster | unknown | 0 |
| `subscription_wise_reports` | SubscriptionWiseReports | unknown | 1 |
| `subscriptions` | Subscription | api_rules, blocked_api_rules, create_date, duration, features, id, limits, name, price, status, updated_at | 2 |
| `swasthya_report_data` | SwasthyaReportData | create_date, id, language_name, last_modified_on, medical_id, status, swashtya_data | 1 |
| `symptom_category` | SymptomCategory | is_active | 1 |
| `symptoms` | Symptoms | is_active | 2 |
| `symptoms_dropdown_item` | SymptomsDropdownItem | unknown | 0 |
| `transactions` | Transaction | amount, comment, coupon_code, create_date, currency, expire_status, free_expire_date, id, invoice_data, is_trial, month, order_id, pay_gate_order_id, pay_gate_order_json, pay_gate_payment_id, pay_gate_payment_status, pay_gate_response_json, pay_gate_signature, pay_gate_webhook_json, payment_date, payment_status, plan_id, plan_id_v2, report_count, updated_at, user_id | 5 |
| `user_api_key_mapping` | UserApiKeyMapping | unknown | 0 |
| `user_diet_choice` | UserDietChoice | choice, choice_type, created_at, id, input_json, parent_id, status, updated_at, user_id | 2 |
| `user_nadi_capture_type` | UserNadiCaptureType | allowed_countries, avoid_device_selection_usb, can_change_capture_type, create_date, expiry_date, free_tier_enrolled, id, is_active, is_star_account, last_modified_on, nadi_capture_type, no_of_reports, plan_type, user_id | 8 |
| `user_notifications_info` | UserNotificationsInfo | unknown | 0 |
| `user_personal_info` | UserPersonalInfo | allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken | 13 |
| `user_report` | UserReport | symptom_prediction | 1 |
| `user_report_descriptions` | UserReportDescription | description_kannada | 1 |
| `user_role` | UserRole | unknown | 2 |
| `user_selected_countries` | UserSelectedCountry | unknown | 0 |
| `user_stages` | UserStages | created_at, id, label, name, status, updated_at | 2 |
| `user_vikruti_descriptions_v1` | UserVikrutiDescriptionV1 | description_kannda | 1 |
| `users` | TuryaaUserModel, User | auth_token, birthday, chat_access, coin, current_stage, height, is_exists, weight | 5 |
| `vikruti_description` | VikrutiDescription | created_at, description, digestion, id, mind_health, status, updated_at, wellbeing | 1 |
| `vikruti_feedback_questions` | VikrutiFeedbackQuestion | created_at, id, options, order, question, status, updated_at, vikruti_type | 1 |
| `wellness_report` | WellnessReport | coach_id, created_at, id, status, updated_at, user_id, wellness_data, wellness_file | 1 |
| `wellness_tracking` | WellnessTracking | created_at, exercise_activities, id, meal_photos, music_activities, sleep_timing, status, updated_at, user_id, wakeup_timing, water_intake, yoga_activities | 1 |
| `whitelisted_mobileno_turyaa` | WhitelistedMobilenoTuryaa | unknown | 0 |
| `yoga_category` | YogaCategory | unknown | 0 |
| `yoga_json` | YogaJson | unknown | 0 |
| `yoga_report_data` | YogaReportData | unknown | 0 |
