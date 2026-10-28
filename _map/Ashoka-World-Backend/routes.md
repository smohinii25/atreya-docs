# Routes: Ashoka-World-Backend

Built from commit `8dfbb37db7d71a400b3656bd50fbed6173908a24` by scripts/routes.sh (static parse, no PHP).

| Route file | URL prefix | Prefix from |
|---|---|---|
| `routes/api.php` | `` | RouteServiceProvider |
| `routes/web.php` | `` | RouteServiceProvider |

**929 routes** (924 unique), 6 closures, 5 shadowed duplicates, 0 unparsed lines, 47 commented-out route lines, 0 controller files not found, 0 guarded.

| Method | URI | Controller@action | Middleware | Name | Source |
|---|---|---|---|---|---|
| GET | `/` | Closure |  |  | `routes/web.php:32` |
| POST | `GetReorderFeatures` | CustomizeDetailsController@GetReorderFeatures | api, auth.token |  | `routes/api.php:1034` |
| POST | `accessUserWisePatientList` | PatientDetailsController@accessUserWisePatientList | api, auth.token |  | `routes/api.php:933` |
| POST | `add-self-admin` | AdminManagementController@addSelfAdmin | api, auth.token |  | `routes/api.php:1356` |
| POST | `addNewClinic` | ClinicController@addNewClinic | api, auth.token |  | `routes/api.php:1013` |
| POST | `addNewSymptoms` | CustomizeDetailsController@addNewSymptoms | api, auth.token |  | `routes/api.php:1030` |
| POST | `addnewDetails` | CustomizeDetailsController@addnewDetails | api, auth.token |  | `routes/api.php:1035` |
| GET | `api-docs/developer` | SwaggerController@developer |  |  | `routes/web.php:56` |
| GET | `api-docs/public` | SwaggerController@user |  |  | `routes/web.php:57` |
| GET | `appVersion/getAppVersionDetails` | PublicFunctionsController@getAppVersionDetails |  |  | `routes/api.php:416` |
| POST | `appVersion/updateAppVersionDetails` | PublicFunctionsController@updateAppVersionDetails |  |  | `routes/api.php:417` |
| POST | `appointment/addAppointment` | AppointmentController@addAppointmentDoctor | api, auth.token |  | `routes/api.php:1084` |
| POST | `appointment/dateWiseAppointment` | AppointmentController@dateWiseAppointment | api, auth.token |  | `routes/api.php:1099` |
| POST | `appointment/dateWisePatientAppointment` | AppointmentController@dateWisePatientAppointment | api, auth.token |  | `routes/api.php:1101` |
| POST | `appointment/deleteAppointment` | AppointmentController@deleteAppointment | api, auth.token |  | `routes/api.php:1087` |
| POST | `appointment/fetchDoctorInfo` | AppointmentController@fetch_doctor_info | api, auth.token |  | `routes/api.php:1109` |
| POST | `appointment/fetchSingleAppointment` | AppointmentController@fetchSingleAppointmentData | api, auth.token |  | `routes/api.php:1093` |
| POST | `appointment/getAllAppointment` | AppointmentController@getAllAppointment | api, auth.token |  | `routes/api.php:1081` |
| GET | `appointment/getAppointmentHistory` | AppointmentController@getAppointmentHistory | api, auth.token |  | `routes/api.php:1097` |
| POST | `appointment/getAppointmentsByDate` | AppointmentController@getAppointmentsByDate | api, auth.token |  | `routes/api.php:1105` |
| GET | `appointment/getCurrentsAppointment` | AppointmentController@getCurrentsAppointment | api, auth.token |  | `routes/api.php:1103` |
| PUT | `appointment/markAppointmentDone` | AppointmentController@markAppointmentDone | api, auth.token |  | `routes/api.php:1107` |
| POST | `appointment/updateAppointment` | AppointmentController@updateAppointment | api, auth.token |  | `routes/api.php:1090` |
| POST | `appointment/validateAppointment` | AppointmentController@validateAppointment | api, auth.token |  | `routes/api.php:1095` |
| GET | `arogyaDarshika` | ReportsWebController@arogyaDarshikaReport |  |  | `routes/api.php:1506` |
| POST | `ashokaDashboard/AllUserAnalytics` | UserAnalyticsController@AllUserAnalytics | atreyaDashboard.authentication |  | `routes/api.php:194` |
| POST | `ashokaDashboard/accessManagement/getRoleWiseAccess` | AshokaAccessManagementController@getRoleWiseAccess | atreyaDashboard.authentication |  | `routes/api.php:326` |
| POST | `ashokaDashboard/accessManagement/updateRoleAccess` | AshokaAccessManagementController@updateRoleAccess | atreyaDashboard.authentication |  | `routes/api.php:328` |
| POST | `ashokaDashboard/activateNtLite` | AshokaUserManangementController@updateNtLiteAccess | atreyaDashboard.authentication |  | `routes/api.php:198` |
| POST | `ashokaDashboard/activeUser` | AshokaUserManangementController@activeUser | atreyaDashboard.authentication |  | `routes/api.php:195` |
| POST | `ashokaDashboard/addNewUser` | AshokaUserManangementController@addNewUser | atreyaDashboard.authentication |  | `routes/api.php:186` |
| POST | `ashokaDashboard/appVersion/getAdminAppVersionDetails` | AshokaAuthController@getAdminAppVersionDetails |  |  | `routes/api.php:153` |
| POST | `ashokaDashboard/appVersion/updateAdminAppVersionDetails` | AshokaAuthController@updateAdminAppVersionDetails |  |  | `routes/api.php:154` |
| POST | `ashokaDashboard/corporate/getAllCorporatePayments` | AshokaCorporateManagementController@getAllCorporatePayments | atreyaDashboard.authentication |  | `routes/api.php:377` |
| POST | `ashokaDashboard/corporate/getCorporateCodeWiseReports` | AshokaCorporateManagementController@getCorporateCodeWiseReports | atreyaDashboard.authentication |  | `routes/api.php:374` |
| POST | `ashokaDashboard/corporate/getRentalBasisReport` | AshokaCorporateManagementController@getRentalBasisReport | atreyaDashboard.authentication |  | `routes/api.php:375` |
| POST | `ashokaDashboard/corporate/saveCorporateMonthlyReportPayment` | AshokaCorporateManagementController@saveCorporateMonthlyReportPayment | atreyaDashboard.authentication |  | `routes/api.php:376` |
| POST | `ashokaDashboard/dailyCron/saveDailyNadiTakenReports` | ReportManagementController@saveDailyNadiTakenReports |  |  | `routes/api.php:172` |
| POST | `ashokaDashboard/device/addDevice` | DeviceManagementController@addDevice | atreyaDashboard.authentication |  | `routes/api.php:242` |
| POST | `ashokaDashboard/device/changeDeviceType` | DeviceManagementController@changeDeviceType | atreyaDashboard.authentication |  | `routes/api.php:262` |
| POST | `ashokaDashboard/device/getActiveDevices` | AshokaAuthController@getActiveDevices | atreyaDashboard.authentication |  | `routes/api.php:233` |
| POST | `ashokaDashboard/device/getAllDevicesList` | DeviceManagementController@getAllDevicesList | atreyaDashboard.authentication |  | `routes/api.php:240` |
| POST | `ashokaDashboard/device/getAllLinkedDevicesList` | DeviceManagementController@getAllLinkedDevicesList | atreyaDashboard.authentication |  | `routes/api.php:241` |
| POST | `ashokaDashboard/device/getDeliveredDevices` | DeviceManagementController@getDeliveredDevices | atreyaDashboard.authentication |  | `routes/api.php:259` |
| POST | `ashokaDashboard/device/getDeviceAccordingToType` | DeviceManagementController@getDeviceAccordingToType | atreyaDashboard.authentication |  | `routes/api.php:263` |
| POST | `ashokaDashboard/device/getDeviceList` | DeviceManagementController@getDeviceList | atreyaDashboard.authentication |  | `routes/api.php:239` |
| POST | `ashokaDashboard/device/getDeviceWiseReports` | DeviceManagementController@getDeviceWiseReports | atreyaDashboard.authentication |  | `routes/api.php:235` |
| POST | `ashokaDashboard/device/getDispatchReadyDevices` | DeviceManagementController@getDispatchReadyDevices | atreyaDashboard.authentication |  | `routes/api.php:258` |
| POST | `ashokaDashboard/device/getDispatchedDevices` | DeviceManagementController@getDispatchedDevices | atreyaDashboard.authentication |  | `routes/api.php:260` |
| POST | `ashokaDashboard/device/getDoctorWiseDevices` | DeviceManagementController@getDoctorWiseDevices | atreyaDashboard.authentication |  | `routes/api.php:236` |
| POST | `ashokaDashboard/device/getDoctorWiseReports` | DeviceManagementController@getDoctorWiseReports | atreyaDashboard.authentication |  | `routes/api.php:237` |
| POST | `ashokaDashboard/device/getInHouseDevices` | DeviceManagementController@getInHouseDevices | atreyaDashboard.authentication |  | `routes/api.php:256` |
| POST | `ashokaDashboard/device/getReadyDevices` | AshokaAuthController@getReadyDevices | atreyaDashboard.authentication |  | `routes/api.php:232` |
| POST | `ashokaDashboard/device/getRejectedDevices` | DeviceManagementController@getRejectedDevices | atreyaDashboard.authentication |  | `routes/api.php:257` |
| POST | `ashokaDashboard/device/markActiveDevice` | DeviceManagementController@markActiveDevice | atreyaDashboard.authentication |  | `routes/api.php:246` |
| POST | `ashokaDashboard/device/markDispatchDevice` | DeviceManagementController@markDispatchDevice | atreyaDashboard.authentication |  | `routes/api.php:249` |
| POST | `ashokaDashboard/device/markDispatchReadyDevice` | DeviceManagementController@markDispatchReadyDevice | atreyaDashboard.authentication |  | `routes/api.php:254` |
| POST | `ashokaDashboard/device/markInHouseDevice` | DeviceManagementController@markInHouseDevice | atreyaDashboard.authentication |  | `routes/api.php:248` |
| POST | `ashokaDashboard/device/markInactiveDevice` | DeviceManagementController@markInactiveDevice | atreyaDashboard.authentication |  | `routes/api.php:247` |
| POST | `ashokaDashboard/device/markMissingDevice` | DeviceManagementController@markMissingDevice | atreyaDashboard.authentication |  | `routes/api.php:250` |
| POST | `ashokaDashboard/device/markReadyDevice` | DeviceManagementController@markReadyDevice | atreyaDashboard.authentication |  | `routes/api.php:245` |
| POST | `ashokaDashboard/device/markRejectedDevice` | DeviceManagementController@markRejectedDevice | atreyaDashboard.authentication |  | `routes/api.php:253` |
| POST | `ashokaDashboard/device/markRepairingDevice` | DeviceManagementController@markRepairingDevice | atreyaDashboard.authentication |  | `routes/api.php:252` |
| POST | `ashokaDashboard/device/markReturnedPermanentlyDevice` | DeviceManagementController@markReturnedPermanentlyDevice | atreyaDashboard.authentication |  | `routes/api.php:251` |
| POST | `ashokaDashboard/device/updateDevice` | DeviceManagementController@updateDevice | atreyaDashboard.authentication |  | `routes/api.php:243` |
| POST | `ashokaDashboard/doctor/checkMobileNumber` | DoctorsManagementController@checkMobileNumber | atreyaDashboard.authentication |  | `routes/api.php:334` |
| POST | `ashokaDashboard/doctor/getDoctorUsageReportBadmin` | UserAnalyticsController@getDoctorUsageReport | atreyaDashboard.authentication |  | `routes/api.php:348` |
| POST | `ashokaDashboard/doctor/getDoctorWiseAllowedFunctions` | DoctorsManagementController@getDoctorWiseAllowedFunctions | atreyaDashboard.authentication |  | `routes/api.php:339` |
| POST | `ashokaDashboard/doctor/getDoctorsInfoBadmin` | DoctorsManagementController@getDoctorsInfoBadmin | atreyaDashboard.authentication |  | `routes/api.php:343` |
| POST | `ashokaDashboard/doctor/getDoctorsInfoBadminV2` | DoctorsManagementController@getDoctorsInfoBadminV2 | atreyaDashboard.authentication |  | `routes/api.php:347` |
| POST | `ashokaDashboard/doctor/getDoctorsMonthlyReportCount` | DoctorsManagementController@getMonthlyReportCounts | atreyaDashboard.authentication |  | `routes/api.php:345` |
| POST | `ashokaDashboard/doctor/getDoctorsReportCountCustomDateRange` | DoctorsManagementController@getDoctorsReportCountCustomDateRange | atreyaDashboard.authentication |  | `routes/api.php:350` |
| POST | `ashokaDashboard/doctor/getNadiWiseDoctorUsageReport` | UserAnalyticsController@getNadiWiseDoctorUsageReport | atreyaDashboard.authentication |  | `routes/api.php:349` |
| POST | `ashokaDashboard/doctor/getSingleDoctorDetails` | DoctorsManagementController@getSingleDoctorDetails | atreyaDashboard.authentication |  | `routes/api.php:333` |
| POST | `ashokaDashboard/doctor/getStarAccounts` | DoctorsManagementController@getStarAccounts | atreyaDashboard.authentication |  | `routes/api.php:338` |
| POST | `ashokaDashboard/doctor/getUserNadiCapturePreference` | DoctorsManagementController@getCaptureTypeSettings | atreyaDashboard.authentication |  | `routes/api.php:356` |
| POST | `ashokaDashboard/doctor/linkDeviceInHouse` | DoctorsManagementController@linkDeviceInHouse | atreyaDashboard.authentication |  | `routes/api.php:335` |
| POST | `ashokaDashboard/doctor/markExternalDoctor` | DoctorsManagementController@markExternalDoctor | atreyaDashboard.authentication |  | `routes/api.php:352` |
| POST | `ashokaDashboard/doctor/markStarAccount` | DoctorsManagementController@markStarAccount | atreyaDashboard.authentication |  | `routes/api.php:337` |
| POST | `ashokaDashboard/doctor/resetPassword` | DoctorsManagementController@resetPassword | atreyaDashboard.authentication |  | `routes/api.php:332` |
| POST | `ashokaDashboard/doctor/unlinkDeviceFromHouse` | DoctorsManagementController@unlinkDeviceFromHouse | atreyaDashboard.authentication |  | `routes/api.php:336` |
| POST | `ashokaDashboard/doctor/updateDoctorReportsAccess` | DoctorsManagementController@updateDoctorReportsAccess | atreyaDashboard.authentication |  | `routes/api.php:340` |
| POST | `ashokaDashboard/doctor/updateUserNadiCapturePreference` | DoctorsManagementController@updateCaptureTypeSettings | atreyaDashboard.authentication |  | `routes/api.php:354` |
| POST | `ashokaDashboard/forgotPassword` | AshokaAuthController@forgotPassword | atreyaDashboard.authentication |  | `routes/api.php:190` |
| POST | `ashokaDashboard/genderWisePatientCountForDoctor` | UserAnalyticsController@genderWisePatientCountForDoctor | atreyaDashboard.authentication |  | `routes/api.php:211` |
| POST | `ashokaDashboard/generatePresignedUrlForS3Bucket` | PublicFunctionsController@getPresignedS3Url | atreyaDashboard.authentication |  | `routes/api.php:222` |
| POST | `ashokaDashboard/getActiveDoctors` | DoctorsManagementController@getActiveDoctors | atreyaDashboard.authentication |  | `routes/api.php:217` |
| POST | `ashokaDashboard/getAllActiveDoctors` | DoctorsManagementController@getAllActiveDoctors | atreyaDashboard.authentication |  | `routes/api.php:218` |
| GET | `ashokaDashboard/getAllDepartments` | AshokaDepartmentsController@getAllDepartments | atreyaDashboard.authentication |  | `routes/api.php:178` |
| POST | `ashokaDashboard/getAllDoctorDetails` | DoctorsManagementController@getAllDoctorDetails | atreyaDashboard.authentication |  | `routes/api.php:216` |
| POST | `ashokaDashboard/getAllRoles` | AshokaRolesController@getAllRoles | atreyaDashboard.authentication |  | `routes/api.php:184` |
| POST | `ashokaDashboard/getAllUser` | AshokaUserManangementController@getAllUser | atreyaDashboard.authentication |  | `routes/api.php:192` |
| POST | `ashokaDashboard/getAllUsersMailAndNumbers` | AshokaUserManangementController@getAllUsersMailAndNumbers | atreyaDashboard.authentication |  | `routes/api.php:180` |
| POST | `ashokaDashboard/getAllowedCountriesUserWise` | AshokaUserManangementController@getAllowedCountriesUserWise | atreyaDashboard.authentication |  | `routes/api.php:202` |
| POST | `ashokaDashboard/getAvoidLocationSelectionUserWise` | AshokaUserManangementController@getAvoidLocationSelectionUserWise | atreyaDashboard.authentication |  | `routes/api.php:205` |
| POST | `ashokaDashboard/getDepartmentWiseRoles` | AshokaRolesController@getDepartmentWiseRoles | atreyaDashboard.authentication |  | `routes/api.php:179` |
| POST | `ashokaDashboard/getDetailsUsingEmailId` | AshokaUserManangementController@getDetailsUsingEmailId |  |  | `routes/api.php:150` |
| POST | `ashokaDashboard/getDoctorAnalytics` | DoctorsManagementController@getDoctorAnalytics | atreyaDashboard.authentication |  | `routes/api.php:219` |
| POST | `ashokaDashboard/getDoctorAnalyticsDate` | DoctorsManagementController@getDoctorAnalyticsDate | atreyaDashboard.authentication |  | `routes/api.php:220` |
| POST | `ashokaDashboard/getDoctorDetails` | DoctorsManagementController@getDoctorDetails | atreyaDashboard.authentication |  | `routes/api.php:215` |
| POST | `ashokaDashboard/getDoctorsForPlanReminders` | AshokaSubscriptionManagementController@getDoctorsForPlanReminders |  |  | `routes/api.php:175` |
| POST | `ashokaDashboard/getNtLiteAccessUserWise` | AshokaUserManangementController@getNtLiteAccessUserWise | atreyaDashboard.authentication |  | `routes/api.php:199` |
| POST | `ashokaDashboard/getRealTimeAnalyticsDate` | DoctorsManagementController@getRealTimeAnalyticsDate | atreyaDashboard.authentication |  | `routes/api.php:221` |
| POST | `ashokaDashboard/inActiveUser` | AshokaUserManangementController@inActiveUser | atreyaDashboard.authentication |  | `routes/api.php:196` |
| POST | `ashokaDashboard/listofActiveDoctors` | UserAnalyticsController@listofActiveDoctors | atreyaDashboard.authentication |  | `routes/api.php:213` |
| POST | `ashokaDashboard/login` | AshokaAuthController@ashokaLogin |  |  | `routes/api.php:148` |
| POST | `ashokaDashboard/report/getAllSalesRequests` | AshokaSalesController@getAllSalesRequests | atreyaDashboard.authentication |  | `routes/api.php:316` |
| POST | `ashokaDashboard/report/getCustomizeSalesRequestData` | ReportManagementController@getCustomizeSalesRequestData | atreyaDashboard.authentication |  | `routes/api.php:315` |
| POST | `ashokaDashboard/report/getDoctorAndDeviceWiseReports` | ReportManagementController@getDoctorAndDeviceWiseReports | atreyaDashboard.authentication |  | `routes/api.php:319` |
| POST | `ashokaDashboard/report/getPlatformWiseNoOfReport` | ReportManagementController@getPlatformWiseNoOfReport | atreyaDashboard.authentication |  | `routes/api.php:314` |
| POST | `ashokaDashboard/report/getPlatformWiseReportCount` | ReportManagementController@getPlatformWiseReportCount | atreyaDashboard.authentication |  | `routes/api.php:320` |
| POST | `ashokaDashboard/report/getPrecedingRequestInDateRange` | AshokaSalesController@getPrecedingRequestInDateRange | atreyaDashboard.authentication |  | `routes/api.php:317` |
| POST | `ashokaDashboard/report/getStatesWiseUsersCount` | ReportManagementController@getStatesWiseUsersCount | atreyaDashboard.authentication |  | `routes/api.php:322` |
| POST | `ashokaDashboard/sales/addQuotation` | AshokaQuotationController@addQuotation | atreyaDashboard.authentication |  | `routes/api.php:298` |
| POST | `ashokaDashboard/sales/addSalesRequest` | AshokaSalesController@addSalesRequest | atreyaDashboard.authentication |  | `routes/api.php:278` |
| POST | `ashokaDashboard/sales/addSubSalesRequest` | AshokaSalesController@addSubSalesRequest | atreyaDashboard.authentication |  | `routes/api.php:279` |
| POST | `ashokaDashboard/sales/getAllSalesRequests` | AshokaSalesController@getAllSalesRequests | atreyaDashboard.authentication |  | `routes/api.php:290` |
| POST | `ashokaDashboard/sales/getAllSubSalesRequests` | AshokaSalesController@getAllSubSalesRequests | atreyaDashboard.authentication |  | `routes/api.php:285` |
| GET | `ashokaDashboard/sales/getAshokaCustomers` | AshokaCustomersController@getAshokaCustomers | atreyaDashboard.authentication |  | `routes/api.php:294` |
| GET | `ashokaDashboard/sales/getAshokaPaymentOrderById/{id}` | AshokaPaymentOrderController@getAshokaPaymentOrderById | atreyaDashboard.authentication |  | `routes/api.php:305` |
| GET | `ashokaDashboard/sales/getAshokaPaymentOrders` | AshokaPaymentOrderController@getAshokaPaymentOrders | atreyaDashboard.authentication |  | `routes/api.php:304` |
| GET | `ashokaDashboard/sales/getQuotation` | AshokaQuotationController@getQuotation | atreyaDashboard.authentication |  | `routes/api.php:300` |
| GET | `ashokaDashboard/sales/getSalesRequests` | AshokaSalesController@getSalesRequests | atreyaDashboard.authentication |  | `routes/api.php:280` |
| GET | `ashokaDashboard/sales/getShipmentTrackingRequestId` | AshokaSalesController@getShipmentTrackingRequestId | atreyaDashboard.authentication |  | `routes/api.php:281` |
| POST | `ashokaDashboard/sales/getSingleCustomer` | AshokaCustomersController@getSingleCustomer | atreyaDashboard.authentication |  | `routes/api.php:296` |
| GET | `ashokaDashboard/sales/getSingleQuotation` | AshokaQuotationController@getSingleQuotation | atreyaDashboard.authentication |  | `routes/api.php:301` |
| POST | `ashokaDashboard/sales/getSubSalesRequestsForSingleRequest` | AshokaSalesController@getSubSalesRequestsForSingleRequest | atreyaDashboard.authentication |  | `routes/api.php:284` |
| POST | `ashokaDashboard/sales/saveAshokaCustomer` | AshokaCustomersController@saveAshokaCustomers | atreyaDashboard.authentication |  | `routes/api.php:293` |
| POST | `ashokaDashboard/sales/saveAshokaPaymentOrder` | AshokaPaymentOrderController@saveAshokaPaymentOrder | atreyaDashboard.authentication |  | `routes/api.php:307` |
| POST | `ashokaDashboard/sales/updateAshokaCustomer` | AshokaCustomersController@updateAshokaCustomer | atreyaDashboard.authentication |  | `routes/api.php:292` |
| PUT | `ashokaDashboard/sales/updateAshokaPaymentOrder/{id}` | AshokaPaymentOrderController@updateAshokaPaymentOrder | atreyaDashboard.authentication |  | `routes/api.php:306` |
| POST | `ashokaDashboard/sales/updateFileNameQuotation` | AshokaQuotationController@updateFileNameQuotation | atreyaDashboard.authentication |  | `routes/api.php:302` |
| POST | `ashokaDashboard/sales/updateFinancePaymentConfirmationStatus` | AshokaSalesController@updateFinancePaymentConfirmationStatus | atreyaDashboard.authentication |  | `routes/api.php:283` |
| POST | `ashokaDashboard/sales/updateQuotation` | AshokaQuotationController@updateQuotation | atreyaDashboard.authentication |  | `routes/api.php:299` |
| POST | `ashokaDashboard/sales/updateRequestPaymentConfirmation` | AshokaSalesController@updateRequestPaymentConfirmation | atreyaDashboard.authentication |  | `routes/api.php:309` |
| POST | `ashokaDashboard/sales/updateRequestStatus` | AshokaSalesController@updateRequestStatus | atreyaDashboard.authentication |  | `routes/api.php:282` |
| POST | `ashokaDashboard/sales/updateSalesRequest` | AshokaSalesController@updateSalesRequest | atreyaDashboard.authentication |  | `routes/api.php:289` |
| POST | `ashokaDashboard/sales/updateSingleSubSalesRequest` | AshokaSalesController@updateSingleSubSalesRequest | atreyaDashboard.authentication |  | `routes/api.php:286` |
| POST | `ashokaDashboard/sales/updateSingleSubSalesRequestSalesPerson` | AshokaSalesController@updateSingleSubSalesRequestSalesPerson | atreyaDashboard.authentication |  | `routes/api.php:287` |
| POST | `ashokaDashboard/shipment/addDispatchLink` | AshokaShipmentManagementController@addDispatchLink | atreyaDashboard.authentication |  | `routes/api.php:390` |
| POST | `ashokaDashboard/shipment/addNewShipmentRecord` | AshokaShipmentManagementController@addNewShipmentRecord | atreyaDashboard.authentication |  | `routes/api.php:382` |
| POST | `ashokaDashboard/shipment/addOrUpdateSalesRequest` | AshokaShipmentManagementController@addOrUpdateSalesRequest | atreyaDashboard.authentication |  | `routes/api.php:388` |
| POST | `ashokaDashboard/shipment/addTrackingId` | AshokaShipmentManagementController@addTrackingId | atreyaDashboard.authentication |  | `routes/api.php:392` |
| POST | `ashokaDashboard/shipment/getAllShipmentRecords` | AshokaShipmentManagementController@getAllShipmentRecords | atreyaDashboard.authentication |  | `routes/api.php:381` |
| POST | `ashokaDashboard/shipment/getDispatchRequests` | AshokaShipmentManagementController@getDispatchRequests | atreyaDashboard.authentication |  | `routes/api.php:391` |
| POST | `ashokaDashboard/shipment/getReadyToDispatchRequests` | AshokaShipmentManagementController@getReadyToDispatchRequests | atreyaDashboard.authentication |  | `routes/api.php:389` |
| POST | `ashokaDashboard/shipment/getSalesDetailsUsingDevices` | AshokaShipmentManagementController@getSalesDetailsUsingDevices | atreyaDashboard.authentication |  | `routes/api.php:393` |
| POST | `ashokaDashboard/shipment/getShipmentDataUsingSalesRecord` | AshokaShipmentManagementController@getShipmentDataUsingSalesRecord | atreyaDashboard.authentication |  | `routes/api.php:387` |
| POST | `ashokaDashboard/shipment/updateDevicesInShipment` | AshokaShipmentManagementController@updateShipmentDevices | atreyaDashboard.authentication |  | `routes/api.php:385` |
| POST | `ashokaDashboard/shipment/updateOrderConfirmationDetails` | AshokaShipmentManagementController@updateOrderConfirmationDetails | atreyaDashboard.authentication |  | `routes/api.php:384` |
| POST | `ashokaDashboard/shipment/updateShipmentInvoiceDetails` | AshokaShipmentManagementController@updateShipmentInvoiceDetails | atreyaDashboard.authentication |  | `routes/api.php:383` |
| POST | `ashokaDashboard/shipment/updateShipmentStatus` | AshokaShipmentManagementController@updateShipmentStatus | atreyaDashboard.authentication |  | `routes/api.php:386` |
| GET | `ashokaDashboard/status/getDeviceStatuses` | AshokaStatusMasterController@getDeviceStatuses | atreyaDashboard.authentication |  | `routes/api.php:228` |
| GET | `ashokaDashboard/status/getSalesRequestPaymentStatuses` | AshokaStatusMasterController@getSalesRequestPaymentStatuses | atreyaDashboard.authentication |  | `routes/api.php:225` |
| GET | `ashokaDashboard/status/getSalesRequestUserTypes` | AshokaStatusMasterController@getSalesRequestUserTypes | atreyaDashboard.authentication |  | `routes/api.php:227` |
| GET | `ashokaDashboard/status/getShipmentTrackingStatuses` | AshokaStatusMasterController@getShipmentTrackingStatuses | atreyaDashboard.authentication |  | `routes/api.php:226` |
| POST | `ashokaDashboard/storeReleaseDetails` | DoctorController@storeReleaseDetails | atreyaDashboard.authentication |  | `routes/api.php:182` |
| POST | `ashokaDashboard/stores/addAsset` | AshokaStoresController@addNewAsset | atreyaDashboard.authentication |  | `routes/api.php:267` |
| POST | `ashokaDashboard/stores/addAssetComponent` | AshokaStoresController@addAssetComponent | atreyaDashboard.authentication |  | `routes/api.php:269` |
| POST | `ashokaDashboard/stores/assignAssetsToUser` | AshokaStoresController@assignAssetsToUser | atreyaDashboard.authentication |  | `routes/api.php:273` |
| GET | `ashokaDashboard/stores/getAllAssets` | AshokaStoresController@getAllAssets | atreyaDashboard.authentication |  | `routes/api.php:268` |
| GET | `ashokaDashboard/stores/getAssetComponents` | AshokaStoresController@getAssetComponents | atreyaDashboard.authentication |  | `routes/api.php:270` |
| POST | `ashokaDashboard/stores/getAssetWiseComponent` | AshokaStoresController@getAssetWiseComponent | atreyaDashboard.authentication |  | `routes/api.php:271` |
| POST | `ashokaDashboard/stores/getAssetWiseUnassignedComponent` | AshokaStoresController@getAssetWiseUnassignedComponent | atreyaDashboard.authentication |  | `routes/api.php:272` |
| POST | `ashokaDashboard/stores/getAssignedAssetToUser` | AshokaStoresController@getAssignedAssetToUser | atreyaDashboard.authentication |  | `routes/api.php:274` |
| POST | `ashokaDashboard/subscription/addNewReportsSubscriptionsForParticularDoctor` | AshokaSubscriptionManagementController@addNewReportsSubscriptionsForParticularDoctor | atreyaDashboard.authentication |  | `routes/api.php:365` |
| GET | `ashokaDashboard/subscription/eligibleUsersForGrant` | NadiReportGrantController@getEligibleUsersForGrant | atreyaDashboard.authentication |  | `routes/api.php:367` |
| POST | `ashokaDashboard/subscription/getAllReportsTypes` | AshokaSubscriptionManagementController@getAllReportsTypes | atreyaDashboard.authentication |  | `routes/api.php:363` |
| POST | `ashokaDashboard/subscription/getAllSubscriptions` | AshokaSubscriptionManagementController@getAllSubscriptions | atreyaDashboard.authentication |  | `routes/api.php:362` |
| POST | `ashokaDashboard/subscription/getAllSubscriptionsTypes` | AshokaSubscriptionManagementController@getAllSubscriptionsTypes | atreyaDashboard.authentication |  | `routes/api.php:364` |
| POST | `ashokaDashboard/subscription/getDoctorWiseReportsSubscription` | AshokaSubscriptionManagementController@getDoctorWiseReportsSubscription | atreyaDashboard.authentication |  | `routes/api.php:361` |
| POST | `ashokaDashboard/subscription/grantReports` | NadiReportGrantController@grantReports | atreyaDashboard.authentication |  | `routes/api.php:368` |
| GET | `ashokaDashboard/subscription/reportBalance/{userId}` | NadiReportGrantController@getUserReportBalance | atreyaDashboard.authentication |  | `routes/api.php:370` |
| GET | `ashokaDashboard/subscription/reportGrantHistory/{userId}` | NadiReportGrantController@getGrantHistory | atreyaDashboard.authentication |  | `routes/api.php:369` |
| POST | `ashokaDashboard/subscriptions/editPlan` | AshokaSubscriptionManagementController@editSubscription | atreyaDashboard.authentication |  | `routes/api.php:399` |
| POST | `ashokaDashboard/subscriptions/editPlanLimit` | AshokaSubscriptionManagementController@editSubscriptionLimit | atreyaDashboard.authentication |  | `routes/api.php:401` |
| GET | `ashokaDashboard/subscriptions/getAllTransactionDetailsForInvoice` | AshokaSubscriptionManagementController@getAllTransactionDetailsForInvoice | atreyaDashboard.authentication |  | `routes/api.php:402` |
| GET | `ashokaDashboard/subscriptions/getEndPoints` | AshokaSubscriptionManagementController@getEndPoints | atreyaDashboard.authentication |  | `routes/api.php:398` |
| GET | `ashokaDashboard/subscriptions/getPlans` | AshokaSubscriptionManagementController@getAllPlans | atreyaDashboard.authentication |  | `routes/api.php:397` |
| GET | `ashokaDashboard/summary/coupons` | NtCouponsController@getAllCoupons |  |  | `routes/api.php:158` |
| POST | `ashokaDashboard/summary/coupons` | NtCouponsController@addCoupon |  |  | `routes/api.php:159` |
| PUT | `ashokaDashboard/summary/coupons/{id}` | NtCouponsController@updateCoupon |  |  | `routes/api.php:160` |
| PATCH | `ashokaDashboard/summary/coupons/{id}/status` | NtCouponsController@toggleCouponStatus |  |  | `routes/api.php:161` |
| POST | `ashokaDashboard/summary/dailyProductionDevicesSummary` | DeviceManagementController@dailyProductionDevicesSummary |  |  | `routes/api.php:165` |
| POST | `ashokaDashboard/summary/getDailySignupNtSummary` | AshokaSalesController@getDailySignupNtSummary |  |  | `routes/api.php:168` |
| POST | `ashokaDashboard/summary/getWeeklySalesPersonsWiseReport` | AshokaSalesController@getWeeklySalesPersonsWiseReport |  |  | `routes/api.php:167` |
| POST | `ashokaDashboard/summary/weeklySaleReportData` | AshokaSalesController@weeklySaleReportData |  |  | `routes/api.php:166` |
| POST | `ashokaDashboard/totalPatientsForDoctor` | UserAnalyticsController@totalPatientsForDoctor | atreyaDashboard.authentication |  | `routes/api.php:209` |
| POST | `ashokaDashboard/totalSignUp` | UserAnalyticsController@totalSignUp | atreyaDashboard.authentication |  | `routes/api.php:207` |
| POST | `ashokaDashboard/updateAllowedCountriesUserWise` | AshokaUserManangementController@updateAllowedCountriesUserWise | atreyaDashboard.authentication |  | `routes/api.php:201` |
| POST | `ashokaDashboard/updateAvoidLocationSelection` | AshokaUserManangementController@updateAvoidLocationSelection | atreyaDashboard.authentication |  | `routes/api.php:204` |
| POST | `ashokaDashboard/updateUser` | AshokaUserManangementController@updateUser | atreyaDashboard.authentication |  | `routes/api.php:188` |
| GET | `auth/google/redirect` | Closure |  |  | `routes/web.php:52` |
| POST | `calculatePlanPrice` | NtTransactionController@calculatePlanPrice | api, auth.token |  | `routes/api.php:1418` |
| GET | `careServicesReport` | ReportsWebController@careServicesReport |  |  | `routes/api.php:1523` |
| POST | `checkGeoIPValidity` | PublicFunctionsController@checkGeoIPValidity | api |  | `routes/api.php:753` |
| POST | `checkMobileNumber` | CheckUserExistOrNotController@checkMobileNumberV2 | api |  | `routes/api.php:763` |
| GET | `checkReportStatus` | ReportsWebController@checkReportStatus | api |  | `routes/api.php:754` |
| POST | `checkUsername` | CheckUserExistOrNotController@checkUsername | api |  | `routes/api.php:764` |
| POST | `checkValidDateTest` | BadminFunctionsController@checkValidDateTest |  |  | `routes/api.php:734` |
| GET | `checkpatientcode` | CheckUserExistOrNotController@checkPatientCode | api, auth.token |  | `routes/api.php:996` |
| GET | `checkusernameormobileno` | CheckUserExistOrNotController@checkMobileNumberOrEmail | api |  | `routes/api.php:1426` |
| POST | `client/askQuery` | AskQuestionController@askQuestion | api, client.authentication |  | `routes/api.php:1451` |
| POST | `client/changePassword` | AccountManagementController@changePassword | api, client.authentication |  | `routes/api.php:1465` |
| POST | `client/clientDetails` | EditProfileController@clientDetails | api, client.authentication |  | `routes/api.php:1462` |
| POST | `client/clientEditProfile` | EditProfileController@clientEditProfile | api, client.authentication |  | `routes/api.php:1450` |
| POST | `client/clientRemainingFees` | EditProfileController@clientRemainingFees | api, client.authentication |  | `routes/api.php:1463` |
| POST | `client/corporate/addNewPatientForCorporate` | orgPatientManagementController@addNewPatientForCorporate | api, client.authentication |  | `routes/api.php:1475` |
| POST | `client/deleteClientAccount` | AccountManagementController@deleteClientAccount | api, client.authentication |  | `routes/api.php:1468` |
| POST | `client/deleteQuery` | AskQuestionController@deleteQuestion | api, client.authentication |  | `routes/api.php:1458` |
| POST | `client/deleteReport` | VisitManagementController@deleteReport | api, client.authentication |  | `routes/api.php:1469` |
| POST | `client/fetchAskedQueriesList` | AskQuestionController@askQuestionList | api, client.authentication |  | `routes/api.php:1452` |
| POST | `client/getBannerList` | AccountManagementController@getBannerList | api, client.authentication |  | `routes/api.php:1464` |
| POST | `client/getDataConsent` | DataConsentController@getDataConsent | api, client.authentication |  | `routes/api.php:1448` |
| POST | `client/getNadiParametersData` | AccountManagementController@getNadiParametersData | api, client.authentication |  | `routes/api.php:1472` |
| POST | `client/getPreviousVisits` | VisitManagementController@getPreviousVisits | api, client.authentication |  | `routes/api.php:1447` |
| POST | `client/savePrakrutiQuestionCorporatePatient` | orgPatientManagementController@savePrakrutiQuestionCorporatePatient | api, client.authentication |  | `routes/api.php:1453` |
| POST | `client/turyaa/homeData` | DietManagementController@homeData | api, client.authentication |  | `routes/api.php:1486` |
| POST | `client/updateDataConsent` | DataConsentController@updateDataConsent | api, client.authentication |  | `routes/api.php:1449` |
| POST | `client/updateQuery` | AskQuestionController@updateQuestion | api, client.authentication |  | `routes/api.php:1457` |
| POST | `client/visitWiseReports` | VisitManagementController@visitWiseReports | api, client.authentication |  | `routes/api.php:1460` |
| POST | `createNtOrder` | NtTransactionController@createNtOrder | api, auth.token |  | `routes/api.php:1415` |
| POST | `cron/get-appointmest-using-ids` | CronController@fetchAppointmentsInfo | api |  | `routes/api.php:808` |
| POST | `cron/get-date-wise-appointment` | CronController@getDateWiseAppointmentDetails | api |  | `routes/api.php:806` |
| GET | `currentUserAccessibleUsers` | DataManagementController@getCurrentUserDataAccess | api, auth.token |  | `routes/api.php:1041` |
| GET | `currentUserAccessibleUsersWithLocations` | DataManagementController@getCurrentAccessibleUsersWithClinics | api, auth.token |  | `routes/api.php:1043` |
| POST | `custom-data/getContentTypesWiseData` | CustomizeDetailsController@fetchTypeWiseCommonData | api, auth.token |  | `routes/api.php:1047` |
| GET | `custom/getCustomizePrakrutiQuestions` | CustomizeDetailsController@getCustomizePrakrutiQuestions | api, auth.token |  | `routes/api.php:1052` |
| POST | `deleteClinic` | ClinicController@deleteClinic | api, auth.token |  | `routes/api.php:1009` |
| POST | `deleteUserAccount` | AuthController@deleteUserAccount | api, auth.token |  | `routes/api.php:1002` |
| GET | `dietReport` | ReportsWebController@dietAndLifestylereport |  |  | `routes/api.php:1508` |
| POST | `doctor/doctorFormDetails` | ReorderFeaturesController@doctorFormDetails | api, auth.token |  | `routes/api.php:1243` |
| PUT | `doctor/updateDoctorInformation` | ReorderFeaturesController@updateDoctorInformation | api, auth.token |  | `routes/api.php:1244` |
| POST | `eMandate/enachRegistration` | ENACHController@enachRegistration |  |  | `routes/api.php:1919` |
| GET | `eMandate/getAllSalesUser` | ENACHController@getAllSalesUser |  |  | `routes/api.php:1922` |
| GET | `eMandate/getEnachCustomers` | ENACHController@getEnachCustomers |  |  | `routes/api.php:1921` |
| GET | `eMandate/getScheduleDebitDetails` | ENACHController@getScheduleDebitDetails |  |  | `routes/api.php:1923` |
| POST | `eMandate/handleResponse` | ENACHController@handleResponse |  |  | `routes/api.php:1920` |
| POST | `eMandate/scheduleDebit` | ENACHController@scheduleDebit |  |  | `routes/api.php:1926` |
| POST | `eMandate/verifyMandate` | ENACHController@verifyMandate |  |  | `routes/api.php:1924` |
| POST | `eMandate/verifyTransaction` | ENACHController@verifyTransaction |  |  | `routes/api.php:1925` |
| POST | `editApproveRejectAppointment` | AppointmentController@updateApprveReject | api, auth.token |  | `routes/api.php:1022` |
| POST | `editFcmToken` | AuthController@updateFcmToken | api, auth.token |  | `routes/api.php:971` |
| POST | `editProfile` | DoctorController@editProfile | api, auth.token |  | `routes/api.php:977` |
| POST | `external-capture/addReportData` | ExternalCaptureController@addReportData | api, auth.token |  | `routes/api.php:1409` |
| POST | `external-capture/generateS3UploadUrl` | PublicFunctionsController@getNTExternalPresignedS3Url | api, auth.token |  | `routes/api.php:1411` |
| POST | `external/nadi/analyzeNadi` | ExternalUserController@analyzeNadiData | api |  | `routes/api.php:860` |
| POST | `external/nadi/validateDevice` | ExternalUserController@validateDeviceNumber | api |  | `routes/api.php:858` |
| POST | `external/nadi/validateNadiRequest` | ExternalUserController@validateNadiRequest | api |  | `routes/api.php:856` |
| GET | `external/patient/getPatients` | ExternalUserController@getPatients | api | external.patient.get | `routes/api.php:866` |
| GET | `external/patient/{patient_code}/reports` | ExternalUserController@getPatientWiseReports | api | external.patient.reports | `routes/api.php:868` |
| GET | `external/report/nadi-guna/{visit_id}` | ExternalUserController@getNtReportData | api | external.report.nt.get | `routes/api.php:873` |
| GET | `external/report/swasthya-darshika/{visit_id}` | ExternalUserController@getSdReportData | api | external.report.sd.get | `routes/api.php:875` |
| GET | `external/report/{visit_id}` | ExternalUserController@getReportData | api | external.report.show | `routes/api.php:872` |
| POST | `external/validateExternalUser` | ExternalUserController@validateExternalUser | api |  | `routes/api.php:853` |
| POST | `fetchClinicInfo` | ClinicController@fetchClinicInfo | api, auth.token |  | `routes/api.php:1012` |
| POST | `fetchLastVisitPrescription` | MedicalInventoryController@fetchLastVisitPrescription | api, auth.token |  | `routes/api.php:938` |
| POST | `fetchPatientNames` | PatientDetailsController@fetchPatientNames | api, auth.token |  | `routes/api.php:931` |
| POST | `fetchSingleClinicInfo` | ClinicController@fetchSingleClinicInfo | api, auth.token |  | `routes/api.php:1010` |
| POST | `fetchUserInfo` | DoctorController@fetchUserInfo | api, auth.token |  | `routes/api.php:988` |
| POST | `flush-cache` | AuthController@flushAllCache |  |  | `routes/api.php:138` |
| POST | `forgotPassword` | AuthController@getForgotPassword | api |  | `routes/api.php:777` |
| POST | `generate-pdf` | NewPdfGenerateController@generatePdf **shadowed** | api |  | `routes/api.php:1433` |
| POST | `generate-pdf` | NewPdfGenerateController@downloadAndSavePDF |  |  | `routes/web.php:41` |
| POST | `generateLambda` | GenerateSwasthyaLambda@generateLambda | api, auth.token |  | `routes/api.php:922` |
| GET | `generatepdf` | PdfGeneratorController@generateAdPdf | api |  | `routes/api.php:1431` |
| GET | `getAccountData` | UserStatsController@getUserAccountData | api, auth.token |  | `routes/api.php:958` |
| POST | `getAddressUsingPincode` | PublicFunctionsController@getAddressUsingPincode | api |  | `routes/api.php:752` |
| GET | `getAllCountries` | PatientDetailsController@getAllCountries | api |  | `routes/api.php:766` |
| POST | `getAllCountries` | PatientDetailsController@getAllCountries | api |  | `routes/api.php:766` |
| POST | `getAllCountriesName` | DoctorController@getAllCountriesName | api |  | `routes/api.php:750` |
| GET | `getAllFeatures` | ReceptionManagementController@getAllFeatures | api, auth.token |  | `routes/api.php:1354` |
| POST | `getAllUserClinics` | ClinicController@getAllUserClinics | api, auth.token |  | `routes/api.php:1016` |
| POST | `getAnswerTypes` | CustomizeDetailsController@getAnswerTypes | api, auth.token |  | `routes/api.php:1039` |
| GET | `getAppLanguages` | PublicFunctionsController@getNTFrontendAppLanguages | api |  | `routes/api.php:771` |
| POST | `getApproveRejectList` | AppointmentController@getApproveReject | api, auth.token |  | `routes/api.php:1021` |
| POST | `getAssociationsCount` | PatientDetailsController@getAssociationsCount | api, auth.token |  | `routes/api.php:935` |
| POST | `getCountryWiseStates` | DoctorController@getCountryWiseStates | api |  | `routes/api.php:751` |
| GET | `getCurrencyType` | SignUpController@getCurrencyType | api |  | `routes/api.php:760` |
| POST | `getCurrencyType` | SignUpController@getCurrencyType | api |  | `routes/api.php:760` |
| GET | `getCurrencyTypes` | AuthController@currencyTypes | api |  | `routes/api.php:767` |
| POST | `getCurrencyTypes` | AuthController@currencyTypes | api |  | `routes/api.php:767` |
| POST | `getCustomizeTab` | CustomizeDetailsController@getCustomizeTab | api, auth.token |  | `routes/api.php:1033` |
| POST | `getDataUsingIp` | S3BucketController@getDataUsingIp |  |  | `routes/api.php:414` |
| POST | `getDietDataTest` | MedicalReportSaveController@getDietDataStateWise |  |  | `routes/api.php:728` |
| POST | `getDinacharyaRutucharya` | DinacharyaController@dinacharyaAndRutucharyaFiles | api, auth.token |  | `routes/api.php:941` |
| GET | `getDisallowedReports` | DoctorController@getDisallowedReports | api, auth.token |  | `routes/api.php:982` |
| GET | `getDocumentTypes` | DoctorController@getDocumentTypes | api |  | `routes/api.php:769` |
| POST | `getDocumentTypes` | DoctorController@getDocumentTypes | api |  | `routes/api.php:769` |
| GET | `getExperienceList` | DoctorController@getExperienceList | api |  | `routes/api.php:761` |
| POST | `getExperienceList` | DoctorController@getExperienceList | api |  | `routes/api.php:761` |
| GET | `getFormLanguages` | DoctorController@getFormLanguages | api |  | `routes/api.php:768` |
| POST | `getFormLanguages` | DoctorController@getFormLanguages | api |  | `routes/api.php:768` |
| POST | `getFormList` | CustomizeDetailsController@getFormList | api, auth.token |  | `routes/api.php:1038` |
| POST | `getGermanyRutucharya` | DinacharyaController@getGermanyRutucharya | api, auth.token |  | `routes/api.php:943` |
| POST | `getHelpVideos` | HelpController@getHelpVideos | api, auth.token |  | `routes/api.php:946` |
| POST | `getLanguage` | PatientDetailsController@fetchLanguageCode | api |  | `routes/api.php:1423` |
| GET | `getLanguages` | DoctorController@getLanguages | api |  | `routes/api.php:765` |
| POST | `getLanguages` | DoctorController@getLanguages | api |  | `routes/api.php:765` |
| POST | `getLimitedActivePatients` | PatientDetailsController@getLimitedActivePatients | api, auth.token |  | `routes/api.php:928` |
| POST | `getLinkDevice` | LinkDeviceContoller@getLinkDevice | api, auth.token |  | `routes/api.php:1263` |
| GET | `getMaritialList` | DoctorController@getMaritialList | api |  | `routes/api.php:762` |
| POST | `getMaritialList` | DoctorController@getMaritialList | api |  | `routes/api.php:762` |
| POST | `getNtFaq` | HelpController@getFaqJson | api |  | `routes/api.php:783` |
| POST | `getNtHelpVideos` | HelpController@getHelpVideosJson | api |  | `routes/api.php:782` |
| GET | `getPhpInfo` | BadminFunctionsController@checkPhpInfo |  |  | `routes/api.php:733` |
| GET | `getProfessionType` | DoctorController@getProfessionType | api |  | `routes/api.php:756` |
| GET | `getReleaseDetails` | DoctorController@getReleaseDetails | api, auth.token |  | `routes/api.php:1007` |
| POST | `getReportWiseLanguages` | ReportsWebController@getReportWiseLanguages | api, auth.token |  | `routes/api.php:924` |
| GET | `getSalutationTypes` | SignUpController@salutationTypes | api |  | `routes/api.php:759` |
| POST | `getSalutationTypes` | SignUpController@salutationTypes | api |  | `routes/api.php:759` |
| POST | `getSinglePlan` | SubscriptionController@getSinglePlanDetails |  |  | `routes/api.php:729` |
| POST | `getSymptomInfo` | CustomizeDetailsController@getSymptomInfo | api, auth.token |  | `routes/api.php:1031` |
| GET | `getUpiDetails` | DoctorController@getUpiDetails | api, auth.token |  | `routes/api.php:985` |
| POST | `getUserCurrentSummary` | AuthController@getUserSummaryV2 | api, auth.token |  | `routes/api.php:951` |
| POST | `getUserCustomizeSummary` | AuthController@getUserCustomizeSummary | api, auth.token |  | `routes/api.php:953` |
| GET | `getUserDefaultClinicDetails` | ClinicController@getUserDefaultClinicDetails | api, auth.token |  | `routes/api.php:1018` |
| POST | `getUserDetailsUsingMobileNumber` | PublicFunctionsController@getUserDetailsUsingMobileNumber | api |  | `routes/api.php:748` |
| POST | `getUserStatsData` | UserStatsController@getUserStatsData | api, auth.token |  | `routes/api.php:955` |
| POST | `getUserSummary` | AuthController@getUserSummary | api, auth.token |  | `routes/api.php:949` |
| GET | `getUserWiseAllowedReports` | DoctorController@getUserWiseAllowedReports | api, auth.token |  | `routes/api.php:979` |
| POST | `getallroles` | AllPrakrutiTypesController@getAllRole | api |  | `routes/api.php:1429` |
| GET | `getdetailsbymobileno` | CheckUserExistOrNotController@getDetailsByMobileNo | api |  | `routes/api.php:1427` |
| POST | `getmedicineprescription` | MedicineContorller@getMedicinePrescribed | api, auth.token |  | `routes/api.php:999` |
| POST | `guna/assingDeviceDetails` | BadminFunctionsController@assingDeviceDetails | api |  | `routes/api.php:898` |
| POST | `guna/getBadminDoctorInfo` | BadminFunctionsController@getDoctorsInfoAll | api |  | `routes/api.php:896` |
| POST | `guna/getPatientList` | UserDetailsController@getPatientList | api |  | `routes/api.php:887` |
| POST | `guna/getSingleClinicData` | GunaLocalityInfoController@getSingleClinicData | api |  | `routes/api.php:891` |
| POST | `guna/getSingleUserData` | UserDetailsController@getSingleUserData | api |  | `routes/api.php:885` |
| POST | `guna/getUserByUsername` | UserDetailsController@getUserByUsername | api |  | `routes/api.php:889` |
| POST | `guna/updateUserDetails` | UserDetailsController@updateUserDetails | api |  | `routes/api.php:893` |
| POST | `infinitePatientList` | PatientDetailsController@infinitePatientList | api, auth.token |  | `routes/api.php:927` |
| POST | `linkDeviceInHouseV2` | LinkDeviceContoller@linkDeviceInHouseV2 | api, auth.token |  | `routes/api.php:1265` |
| POST | `loadNewAppointment` | AppointmentController@load_new_appointment | api, auth.token |  | `routes/api.php:1023` |
| POST | `login` | AuthController@login | api |  | `routes/api.php:737` |
| POST | `loginOtpBasedUser` | AuthController@loginOtpBasedUser | api |  | `routes/api.php:739` |
| POST | `logout` | AuthController@logout | api, auth.token |  | `routes/api.php:968` |
| POST | `markClinicAsDefault` | ClinicController@markClinicAsDefault | api, auth.token |  | `routes/api.php:1015` |
| POST | `markOnImage` | AppointmentController@markonimageedit | api, auth.token |  | `routes/api.php:1024` |
| POST | `medicalForm/getCategoryWiseQuestions` | CustomizeDetailsController@getCategoryWiseQuestions | api, auth.token |  | `routes/api.php:1068` |
| POST | `medicalForm/getCategoryWiseQuestionsList` | CustomizeDetailsController@getCategoryWiseQuestionsList | api, auth.token |  | `routes/api.php:1069` |
| POST | `medicalForm/getCateogoryWiseQuestionsForSingleUser` | CustomizeDetailsController@getCateogoryWiseQuestionsForSingleUser | api, auth.token |  | `routes/api.php:1075` |
| POST | `medicalForm/getDoctorQuestions` | CustomizeDetailsController@getDoctorQuestions | api, auth.token |  | `routes/api.php:1071` |
| POST | `medicalForm/getFormCategories` | CustomizeDetailsController@getDefaultFormCategories | api, auth.token |  | `routes/api.php:1066` |
| POST | `medicalForm/updateCateogoryWiseQuestions` | CustomizeDetailsController@updateCateogoryWiseQuestions | api, auth.token |  | `routes/api.php:1073` |
| POST | `medicalForm/updateCateogoryWiseQuestionsForSingleUser` | CustomizeDetailsController@updateCateogoryWiseQuestionsForSingleUser | api, auth.token |  | `routes/api.php:1074` |
| POST | `medicalFormList` | CustomizeDetailsController@medicalFormList | api, auth.token |  | `routes/api.php:1029` |
| POST | `medicalInventory/addCompany` | CompanyController@addCompany | api, auth.token |  | `routes/api.php:1270` |
| POST | `medicalInventory/addIngredient` | IngredientController@addIngredient | api, auth.token |  | `routes/api.php:1289` |
| POST | `medicalInventory/addMedicine` | MedicineController@addMedicine | api, auth.token |  | `routes/api.php:1272` |
| POST | `medicalInventory/addNewMedicineType` | MedicineController@addNewMedicineType | api, auth.token |  | `routes/api.php:1309` |
| POST | `medicalInventory/addNewPrescriptionIngredient` | IngredientController@addNewPrescriptionIngredient | api, auth.token |  | `routes/api.php:1290` |
| POST | `medicalInventory/addPudi` | PudiController@addPudi | api, auth.token |  | `routes/api.php:1280` |
| POST | `medicalInventory/deleteCompany` | CompanyController@deleteCompany | api, auth.token |  | `routes/api.php:1271` |
| POST | `medicalInventory/deleteIngredient` | IngredientController@deleteIngredient | api, auth.token |  | `routes/api.php:1300` |
| POST | `medicalInventory/deleteMedicine` | MedicineController@deleteMedicine | api, auth.token |  | `routes/api.php:1279` |
| POST | `medicalInventory/deleteMedicineType` | MedicineController@deleteMedicineType | api, auth.token |  | `routes/api.php:1311` |
| POST | `medicalInventory/deletePudi` | PudiController@deletePudi | api, auth.token |  | `routes/api.php:1286` |
| POST | `medicalInventory/fetchLastVisitPrescriptions` | MedicalInventoryController@fetchLastVisitPrescriptions | api, auth.token |  | `routes/api.php:1275` |
| POST | `medicalInventory/fetchPreviousPrescriptions` | MedicalInventoryController@fetchPreviousPrescriptions | api, auth.token |  | `routes/api.php:1276` |
| POST | `medicalInventory/fetchSingleMedicine` | MedicineController@fetchSingleMedicine | api, auth.token |  | `routes/api.php:1273` |
| POST | `medicalInventory/fetchSinglePudi` | PudiController@fetchSinglePudi | api, auth.token |  | `routes/api.php:1287` |
| GET | `medicalInventory/getAllCompany` | CompanyController@getCompanyList | api, auth.token |  | `routes/api.php:1269` |
| GET | `medicalInventory/getAllIngredient` | IngredientController@getAllIngredient | api, auth.token |  | `routes/api.php:1298` |
| GET | `medicalInventory/getAllMedicine` | MedicineController@getAllMedicine | api, auth.token |  | `routes/api.php:1282` |
| GET | `medicalInventory/getAllMedicineNamesWithTypes` | MedicineController@getAllMedicineNamesWithTypes | api, auth.token |  | `routes/api.php:1305` |
| POST | `medicalInventory/getAllMedicineTypes` | MedicineController@getAllMedicineTypes | api, auth.token |  | `routes/api.php:1307` |
| GET | `medicalInventory/getAllPudi` | PudiController@getAllPudi | api, auth.token |  | `routes/api.php:1288` |
| POST | `medicalInventory/getAllQuantitiesWithType` | MedicineController@getAllQuantitiesWithType | api, auth.token |  | `routes/api.php:1313` |
| GET | `medicalInventory/getAllQuantity` | MedicineController@getAllQuantity | api, auth.token |  | `routes/api.php:1301` |
| POST | `medicalInventory/getAllSupplimentMedicineTypes` | MedicineController@getAllSupplimentMedicineTypes | api, auth.token |  | `routes/api.php:1308` |
| POST | `medicalInventory/getCompanyDetails` | CompanyController@getCompanyDetails | api, auth.token |  | `routes/api.php:1302` |
| POST | `medicalInventory/getIngredientDetails` | IngredientController@fetchSingleIngredient | api, auth.token |  | `routes/api.php:1299` |
| POST | `medicalInventory/getMedicineNamesRespectToType` | MedicineController@getMedicineNamesRespectToType | api, auth.token |  | `routes/api.php:1314` |
| POST | `medicalInventory/getMedicineTiming` | MedicalInventoryController@getMedicineTiming | api, auth.token |  | `routes/api.php:1316` |
| POST | `medicalInventory/getMedicineWithComsume` | MedicalInventoryController@getMedicineWithComsume | api, auth.token |  | `routes/api.php:1317` |
| POST | `medicalInventory/getPudiList` | MedicalInventoryController@getPudiList | api, auth.token |  | `routes/api.php:1268` |
| POST | `medicalInventory/getQuantity` | MedicineController@getQuantity | api, auth.token |  | `routes/api.php:1277` |
| GET | `medicalInventory/getSupplementsAllMedicine` | MedicineController@getSupplementsAllMedicine | api, auth.token |  | `routes/api.php:1283` |
| GET | `medicalInventory/medicineTypes` | MedicineController@medicineTypes | api, auth.token |  | `routes/api.php:1284` |
| POST | `medicalInventory/prescriptionInfo` | MedicalInventoryController@fetchPrescriptionInformation | api, auth.token |  | `routes/api.php:1274` |
| GET | `medicalInventory/summary` | MedicalInventoryController@getMedicalInventorySummary | api, auth.token |  | `routes/api.php:1318` |
| GET | `medicalInventory/supplementMedicineTypes` | MedicineController@getSupplementTypes | api, auth.token |  | `routes/api.php:1285` |
| POST | `medicalInventory/updateCompany` | CompanyController@updateCompany | api, auth.token |  | `routes/api.php:1303` |
| POST | `medicalInventory/updateIngredient` | IngredientController@updateIngredient | api, auth.token |  | `routes/api.php:1297` |
| POST | `medicalInventory/updateMedicine` | MedicineController@updateMedicine | api, auth.token |  | `routes/api.php:1278` |
| POST | `medicalInventory/updateMedicineType` | MedicineController@updateMedicineType | api, auth.token |  | `routes/api.php:1310` |
| POST | `medicalInventory/updatePudi` | PudiController@updatePudi | api, auth.token |  | `routes/api.php:1281` |
| POST | `medicalInventory/uploadIngredient` | IngredientController@bulkAddIngredientCsv | api, auth.token |  | `routes/api.php:1293` |
| POST | `medicalInventory/uploadMedicine` | MedicineController@bulkAddMedicineCsv | api, auth.token |  | `routes/api.php:1294` |
| POST | `medicalInventory/uploadSupplement` | MedicineController@bulkAddSupplementCsv | api, auth.token |  | `routes/api.php:1295` |
| GET | `medicalVisitReport` | ReportsWebController@medicalVisitReport |  |  | `routes/api.php:1517` |
| GET | `medicalVisitReportV2` | ReportsWebController@medicalVisitReportV2 |  |  | `routes/api.php:1519` |
| POST | `nadi-pariksha-admin/add-admin` | CoachDashboardController@addAdmin | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:114` |
| POST | `nadi-pariksha-admin/add-coupon` | CoachDashboardController@addCoupon | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:87` |
| GET | `nadi-pariksha-admin/admin-users` | CoachDashboardController@adminUsersManagement | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:112` |
| GET | `nadi-pariksha-admin/auth/google/callback` | CoachDashboardController@handleGoogleCallback |  |  | `routes/web.php:70` |
| GET | `nadi-pariksha-admin/coach-dashboard` | CoachDashboardController@adminCoachManagement | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:96` |
| GET | `nadi-pariksha-admin/coach-user-details/{id}` | CoachDashboardController@adminCoachUserDetails | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:97` |
| GET | `nadi-pariksha-admin/coupon-management` | CoachDashboardController@couponManagement | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:83` |
| GET | `nadi-pariksha-admin/dashboard` | CoachDashboardController@adminDashboard | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:82` |
| POST | `nadi-pariksha-admin/deactivate-admin` | CoachDashboardController@deactivateAdmin | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:115` |
| POST | `nadi-pariksha-admin/delete-coupon` | CoachDashboardController@deleteCoupon | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:89` |
| GET | `nadi-pariksha-admin/doctor/edit/{id}` | CoachDashboardController@editDoctorDetailsView | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:124` |
| POST | `nadi-pariksha-admin/doctor/update/{id}` | CoachDashboardController@updateDoctorDetails | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:125` |
| GET | `nadi-pariksha-admin/doctor/{id}` | CoachDashboardController@viewDoctorDetails | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:123` |
| POST | `nadi-pariksha-admin/edit-coupon` | CoachDashboardController@editCoupon | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:88` |
| GET | `nadi-pariksha-admin/get-all-admins` | CoachDashboardController@getAllAdminUsers | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:113` |
| GET | `nadi-pariksha-admin/get-all-users` | CoachDashboardController@getAllUsersForAdmin | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:99` |
| GET | `nadi-pariksha-admin/get-coupons` | CoachDashboardController@getCoupons | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:86` |
| GET | `nadi-pariksha-admin/get-marketing-leads` | CoachDashboardController@getMarketingLeads | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:106` |
| GET | `nadi-pariksha-admin/get-payments` | CoachDashboardController@getPayments | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:90` |
| GET | `nadi-pariksha-admin/getAllDoctorsDetails` | CoachDashboardController@getAllDoctorsDetails | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:122` |
| GET | `nadi-pariksha-admin/getAlladminDashFeatures` | CoachDashboardController@getAlladminDashFeatures | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:118` |
| GET | `nadi-pariksha-admin/login` | CoachDashboardController@showAdminLoginPage |  |  | `routes/web.php:72` |
| POST | `nadi-pariksha-admin/login-validation` | CoachDashboardController@adminLoginValidation |  |  | `routes/web.php:73` |
| GET | `nadi-pariksha-admin/logout` | CoachDashboardController@adminLogout |  | adminLogout | `routes/web.php:74` |
| POST | `nadi-pariksha-admin/logout` | CoachDashboardController@adminLogout |  | adminLogout | `routes/web.php:74` |
| POST | `nadi-pariksha-admin/make-report-free` | CoachDashboardController@makeReportFree **shadowed** | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:100` |
| POST | `nadi-pariksha-admin/make-report-free` | CoachDashboardController@makeFreeAdminPayment | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:102` |
| GET | `nadi-pariksha-admin/marketing-leads` | CoachDashboardController@showMarketingLeads | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:105` |
| GET | `nadi-pariksha-admin/otp-list` | CoachDashboardController@showOtpListPage | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:107` |
| GET | `nadi-pariksha-admin/payment-management` | CoachDashboardController@paymentManagement | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:84` |
| GET | `nadi-pariksha-admin/renderNadiReportPdfForAdmin` | NadiParikshaController@renderNadiReportPdfBrowserShot | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:79` |
| GET | `nadi-pariksha-admin/report-price-management` | CoachDashboardController@reportPriceManagement | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:91` |
| GET | `nadi-pariksha-admin/reset-nadi-report` | NadiParikshaController@getNadiReport | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:80` |
| POST | `nadi-pariksha-admin/reset-profile` | CoachDashboardController@resetProfile | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:108` |
| POST | `nadi-pariksha-admin/switchAdminRole` | CoachDashboardController@switchAdminRole | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:116` |
| POST | `nadi-pariksha-admin/update-report-price` | CoachDashboardController@updateReportPrice | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:92` |
| POST | `nadi-pariksha-admin/updateAdminUserFeatures` | CoachDashboardController@updateAdminUserFeatures | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:119` |
| GET | `nadi-pariksha-admin/users-management` | CoachDashboardController@usersManagement | nadiPariksha.adminDashboardAuthentication |  | `routes/web.php:94` |
| GET | `nadi-pariksha-coach` | CoachDashboardController@index |  |  | `routes/web.php:59` |
| GET | `nadi-pariksha-coach-login` | CoachDashboardController@showLoginPage |  |  | `routes/web.php:62` |
| GET | `nadi-pariksha-coach/user-details/{id}` | CoachDashboardController@showUserDetails |  |  | `routes/web.php:60` |
| POST | `nadi-pariksha-login-validation` | CoachDashboardController@loginValidation |  |  | `routes/web.php:64` |
| GET | `nadi-report/pdf/{userId}` | NadiParikshaController@testrenderNadiReportPdf **shadowed** |  |  | `routes/web.php:25` |
| GET | `nadi-report/pdf/{userId}` | NadiParikshaController@testrenderNadiReportPdf |  |  | `routes/web.php:138` |
| POST | `nadi/baselineCalculation` | NadiReportController@baselineCalculation | api, auth.token |  | `routes/api.php:1255` |
| POST | `nadi/report` | NadiReportController@nadiReportDefinition | api, auth.token |  | `routes/api.php:1256` |
| POST | `nadi/reportInfo` | NadiReportController@nadiReportInfo | api, auth.token |  | `routes/api.php:1254` |
| POST | `nadiDataAnalysis` | MedicalReportSaveController@nadiDataAnalysis | api, auth.token |  | `routes/api.php:964` |
| GET | `nadiSwasthyaReport` | ReportsWebController@nadiSwasthyaReport |  |  | `routes/api.php:1543` |
| GET | `nadiTaranginiReport` | ReportsWebController@nadiNaranginiReport |  |  | `routes/api.php:1504` |
| GET | `nadiTaranginiReportV3` | ReportsWebController@nadiNaranginiReportV3 |  |  | `routes/api.php:1530` |
| POST | `nadi_pariksha/addDoctorsDetails` | NpAppVersionController@addDoctorsDetails |  |  | `routes/api.php:1775` |
| POST | `nadi_pariksha/addDoctorsDetailsFromAdminDash` | NpAppVersionController@addDoctorsDetailsFromAdminDash |  |  | `routes/api.php:1776` |
| GET | `nadi_pariksha/cohortManagement` | NpCohortManagement@cohortManagement | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1841` |
| POST | `nadi_pariksha/connectwithJiva` | NPUserController@connectwithJiva | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1830` |
| POST | `nadi_pariksha/createOrder` | NpPaymentControllerV2@createOrderV1 | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1872` |
| POST | `nadi_pariksha/createOrderV2` | NPPaymentController@createOrderV2 | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1875` |
| POST | `nadi_pariksha/firebase/sendToAllUsers` | NpFirebaseNotificationController@sendToAllUsers |  |  | `routes/api.php:1891` |
| POST | `nadi_pariksha/firebase/sendToMultipleTopics` | NpFirebaseNotificationController@sendToMultipleTopics |  |  | `routes/api.php:1895` |
| POST | `nadi_pariksha/firebase/sendToSingleTopic` | NpFirebaseNotificationController@sendToSingleTopic |  |  | `routes/api.php:1894` |
| POST | `nadi_pariksha/firebase/sendToSpecificUser` | NpFirebaseNotificationController@sendToSpecificUser |  |  | `routes/api.php:1890` |
| GET | `nadi_pariksha/firebase/topics` | NpFirebaseNotificationController@getTopics |  |  | `routes/api.php:1896` |
| GET | `nadi_pariksha/getAllDoctorsDetails` | NpAppVersionController@getAllDoctorsDetails | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1863` |
| GET | `nadi_pariksha/getAllUserDetailsForSheets` | NpPublicController@getAllUserDetailsForSheets |  |  | `routes/api.php:1780` |
| GET | `nadi_pariksha/getAllUserDetailsForSheetsSwasthyaData` | NpGoogleCronController@getAllUserDetailsForSheetsSwasthyaData |  |  | `routes/api.php:1781` |
| GET | `nadi_pariksha/getAppVersionDetails` | NpAppVersionController@getAppVersionDetails | NadiParikshaPublic |  | `routes/api.php:1809` |
| GET | `nadi_pariksha/getDoctorDetails` | NpAppVersionController@getDoctorDetails | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1864` |
| GET | `nadi_pariksha/getMasterContentBanner` | NPUserController@getMasterContentBanner | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1829` |
| GET | `nadi_pariksha/getNPPurchaseDetails` | NPPaymentController@getNPPurchaseDetails | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1868` |
| GET | `nadi_pariksha/getNPReportPricing` | NPPaymentController@getNPReportPricing | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1867` |
| GET | `nadi_pariksha/getNPUserInfoStatus` | NPUserController@getNPUserInfoStatus | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1825` |
| GET | `nadi_pariksha/getNPUserPersonalInfo` | NPUserController@getNPUserPersonalInfo | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1826` |
| GET | `nadi_pariksha/getNadiReport` | NadiParikshaController@getNadiReport | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1845` |
| GET | `nadi_pariksha/getNadiReportForCoach/{userId}` | CoachDashboardController@getNadiReportForCoach |  |  | `routes/api.php:1903` |
| GET | `nadi_pariksha/getNadiReportPdf` | NadiParikshaController@getNadiReportPdf | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1846` |
| GET | `nadi_pariksha/getNadiReportPdfBrowsershot` | NadiParikshaController@getNadiReportPdfBrowsershot | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1854` |
| GET | `nadi_pariksha/getNpDayFiveReminderUsers` | NpPublicController@getNpDayFiveReminderUsers | NadiParikshaPublic |  | `routes/api.php:1801` |
| GET | `nadi_pariksha/getNpDynamicUiJsonUrl` | NadiParikshaController@getNpDynamicUiJsonUrl | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1857` |
| GET | `nadi_pariksha/getNpHourlyReportUsers` | NpPublicController@getNpHourlyReportUsers | NadiParikshaPublic |  | `routes/api.php:1800` |
| GET | `nadi_pariksha/getPayments` | CoachDashboardController@getPayments |  |  | `routes/api.php:1907` |
| GET | `nadi_pariksha/getPrakritiDetails` | NadiParikshaController@getPrakritiDetails | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1821` |
| GET | `nadi_pariksha/getSurveyQuestions` | NpSurveyQuestionController@getSurveyQuestions | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1839` |
| GET | `nadi_pariksha/getUserAllDetailsForCoach` | CoachDashboardController@getUserAllDetailsForCoach |  |  | `routes/api.php:1901` |
| GET | `nadi_pariksha/getUserAllVisits` | NPUserController@getUserAllVisits | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1827` |
| GET | `nadi_pariksha/getUserPrakritiAnswers/{userId}` | CoachDashboardController@getUserPrakritiAnswersForCoach |  |  | `routes/api.php:1902` |
| GET | `nadi_pariksha/getUserSurveyAnswersWithQuestions/{userId}` | CoachDashboardController@getUserSurveyAnswersWithQuestions |  |  | `routes/api.php:1905` |
| GET | `nadi_pariksha/getVikrutiDetails` | NadiParikshaController@getVikrutiDetailsV2 | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1822` |
| GET | `nadi_pariksha/getVikrutiDetailsV2` | NadiParikshaController@getVikrutiDetailsV2 | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1823` |
| GET | `nadi_pariksha/getlanguages` | NadiParikshaController@getLanguages | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1817` |
| POST | `nadi_pariksha/jivaWebhook` | NpPublicController@jivaWebhook | NadiParikshaPublic |  | `routes/api.php:1802` |
| POST | `nadi_pariksha/nadiAnalysis` | NPnadiController@nadiAnalysis | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1833` |
| GET | `nadi_pariksha/nadiCaptureView` | NadiParikshaController@nadiCaptureView | NadiParikshaPublic |  | `routes/api.php:1804` |
| POST | `nadi_pariksha/nadiParikshaNadiAnalysis` | NadiParikshaController@nadiParikshaNadiAnalysis | NadiParikshaPublic |  | `routes/api.php:1806` |
| POST | `nadi_pariksha/nadiVisitParameters` | NPUserController@nadiVisitParameters | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1828` |
| POST | `nadi_pariksha/otp/send_otp` | NadiParikshaOTPSmsController@sendOtp | NadiParikshaPublic |  | `routes/api.php:1789` |
| POST | `nadi_pariksha/otp/verify_otp` | NadiParikshaOTPSmsController@verifyOtp | NadiParikshaPublic |  | `routes/api.php:1790` |
| GET | `nadi_pariksha/prakriti_questions` | NadiParikshaController@getQuestions | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1819` |
| GET | `nadi_pariksha/principles` | AyurvedaStaticController@getPrinciples | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1815` |
| POST | `nadi_pariksha/razorpayWebhookV1` | NpPaymentControllerV2@razorpayWebhookV1 | NadiParikshaPublic |  | `routes/api.php:1785` |
| GET | `nadi_pariksha/renderNadiReportPdf` | NadiParikshaController@renderNadiReportPdfBrowserShot | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1849` |
| POST | `nadi_pariksha/saveNPPayment` | NPPaymentController@savePayments | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1869` |
| POST | `nadi_pariksha/saveNotifyMe` | NPUserController@saveNotifyMe | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1836` |
| POST | `nadi_pariksha/savePrakrutiQuestions` | NadiParikshaController@savePrakrutiQuestions | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1820` |
| POST | `nadi_pariksha/saveSurveyAnswers` | NpSurveyQuestionController@saveSurveyAnswers | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1840` |
| POST | `nadi_pariksha/smsWebHook` | NpAppVersionController@smsWebHook |  |  | `routes/api.php:1778` |
| POST | `nadi_pariksha/storeUserActivity` | NPUserController@storeUserActivity | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1837` |
| GET | `nadi_pariksha/testrenderNadiReportPdf` | NadiParikshaController@renderNadiReportPdfBrowserShot **shadowed** | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1851` |
| GET | `nadi_pariksha/testrenderNadiReportPdf` | NadiParikshaController@renderNadiReportPdfBrowserShot | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1855` |
| POST | `nadi_pariksha/toggleNpInteraction` | NadiParikshaController@toggleNpInteraction | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1858` |
| POST | `nadi_pariksha/updateAppVersionDetails` | NpAppVersionController@updateAppVersionDetails | NadiParikshaPublic |  | `routes/api.php:1810` |
| POST | `nadi_pariksha/updateLanguage` | NadiParikshaController@updateLanguage | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1818` |
| POST | `nadi_pariksha/uploadNpDynamicUiJson` | NadiParikshaController@uploadNpDynamicUiJson | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1856` |
| POST | `nadi_pariksha/userProfileCreation` | NPUserController@userProfileCreation | NadiParikshaPublic |  | `routes/api.php:1787` |
| POST | `nadi_pariksha/v2/otp/send_otp` | NadiParikshaOTPSmsController@sendOtpV2 | NadiParikshaPublic |  | `routes/api.php:1795` |
| POST | `nadi_pariksha/v2/otp/verify_otp` | NadiParikshaOTPSmsController@verifyOtpV2 | NadiParikshaPublic |  | `routes/api.php:1796` |
| POST | `nadi_pariksha/validateCoupon` | NPPaymentController@validateCoupon | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1870` |
| POST | `nadi_pariksha/verifyPayment` | NpPaymentControllerV2@verifyPaymentV1 | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1873` |
| POST | `nadi_pariksha/verifyPaymentV2` | NPPaymentController@verifyPaymentV2 | NadiParikshaPublic, nadiPariksha.authentication |  | `routes/api.php:1876` |
| POST | `nadi_pariksha/weeklyJivaBookingsWebhook` | NPUserController@weeklyJivaBookingsWebhook |  |  | `routes/api.php:1779` |
| POST | `newReport` | SpaReportController@spaNewReport | api |  | `routes/api.php:758` |
| POST | `notification/addNewNotification` | NotificationController@addNewNotification | api, auth.token |  | `routes/api.php:1326` |
| POST | `notification/fetchAllNotificationTopicList` | NotificationController@fetchAllNotificationTopicList | api, auth.token |  | `routes/api.php:1334` |
| POST | `notification/fetchAllNotifications` | NotificationController@fetchAllNotifications | api, auth.token |  | `routes/api.php:1324` |
| POST | `notification/fetchSingleNotification` | NotificationController@fetchSingleNotification | api, auth.token |  | `routes/api.php:1328` |
| POST | `notification/fetchUserTopics` | NotificationController@fetchUserTopics | api, auth.token |  | `routes/api.php:1336` |
| POST | `notification/markAsReadNotification` | NotificationController@markAsReadNotification | api, auth.token |  | `routes/api.php:1325` |
| POST | `notification/markasUnreadNotification` | NotificationController@markasUnreadNotification | api, auth.token |  | `routes/api.php:1327` |
| POST | `notification/sendToSingleTopic` | NotificationController@sendToSingleTopic | api, auth.token |  | `routes/api.php:1332` |
| POST | `notification/sendToSingleUser` | NotificationController@sendToSingleUser | api, auth.token |  | `routes/api.php:1330` |
| POST | `nt-admin/access-management/addUser` | UserManagementController@addUser | api, auth.token |  | `routes/api.php:1364` |
| POST | `nt-admin/access-management/consultationTypeCounts` | UserManagementController@getConsultationTypeCounts | api, auth.token |  | `routes/api.php:1380` |
| POST | `nt-admin/access-management/editProfile` | UserManagementController@editProfile | api, auth.token |  | `routes/api.php:1374` |
| POST | `nt-admin/access-management/editUserProfile` | UserManagementController@editUserProfile | api, auth.token |  | `routes/api.php:1376` |
| POST | `nt-admin/access-management/features` | FeaturesController@getFeatures | api, auth.token |  | `routes/api.php:1361` |
| GET | `nt-admin/access-management/getActiveUserDetails` | UserManagementController@getActiveUserDetails | api, auth.token |  | `routes/api.php:1367` |
| GET | `nt-admin/access-management/getAllFeatureDetails` | FeaturesController@getAllFeatureDetails | api, auth.token |  | `routes/api.php:1360` |
| GET | `nt-admin/access-management/getAllRoles` | UserManagementController@getAllRoles | api, auth.token |  | `routes/api.php:1371` |
| GET | `nt-admin/access-management/getChildRole` | UserManagementController@getChildRole | api, auth.token |  | `routes/api.php:1372` |
| GET | `nt-admin/access-management/getCurrentUserDetails` | UserManagementController@getCurrentUserDetails | api, auth.token |  | `routes/api.php:1366` |
| POST | `nt-admin/access-management/getUserDetails` | UserManagementController@getUserDetails | api, auth.token |  | `routes/api.php:1368` |
| POST | `nt-admin/access-management/getUserWiseActiveClinicDetails` | UserManagementController@getUserWiseActiveClinicDetails | api, auth.token |  | `routes/api.php:1369` |
| POST | `nt-admin/access-management/getUsersByRole` | UserManagementController@getUsersByRole | api, auth.token |  | `routes/api.php:1378` |
| POST | `nt-admin/access-management/updateFeatures` | FeaturesController@updateUserWiseFeatures | api, auth.token |  | `routes/api.php:1362` |
| POST | `nt-admin/access-management/updateUserPassword` | UserManagementController@updateUserPassword | api, auth.token |  | `routes/api.php:1375` |
| POST | `nt-admin/access-management/updateUserStatus` | UserManagementController@updateUserStatus | api, auth.token |  | `routes/api.php:1365` |
| POST | `nt-admin/data-management/updateUserWiseDataAccess` | DataManagementController@updateUserWiseDataAccess | api, auth.token |  | `routes/api.php:1386` |
| POST | `nt-admin/data-management/userWiseDataAccess` | DataManagementController@getDataAccess | api, auth.token |  | `routes/api.php:1384` |
| POST | `nt-capture/analyze/report` | ExternalUserController@analyzeReport | api | external.analyze.report | `routes/api.php:848` |
| POST | `nt-capture/internal/generateReportWebViewUrl` | ExternalUserController@webViewReportUrlGenerate | api |  | `routes/api.php:824` |
| POST | `nt-capture/internal/getCredentials` | ExternalUserController@getInternalCredentials | api |  | `routes/api.php:816` |
| POST | `nt-capture/internal/getWebhookUrl` | ExternalUserController@getWebhookUrl | api |  | `routes/api.php:820` |
| POST | `nt-capture/internal/regenerateCredentials` | ExternalUserController@regenerateInternalCredentials | api |  | `routes/api.php:818` |
| POST | `nt-capture/internal/updateWebhookUrl` | ExternalUserController@updateWebhookUrl | api |  | `routes/api.php:822` |
| GET | `nt-capture/patient/getPatients` | ExternalUserController@getPatients | api | ntcapture.patient.get | `routes/api.php:831` |
| GET | `nt-capture/patient/{patient_code}/reports` | ExternalUserController@getPatientWiseReports | api | ntcapture.patient.reports | `routes/api.php:833` |
| GET | `nt-capture/report/nadi-guna/{visit_id}` | ExternalUserController@getNtReportData | api | ntcapture.report.nt.get | `routes/api.php:839` |
| GET | `nt-capture/report/swasthya-darshika/{visit_id}` | ExternalUserController@getSdReportData | api | ntcapture.report.sd.get | `routes/api.php:841` |
| GET | `nt-capture/report/{visit_id}` | ExternalUserController@getReportData | api | ntcapture.report.show | `routes/api.php:837` |
| POST | `nt-jiva/getLatestTongueData` | PatientDetailsController@getLatestTongueDataNtJiva | api |  | `routes/api.php:802` |
| POST | `nt-jiva/getTongueData` | PatientDetailsController@getTongueDataNtJiva | api |  | `routes/api.php:801` |
| POST | `nt-jiva/patientPreviousVisit` | PatientDetailsController@patientPreviousVisitNtJiva | api |  | `routes/api.php:800` |
| POST | `nt-jiva/send-otp` | OtpSmsController@sendOtpNtJiva | api |  | `routes/api.php:798` |
| POST | `nt-jiva/verify-otp` | OtpSmsController@verifyOtpNtJiva | api |  | `routes/api.php:799` |
| GET | `ntRecommendationReport` | ReportsWebController@ntRecommendationsReport |  |  | `routes/api.php:1525` |
| GET | `onePagerNadiTaranginiReport` | ReportsWebController@onePagerNadiTaranginiReport |  |  | `routes/api.php:1540` |
| POST | `org/analytics/getDashboardAnalysis` | orgAnalyticsController@getDashboardAnalysis | corporate.authentication |  | `routes/api.php:1589` |
| POST | `org/analytics/getFranchiseAnalytics` | orgAnalyticsController@getFranchiseAnalytics | corporate.authentication |  | `routes/api.php:1587` |
| POST | `org/expert/addNewPatientForCorporate` | orgPatientManagementController@addNewPatientForCorporate | corporate.authentication |  | `routes/api.php:1568` |
| POST | `org/expert/createExpert` | orgExpertsController@addOrgExpert | corporate.authentication |  | `routes/api.php:1562` |
| POST | `org/expert/deleteExperts` | orgExpertsController@deleteOrgExpert | corporate.authentication |  | `routes/api.php:1571` |
| POST | `org/expert/generateAddPatientUrl` | orgPatientManagementController@generateAddPatientUrl | corporate.authentication |  | `routes/api.php:1564` |
| POST | `org/expert/getExperts` | orgExpertsController@getAllExperts | corporate.authentication |  | `routes/api.php:1566` |
| POST | `org/expert/getFranchiseWiseDoctors` | orgExpertsController@getFranchiseWiseDoctors | corporate.authentication |  | `routes/api.php:1573` |
| POST | `org/franchise/addNewFranchise` | orgFranchiseController@addNewFranchise | corporate.authentication |  | `routes/api.php:1578` |
| POST | `org/franchise/getAllFranchises` | orgFranchiseController@getAllFranchises | corporate.authentication |  | `routes/api.php:1579` |
| POST | `org/franchise/getSingleFranchise` | orgFranchiseController@getSingleFranchise | corporate.authentication |  | `routes/api.php:1580` |
| POST | `org/franchise/updateNewFranchise` | orgFranchiseController@updateNewFranchise | corporate.authentication |  | `routes/api.php:1581` |
| POST | `org/getDetailsUsingAddPatientUrl` | orgPatientManagementController@getDetailsUsingAddPatientUrl |  |  | `routes/api.php:1556` |
| POST | `org/orgLogin` | orgAuthController@orgLogin |  |  | `routes/api.php:1555` |
| POST | `org/orgSignUp` | orgSignUpController@organizationSignUp |  |  | `routes/api.php:1551` |
| POST | `org/sendEmailOtp` | orgAuthController@sendEmailOtp |  |  | `routes/api.php:1553` |
| POST | `otp/send-email-otp` | OtpSmsController@sendEmailOtp | api |  | `routes/api.php:790` |
| POST | `otp/send-otp` | OtpSmsController@sendOtp | api |  | `routes/api.php:788` |
| POST | `otp/send-verification-otp` | OtpSmsController@sendVerificationOtp | api |  | `routes/api.php:793` |
| POST | `otp/verify-email-otp` | OtpSmsController@verifyEmailOtp | api |  | `routes/api.php:791` |
| POST | `otp/verify-otp` | OtpSmsController@verifyOtp | api |  | `routes/api.php:789` |
| POST | `otp/verify-verification-otp` | OtpSmsController@verifyVerificationOtp | api |  | `routes/api.php:794` |
| GET | `patanjaliReport` | ReportsWebController@patanjaliReport |  |  | `routes/api.php:1536` |
| POST | `patient/add-new-symptom` | PatientDetailsController@addNewSymptom | api, auth.token |  | `routes/api.php:1134` |
| POST | `patient/addAnonymousClient` | PatientDetailsController@addAnonymousClient | api, auth.token |  | `routes/api.php:1122` |
| POST | `patient/addClient` | PatientDetailsController@addNewClient | api, auth.token |  | `routes/api.php:1145` |
| POST | `patient/clinicDetails` | PatientDetailsController@loadClinic | api, auth.token |  | `routes/api.php:1136` |
| POST | `patient/deletePatient` | PatientDetailsController@deletePatient | api, auth.token |  | `routes/api.php:1120` |
| POST | `patient/deletePatientQuery` | PatientDetailsController@deletePatientQuery | api, auth.token |  | `routes/api.php:1140` |
| POST | `patient/deleteReport` | PatientDetailsController@deleteVisitReport | api, auth.token |  | `routes/api.php:1118` |
| POST | `patient/getBannerList` | PatientDetailsController@getBannerList | api, auth.token |  | `routes/api.php:1143` |
| POST | `patient/getClientDetails` | PatientDetailsController@getClientDetails | api, auth.token |  | `routes/api.php:1126` |
| POST | `patient/getTopicsList` | PatientDetailsController@getTopicsList | api, auth.token |  | `routes/api.php:1144` |
| POST | `patient/patientAppointmentInfo` | PatientDetailsController@patientAppointmentInfo | api, auth.token |  | `routes/api.php:1142` |
| POST | `patient/patientPreviousVisit` | PatientDetailsController@patientPreviousVisit | api, auth.token |  | `routes/api.php:1114` |
| POST | `patient/patientPreviousVisit-2` | PatientDetailsController@patientPreviousVisit2 | api, auth.token |  | `routes/api.php:1128` |
| POST | `patient/patientProgress` | PatientDetailsController@patientProgress | api, auth.token |  | `routes/api.php:1146` |
| POST | `patient/previousVisitsDetails` | PatientDetailsController@previousVisitsDetails | api, auth.token |  | `routes/api.php:1116` |
| POST | `patient/remainingFees` | PatientDetailsController@remainingFees | api, auth.token |  | `routes/api.php:1130` |
| POST | `patient/saveFees` | PatientDetailsController@saveFees | api, auth.token |  | `routes/api.php:1131` |
| POST | `patient/showPatientQueries` | PatientDetailsController@showPatientQueries | api, auth.token |  | `routes/api.php:1137` |
| POST | `patient/updateClient` | PatientDetailsController@updateClient | api, auth.token |  | `routes/api.php:1123` |
| POST | `patient/updatePatientQueries` | PatientDetailsController@updateQueries | api, auth.token |  | `routes/api.php:1138` |
| POST | `patientList` | PatientDetailsController@getPatientList | api, auth.token |  | `routes/api.php:926` |
| POST | `patientweeklydiet` | AllPrakrutiTypesController@getPatientWeekelyDiet | api, auth.token |  | `routes/api.php:993` |
| GET | `payment-invoices` | NtTransactionController@getPaymentInvoices | api, auth.token |  | `routes/api.php:1417` |
| GET | `pdf` | Closure |  |  | `routes/web.php:38` |
| POST | `planDetails` | LinkDeviceContoller@getPlanDetails | api, auth.token |  | `routes/api.php:1264` |
| GET | `planStatus` | NtTransactionController@getPlanStatus | api, auth.token |  | `routes/api.php:960` |
| POST | `postFetchNadiInfo` | ReportsWebController@postFetchNadiInfo |  |  | `routes/api.php:1527` |
| POST | `postPatanjaliReport` | ReportsWebController@postPatanjaliReport |  |  | `routes/api.php:1537` |
| POST | `prakruti/fetchPrakrutiQuestions` | PrakrutiController@fetchPrakrutiQuestions | api, auth.token |  | `routes/api.php:1227` |
| POST | `prakruti/fetchPrakrutiQuestionsNtLite` | PrakrutiController@fetchPrakrutiQuestionsNtLite | api, auth.token |  | `routes/api.php:1229` |
| POST | `prakruti/getAllPrakrutiTypes` | PrakrutiController@getAllPrakrutiTypes | api, auth.token |  | `routes/api.php:1235` |
| POST | `prakruti/saveManualPrakruti` | PrakrutiController@saveManualPrakruti | api, auth.token |  | `routes/api.php:1238` |
| POST | `prakruti/savePrakrutiQuestions` | PrakrutiController@savePrakrutiQuestions | api, auth.token |  | `routes/api.php:1232` |
| GET | `prescriptionReport` | ReportsWebController@prescriptionReport |  |  | `routes/api.php:1521` |
| GET | `profile` | AuthController@profile | api, auth.token |  | `routes/api.php:969` |
| POST | `profile-info/showUserInformation` | ProfileInfoController@showUserInformation | api, auth.token |  | `routes/api.php:1249` |
| PUT | `profile-info/updateUserInformation` | ProfileInfoController@updateUserInfo | api, auth.token |  | `routes/api.php:1250` |
| GET | `public/allRoles` | UserManagementController@allRoles | api |  | `routes/api.php:903` |
| GET | `rate-us` | NPUserController@redirect |  |  | `routes/api.php:1932` |
| POST | `reception-api/appointment/addAppointment` | AppointmentController@addAppointmentDoctor | reception.authentication |  | `routes/api.php:1741` |
| POST | `reception-api/appointment/dateWiseAppointment` | AppointmentController@dateWiseAppointment | reception.authentication |  | `routes/api.php:1754` |
| POST | `reception-api/appointment/dateWisePatientAppointment` | AppointmentController@dateWisePatientAppointment | reception.authentication |  | `routes/api.php:1756` |
| POST | `reception-api/appointment/deleteAppointment` | AppointmentController@deleteAppointment | reception.authentication |  | `routes/api.php:1744` |
| POST | `reception-api/appointment/fetchSingleAppointment` | AppointmentController@fetchSingleAppointmentData | reception.authentication |  | `routes/api.php:1750` |
| POST | `reception-api/appointment/getAllAppointment` | AppointmentController@getAllAppointment | reception.authentication |  | `routes/api.php:1738` |
| GET | `reception-api/appointment/getAppointmentHistory` | AppointmentController@getAppointmentHistory | reception.authentication |  | `routes/api.php:1752` |
| GET | `reception-api/appointment/getCurrentsAppointment` | AppointmentController@getCurrentsAppointment | reception.authentication |  | `routes/api.php:1758` |
| PUT | `reception-api/appointment/markAppointmentDone` | AppointmentController@markAppointmentDone | reception.authentication |  | `routes/api.php:1760` |
| POST | `reception-api/appointment/updateAppointment` | AppointmentController@updateAppointment | reception.authentication |  | `routes/api.php:1747` |
| POST | `reception-api/getLimitedActivePatients` | PatientDetailsController@getLimitedActivePatients | reception.authentication |  | `routes/api.php:1686` |
| POST | `reception-api/infinitePatientList` | PatientDetailsController@infinitePatientList | reception.authentication |  | `routes/api.php:1685` |
| POST | `reception-api/patient/addAnonymousClient` | PatientDetailsController@addAnonymousClient | reception.authentication |  | `routes/api.php:1692` |
| POST | `reception-api/patient/addClient` | PatientDetailsController@addNewClient | reception.authentication |  | `routes/api.php:1691` |
| POST | `reception-api/patient/fetchPatientNames` | PatientDetailsController@fetchPatientNames | reception.authentication |  | `routes/api.php:1695` |
| POST | `reception-api/patient/getClientDetails` | PatientDetailsController@getClientDetails | reception.authentication |  | `routes/api.php:1694` |
| POST | `reception-api/patient/updateClient` | PatientDetailsController@updateClient | reception.authentication |  | `routes/api.php:1693` |
| POST | `reception-api/patientList` | PatientDetailsController@getPatientList | reception.authentication |  | `routes/api.php:1684` |
| POST | `reception-api/prakruti/fetchPrakrutiQuestions` | PrakrutiController@fetchPrakrutiQuestions | reception.authentication |  | `routes/api.php:1700` |
| POST | `reception-api/prakruti/getAllPrakrutiTypes` | PrakrutiController@getAllPrakrutiTypes | reception.authentication |  | `routes/api.php:1706` |
| POST | `reception-api/prakruti/saveManualPrakruti` | PrakrutiController@saveManualPrakruti | reception.authentication |  | `routes/api.php:1709` |
| POST | `reception-api/prakruti/savePrakrutiQuestions` | PrakrutiController@savePrakrutiQuestions | reception.authentication |  | `routes/api.php:1703` |
| POST | `reception-api/report/fetchManualNadiKeywords` | MedicalReportSaveController@fetchManualNadiKeywords | reception.authentication |  | `routes/api.php:1725` |
| POST | `reception-api/report/fetchMarkOnImageUrl` | MedicalReportSaveController@fetchMarkOnImageUrl | reception.authentication |  | `routes/api.php:1727` |
| POST | `reception-api/report/fetchNewVisitCategoryWiseQuestions` | MedicalReportSaveController@fetchNewVisitCategoryWiseQuestions | reception.authentication |  | `routes/api.php:1719` |
| POST | `reception-api/report/fetchNewVisitInformation` | MedicalReportSaveController@newVisitInfoV2 | reception.authentication |  | `routes/api.php:1715` |
| POST | `reception-api/report/getNewMedicalId` | MedicalReportSaveController@getNewMedicalIdV2 | reception.authentication |  | `routes/api.php:1713` |
| POST | `reception-api/report/nadiDataAnalysis` | MedicalReportSaveController@nadiDataAnalysis | reception.authentication |  | `routes/api.php:1731` |
| POST | `reception-api/report/saveCategoryWiseVikrutiQuestions` | MedicalReportSaveController@saveCategoryWiseVikrutiQuestions | reception.authentication |  | `routes/api.php:1721` |
| POST | `reception-api/report/saveManualNadi` | MedicalReportSaveController@saveManualNadi | reception.authentication |  | `routes/api.php:1723` |
| POST | `reception-api/report/saveMarkOnImageUrl` | MedicalReportSaveController@saveMarkOnImageUrl | reception.authentication |  | `routes/api.php:1729` |
| POST | `reception-api/report/saveVikrutiQuestions` | MedicalReportSaveController@saveVikrutiQuestions | reception.authentication |  | `routes/api.php:1717` |
| POST | `reception-api/searchPatientUsingName` | PatientDetailsController@searchPatientUsingName | reception.authentication |  | `routes/api.php:1687` |
| POST | `reception/addReception` | ReceptionManagementController@addReception | api, auth.token |  | `routes/api.php:1394` |
| POST | `reception/editReception` | ReceptionManagementController@editReception | api, auth.token |  | `routes/api.php:1395` |
| POST | `reception/getReception` | ReceptionManagementController@getReception | api, auth.token |  | `routes/api.php:1396` |
| GET | `reception/manage/getReceptionFeatures` | ReceptionManagementController@getReceptionFeatures | api, auth.token |  | `routes/api.php:1402` |
| POST | `reception/manage/updateReceptionFeaturePermission` | ReceptionManagementController@updateReceptionFeaturePermission | api, auth.token |  | `routes/api.php:1404` |
| POST | `reception/manage/updateReceptionPermission` | ReceptionManagementController@updateReceptionPermission | api, auth.token |  | `routes/api.php:1400` |
| POST | `reception/markReceptionActiveOrInactive` | ReceptionManagementController@markReceptionActiveOrInactive | api, auth.token |  | `routes/api.php:1397` |
| POST | `report/addMedicineForPrescriptionNewV3` | MedicalReportSaveController@addMedicineForPrescriptionNewV3 | api, auth.token |  | `routes/api.php:1176` |
| POST | `report/deleteMedicineFromPrescriptionNewV3` | MedicalReportSaveController@deleteMedicineFromPrescriptionNewV3 | api, auth.token |  | `routes/api.php:1177` |
| POST | `report/deleteSinglePrescription` | MedicalReportSaveController@deleteSinglePrescription | api, auth.token |  | `routes/api.php:1188` |
| POST | `report/fetchManualNadiKeywords` | MedicalReportSaveController@fetchManualNadiKeywords | api, auth.token |  | `routes/api.php:1157` |
| POST | `report/fetchMarkOnImage` | MedicalReportSaveController@fetchMarkOnImage | api, auth.token |  | `routes/api.php:1170` |
| POST | `report/fetchMarkOnImageUrl` | MedicalReportSaveController@fetchMarkOnImageUrl | api, auth.token |  | `routes/api.php:1171` |
| POST | `report/fetchNewVisitInformation` | MedicalReportSaveController@newVisitInfo | api, auth.token |  | `routes/api.php:1192` |
| POST | `report/fetchSingleMedicinePrescription` | MedicalReportSaveController@fetchSingleMedicinePrescription | api, auth.token |  | `routes/api.php:1189` |
| POST | `report/generateWeeklyDiet` | MedicalReportSaveController@generateWeeklyDiet | api, auth.token |  | `routes/api.php:1210` |
| POST | `report/generateYogaPlanner` | MedicalReportSaveController@generateYogaPlanner | api, auth.token |  | `routes/api.php:1217` |
| POST | `report/getCurrentVisitInputForYogaPlanner` | MedicalReportSaveController@getInputForYogaPlanner | api, auth.token |  | `routes/api.php:1215` |
| POST | `report/getDietAndLifestyle` | MedicalReportSaveController@getDietAndLifestyle | api, auth.token |  | `routes/api.php:1196` |
| POST | `report/getLastPrescription` | MedicalReportSaveController@getLastPrescription | api, auth.token |  | `routes/api.php:1179` |
| POST | `report/getMedicineFromPrescriptionNewV3` | MedicalReportSaveController@getMedicineFromPrescriptionNewV3 | api, auth.token |  | `routes/api.php:1178` |
| POST | `report/getNewMedicalId` | MedicalReportSaveController@getNewMedicalId | api, auth.token |  | `routes/api.php:1154` |
| POST | `report/getPudiIngredient` | MedicalReportSaveController@getPudiIngredient | api, auth.token |  | `routes/api.php:1202` |
| POST | `report/getStrotas` | MedicalReportSaveController@getStrotas | api, auth.token |  | `routes/api.php:1201` |
| POST | `report/getTypeWiseFeatureDetails` | FeaturesController@getTypeWiseFeatureDetails | api, auth.token |  | `routes/api.php:1208` |
| POST | `report/getVikrutiWiseDietAndLifestyle` | MedicalReportSaveController@getVikrutiWiseDietAndLifestyle | api, auth.token |  | `routes/api.php:1198` |
| POST | `report/newVisitQues` | MedicalReportSaveController@saveNewVisitQues | api, auth.token |  | `routes/api.php:1193` |
| POST | `report/saveCategoryWiseVikrutiQuestions` | MedicalReportSaveController@saveCategoryWiseVikrutiQuestions | api, auth.token |  | `routes/api.php:1161` |
| POST | `report/saveDietAndLifestyle` | MedicalReportSaveController@saveDietAndLifestyle | api, auth.token |  | `routes/api.php:1195` |
| POST | `report/saveDietAndLifestyleManually` | MedicalReportSaveController@saveDietAndLifestyleMaually | api, auth.token |  | `routes/api.php:1199` |
| POST | `report/saveManualNadi` | MedicalReportSaveController@saveManualNadi | api, auth.token |  | `routes/api.php:1164` |
| POST | `report/saveMarkOnImage` | MedicalReportSaveController@saveMarkOnImage | api, auth.token |  | `routes/api.php:1167` |
| POST | `report/saveMarkOnImageUrl` | MedicalReportSaveController@saveMarkOnImageUrl | api, auth.token |  | `routes/api.php:1168` |
| POST | `report/savePrescriptionData` | MedicalReportSaveController@savePreScription | api, auth.token |  | `routes/api.php:1174` |
| POST | `report/savePrescriptionDataV2` | MedicalReportSaveController@savePrescriptionNew | api, auth.token |  | `routes/api.php:1175` |
| POST | `report/saveRecommendations` | MedicalReportSaveController@saveRecommendations | api, auth.token |  | `routes/api.php:1206` |
| POST | `report/saveSinglePrescription` | MedicalReportSaveController@saveSinglePrescription | api, auth.token |  | `routes/api.php:1182` |
| POST | `report/saveSinglePrescriptionV2` | MedicalReportSaveController@saveSinglePrescriptionV2 | api, auth.token |  | `routes/api.php:1183` |
| POST | `report/saveSinglePrescriptionV3` | MedicalReportSaveController@saveSinglePrescriptionV3 | api, auth.token |  | `routes/api.php:1184` |
| POST | `report/saveVikrutiQuestions` | MedicalReportSaveController@saveVikrutiQuestions | api, auth.token |  | `routes/api.php:1160` |
| POST | `report/updateSinglePrescription` | MedicalReportSaveController@updateSinglePrescription | api, auth.token |  | `routes/api.php:1186` |
| POST | `report/updateSinglePrescriptionV2` | MedicalReportSaveController@updateSinglePrescriptionV2 | api, auth.token |  | `routes/api.php:1187` |
| POST | `report/updateSinglePrescriptionV3` | MedicalReportSaveController@updateSinglePrescriptionV3 | api, auth.token |  | `routes/api.php:1185` |
| POST | `report/updateWeeklyDiet` | MedicalReportSaveController@updateWeeklyDiet | api, auth.token |  | `routes/api.php:1212` |
| POST | `report/updateYogaPlanner` | MedicalReportSaveController@updateYogaPlanner | api, auth.token |  | `routes/api.php:1219` |
| POST | `report/visitWiseAllowedReports` | MedicalReportSaveController@visitWiseAllowedReports | api, auth.token |  | `routes/api.php:1205` |
| POST | `reportManagement/customizeReportPages` | CustomizeDetailsController@updateUserReportPages | api, auth.token |  | `routes/api.php:1060` |
| POST | `reportManagement/customizeSingleUserReportPages` | CustomizeDetailsController@updateSingleUserWiseReportPages | api, auth.token |  | `routes/api.php:1061` |
| POST | `reportManagement/fetchSingleUserWiseReportPages` | CustomizeDetailsController@fetchSingleUserWiseReportPages | api, auth.token |  | `routes/api.php:1062` |
| POST | `reportManagement/getReportPages` | CustomizeDetailsController@getReportPages | api, auth.token |  | `routes/api.php:1058` |
| POST | `reportManagement/getReportWiseNoOfPages` | CustomizeDetailsController@getReportWiseNoOfPages | api, auth.token |  | `routes/api.php:1059` |
| GET | `research-dashboard-pulse-data` | ResearchDasbhoardController@pulseDashboardData |  | research.dashboard.pulse.data | `routes/web.php:30` |
| POST | `research-dashboard-pulse-data` | ResearchDasbhoardController@pulseDashboardData |  | research.dashboard.pulse.data | `routes/web.php:30` |
| GET | `research-dashboard-pulse-view` | ResearchDasbhoardController@vataDashboard |  | research.dashboard.pulse.view | `routes/web.php:28` |
| POST | `research-dashboard-pulse-view` | ResearchDasbhoardController@vataDashboard |  | research.dashboard.pulse.view | `routes/web.php:28` |
| POST | `research-dashboard/fetchTenSecondNadiData` | ResearchDasbhoardController@fetchTenSecondNadiData | api, auth.token |  | `routes/api.php:914` |
| POST | `research-dashboard/getLabelUsingMedicalId` | ResearchDasbhoardController@getLabelUsingMedicalId | api, auth.token |  | `routes/api.php:916` |
| POST | `research-dashboard/getNadiAnalysis2Data` | ResearchDasbhoardController@getNadiAnalysis2Data | api, auth.token |  | `routes/api.php:918` |
| GET | `research-dashboard/patientList` | ResearchDasbhoardController@patientList | api, auth.token |  | `routes/api.php:910` |
| POST | `research-dashboard/patientVisits` | ResearchDasbhoardController@patientVisits | api, auth.token |  | `routes/api.php:912` |
| GET | `research/dashboard-pulse-view` | ResearchDasbhoardController@vataDashboard |  |  | `routes/web.php:29` |
| POST | `research/dashboard-pulse-view` | ResearchDasbhoardController@vataDashboard |  |  | `routes/web.php:29` |
| POST | `researchDashboard/addAniruddhaRule` | AniruddhaRuleListController@addAniruddhaRule | research.authentication |  | `routes/api.php:604` |
| POST | `researchDashboard/addNewCategoryValue` | CategoryValueController@addNewCategoryValue | research.authentication |  | `routes/api.php:720` |
| POST | `researchDashboard/addNewCommonJson` | CommonJsonController@addNewCommonJson | research.authentication |  | `routes/api.php:631` |
| POST | `researchDashboard/addNewDayName` | DayNamesJsonController@addNewDayName | research.authentication |  | `routes/api.php:622` |
| POST | `researchDashboard/addNewExerciseCategory` | ExerciseCategoryController@addNewExerciseCategory | research.authentication |  | `routes/api.php:649` |
| POST | `researchDashboard/addNewExerciseTag` | ExerciseTagsController@addNewExerciseTag | research.authentication |  | `routes/api.php:701` |
| POST | `researchDashboard/addNewMealCategory` | MealsCategoryController@addNewMealCategory | research.authentication |  | `routes/api.php:614` |
| POST | `researchDashboard/addNewMusicLibraryData` | MusicLibraryController@addNewMusicLibraryData | research.authentication |  | `routes/api.php:710` |
| POST | `researchDashboard/addNewMusicTag` | MusicTagsController@addNewMusicTag | research.authentication |  | `routes/api.php:658` |
| POST | `researchDashboard/addNewRecipeCategory` | RecipeCategoryController@addNewRecipeCategory | research.authentication |  | `routes/api.php:677` |
| POST | `researchDashboard/addNewRecipePreference` | RecipePreferenceJsonController@addNewRecipePreference | research.authentication |  | `routes/api.php:640` |
| POST | `researchDashboard/addNewStateName` | StatesNamesController@addNewStateName | research.authentication |  | `routes/api.php:684` |
| POST | `researchDashboard/addNewYogaCategory` | YogaCategoryController@addNewYogaCategory | research.authentication |  | `routes/api.php:667` |
| POST | `researchDashboard/addNewYogaJsonData` | YogaJsonController@addNewYogaJsonData | research.authentication |  | `routes/api.php:693` |
| POST | `researchDashboard/addRule` | JsonArrayRuleListController@addRule | research.authentication |  | `routes/api.php:595` |
| POST | `researchDashboard/deleteAniruddhaRule` | AniruddhaRuleListController@deleteAniruddhaRule | research.authentication |  | `routes/api.php:603` |
| POST | `researchDashboard/deleteCategoryValue` | CategoryValueController@deleteCategoryValue | research.authentication |  | `routes/api.php:719` |
| POST | `researchDashboard/deleteCommonJson` | CommonJsonController@deleteCommonJson | research.authentication |  | `routes/api.php:630` |
| POST | `researchDashboard/deleteDayName` | DayNamesJsonController@deleteDayName | research.authentication |  | `routes/api.php:621` |
| POST | `researchDashboard/deleteExerciseCategory` | ExerciseCategoryController@deleteExerciseCategory | research.authentication |  | `routes/api.php:648` |
| POST | `researchDashboard/deleteExerciseTag` | ExerciseTagsController@deleteExerciseTag | research.authentication |  | `routes/api.php:702` |
| POST | `researchDashboard/deleteMealCategory` | MealsCategoryController@deleteMealCategory | research.authentication |  | `routes/api.php:612` |
| POST | `researchDashboard/deleteMusicLibraryData` | MusicLibraryController@deleteMusicLibraryData | research.authentication |  | `routes/api.php:709` |
| POST | `researchDashboard/deleteMusicTag` | MusicTagsController@deleteMusicTag | research.authentication |  | `routes/api.php:657` |
| POST | `researchDashboard/deleteRecipeCategory` | RecipeCategoryController@deleteRecipeCategory | research.authentication |  | `routes/api.php:676` |
| POST | `researchDashboard/deleteRecipePreference` | RecipePreferenceJsonController@deleteRecipePreference | research.authentication |  | `routes/api.php:639` |
| POST | `researchDashboard/deleteRule` | JsonArrayRuleListController@deleteRule | research.authentication |  | `routes/api.php:594` |
| POST | `researchDashboard/deleteStateName` | StatesNamesController@deleteStateName | research.authentication |  | `routes/api.php:686` |
| POST | `researchDashboard/deleteYogaCategory` | YogaCategoryController@deleteYogaCategory | research.authentication |  | `routes/api.php:666` |
| POST | `researchDashboard/deleteYogaJsonData` | YogaJsonController@deleteYogaJsonData | research.authentication |  | `routes/api.php:694` |
| POST | `researchDashboard/editAniruddhaRule` | AniruddhaRuleListController@editAniruddhaRule | research.authentication |  | `routes/api.php:605` |
| POST | `researchDashboard/editCategoryValue` | CategoryValueController@editCategoryValue | research.authentication |  | `routes/api.php:718` |
| POST | `researchDashboard/editCommonJson` | CommonJsonController@editCommonJson | research.authentication |  | `routes/api.php:632` |
| POST | `researchDashboard/editDayName` | DayNamesJsonController@editDayName | research.authentication |  | `routes/api.php:623` |
| POST | `researchDashboard/editExerciseCategory` | ExerciseCategoryController@editExerciseCategory | research.authentication |  | `routes/api.php:650` |
| POST | `researchDashboard/editMealCategory` | MealsCategoryController@editMealCategory | research.authentication |  | `routes/api.php:613` |
| POST | `researchDashboard/editMusicTag` | MusicTagsController@editMusicTag | research.authentication |  | `routes/api.php:659` |
| POST | `researchDashboard/editRecipePreference` | RecipePreferenceJsonController@editRecipePreference | research.authentication |  | `routes/api.php:641` |
| POST | `researchDashboard/editRule` | JsonArrayRuleListController@editRule | research.authentication |  | `routes/api.php:596` |
| POST | `researchDashboard/editStateName` | StatesNamesController@editStateName | research.authentication |  | `routes/api.php:685` |
| POST | `researchDashboard/editYogaCategory` | YogaCategoryController@editYogaCategory | research.authentication |  | `routes/api.php:668` |
| POST | `researchDashboard/getAllAniruddhaRules` | AniruddhaRuleListController@getAllAniruddhaRuleList | research.authentication |  | `routes/api.php:602` |
| POST | `researchDashboard/getAllCommonJsonData` | CommonJsonController@getAllCommonJsonData | research.authentication |  | `routes/api.php:629` |
| POST | `researchDashboard/getAllDayNames` | DayNamesJsonController@getAllDayNames | research.authentication |  | `routes/api.php:620` |
| POST | `researchDashboard/getAllExerciseCategory` | ExerciseCategoryController@getAllExerciseCategory | research.authentication |  | `routes/api.php:647` |
| POST | `researchDashboard/getAllExerciseTags` | ExerciseTagsController@getAllExerciseTags | research.authentication |  | `routes/api.php:699` |
| POST | `researchDashboard/getAllMealsCategory` | MealsCategoryController@getAllMealsCategory | research.authentication |  | `routes/api.php:611` |
| POST | `researchDashboard/getAllMusicData` | MusicLibraryController@getAllMusicData | research.authentication |  | `routes/api.php:707` |
| POST | `researchDashboard/getAllMusicTags` | MusicTagsController@getAllMusicTags | research.authentication |  | `routes/api.php:656` |
| POST | `researchDashboard/getAllRecipeCategory` | RecipeCategoryController@getAllRecipeCategory | research.authentication |  | `routes/api.php:674` |
| POST | `researchDashboard/getAllRecipePreferenceJsonData` | RecipePreferenceJsonController@getAllRecipePreferenceJsonData | research.authentication |  | `routes/api.php:638` |
| POST | `researchDashboard/getAllRules` | JsonArrayRuleListController@getAllRuleList | research.authentication |  | `routes/api.php:593` |
| POST | `researchDashboard/getAllStatesNames` | StatesNamesController@getAllStatesNames | research.authentication |  | `routes/api.php:683` |
| POST | `researchDashboard/getAllYogaCategory` | YogaCategoryController@getAllYogaCategory | research.authentication |  | `routes/api.php:665` |
| POST | `researchDashboard/getAllYogaData` | YogaJsonController@getAllYogaData | research.authentication |  | `routes/api.php:691` |
| POST | `researchDashboard/getAniruddhaRecipeTagging` | RecipeCategoryController@getAniruddhaRecipeTagging | research.authentication |  | `routes/api.php:678` |
| POST | `researchDashboard/getCategoryValueData` | CategoryValueController@getCategoryValueData | research.authentication |  | `routes/api.php:717` |
| POST | `researchDashboard/researchLogin` | AuthenticateController@researchLogin |  |  | `routes/api.php:587` |
| POST | `researchDashboard/updateExerciseData` | ExerciseTagsController@updateExerciseData | research.authentication |  | `routes/api.php:700` |
| POST | `researchDashboard/updateMusicData` | MusicLibraryController@updateMusicData | research.authentication |  | `routes/api.php:708` |
| POST | `researchDashboard/updateRecipeCategory` | RecipeCategoryController@updateRecipeCategory | research.authentication |  | `routes/api.php:675` |
| POST | `researchDashboard/updateYogaJsonData` | YogaJsonController@updateYogaJsonData | research.authentication |  | `routes/api.php:692` |
| GET | `rutucharyaReport` | ReportsWebController@aiGeneratedRutucharyaReport |  |  | `routes/api.php:1512` |
| POST | `sampleEncrypt` | S3BucketController@sampleEncrypt |  |  | `routes/api.php:732` |
| POST | `saveNadiKeywords` | CustomizeDetailsController@saveNadiKeywords | api, auth.token |  | `routes/api.php:1037` |
| POST | `searchPatientUsingName` | PatientDetailsController@searchPatientUsingName | api, auth.token |  | `routes/api.php:929` |
| POST | `selectManualNadiKeywords` | CustomizeDetailsController@selectManualNadiKeywords | api, auth.token |  | `routes/api.php:1032` |
| POST | `sendToMultipleTopics` | FirebaseController@sendToMultipleTopics |  |  | `routes/api.php:1502` |
| POST | `sendToSingleClient` | FirebaseController@sendToSingleClient |  |  | `routes/api.php:1498` |
| POST | `sendToSingleTopic` | FirebaseController@sendToSingleTopic |  |  | `routes/api.php:1500` |
| POST | `signup` | SignUpController@SignUp | api |  | `routes/api.php:741` |
| POST | `signupV2` | SignUpController@SignUpV2 | api |  | `routes/api.php:744` |
| GET | `spa` | Closure |  |  | `routes/web.php:43` |
| GET | `spaReport` | ReportsWebController@spaReport |  |  | `routes/api.php:1533` |
| POST | `storeDisallowedReports` | DoctorController@storeDisallowedReports | api, auth.token |  | `routes/api.php:981` |
| GET | `subscriptions/checkSubscriptionStatus` | SubscriptionController@checkSubscriptionStatus | api, auth.token |  | `routes/api.php:1346` |
| GET | `subscriptions/getAllTransactions` | SubscriptionController@getAllTransactions | api, auth.token |  | `routes/api.php:1345` |
| GET | `subscriptions/getEndPoints` | SubscriptionController@getEndPoints | api, auth.token |  | `routes/api.php:1341` |
| GET | `subscriptions/getPlans` | SubscriptionController@getAllPlans | api, auth.token |  | `routes/api.php:1340` |
| POST | `subscriptions/getReportWisePlans` | SubscriptionController@getReportWisePlans | api, auth.token |  | `routes/api.php:1348` |
| GET | `subscriptions/getUserPlan` | SubscriptionController@getUserPlan | api, auth.token |  | `routes/api.php:1344` |
| POST | `subscriptions/purchasePlan` | SubscriptionController@purchasePlan | api, auth.token |  | `routes/api.php:1343` |
| POST | `subscriptions/startTrial` | SubscriptionController@startTrial | api, auth.token |  | `routes/api.php:1342` |
| GET | `swasthyaDarshikaReport` | ReportsWebController@swasthyaDarshikaReportV2 |  |  | `routes/api.php:1544` |
| GET | `swasthyaDarshikaReportV2` | ReportsWebController@swasthyaDarshikaReportV2 |  |  | `routes/api.php:1546` |
| POST | `test-generate-invoice` | NtTransactionController@testGenerateInvoice | api, auth.token |  | `routes/api.php:1419` |
| POST | `testUploadS3` | S3BucketController@uploadToS3 |  |  | `routes/api.php:731` |
| POST | `turyaa` | getAllTuryaaController@index |  |  | `routes/api.php:422` |
| POST | `turyaa/addUserDataInSheet` | CoachController@addUserDataInSheet |  |  | `routes/api.php:432` |
| POST | `turyaa/addtongueJsonByID` | CoachController@addtongueJsonByID |  |  | `routes/api.php:433` |
| POST | `turyaa/coach/change-stage` | CoachController@changeStage | turyaa.authentication |  | `routes/api.php:483` |
| POST | `turyaa/coach/edit-wellness-report` | WellnessReportController@editWellnessReportData | turyaa.authentication |  | `routes/api.php:493` |
| POST | `turyaa/coach/get-all-diet-pdf` | WellnessReportController@getAllDietPdf | turyaa.authentication |  | `routes/api.php:489` |
| POST | `turyaa/coach/get-all-wellness-report` | WellnessReportController@getAllWellnessReportData | turyaa.authentication |  | `routes/api.php:487` |
| POST | `turyaa/coach/get-wellness-report-data` | WellnessReportController@getWellnessReportData | turyaa.authentication |  | `routes/api.php:485` |
| POST | `turyaa/coach/get-wellness-report-data-for-edit` | WellnessReportController@getWellnessReportDataForEdit | turyaa.authentication |  | `routes/api.php:492` |
| POST | `turyaa/coach/get-wellness-report-dataV2` | WellnessReportController@getWellnessReportDataV2 | turyaa.authentication |  | `routes/api.php:490` |
| POST | `turyaa/coach/getAllQuestionAnswerAndGoal` | CoachController@getAllQuestionAnswerAndGoal | turyaa.authentication |  | `routes/api.php:481` |
| POST | `turyaa/coach/getAnalysisData` | CoachController@getAnalysisData | turyaa.authentication |  | `routes/api.php:482` |
| POST | `turyaa/coach/progressTrackerofUser` | WellnessReportController@progressTrackerofUsers | turyaa.authentication |  | `routes/api.php:494` |
| POST | `turyaa/coach/save-wellness-report` | WellnessReportController@saveWellnessReportData | turyaa.authentication |  | `routes/api.php:486` |
| POST | `turyaa/coach/save-wellness-reportV2` | WellnessReportController@saveWellnessReportDataV2 | turyaa.authentication |  | `routes/api.php:491` |
| POST | `turyaa/coach/send-wellness-report-on-whatsapp` | WellnessReportController@sendTuryaaStageReport | turyaa.authentication |  | `routes/api.php:488` |
| GET | `turyaa/dailyProgressTracker` | DailyQuestionsController@dailyProgressTracker | turyaa.authentication |  | `routes/api.php:468` |
| POST | `turyaa/dislikeMeal` | DietManagementController@dislikeMeal | turyaa.authentication |  | `routes/api.php:446` |
| POST | `turyaa/editUser` | getAllTuryaaController@addUser |  |  | `routes/api.php:436` |
| POST | `turyaa/get-all-stages` | CoachController@getAllStages | turyaa.authentication |  | `routes/api.php:438` |
| POST | `turyaa/get-wellness-data` | WellnessController@getWellnessData | turyaa.authentication |  | `routes/api.php:472` |
| POST | `turyaa/get-wellness-dataV2` | WellnessController@getWellnessDataV2 | turyaa.authentication |  | `routes/api.php:476` |
| GET | `turyaa/getActivitiesStatus` | DailyQuestionsController@getActivitiesStatus | turyaa.authentication |  | `routes/api.php:467` |
| POST | `turyaa/getAllUserMobileNo` | getAllTuryaaController@getALLUserMobileNo |  |  | `routes/api.php:435` |
| GET | `turyaa/getDailyQuestions` | DailyQuestionsController@getDailyQuestions | turyaa.authentication |  | `routes/api.php:462` |
| GET | `turyaa/getDailyQuestionsV2` | DailyQuestionsController@getDailyQuestionsV2 | turyaa.authentication |  | `routes/api.php:463` |
| POST | `turyaa/getDemoVideoJson` | getAllTuryaaController@demoVideoJson |  |  | `routes/api.php:524` |
| GET | `turyaa/getFaqData` | FaqDataController@getFaqData |  |  | `routes/api.php:529` |
| GET | `turyaa/getGoalQuestion` | QuestionsController@getGoalQuestion | turyaa.authentication |  | `routes/api.php:454` |
| GET | `turyaa/getKnowledgeData` | KnowledgeDataController@getKnowledgeData |  |  | `routes/api.php:526` |
| GET | `turyaa/getPrakrutiQuestions` | getAllTuryaaController@getPrakrutiQuestions | turyaa.authentication |  | `routes/api.php:439` |
| GET | `turyaa/getQuestions` | QuestionsController@getAllQuestions | turyaa.authentication |  | `routes/api.php:450` |
| GET | `turyaa/getTongueAnalysisUrl` | NadiController@getTongueUrl | turyaa.authentication |  | `routes/api.php:460` |
| GET | `turyaa/getUserDetails` | getAllTuryaaController@getUserInfo | turyaa.authentication |  | `routes/api.php:442` |
| POST | `turyaa/getonBoardingNadiAnalysisData` | NadiController@onBoardingNadiAnalysisData | turyaa.authentication |  | `routes/api.php:516` |
| POST | `turyaa/likeMeal` | DietManagementController@likedMeal | turyaa.authentication |  | `routes/api.php:445` |
| POST | `turyaa/nadiAnalysis` | NadiController@nadiAnalysis | turyaa.authentication |  | `routes/api.php:457` |
| POST | `turyaa/onBoardingNadiAnalysis` | NadiController@onBoardingNadiAnalysis | turyaa.authentication |  | `routes/api.php:515` |
| POST | `turyaa/onBoardingNadiAnalysisWithoutData` | NadiController@onBoardingNadiAnalysisWithoutData | turyaa.authentication |  | `routes/api.php:518` |
| POST | `turyaa/otp/send-otp` | TuryaaOTPSmsController@sendOtp |  |  | `routes/api.php:426` |
| POST | `turyaa/otp/send-otpV2` | TuryaaOTPSmsController@sendOtpV2 |  |  | `routes/api.php:428` |
| POST | `turyaa/otp/verify-otp` | TuryaaOTPSmsController@verifyOtp |  |  | `routes/api.php:427` |
| POST | `turyaa/otp/verify-otpV2` | TuryaaOTPSmsController@verifyOtpV2 |  |  | `routes/api.php:429` |
| POST | `turyaa/removeDietChoice` | DietManagementController@removeDietChoice | turyaa.authentication |  | `routes/api.php:447` |
| POST | `turyaa/save-meal-image` | WellnessController@saveOrUpdatemealImage | turyaa.authentication |  | `routes/api.php:474` |
| POST | `turyaa/save-meal-imageV2` | WellnessController@saveOrUpdatemealImageV2 | turyaa.authentication |  | `routes/api.php:478` |
| POST | `turyaa/save-wellness-data` | WellnessController@saveOrUpdateWellnessData | turyaa.authentication |  | `routes/api.php:473` |
| POST | `turyaa/save-wellness-dataV2` | WellnessController@saveOrUpdateWellnessDataV2 | turyaa.authentication |  | `routes/api.php:477` |
| POST | `turyaa/saveDailyQuestions` | DailyQuestionsController@saveDailyQuestions | turyaa.authentication |  | `routes/api.php:464` |
| POST | `turyaa/saveDailyQuestionsV2` | DailyQuestionsController@saveDailyQuestionsV2 | turyaa.authentication |  | `routes/api.php:465` |
| POST | `turyaa/saveFaqData` | FaqDataController@saveFaqData | turyaa.authentication |  | `routes/api.php:520` |
| POST | `turyaa/saveImage` | getAllTuryaaController@saveImageToS3Bucket | turyaa.authentication |  | `routes/api.php:470` |
| POST | `turyaa/saveKnowledgeData` | KnowledgeDataController@saveKnowledgeData |  |  | `routes/api.php:527` |
| POST | `turyaa/savePrakrutiQuestions` | getAllTuryaaController@savePrakrutiQuestions | turyaa.authentication |  | `routes/api.php:440` |
| POST | `turyaa/saveQuestions` | QuestionsController@saveAllQuestions | turyaa.authentication |  | `routes/api.php:451` |
| POST | `turyaa/send-topic-notification` | FirebaseNotificationController@sendToTopic | turyaa.authentication |  | `routes/api.php:521` |
| POST | `turyaa/tongueCapture` | NadiController@tongueCapture | turyaa.authentication |  | `routes/api.php:458` |
| POST | `turyaa/tongueCaptureV2` | NadiController@tongueCaptureV2 | turyaa.authentication |  | `routes/api.php:459` |
| POST | `turyaa/turyaaDiet` | DietManagementController@turyaaDiet | turyaa.authentication |  | `routes/api.php:443` |
| POST | `turyaa/updateDiet` | DietManagementController@dislikeAndUpdateDiet | turyaa.authentication |  | `routes/api.php:444` |
| POST | `turyaa/updateGoal` | QuestionsController@updateGoal | turyaa.authentication |  | `routes/api.php:455` |
| POST | `turyaa/v2/editUserV2` | getAllTuryaaController@addUserV2 | turyaa.authentication |  | `routes/api.php:499` |
| POST | `turyaa/v2/getCategoryQuestions` | QuestionsController@getCategoryQuestions | turyaa.authentication |  | `routes/api.php:502` |
| GET | `turyaa/v2/getQuestions` | QuestionsController@getAllQuestionsV2 | turyaa.authentication |  | `routes/api.php:506` |
| POST | `turyaa/v2/getUserInfo` | getAllTuryaaController@getUserInfoV2 | turyaa.authentication |  | `routes/api.php:504` |
| POST | `turyaa/v2/getUserPersonalInfo` | getAllTuryaaController@getUserPersonalInfo | turyaa.authentication |  | `routes/api.php:500` |
| POST | `turyaa/v2/getVikrutiFeedbackQuestions` | QuestionsController@getVikrutiFeedbackQuestions | turyaa.authentication |  | `routes/api.php:512` |
| POST | `turyaa/v2/getWomenQuestions` | QuestionsController@getWomenQuestions | turyaa.authentication |  | `routes/api.php:509` |
| POST | `turyaa/v2/saveCategoryQuestions` | QuestionsController@saveCategoryQuestions | turyaa.authentication |  | `routes/api.php:511` |
| POST | `turyaa/v2/saveNadiAnalysisFeedback` | NadiController@saveNadiAnalysisFeedback | turyaa.authentication |  | `routes/api.php:513` |
| POST | `turyaa/v2/saveQuestions` | QuestionsController@saveAllQuestionsV2 | turyaa.authentication |  | `routes/api.php:507` |
| POST | `turyaa/v2/updateGoal` | QuestionsController@updateGoalV2 | turyaa.authentication |  | `routes/api.php:503` |
| POST | `turyaa/validateEmail` | getAllTuryaaController@checkEmail |  |  | `routes/api.php:525` |
| POST | `updateApplicationLanguages` | DoctorController@updateApplicationLanguages | api |  | `routes/api.php:785` |
| POST | `updateClinic` | ClinicController@updateClinicInfo | api, auth.token |  | `routes/api.php:1014` |
| POST | `updateFormDetails` | CustomizeDetailsController@updateFormDetails | api, auth.token |  | `routes/api.php:1036` |
| POST | `updateLanguageJson` | PublicFunctionsController@uploadNTFrontendAppLanguageJson | api |  | `routes/api.php:773` |
| POST | `updateReorder` | CustomizeDetailsController@updateReorder | api, auth.token |  | `routes/api.php:1027` |
| POST | `updateUpiDetails` | DoctorController@updateUpiDetails | api, auth.token |  | `routes/api.php:984` |
| POST | `updateWelcomeTour` | DoctorController@updateWelcomeTour | api, auth.token |  | `routes/api.php:1004` |
| POST | `updateYogaPlannerPublic` | MedicalReportSaveController@updateYogaPlannerPublic | api |  | `routes/api.php:779` |
| POST | `updatepassword` | UpdatePasswordController@updatePassword | api, auth.token |  | `routes/api.php:975` |
| GET | `user` | Closure | auth:sanctum |  | `routes/api.php:1492` |
| GET | `userAllowedReports` | DoctorController@userAllowedReports | api, auth.token |  | `routes/api.php:990` |
| POST | `v1/analyzeNadi` | NadiAnalysisController@computeNadiPublic |  |  | `routes/api.php:141` |
| POST | `v1/diet/computeDiet` | DietAndRecipesManagementController@computeDiet | auth.token |  | `routes/api.php:1615` |
| POST | `v1/diet/computeIngredients` | DietAndRecipesManagementController@computeIngredients | auth.token |  | `routes/api.php:1614` |
| POST | `v1/diet/computeRecipes` | DietAndRecipesManagementController@computeRecipes | auth.token |  | `routes/api.php:1616` |
| GET | `v1/getAllPrakrutiTypes` | prakrutiManagementController@getAllPrakrutiTypes | auth.token |  | `routes/api.php:1626` |
| POST | `v1/nadiDataAnalysis` | NadiAnalysisController@nadiAnalysis | auth.token |  | `routes/api.php:1625` |
| POST | `v1/prakruti/computePrakruti` | prakrutiManagementController@computePrakruti | auth.token |  | `routes/api.php:1602` |
| POST | `v1/prakruti/computePredefinedQuestionsBasedPrakruti` | prakrutiManagementController@computePredefinedQuestionsBasedPrakruti | auth.token |  | `routes/api.php:1606` |
| GET | `v1/prakruti/getPrakrutiQuestions` | prakrutiManagementController@getPrakrutiQuestions | auth.token |  | `routes/api.php:1605` |
| POST | `v1/reports/computeAarogyaDarshika` | NadiAnalysisController@computeAarogyaDarshika | auth.token |  | `routes/api.php:1620` |
| POST | `v1/reports/computeSpaReport` | NadiAnalysisController@computeSpaReport | auth.token |  | `routes/api.php:1621` |
| POST | `v1/reports/computeYogaReport` | NadiAnalysisController@computeYogaReport | auth.token |  | `routes/api.php:1622` |
| POST | `v1/vikruti/computeNadi` | NadiAnalysisController@computeNadi | auth.token |  | `routes/api.php:1610` |
| GET | `v2/client/getClientDetails` | AuthController@getClientDetails | client.authentication |  | `routes/api.php:1674` |
| POST | `v2/editProfile` | DoctorController@editProfileVersionTwo | auth.token |  | `routes/api.php:1642` |
| GET | `v2/getDoctorData` | AuthController@getDoctorData | auth.token |  | `routes/api.php:1641` |
| GET | `v2/getSeasonalTips` | PublicFunctionsController@getSeasonalTips |  |  | `routes/api.php:1637` |
| POST | `v2/loginValidation` | AuthController@loginValidation |  |  | `routes/api.php:1639` |
| POST | `v2/patient/patientPreviousVisit` | PatientDetailsController@patientPreviousVisitV2 | auth.token |  | `routes/api.php:1647` |
| POST | `v2/report/fetchNewVisitCategoryWiseQuestions` | MedicalReportSaveController@fetchNewVisitCategoryWiseQuestions | auth.token |  | `routes/api.php:1665` |
| POST | `v2/report/fetchNewVisitInformation` | MedicalReportSaveController@newVisitInfoV2 | auth.token |  | `routes/api.php:1653` |
| POST | `v2/report/getCurrentVisitInfo` | MedicalReportSaveController@getCurrentVisitInfo | auth.token |  | `routes/api.php:1659` |
| POST | `v2/report/getCurrentVisitInputForDiet` | MedicalReportSaveController@getCurrentVisitInputForDiet | auth.token |  | `routes/api.php:1657` |
| POST | `v2/report/getLastVisitInformation` | MedicalReportSaveController@getLastVisitInformation | auth.token |  | `routes/api.php:1661` |
| POST | `v2/report/getLastVisitMandatoryQuesitons` | MedicalReportSaveController@getLastVisitMandatoryQuesitons | auth.token |  | `routes/api.php:1663` |
| POST | `v2/report/getNewMedicalId` | MedicalReportSaveController@getNewMedicalIdV2 | auth.token |  | `routes/api.php:1651` |
| POST | `v2/report/getVikrutiWiseDietAndLifestyle` | MedicalReportSaveController@getVikrutiWiseDietAndLifestyleV2 | auth.token |  | `routes/api.php:1654` |
| POST | `v2/report/saveDietAndLifestyleManually` | MedicalReportSaveController@saveDietAndLifestyleMauallyV2 | auth.token |  | `routes/api.php:1655` |
| POST | `v2/signup` | SignUpController@SignUpV2 |  |  | `routes/api.php:1636` |
| POST | `v2/updateReportLanguage` | DoctorController@updateReportLanguage | auth.token |  | `routes/api.php:1644` |
| POST | `validateCorporateCode` | AuthController@corporateCode | api, auth.token |  | `routes/api.php:972` |
| POST | `validateDeviceWithSerialNo` | LinkDeviceContoller@validateDeviceWithSerialNo | api |  | `routes/api.php:746` |
| POST | `verifyTransaction` | NtTransactionController@verifyTransaction | api, auth.token |  | `routes/api.php:1416` |
| GET | `web-nadi-report/pdf/{userId}` | NadiParikshaController@testViewNadiReport **shadowed** |  |  | `routes/web.php:26` |
| GET | `web-nadi-report/pdf/{userId}` | NadiParikshaController@testViewNadiReport |  |  | `routes/web.php:139` |
| POST | `webhook/razorpay/nadi` | NtTransactionController@razorpayWebhook |  |  | `routes/api.php:1934` |
| GET | `weeklyDietReport` | ReportsWebController@weeklyDietReport |  |  | `routes/api.php:1510` |
| GET | `welcome-tour` | WelcomeTourController@getTourSteps | api, auth.token |  | `routes/api.php:1005` |
| POST | `welcome-tour/complete` | WelcomeTourController@completeTour | api, auth.token |  | `routes/api.php:1006` |
| GET | `yoga` | Closure |  |  | `routes/web.php:48` |
| GET | `yogaPlannerReport` | ReportsWebController@aiGeneratedyogaPlannerReport |  |  | `routes/api.php:1514` |
| GET | `yogaReport` | ReportsWebController@yogaReport |  |  | `routes/api.php:1535` |
| POST | `zipFileNadiAnalysis` | MedicalReportSaveController@zipFileNadiAnalysis | api, auth.token |  | `routes/api.php:966` |

## Unparsed

None.
