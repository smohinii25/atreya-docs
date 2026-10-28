# Fact pack: auth (Authentication & sign-up)

Generated 2026-10-27 by scripts/module-facts.sh. Product nt, critical false. Every line below is from code or a human-owned doc; cite the source given.

Commits: Ashoka-World-Backend `8dfbb37db7d71a400b3656bd50fbed6173908a24`, Nadi-Tarangini-App `0b7deec6de2b0b8b4f05eab4be8c8430523829bf`, Nadi-Tarangini-Frontend `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d`

## Backend routes (25)

### POST checkMobileNumber
- controller: CheckUserExistOrNotController@checkMobileNumberV2 (found) · route: `Ashoka-World-Backend:routes/api.php:763` · middleware: api
- called by: Nadi-Tarangini-Frontend NewSignUpController@checkDoctorMobileNo; Nadi-Tarangini-Frontend NtLiteSignUpController@checkMobileNo
- errors: 400 "Phone number is required" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:229`); 400 "Phone number must be numeric" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:236`); 400 "Country code field is required if phone number is provided" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:243`); 400 "Invalid country code" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:251`); 400 "Invalid country code" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:264`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:282`); 400 "Invalid phone number length. The required length is " (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:298`); 400 "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:301`)

### POST checkUsername
- controller: CheckUserExistOrNotController@checkUsername (found) · route: `Ashoka-World-Backend:routes/api.php:764` · middleware: api
- called by: Nadi-Tarangini-Frontend NewSignUpController@checkDoctorUsername; Nadi-Tarangini-Frontend NtLiteSignUpController@checkUsername
- errors: 400 "User name is required" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:182`); 400 "User already exists with the same username. Please try with another username" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:195`); ? "Valid username" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:201`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:209`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:215`)

### GET checkusernameormobileno
- controller: CheckUserExistOrNotController@checkMobileNumberOrEmail (found) · route: `Ashoka-World-Backend:routes/api.php:1426` · middleware: api
- called by: no screen in this workspace
- errors: 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:70`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:76`)

### POST editFcmToken
- controller: AuthController@updateFcmToken (found) · route: `Ashoka-World-Backend:routes/api.php:971` · middleware: api, auth.token
- called by: Nadi-Tarangini-App updateFCMtokenAshoka (LoginWithOtpScreen, LoginWithUsernameScreen); Nadi-Tarangini-Frontend loginController@editFcmToken
- errors: 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1874`)

### POST forgotPassword
- controller: AuthController@getForgotPassword (found) · route: `Ashoka-World-Backend:routes/api.php:777` · middleware: api
- called by: Nadi-Tarangini-App forgotPassword (ForgotPasswordScreen); Nadi-Tarangini-Frontend forgotPasswordController@checkForgotPassword (auth.forgot_password)
- validation: `user_name`: required|string (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1652`)
- errors: 404 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1679`); 422 "Password not updated" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1696`); ? "Forgot password successfully. Password sent to whatsapp/email" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1751`); ? "Forgot password successfully. Password sent to email but not on whatsapp" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1762`); ? "Forgot password successfully. Password sent to whatsapp but not on email" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1773`); ? "No contact information found. Please contact customer care." (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1784`); ? "No contact information found. Please contact customer care." (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1795`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:1806`)

### GET getCurrencyType
- controller: SignUpController@getCurrencyType (found) · route: `Ashoka-World-Backend:routes/api.php:760` · middleware: api
- called by: no screen in this workspace
- errors: ? "Get currency types" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1130`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1151`)

### POST getCurrencyType
- controller: SignUpController@getCurrencyType (found) · route: `Ashoka-World-Backend:routes/api.php:760` · middleware: api
- called by: Nadi-Tarangini-App fetchCurrencyType (EditDoctorAccount, KycScreen)
- errors: ? "Get currency types" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1130`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1151`)

### GET getSalutationTypes
- controller: SignUpController@salutationTypes (found) · route: `Ashoka-World-Backend:routes/api.php:759` · middleware: api
- called by: no screen in this workspace
- errors: ? "Get salutation types" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1353`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1373`)

### POST getSalutationTypes
- controller: SignUpController@salutationTypes (found) · route: `Ashoka-World-Backend:routes/api.php:759` · middleware: api
- called by: Nadi-Tarangini-App fetchSalutationTypes (SignUpScreen); Nadi-Tarangini-Frontend AdminDashboardController@createUser (admin.create_user); Nadi-Tarangini-Frontend DashboardController@addSelfAdmin (add_self_admin); Nadi-Tarangini-Frontend DashboardController@updateKycDetails (my_account.update_kyc); Nadi-Tarangini-Frontend EditDoctorDetailsController@editDoctorDetails (my_account.myaccount); Nadi-Tarangini-Frontend EditDoctorDetailsController@editDoctorProfile (my_account.edit_profile); Nadi-Tarangini-Frontend NewSignUpController@doctorSignUp (auth.signup)
- errors: ? "Get salutation types" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1353`); 500 "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1373`)

### GET getdetailsbymobileno
- controller: CheckUserExistOrNotController@getDetailsByMobileNo (found) · route: `Ashoka-World-Backend:routes/api.php:1427` · middleware: api
- called by: no screen in this workspace
- errors: ? "Please provide valid phone number" (`Ashoka-World-Backend:app/Http/Controllers/CheckUserExistOrNotController.php:146`)

### POST login
- controller: AuthController@login (found) · route: `Ashoka-World-Backend:routes/api.php:737` · middleware: api
- called by: no screen in this workspace
- validation: `user_name`: required|string (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:50`); `password`: required|string (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:51`)
- errors: 400 "Both username and password are required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:63`); ? "Username is required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:73`); ? "Password is required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:86`); ? "Both username and password are required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:97`); 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:110`); 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:114`); 401 "User has been blocked" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:118`); 401 "Invalid password" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:122`)

### POST loginOtpBasedUser
- controller: AuthController@loginOtpBasedUser (found) · route: `Ashoka-World-Backend:routes/api.php:739` · middleware: api
- called by: Nadi-Tarangini-App loginOtpBasedUser (LoginWithOtpScreen, LoginWithUsernameScreen, SplashScreen); Nadi-Tarangini-Frontend DashboardController@switchToAdmin; Nadi-Tarangini-Frontend DashboardController@switchToDoctor (admin.admin_dashboard, admin.all_report_view, admin.create_user, admin.data_management); Nadi-Tarangini-Frontend DashboardController@updateKycDetails (my_account.update_kyc); Nadi-Tarangini-Frontend loginController@checkLoginCredentials (auth.login); Nadi-Tarangini-Frontend loginController@getUserDetailsOtpBasedLogin (auth.login)
- errors: 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:806`); 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:810`); 401 "User has been blocked" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:814`); 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:894`); 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:906`); 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:913`); 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:921`); 401 "User has been blocked" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:983`)

### POST logout
- controller: AuthController@logout (found) · route: `Ashoka-World-Backend:routes/api.php:968` · middleware: api, auth.token
- called by: no screen in this workspace

### POST otp/send-email-otp
- controller: OtpSmsController@sendEmailOtp (found) · route: `Ashoka-World-Backend:routes/api.php:790` · middleware: api
- called by: Nadi-Tarangini-App sendEmailOtp (LoginWithOtpScreen); Nadi-Tarangini-Frontend loginController@sendEmailLoginOtp (auth.login)
- errors: 400 "Email is required" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:359`); 400 "Email not registered" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:373`); 200 "OTP sent successfully" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:384`); 200 "OTP sent successfully" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:415`); 500 "OTP not sent. Please check the email" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:420`)

### POST otp/send-otp
- controller: OtpSmsController@sendOtp (found) · route: `Ashoka-World-Backend:routes/api.php:788` · middleware: api
- called by: Nadi-Tarangini-App sendMobileOtp (LoginWithOtpScreen); Nadi-Tarangini-Frontend loginController@sendWhatsappLoginOtp (auth.login)
- errors: 400 "Invalid phone number length" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:54`); 400 "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:57`); 400 "Phone number not registered" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:71`); 200 "OTP sent successfully" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:82`); 200 "OTP sent successfully" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:92`); 500 "OTP not sent. Please check the phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:94`)

### POST otp/send-verification-otp
- controller: OtpSmsController@sendVerificationOtp (found) · route: `Ashoka-World-Backend:routes/api.php:793` · middleware: api
- called by: Nadi-Tarangini-App sendVerificationOtp (AddClinicScreen, EditClinicScreen, EditDoctorAccount, KycScreen); Nadi-Tarangini-Frontend OtpVerificationController@sendVerificationOtpsignup (admin.create_user, admin.edit_profile, auth.admin_signUp, auth.college_signUp)
- validation: `type`: required|string|in:email,mobile (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:479`); `action`: required|string|in:signup,profile_edit,kyc_update,add_clinic,update_clinic,admin_add_user,admin_update_user (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:480`); `email`: required_if:type,email|nullable|email (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:481`); `country_code`: required_if:type,mobile|nullable|string (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:482`); `mobile_no`: required_if:type,mobile|nullable|numeric (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:483`)
- errors: ? "OTP sent successfully via {$type} for {$action}." (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:500`); 500 "Failed to send OTP via email." (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:564`); 400 "Invalid phone number length" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:597`); 400 "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:600`); 500 "OTP not sent. Please check the phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:606`); ? "OTP sent successfully via {$type} for {$action}." (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:617`)

### POST otp/verify-email-otp
- controller: OtpSmsController@verifyEmailOtp (found) · route: `Ashoka-World-Backend:routes/api.php:791` · middleware: api
- called by: Nadi-Tarangini-App verifyEmailOtp (LoginWithOtpScreen); Nadi-Tarangini-Frontend loginController@verifyEmailLoginOtp (auth.login)
- errors: 400 "Email is required" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:433`); 400 "OTP is required" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:436`); 400 "Expired OTP" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:439`); 200 "OTP verified successfully" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:452`); 400 "Invalid OTP" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:457`)

### POST otp/verify-otp
- controller: OtpSmsController@verifyOtp (found) · route: `Ashoka-World-Backend:routes/api.php:789` · middleware: api
- called by: Nadi-Tarangini-App verifyMobileOtp (LoginWithOtpScreen); Nadi-Tarangini-Frontend loginController@verifyWhatsappLoginOtp (auth.login)
- errors: 400 "Invalid phone number length" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:120`); 400 "The provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:123`); 400 "Invalid OTP" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:127`); 400 "Expired OTP" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:136`); ? "OTP verified successfully" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:188`); 200 "OTP verified successfully" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:197`); 400 "Invalid OTP" (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:199`)

### POST otp/verify-verification-otp
- controller: OtpSmsController@verifyVerificationOtp (found) · route: `Ashoka-World-Backend:routes/api.php:794` · middleware: api
- called by: Nadi-Tarangini-App verifyVerificationOtp; Nadi-Tarangini-Frontend OtpVerificationController@verifyVerificationOtpsignup (admin.create_user, admin.edit_profile, auth.admin_signUp, auth.college_signUp)
- validation: `type`: required|string|in:email,mobile (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:628`); `action`: required|string|in:signup,profile_edit,kyc_update,add_clinic,update_clinic,admin_add_user,admin_update_user (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:629`); `otp`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:630`); `email`: required_if:type,email|nullable|email (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:631`); `country_code`: required_if:type,mobile|nullable|string (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:632`); `mobile_no`: required_if:type,mobile|nullable|numeric (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:633`)
- errors: 422 "The code is invalid or has expired. Please try again." (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:656`); ? "OTP verified successfully." (`Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:666`)

### POST signup
- controller: SignUpController@SignUp (found) · route: `Ashoka-World-Backend:routes/api.php:741` · middleware: api
- called by: no screen in this workspace
- validation: `salutation_type`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:48`); `user_name`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:49`); `password`: required|regex:/[0-9]/ (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:50`); `lastname`: required|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:51`); `middlename`: nullable|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:52`); `email`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:53`); `firstname`: required|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:54`); `gender`: required|in:M,F,D,N (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:55`); `dateofbirth`: required|date_format:Y-m-d (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:56`); `mobile_no`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:57`); `experience`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:58`); `profile_picture`: nullable|image|mimes:jpeg,png,jpg (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:59`); `clinic_logo`: nullable|image|mimes:jpeg,png,jpg (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:60`); `clinic_name`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:61`); `street`: nullable (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:63`); `landmark`: nullable (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:64`); `city`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:65`); `state`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:66`); `country`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:67`); `pincode`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:68`); `clinic_phone_no`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:69`); `currency_type`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:74`); `visit_days`: nullable (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:75`); `id_number`: nullable (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:76`); `id_type`: nullable (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:77`); `maritalstatus`: nullable (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:78`); `profile_picture`: nullable|image|mimes:jpeg,png,jpg (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:79`)
- errors: ? "Provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:85`); ? "Provided clinic country code is not valid for the given clinic number" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:107`); ? "Clinic country code field is required when clinic phone no is present" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:158`); ? "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:202`); 400 "User must be at least 18 years old" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:220`); 400 "User must be younger than 100 years old" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:226`); 400 "Phone number already exists" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:238`); 400 "Invalid salutation type" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:245`)

### POST signupV2
- controller: SignUpController@SignUpV2 (found) · route: `Ashoka-World-Backend:routes/api.php:744` · middleware: api
- called by: Nadi-Tarangini-App signUp (SignUpScreen)
- validation: `salutation_type`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:706`); `user_name`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:707`); `password`: required|regex:/[0-9]/ (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:708`); `lastname`: required|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:709`); `email`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:710`); `firstname`: required|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:711`); `gender`: required|in:M,F,D,N (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:712`); `mobile_no`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:713`); `profession_type_id`: nullable|numeric (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:714`); `ayush_no`: nullable|string (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:715`); `clinic_name`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:716`); `state`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:719`); `country`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:720`)
- errors: ? "Provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:727`); ? "Clinic name is required" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:766`); ? "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:802`); 400 "Phone number already exists" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:825`); 400 "Invalid salutation type" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:832`); 400 "Please select a valid gender" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:838`); 400 "Please select a valid gender" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:842`); 400 "Please select a valid gender" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:847`)

### POST updatepassword
- controller: UpdatePasswordController@updatePassword (found) · route: `Ashoka-World-Backend:routes/api.php:975` · middleware: api, auth.token
- called by: Nadi-Tarangini-App updatePassword (MyAccountScreen); Nadi-Tarangini-Frontend ChangePasswordController@updatePassword (my_account.myaccount)
- validation: `current_password`: required (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:16`)
- errors: ? "New password must contain at least one digit." (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:24`); 400 "Minimum 6 digits password is required" (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:38`); 400 "User not found" (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:51`); 400 "New password must be different from the old password." (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:56`); 200 "Password updated successfully" (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:62`); 400 "Incorrect current password" (`Ashoka-World-Backend:app/Http/Controllers/UpdatePasswordController.php:64`)

### POST v2/loginValidation
- controller: AuthController@loginValidation (found) · route: `Ashoka-World-Backend:routes/api.php:1639` · middleware: none
- called by: Nadi-Tarangini-App loginUser (LoginWithUsernameScreen); Nadi-Tarangini-Frontend loginController@checkLoginCredentials (auth.login)
- validation: `user_name`: required|string (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:415`); `password`: required|string (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:416`)
- errors: 400 "Both username and password are required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:429`); 400 "Username is required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:438`); 400 "Password is required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:447`); 400 "Both username and password are required" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:454`); 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:466`); 401 "Invalid username" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:471`); 401 "User has been blocked" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:476`); 401 "Invalid password" (`Ashoka-World-Backend:app/Http/Controllers/AuthController.php:481`)

### POST v2/signup
- controller: SignUpController@SignUpV2 (found) · route: `Ashoka-World-Backend:routes/api.php:1636` · middleware: none
- called by: Nadi-Tarangini-Frontend NewSignUpController@updateSignUpDetails (auth.admin_signUp, auth.college_signUp, auth.signup); Nadi-Tarangini-Frontend NtLiteSignUpController@submitSignUp (auth.nt_lite_signup)
- validation: `salutation_type`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:706`); `user_name`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:707`); `password`: required|regex:/[0-9]/ (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:708`); `lastname`: required|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:709`); `email`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:710`); `firstname`: required|regex:/^[a-zA-Z\s]+$/ (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:711`); `gender`: required|in:M,F,D,N (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:712`); `mobile_no`: required|numeric (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:713`); `profession_type_id`: nullable|numeric (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:714`); `ayush_no`: nullable|string (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:715`); `clinic_name`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:716`); `state`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:719`); `country`: required (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:720`)
- errors: ? "Provided country code is not valid for the given phone number" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:727`); ? "Clinic name is required" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:766`); ? "Internal server error" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:802`); 400 "Phone number already exists" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:825`); 400 "Invalid salutation type" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:832`); 400 "Please select a valid gender" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:838`); 400 "Please select a valid gender" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:842`); 400 "Please select a valid gender" (`Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:847`)

### POST validateCorporateCode
- controller: AuthController@corporateCode (found) · route: `Ashoka-World-Backend:routes/api.php:972` · middleware: api, auth.token
- called by: no screen in this workspace

## Backend routes no screen calls

`GET checkusernameormobileno`, `GET getdetailsbymobileno`, `POST login`, `POST logout`, `POST signup`, `POST validateCorporateCode`

## Web routes (26)

- Nadi-Tarangini-Frontend `POST checkDoctorMobileNo` → NewSignUpController@checkDoctorMobileNo · `Nadi-Tarangini-Frontend:routes/web.php:331`
- Nadi-Tarangini-Frontend `POST checkDoctorUsername` → NewSignUpController@checkDoctorUsername · `Nadi-Tarangini-Frontend:routes/web.php:332`
- Nadi-Tarangini-Frontend `POST checkForgotPassword` → forgotPasswordController@checkForgotPassword · `Nadi-Tarangini-Frontend:routes/web.php:318`
- Nadi-Tarangini-Frontend `POST checkLoginCredintial` → loginController@checkLoginCredentials · `Nadi-Tarangini-Frontend:routes/web.php:316`
- Nadi-Tarangini-Frontend `POST checkValidationsLinkDevice` → NewSignUpController@checkValidationsLinkDevice · `Nadi-Tarangini-Frontend:routes/web.php:333`
- Nadi-Tarangini-Frontend `POST editFcmToken` → loginController@editFcmToken · `Nadi-Tarangini-Frontend:routes/web.php:367` · check_auth_token, fetch_notifications, ensure_normal_dashboard_mode
- Nadi-Tarangini-Frontend `GET forgotPassword` → forgotPasswordController@forgotPassword · `Nadi-Tarangini-Frontend:routes/web.php:317`
- Nadi-Tarangini-Frontend `GET get-all-roles` → loginController@getAllRoles · `Nadi-Tarangini-Frontend:routes/web.php:92`
- Nadi-Tarangini-Frontend `POST getUserDetailsOtpBasedLogin` → loginController@getUserDetailsOtpBasedLogin · `Nadi-Tarangini-Frontend:routes/web.php:90`
- Nadi-Tarangini-Frontend `POST linkDeviceAfterValidation` → NewSignUpController@linkDeviceAfterValidation · `Nadi-Tarangini-Frontend:routes/web.php:334`
- Nadi-Tarangini-Frontend `GET login` → loginController@login · `Nadi-Tarangini-Frontend:routes/web.php:313`
- Nadi-Tarangini-Frontend `GET logout` → LoginController@logout · `Nadi-Tarangini-Frontend:routes/web.php:342`
- Nadi-Tarangini-Frontend `POST logout` → LoginController@logout · `Nadi-Tarangini-Frontend:routes/web.php:342`
- Nadi-Tarangini-Frontend `GET nt-lite/logout` → LoginController@logout · `Nadi-Tarangini-Frontend:routes/web.php:341`
- Nadi-Tarangini-Frontend `POST nt-lite/logout` → LoginController@logout · `Nadi-Tarangini-Frontend:routes/web.php:341`
- Nadi-Tarangini-Frontend `POST send-email-login-otp` → loginController@sendEmailLoginOtp · `Nadi-Tarangini-Frontend:routes/web.php:84`
- Nadi-Tarangini-Frontend `POST send-login-otp` → loginController@sendWhatsappLoginOtp · `Nadi-Tarangini-Frontend:routes/web.php:82`
- Nadi-Tarangini-Frontend `POST send-verification-otp` → OtpVerificationController@sendVerificationOtpsignup · `Nadi-Tarangini-Frontend:routes/web.php:307`
- Nadi-Tarangini-Frontend `GET sign-up` → NewSignUpController@doctorSignUp · `Nadi-Tarangini-Frontend:routes/web.php:325`
- Nadi-Tarangini-Frontend `GET sign-up-admin` → NewSignUpController@adminSignUp · `Nadi-Tarangini-Frontend:routes/web.php:329`
- Nadi-Tarangini-Frontend `GET sign-up-college` → NewSignUpController@collegeSignUp · `Nadi-Tarangini-Frontend:routes/web.php:328`
- Nadi-Tarangini-Frontend `GET signup` → NewSignUpController@signup · `Nadi-Tarangini-Frontend:routes/web.php:326`
- Nadi-Tarangini-Frontend `POST updateSignUpDetails` → NewSignUpController@updateSignUpDetails · `Nadi-Tarangini-Frontend:routes/web.php:327`
- Nadi-Tarangini-Frontend `POST verify-email-login-otp` → loginController@verifyEmailLoginOtp · `Nadi-Tarangini-Frontend:routes/web.php:88`
- Nadi-Tarangini-Frontend `POST verify-login-otp` → loginController@verifyWhatsappLoginOtp · `Nadi-Tarangini-Frontend:routes/web.php:86`
- Nadi-Tarangini-Frontend `POST verify-verification-otp` → OtpVerificationController@verifyVerificationOtpsignup · `Nadi-Tarangini-Frontend:routes/web.php:308`

## Screens (11)

- Nadi-Tarangini-App **ForgotPasswordScreen** `Nadi-Tarangini-App:lib/common_files/Login/view/forgot_password_screen.dart` · route /forgotPasswordScreen · goes to /loginScreen
- Nadi-Tarangini-App **LoginScreen** `Nadi-Tarangini-App:lib/common_files/Login/view/login_screen.dart` · route /loginScreen · goes to /signupScreen
- Nadi-Tarangini-App **LoginWithOtpScreen** `Nadi-Tarangini-App:lib/common_files/Login/view/login_with_otp.dart` · goes to /dashboardScreen, /geoRestrictedScreen, /kycScreen, /reportScreenPatient
- Nadi-Tarangini-App **LoginWithUsernameScreen** `Nadi-Tarangini-App:lib/common_files/Login/view/login_with_username_screen.dart` · goes to /dashboardScreen, /forgotPasswordScreen, /geoRestrictedScreen, /kycScreen, /reportScreenPatient
- Nadi-Tarangini-App **SignUpScreen** `Nadi-Tarangini-App:lib/common_files/signup/view/signup_screen.dart` · route /signupScreen · goes to /loginScreen, /webViewScreen
- Nadi-Tarangini-Frontend **auth.admin_signUp** `Nadi-Tarangini-Frontend:resources/views/auth/admin_signUp.blade.php` · route GET sign-up-admin · rendered by NewSignUpController@adminSignUp
- Nadi-Tarangini-Frontend **auth.college_signUp** `Nadi-Tarangini-Frontend:resources/views/auth/college_signUp.blade.php` · route GET sign-up-college · rendered by NewSignUpController@collegeSignUp
- Nadi-Tarangini-Frontend **auth.forgot_password** `Nadi-Tarangini-Frontend:resources/views/auth/forgot_password.blade.php` · route GET forgotPassword · rendered by forgotPasswordController@forgotPassword · goes to GET login
- Nadi-Tarangini-Frontend **auth.login** `Nadi-Tarangini-Frontend:resources/views/auth/login.blade.php` · route GET login · rendered by loginController@login · goes to /images/nt_v2/common/drop-down.svg, GET forgotPassword, GET signup
- Nadi-Tarangini-Frontend **auth.signup** `Nadi-Tarangini-Frontend:resources/views/auth/signup.blade.php` · route GET sign-up · rendered by NewSignUpController@doctorSignUp
- Nadi-Tarangini-Frontend **auth.tabs** `Nadi-Tarangini-Frontend:resources/views/auth/tabs.blade.php` · route GET signup · rendered by NewSignUpController@signup · goes to GET sign-up, GET sign-up-admin

## API calls (75)

| Client | Caller | Call | Route | Status | Source |
|---|---|---|---|---|---|
| Nadi-Tarangini-App | checkGeoIPValidity | POST `/checkGeoIPValidity` | POST checkGeoIPValidity | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2519` |
| Nadi-Tarangini-App | fetchAllCountriesName | POST `/getAllCountriesName` | POST getAllCountriesName | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:735` |
| Nadi-Tarangini-App | fetchCountryList | GET `/getAllCountries` | GET getAllCountries | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:202` |
| Nadi-Tarangini-App | fetchCountryWiseState | POST `/getCountryWiseStates` | POST getCountryWiseStates | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:773` |
| Nadi-Tarangini-App | fetchCurrencyType | POST `/getCurrencyType` | POST getCurrencyType | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1709` |
| Nadi-Tarangini-App | fetchSalutationTypes | POST `/getSalutationTypes` | POST getSalutationTypes | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:812` |
| Nadi-Tarangini-App | fetchTopicsListAshoka | POST `/notification/fetchUserTopics` | POST notification/fetchUserTopics | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:413` |
| Nadi-Tarangini-App | forgotPassword | POST `/forgotPassword` | POST forgotPassword | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:718` |
| Nadi-Tarangini-App | getAllRoles | GET `/public/allRoles` | GET public/allRoles | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:63` |
| Nadi-Tarangini-App | getAppLanguages | GET `/getAppLanguages` | GET getAppLanguages | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2476` |
| Nadi-Tarangini-App | getAppVersionDetailst | GET `/appVersion/getAppVersionDetails` | GET appVersion/getAppVersionDetails | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2129` |
| Nadi-Tarangini-App | getHelpCenterVideo | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2151` |
| Nadi-Tarangini-App | getPatientData | GET `/v2/client/getClientDetails` | GET v2/client/getClientDetails | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:376` |
| Nadi-Tarangini-App | getPinCodeDetails | POST `/getAddressUsingPincode` | POST getAddressUsingPincode | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:758` |
| Nadi-Tarangini-App | getProfessionType | GET `/getProfessionType` | GET getProfessionType | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:612` |
| Nadi-Tarangini-App | getUserDetailsUsingMobileNumber | POST `/getUserDetailsUsingMobileNumber` | POST getUserDetailsUsingMobileNumber | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:510` |
| Nadi-Tarangini-App | loginOtpBasedUser | POST `/loginOtpBasedUser` | POST loginOtpBasedUser | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:431` |
| Nadi-Tarangini-App | loginUser | POST `/v2/loginValidation` | POST v2/loginValidation | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:357` |
| Nadi-Tarangini-App | sendEmailOtp | POST `/otp/send-email-otp` | POST otp/send-email-otp | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:481` |
| Nadi-Tarangini-App | sendMobileOtp | POST `/otp/send-otp` | POST otp/send-otp | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:448` |
| Nadi-Tarangini-App | sendVerificationOtp | POST `/otp/send-verification-otp` | POST otp/send-verification-otp | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2486` |
| Nadi-Tarangini-App | signUp | POST `/signupV2` | POST signupV2 | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:675` |
| Nadi-Tarangini-App | updateFCMtokenAshoka | POST `/editFcmToken` | POST editFcmToken | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:391` |
| Nadi-Tarangini-App | updatePassword | POST `/updatepassword` | POST updatepassword | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:1316` |
| Nadi-Tarangini-App | verifyEmailOtp | POST `/otp/verify-email-otp` | POST otp/verify-email-otp | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:494` |
| Nadi-Tarangini-App | verifyMobileOtp | POST `/otp/verify-otp` | POST otp/verify-otp | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:465` |
| Nadi-Tarangini-App | verifyVerificationOtp | POST `/otp/verify-verification-otp` | POST otp/verify-verification-otp | matched | `Nadi-Tarangini-App:lib/common_files/api_services/api_repository.dart:2498` |
| Nadi-Tarangini-Frontend | AdminDashboardController@createUser | POST `/getSalutationTypes` | POST getSalutationTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/AdminDashboardController.php:1200` |
| Nadi-Tarangini-Frontend | ChangePasswordController@updatePassword | POST `/updatepassword` | POST updatepassword | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/ChangePasswordController.php:29` |
| Nadi-Tarangini-Frontend | DashboardController@addSelfAdmin | POST `/getSalutationTypes` | POST getSalutationTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1283` |
| Nadi-Tarangini-Frontend | DashboardController@switchToAdmin | POST `/loginOtpBasedUser` | POST loginOtpBasedUser | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1374` |
| Nadi-Tarangini-Frontend | DashboardController@switchToDoctor | POST `/loginOtpBasedUser` | POST loginOtpBasedUser | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:1404` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/getSalutationTypes` | POST getSalutationTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:684` |
| Nadi-Tarangini-Frontend | DashboardController@updateKycDetails | POST `/loginOtpBasedUser` | POST loginOtpBasedUser | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/DashboardController.php:667` |
| Nadi-Tarangini-Frontend | EditDoctorDetailsController@editDoctorDetails | POST `/getSalutationTypes` | POST getSalutationTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditDoctorDetailsController.php:22` |
| Nadi-Tarangini-Frontend | EditDoctorDetailsController@editDoctorProfile | POST `/getSalutationTypes` | POST getSalutationTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/EditDoctorDetailsController.php:216` |
| Nadi-Tarangini-Frontend | NewSignUpController@adminSignUp | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:333` |
| Nadi-Tarangini-Frontend | NewSignUpController@adminSignUp | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:343` |
| Nadi-Tarangini-Frontend | NewSignUpController@checkDoctorMobileNo | POST `/checkMobileNumber` | POST checkMobileNumber | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:171` |
| Nadi-Tarangini-Frontend | NewSignUpController@checkDoctorUsername | POST `/checkUsername` | POST checkUsername | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:211` |
| Nadi-Tarangini-Frontend | NewSignUpController@checkValidationsLinkDevice | POST `/validateDeviceWithSerialNo` | POST validateDeviceWithSerialNo | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:251` |
| Nadi-Tarangini-Frontend | NewSignUpController@collegeSignUp | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:149` |
| Nadi-Tarangini-Frontend | NewSignUpController@doctorSignUp | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:29` |
| Nadi-Tarangini-Frontend | NewSignUpController@doctorSignUp | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:46` |
| Nadi-Tarangini-Frontend | NewSignUpController@doctorSignUp | GET `/getProfessionType` | GET getProfessionType | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:34` |
| Nadi-Tarangini-Frontend | NewSignUpController@doctorSignUp | POST `/getSalutationTypes` | POST getSalutationTypes | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:24` |
| Nadi-Tarangini-Frontend | NewSignUpController@linkDeviceAfterValidation | POST `/linkDeviceInHouseV2` | POST linkDeviceInHouseV2 | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:295` |
| Nadi-Tarangini-Frontend | NewSignUpController@updateSignUpDetails | POST `/v2/signup` | POST v2/signup | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NewSignUpController.php:91` |
| Nadi-Tarangini-Frontend | NtLiteSignUpController@checkMobileNo | POST `/checkMobileNumber` | POST checkMobileNumber | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:132` |
| Nadi-Tarangini-Frontend | NtLiteSignUpController@checkUsername | POST `/checkUsername` | POST checkUsername | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:170` |
| Nadi-Tarangini-Frontend | NtLiteSignUpController@submitSignUp | POST `/v2/signup` | POST v2/signup | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/NtLiteSignUpController.php:77` |
| Nadi-Tarangini-Frontend | OtpVerificationController@sendVerificationOtpsignup | POST `/otp/send-verification-otp` | POST otp/send-verification-otp | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/OtpVerificationController.php:33` |
| Nadi-Tarangini-Frontend | OtpVerificationController@verifyVerificationOtpsignup | POST `/otp/verify-verification-otp` | POST otp/verify-verification-otp | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/OtpVerificationController.php:77` |
| Nadi-Tarangini-Frontend | forgotPasswordController@checkForgotPassword | POST `/forgotPassword` | POST forgotPassword | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/forgotPasswordController.php:51` |
| Nadi-Tarangini-Frontend | forgotPasswordController@forgotPassword | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/forgotPasswordController.php:25` |
| Nadi-Tarangini-Frontend | loginController@checkLoginCredentials | POST `/loginOtpBasedUser` | POST loginOtpBasedUser | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:79` |
| Nadi-Tarangini-Frontend | loginController@checkLoginCredentials | GET `/nt-admin/access-management/getAllFeatureDetails` | GET nt-admin/access-management/getAllFeatureDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:209` |
| Nadi-Tarangini-Frontend | loginController@checkLoginCredentials | GET `/subscriptions/getEndPoints` | GET subscriptions/getEndPoints | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:255` |
| Nadi-Tarangini-Frontend | loginController@checkLoginCredentials | GET `/v2/client/getClientDetails` | GET v2/client/getClientDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:94` |
| Nadi-Tarangini-Frontend | loginController@checkLoginCredentials | POST `/v2/loginValidation` | POST v2/loginValidation | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:63` |
| Nadi-Tarangini-Frontend | loginController@editFcmToken | POST `/editFcmToken` | POST editFcmToken | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:350` |
| Nadi-Tarangini-Frontend | loginController@getAllRoles | GET `/public/allRoles` | GET public/allRoles | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:728` |
| Nadi-Tarangini-Frontend | loginController@getUserDetailsOtpBasedLogin | POST `/loginOtpBasedUser` | POST loginOtpBasedUser | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:446` |
| Nadi-Tarangini-Frontend | loginController@getUserDetailsOtpBasedLogin | GET `/nt-admin/access-management/getAllFeatureDetails` | GET nt-admin/access-management/getAllFeatureDetails | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:589` |
| Nadi-Tarangini-Frontend | loginController@getUserDetailsOtpBasedLogin | GET `/subscriptions/getEndPoints` | GET subscriptions/getEndPoints | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:635` |
| Nadi-Tarangini-Frontend | loginController@login | POST `/getAllCountries` | POST getAllCountries | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:30` |
| Nadi-Tarangini-Frontend | loginController@login | POST `/getNtHelpVideos` | POST getNtHelpVideos | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:37` |
| Nadi-Tarangini-Frontend | loginController@sendEmailLoginOtp | POST `/otp/send-email-otp` | POST otp/send-email-otp | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:684` |
| Nadi-Tarangini-Frontend | loginController@sendWhatsappLoginOtp | POST `/otp/send-otp` | POST otp/send-otp | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:319` |
| Nadi-Tarangini-Frontend | loginController@verifyEmailLoginOtp | POST `/otp/verify-email-otp` | POST otp/verify-email-otp | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:696` |
| Nadi-Tarangini-Frontend | loginController@verifyWhatsappLoginOtp | POST `/getUserDetailsUsingMobileNumber` | POST getUserDetailsUsingMobileNumber | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:386` |
| Nadi-Tarangini-Frontend | loginController@verifyWhatsappLoginOtp | POST `/otp/verify-otp` | POST otp/verify-otp | matched | `Nadi-Tarangini-Frontend:app/Http/Controllers/loginController.php:378` |

## Tables (11)

- `api_endpoints` (models: ApiEndpoints): create_date, id, is_active, is_public, is_public_reception, method, name, updated_date, url
- `corporate_info` (models: CorporateInfo): add_patient_url, city, corp_role_id, corporate_id, corporate_type, country, doctors_info, pincode, profile_image, state
- `country_wise_states` (models: CountryWiseStates): timezone
- `currency_type` (models: CurrencyType): columns not in migrations
- `locality_info` (models: LocalityInfo): is_default, timezone
- `pg_device_mapping` (models: PgDeviceMapping): columns not in migrations
- `salutation_types` (models: SalutationTypes): columns not in migrations
- `subscriptions` (models: Subscription): api_rules, blocked_api_rules, create_date, duration, features, id, limits, name, price, status, updated_at
- `transactions` (models: Transaction): amount, comment, coupon_code, create_date, currency, expire_status, free_expire_date, id, invoice_data, is_trial, month, order_id, pay_gate_order_id, pay_gate_order_json, pay_gate_payment_id, pay_gate_payment_status, pay_gate_response_json, pay_gate_signature, pay_gate_webhook_json, payment_date, payment_status, plan_id, plan_id_v2, report_count, updated_at, user_id
- `user_nadi_capture_type` (models: UserNadiCaptureType): allowed_countries, avoid_device_selection_usb, can_change_capture_type, create_date, expiry_date, free_tier_enrolled, id, is_active, is_star_account, last_modified_on, nadi_capture_type, no_of_reports, plan_type, user_id
- `user_personal_info` (models: UserPersonalInfo): allowed_functions, app_language, ayush_no, clinic_id, external_user_status, is_parent, parent_id, plan_expire_date, plan_id, profession_type_id, reception_id, verified_role_id, welcome_tours_taken

## External systems

- Firebase (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:1085`
- Firebase (Nadi-Tarangini-App): `Nadi-Tarangini-App:lib/common_files/Login/controller/login_bloc/login_bloc.dart:5,173,196`
- S3 (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:139,832,1714`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:491,539,595`
- Samvit Chakra (Ashoka-World-Backend): `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:662`

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
