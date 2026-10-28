# Screens: Nadi-Tarangini-App (flutter)

Built from commit `0b7deec6de2b0b8b4f05eab4be8c8430523829bf` by scripts/screens.sh.

screens: 60 · go_routes: 61 · routes_without_screen_class: 8 · screen_classes_without_route: 7 · screens_file_not_found: 0

| Screen | File | GoRoute path(s) | Navigates to |
|---|---|---|---|
| AddAppointmentScreen | `lib/doctor_dashboard/appointments/view/add_appointment.dart` | `/addAppointmentScreen` | /addPatientScreen |
| AddClinicScreen | `lib/doctor_dashboard/my_account/view/my_clinic/add_clinic.dart` | `/addClinicScreen` |  |
| AddCompanyScreen | `lib/doctor_dashboard/inventory/view/company/add_company_screen.dart` | `/addCompanyScreen` | /companyListScreen |
| AddIngredientScreen | `lib/doctor_dashboard/inventory/view/ingredient/add_ingredient_screen.dart` | `/addIngredientScreen` | /ingredientListScreen |
| AddMedicineScreen | `lib/doctor_dashboard/inventory/view/medicine/add_medicine_screen.dart` | `/addMedicineScreen` | /medicineListScreen |
| AddMedicineTypeScreen | `lib/doctor_dashboard/inventory/view/medicine_type/add_medicine_type_screen.dart` | `/addMedicineTypeScreen` | /medicineTypeListScreen |
| AddPatientFromAppointmentScreen | `lib/doctor_dashboard/patient/view/add_patient/add_patient_from_appointment_screen.dart` |  | /addAppointmentScreen |
| AddPatientScreen | `lib/doctor_dashboard/patient/view/add_patient/add_patient_screen.dart` | `/addPatientScreen` | /addAppointmentScreen, /dashboardScreen, /patientScreen |
| AddSupplementScreen | `lib/doctor_dashboard/inventory/view/supplements/add_supplement_screen.dart` | `/addSupplementScreen` | /supplementListScreen |
| AllReportScreen | `lib/patient_module/view/all_report_screen.dart` |  |  |
| AppointmentScreen | `lib/doctor_dashboard/appointments/view/appointment_screen.dart` | `/appointmentListScreen` | /addAppointmentScreen |
| ChatRegistrationScreen | `lib/doctor_dashboard/chotbot/view/chat_registration_screen.dart` | `/chatRegistration` |  |
| ChatScreen | `lib/doctor_dashboard/chotbot/view/chat_screen.dart` | `/chatScreen` |  |
| CheckOutScreen | `lib/doctor_dashboard/subscription/view/checkout_screen.dart` | `/checkoutScreen` |  |
| ComingSoonPage | `lib/patient_module/view/comming_soon_page.dart` |  |  |
| CompanyListScreen | `lib/doctor_dashboard/inventory/view/company/company_list_screen.dart` | `/companyListScreen` | /addCompanyScreen, /editCompanyScreen, /inventoryScreen |
| ContactScreen | `lib/patient_module/view/contact_screen.dart` |  |  |
| DashboardScreen | `lib/doctor_dashboard/dashboard/view/dashboard_screen.dart` | `/dashboardScreen` | /addAppointmentScreen, /addPatientScreen, /appointmentListScreen, /assessmentScreen, /drawerMenu, /notificationScreen, /patientScreen, /reportScreen |
| DietScreen | `lib/patient_module/view/diet_screen.dart` | `/dietScreen` | /patientDashboard |
| EditAppointmentScreen | `lib/doctor_dashboard/appointments/view/edit_appointment.dart` | `/editAppointmentScreen` | /appointmentListScreen |
| EditClinicScreen | `lib/doctor_dashboard/my_account/view/my_clinic/edit_clinic.dart` | `/editClinicScreen` |  |
| EditCompanyScreen | `lib/doctor_dashboard/inventory/view/company/edit_company_screen.dart` | `/editCompanyScreen` | /companyListScreen |
| EditIngredientScreen | `lib/doctor_dashboard/inventory/view/ingredient/edit_ingredient_screen.dart` | `/editIngredientScreen` | /ingredientListScreen |
| EditMedicineScreen | `lib/doctor_dashboard/inventory/view/medicine/edit_medicine_screen.dart` | `/editMedicineScreen` | /medicineListScreen |
| EditPatientProfileScreen | `lib/patient_module/view/edit_patient_profile_screen.dart` | `/editPatientProfile` | /drawerMenuPatient |
| EditPatientScreen | `lib/doctor_dashboard/patient/view/edit_patient/edit_patient_screen.dart` | `/editPatientScreen` |  |
| EditSupplementScreen | `lib/doctor_dashboard/inventory/view/supplements/edit_supplement_screen.dart` | `/editSupplementScreen` | /supplementListScreen |
| FillPrakrutiScreen | `lib/doctor_dashboard/nadi_flow_new/view/fill_prakruti_screen.dart` | `/fillPrakrutiScreen` | /assessmentScreen, /patientScreen |
| ForgotPasswordScreen | `lib/common_files/Login/view/forgot_password_screen.dart` | `/forgotPasswordScreen` | /loginScreen |
| GeoRestrictedScreen | `lib/doctor_dashboard/dashboard/view/geo_restricted_screen.dart` | `/geoRestrictedScreen` |  |
| HelpCenterScreen | `lib/doctor_dashboard/help_center/view/help_center.dart` | `/helpCenterScreen` |  |
| IngredientListScreen | `lib/doctor_dashboard/inventory/view/ingredient/ingredient_list_screen.dart` | `/ingredientListScreen` | /addIngredientScreen, /editIngredientScreen, /inventoryScreen |
| InventoryScreen | `lib/doctor_dashboard/inventory/view/inventory_screen.dart` | `/inventoryScreen` | /companyListScreen, /ingredientListScreen, /medicineListScreen, /medicineTypeListScreen, /supplementListScreen |
| InvoicePdfScreen | `lib/doctor_dashboard/subscription/view/invoice_screen.dart` | `/invoiceScreen` |  |
| KycScreen | `lib/doctor_dashboard/kyc/view/kyc_screen.dart` | `/kycScreen` | /dashboardScreen |
| LanguageScreen | `lib/common_files/language/language_screen.dart` | `/languageScreen` | /onBoardingScreen |
| LoginScreen | `lib/common_files/Login/view/login_screen.dart` | `/loginScreen` | /signupScreen |
| LoginWithOtpScreen | `lib/common_files/Login/view/login_with_otp.dart` |  | /dashboardScreen, /geoRestrictedScreen, /kycScreen, /reportScreenPatient |
| LoginWithUsernameScreen | `lib/common_files/Login/view/login_with_username_screen.dart` |  | /dashboardScreen, /forgotPasswordScreen, /geoRestrictedScreen, /kycScreen, /reportScreenPatient |
| MainAssessmentScreen | `lib/doctor_dashboard/nadi_flow_new/view/main_assessment_screen.dart` | `/assessmentScreen` |  |
| MedicineListScreen | `lib/doctor_dashboard/inventory/view/medicine/medicine_list_screen.dart` | `/medicineListScreen` | /addMedicineScreen, /editMedicineScreen, /inventoryScreen |
| MedicineTypeListScreen | `lib/doctor_dashboard/inventory/view/medicine_type/medicine_type_list_screen.dart` | `/medicineTypeListScreen` | /addMedicineTypeScreen, /inventoryScreen |
| MyAccountScreen | `lib/doctor_dashboard/my_account/view/my_account_screen.dart` | `/myAccountScreen/:tabId` | /drawerMenu, /loginScreen |
| MyDevicesScreen | `lib/doctor_dashboard/my_account/view/my_device_screen.dart` |  | /drawerMenu |
| NadiReportScreen | `lib/doctor_dashboard/visit_reports/view/nadi_report_screen.dart` | `/nadiReportScreen` |  |
| NotificationScreen | `lib/doctor_dashboard/notifications/view/notification_screen.dart` | `/notificationScreen` | /dashboardScreen |
| OnboardingScreen | `lib/on_boarding/on_boarding_screen.dart` | `/onBoardingScreen` | /loginScreen |
| PatientScreen | `lib/doctor_dashboard/patient/view/patient_list/patient_screen.dart` | `/patientScreen` | /addPatientScreen, /assessmentScreen, /editPatientScreen, /fillPrakrutiScreen, /reportScreen, /viewPatientScreen |
| PricingPlanScreen | `lib/doctor_dashboard/subscription/view/pricing_plan_screen.dart` | `/pricingPlanScreen` |  |
| ReportScreen | `lib/patient_module/view/report_screen.dart` | `/reportScreenPatient` |  |
| RutucharyaScreen | `lib/doctor_dashboard/rutucharya/view/rutucharya_screen.dart` | `/rutucharyaScreen` |  |
| SignUpScreen | `lib/common_files/signup/view/signup_screen.dart` | `/signupScreen` | /loginScreen, /webViewScreen |
| SplashScreen | `lib/splash_screen.dart` | `/` | /dashboardScreen, /geoRestrictedScreen, /kycScreen, /languageScreen, /loginScreen, /onBoardingScreen, /reportScreenPatient |
| SupplementListScreen | `lib/doctor_dashboard/inventory/view/supplements/supplement_list_screen.dart` | `/supplementListScreen` | /addSupplementScreen, /editSupplementScreen, /inventoryScreen |
| UpdateDataConsentScreen | `lib/patient_module/view/update_data_consent_screen.dart` | `/updateDataConsentScreen` | /drawerMenuPatient |
| ViewAppointmentScreen | `lib/doctor_dashboard/appointments/view/view_appointment_screen.dart` | `/viewAppointmentScreen` | /appointmentListScreen |
| ViewPatientScreen | `lib/doctor_dashboard/patient/view/view_patient/view_patient_screen.dart` | `/viewPatientScreen` |  |
| VisitReportListScreen | `lib/doctor_dashboard/visit_reports/view/visit_report_list_screen.dart` | `/reportScreen` | /fillPrakrutiScreen |
| VisitReportScreen | `lib/doctor_dashboard/visit_reports/view/visit_report_screen.dart` | `/visitReportScreen` |  |
| WebViewScreen | `lib/common_files/common_widgets/web_view_screen_widget.dart` | `/webViewScreen` |  |
