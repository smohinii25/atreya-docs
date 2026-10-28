# Screens: Ashoka-World-Backend (blade)

Built from commit `8dfbb37db7d71a400b3656bd50fbed6173908a24` by scripts/screens.sh.

screens: 221 · partials: 130 · rendered_by_controller: 51 · reachable_by_route: 49 · js_calls: 34 · js_calls_credited: 33 · js_calls_unresolved: 9

| View | Rendered by | Routes | Links to |
|---|---|---|---|
| `concents.deleteClinicPage` |  |  |  |
| `concents.previusReportNotSupported` | ReportsWebController@swasthyaDarshikaReportV2 | `GET swasthyaDarshikaReport`, `GET swasthyaDarshikaReportV2` |  |
| `concents.revokeReportPatient` | ReportsWebController@aiGeneratedRutucharyaReport, ReportsWebController@aiGeneratedyogaPlannerReport, ReportsWebController@arogyaDarshikaReport, ReportsWebController@careServicesReport, ReportsWebController@dietAndLifestylereport, ReportsWebController@medicalVisitReport, ReportsWebController@medicalVisitReportV2, ReportsWebController@nadiNaranginiReport, ReportsWebController@nadiNaranginiReportV3, ReportsWebController@nadiSwasthyaReport, ReportsWebController@ntRecommendationsReport, ReportsWebController@onePagerNadiTaranginiReport, ReportsWebController@prescriptionReport, ReportsWebController@spaReport, ReportsWebController@swasthyaDarshikaReport, ReportsWebController@swasthyaDarshikaReportV2, ReportsWebController@weeklyDietReport, ReportsWebController@yogaReport | `GET arogyaDarshika`, `GET careServicesReport`, `GET dietReport`, `GET medicalVisitReport`, `GET medicalVisitReportV2`, `GET nadiSwasthyaReport`, `GET nadiTaranginiReport`, `GET nadiTaranginiReportV3`, `GET ntRecommendationReport`, `GET onePagerNadiTaranginiReport`, `GET prescriptionReport`, `GET rutucharyaReport`, `GET spaReport`, `GET swasthyaDarshikaReport`, `GET swasthyaDarshikaReportV2`, `GET weeklyDietReport`, `GET yogaPlannerReport`, `GET yogaReport` |  |
| `errors.404` | ReportsWebController@aiGeneratedRutucharyaReport, ReportsWebController@aiGeneratedyogaPlannerReport, ReportsWebController@arogyaDarshikaReport, ReportsWebController@careServicesReport, ReportsWebController@dietAndLifestylereport, ReportsWebController@medicalVisitReport, ReportsWebController@medicalVisitReportV2, ReportsWebController@nadiNaranginiReport, ReportsWebController@nadiNaranginiReportV3, ReportsWebController@nadiSwasthyaReport, ReportsWebController@ntRecommendationsReport, ReportsWebController@onePagerNadiTaranginiReport, ReportsWebController@patanjaliReport, ReportsWebController@postFetchNadiInfo, ReportsWebController@prescriptionReport, ReportsWebController@spaReport, ReportsWebController@swasthyaDarshikaReport, ReportsWebController@swasthyaDarshikaReportV2, ReportsWebController@weeklyDietReport, ReportsWebController@yogaReport | `GET arogyaDarshika`, `GET careServicesReport`, `GET dietReport`, `GET medicalVisitReport`, `GET medicalVisitReportV2`, `GET nadiSwasthyaReport`, `GET nadiTaranginiReport`, `GET nadiTaranginiReportV3`, `GET ntRecommendationReport`, `GET onePagerNadiTaranginiReport`, `GET patanjaliReport`, `GET prescriptionReport`, `GET rutucharyaReport`, `GET spaReport`, `GET swasthyaDarshikaReport`, `GET swasthyaDarshikaReportV2`, `GET weeklyDietReport`, `GET yogaPlannerReport`, `GET yogaReport`, `POST postFetchNadiInfo` | / |
| `errors.405` |  |  |  |
| `errors.500` |  |  |  |
| `errors.reloadPageWrong` | ReportsWebController@ntRecommendationsReport, ReportsWebController@swasthyaDarshikaReportV2 | `GET ntRecommendationReport`, `GET swasthyaDarshikaReport`, `GET swasthyaDarshikaReportV2` |  |
| `invoice` |  |  |  |
| `nadi-pariksha.admin.admin_coach_management` | CoachDashboardController@adminCoachManagement | `GET nadi-pariksha-admin/coach-dashboard` | /nadi-pariksha-admin/dashboard |
| `nadi-pariksha.admin.admin_coach_user_details` | CoachDashboardController@adminCoachUserDetails | `GET nadi-pariksha-admin/coach-user-details/{id}` | /nadi-pariksha-admin/coach-dashboard, /nadi-pariksha-admin/dashboard |
| `nadi-pariksha.admin.admin_coupon_management` | CoachDashboardController@couponManagement | `GET nadi-pariksha-admin/coupon-management` |  |
| `nadi-pariksha.admin.admin_dasbhoard_access_denied` |  |  | /nadi-pariksha-admin/dashboard |
| `nadi-pariksha.admin.admin_dashboard` | CoachDashboardController@adminDashboard | `GET nadi-pariksha-admin/dashboard` |  |
| `nadi-pariksha.admin.admin_doctor_edit` | CoachDashboardController@editDoctorDetailsView | `GET nadi-pariksha-admin/doctor/edit/{id}` |  |
| `nadi-pariksha.admin.admin_doctor_view_details` | CoachDashboardController@viewDoctorDetails | `GET nadi-pariksha-admin/doctor/{id}` | /nadi-pariksha-admin/getAllDoctorsDetails |
| `nadi-pariksha.admin.admin_doctors_catlogue` | CoachDashboardController@getAllDoctorsDetails | `GET nadi-pariksha-admin/getAllDoctorsDetails` |  |
| `nadi-pariksha.admin.admin_loginPage` |  |  |  |
| `nadi-pariksha.admin.admin_management` | CoachDashboardController@adminUsersManagement | `GET nadi-pariksha-admin/admin-users` |  |
| `nadi-pariksha.admin.admin_marketing_leads` | CoachDashboardController@showMarketingLeads | `GET nadi-pariksha-admin/marketing-leads` | /nadi-pariksha-admin/dashboard |
| `nadi-pariksha.admin.admin_payment_management` | CoachDashboardController@paymentManagement | `GET nadi-pariksha-admin/payment-management` |  |
| `nadi-pariksha.admin.admin_report_price_management` | CoachDashboardController@reportPriceManagement | `GET nadi-pariksha-admin/report-price-management` |  |
| `nadi-pariksha.admin.admin_users_management` | CoachDashboardController@usersManagement | `GET nadi-pariksha-admin/users-management` |  |
| `nadi-pariksha.admin.otp_list` | CoachDashboardController@showOtpListPage | `GET nadi-pariksha-admin/otp-list` |  |
| `nadi-pariksha.capture_nadi` | NadiParikshaController@nadiCaptureView | `GET nadi_pariksha/nadiCaptureView` |  |
| `nadi-pariksha.nadiParikshaReportPdf.header` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.nadiParikshaLayoutPdf` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.nadiParikshaReportPdf` | NadiParikshaController@testViewNadiReport, NadiParikshaController@testrenderNadiReportPdf | `GET nadi-report/pdf/{userId}`, `GET web-nadi-report/pdf/{userId}` |  |
| `nadi-pariksha.nadiParikshaReportPdf.page1` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page10` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page11` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page12` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page13` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page2` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page3` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page4` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page5` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page6` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page7` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page8` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdf.page9` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.header` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.nadiParikshaLayoutPdf` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.nadiParikshaReportPdf` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page1` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page10` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page11` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page12` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page13` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page2` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page3` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page4` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page5` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page6` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page7` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page8` |  |  |  |
| `nadi-pariksha.nadiParikshaReportPdfNew.page9` |  |  |  |
| `nadi-pariksha.np_dashboard` | CoachDashboardController@index | `GET nadi-pariksha-coach` | /nadi-pariksha-coach/user-details/ |
| `nadi-pariksha.np_loginPage` | CoachDashboardController@showLoginPage | `GET nadi-pariksha-coach-login` |  |
| `nadi-pariksha.np_user_details` | CoachDashboardController@showUserDetails | `GET nadi-pariksha-coach/user-details/{id}` | /nadi-pariksha-coach |
| `pdf` |  |  |  |
| `reports.arogyaDarshika` | ReportsWebController@arogyaDarshikaReport, ReportsWebController@postFetchNadiInfo | `GET arogyaDarshika`, `POST postFetchNadiInfo` |  |
| `reports.careServicesReport` | ReportsWebController@careServicesReport | `GET careServicesReport` |  |
| `reports.dietReport` | ReportsWebController@dietAndLifestylereport | `GET dietReport` |  |
| `reports.loadingReport` | ReportsWebController@showLoadingPage |  |  |
| `reports.medicalReport` | ReportsWebController@medicalVisitReport | `GET medicalVisitReport` |  |
| `reports.medicalReportV2` | ReportsWebController@medicalVisitReportV2 | `GET medicalVisitReportV2` |  |
| `reports.nadiSwasthyaReport` | ReportsWebController@nadiSwasthyaReport | `GET nadiSwasthyaReport` |  |
| `reports.nadiTaranginiReport` | ReportsWebController@nadiNaranginiReport | `GET nadiTaranginiReport` |  |
| `reports.nadiTaranginiReportV3` | ReportsWebController@nadiNaranginiReportV3 | `GET nadiTaranginiReportV3` |  |
| `reports.ntRecommendationReport` | ReportsWebController@ntRecommendationsReport | `GET ntRecommendationReport` |  |
| `reports.onePagerNadiTaranginiReport` | ReportsWebController@onePagerNadiTaranginiReport | `GET onePagerNadiTaranginiReport` |  |
| `reports.patanjaliReport` | ReportsWebController@patanjaliReport | `GET patanjaliReport` |  |
| `reports.prescriptionReport` | ReportsWebController@prescriptionReport | `GET prescriptionReport` |  |
| `reports.prescriptionReportV2` | ReportsWebController@prescriptionReport | `GET prescriptionReport` |  |
| `reports.rutucharyaNotGenerated` | ReportsWebController@aiGeneratedRutucharyaReport | `GET rutucharyaReport` |  |
| `reports.rutucharyaReport` | ReportsWebController@aiGeneratedRutucharyaReport | `GET rutucharyaReport` |  |
| `reports.spaReport` | ReportsWebController@spaReport | `GET spaReport` |  |
| `reports.swasthyaDarshikaReport` | ReportsWebController@swasthyaDarshikaReport |  |  |
| `reports.swasthyaDarshikaReportV2` | ReportsWebController@swasthyaDarshikaReportV2 | `GET swasthyaDarshikaReport`, `GET swasthyaDarshikaReportV2` |  |
| `reports.weeklyDietNotGenerated` | ReportsWebController@weeklyDietReport | `GET weeklyDietReport` |  |
| `reports.weeklyDietReport` | ReportsWebController@weeklyDietReport | `GET weeklyDietReport` |  |
| `reports.yogaPlannerNotGenerated` | ReportsWebController@aiGeneratedyogaPlannerReport | `GET yogaPlannerReport` |  |
| `reports.yogaPlannerReport` | ReportsWebController@aiGeneratedyogaPlannerReport | `GET yogaPlannerReport` | /updateYogaPlannerPublic |
| `reports.yogaReport` | ReportsWebController@yogaReport | `GET yogaReport` |  |
| `research_dashboard_vata` | ResearchDasbhoardController@vataDashboard | `GET research-dashboard-pulse-view`, `GET research/dashboard-pulse-view`, `POST research-dashboard-pulse-view`, `POST research/dashboard-pulse-view` |  |
| `swagger.developer` | SwaggerController@developer | `GET api-docs/developer` |  |
| `swagger.user` | SwaggerController@user | `GET api-docs/public` |  |
| `turyaa.stageReport` |  |  |  |
| `turyaa.turyaaDietUi` |  |  |  |
| `vendor.l5-swagger.index` |  |  | l5-swagger. |
| `welcome` |  |  |  |

Partials (layouts, components, modals, emails): 130
