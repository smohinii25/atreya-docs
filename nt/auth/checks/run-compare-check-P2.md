# Run-compare check: P53–P105
| # | Run 1 | Run 2 | Decision | Evidence (short; cite Repo:path:line; no values) |
|---|---|---|---|---|
| P53 | n/a | Verified | Add from run 2 | Backend:app/Http/Controllers/UpdatePasswordController.php:50-51 returns 400 "User not found" when no active user. |
| P54 | Verified | Verified | Keep run 2 | UpdatePasswordController.php:24 has the message. The error branch returns 400 at :34, so Q8 is a fair open point. R2 is the superset. |
| P55 | Verified | Verified | Merge both | Frontend:routes/web.php:604 (POST /updatePassword to ChangePasswordController@updatePassword); App:doctor_dashboard/my_account/view/my_account_screen.dart uses change_password_bloc. R1 has the route, R2 the controller. |
| P56 | Verified | Verified | Add from run 2 | AuthController.php:1859-1866 sets fcm_token for header user_id and returns the "Fcm Token Updated" desc. Callers: Frontend loginController.php:350, App api_repository.dart:391. |
| P57 | Verified | Verified | Keep run 2 | AuthController.php:1870 DB::rollBack and :1874 500 "Internal server error"; R2 adds the rollback. |
| P58 | Verified | Verified | Keep run 2 | login_bloc.dart:198/:418 call updateFCMtokenAshoka; login_bloc is used by login_screen, login_with_otp, login_with_username_screen. Web: loginController.php:325-350. |
| P59 | n/a | Verified | Add from run 2 | api_repository.dart:812, :1709 use POST for salutation and currency. Frontend NewSignUpController.php:24 posts. No GET caller found in Frontend/App. |
| P60 | Verified | Verified | Keep run 2 | SignUpController.php:1353/:1130 (messages) and :1373/:1151 (500 "Internal server error"). R2 adds the 500 cites. |
| P61 | Mismatch | Verified | Keep run 2 | R1 "clinic screens (app)": fetchCurrencyType is called only from kyc_bloc.dart:160 and edit_account_bloc.dart:86, salutation from signup_bloc; no clinic screen. R2 SignUpScreen and KycScreen are correct. Web forms use SignUp/NewSignUp/Admin/EditDoctor controllers. |
| P62 | n/a | Verified | Add from run 2 | Frontend:routes/web.php:325, :328, :329; login.blade.php:181; tabs.blade.php:27; login_screen.dart:205/:212 embed the username and OTP screens. |
| P63 | Verified | Verified | Merge both | App:common_files/Login/view/login_screen.dart:205, :212 open both screens; router.dart:157 has /loginScreen but no route for them. Both statements are true. |
| P64 | Verified | Verified | Wording only | Label only (Mobile vs App). |
| P65 | Verified | Verified | Wording only | Backend:routes/api.php lines match in both (737, 739, 741, 744, 759, 760, 763, 764, 777, 788-794, 968-975, 1426-1427, 1636, 1639). Layout only. |
| P66 | Verified | Verified | Add from run 2 | Frontend:DashboardController.php:660-667 (updateKycDetails), :1369 (switchToAdmin), loginController.php:79; App login_bloc.dart:110, :369. |
| P67 | Verified | Verified | Keep run 2 | Frontend OtpVerificationController.php:33, :77; App otp_verification_cubit.dart used by signup_screen, kyc_screen, add_clinic, edit_clinic. R2 is more specific. |
| P68 | Verified | Verified | Keep run 2 | Salutation: Frontend NewSignUpController.php:24 and others, App signup_bloc.dart. Currency: App kyc_bloc.dart:160 (also edit_account_bloc.dart:86); Frontend calls getCurrencyTypes (plural), not this route. |
| P69 | Verified | Verified | Keep run 2 | Frontend ChangePasswordController.php:29, loginController.php:350; App change_password_bloc.dart, login_bloc.dart:198. |
| P70 | Verified | Verified | Keep run 2 | Frontend SignUpController.php:71 posts to /signup; its routes are commented out in routes/web.php:319-324; App strings_const.dart:14 signUpUrl is never used. R2 says which "SignUpController". |
| P71 | Verified | Verified | Wording only | Both match _map facts.md:278 and models.md:379 (26 columns); only the subset shown differs. |
| P72 | Verified | Verified | Keep run 2 | facts.md:277 lists 11 columns; R2 lists all, R1 uses "…". |
| P73 | n/a | Verified | Add from run 2 | AuthController.php:459, :485, :493, :1862 use those columns; facts.md Tables for user_personal_info does not list them. |
| P74 | Verified | Verified | Wording only | Both sources exist and agree (models.md:379 and facts.md:268-280). UserPersonalInfo.php:19 sets table. |
| P75 | Verified | Verified | Keep run 2 | R1 12 rows (277-288) and R2 24 rows (247-270) all match code: AuthController.php:466/:476/:481/:528/:806/:814/:1652/:1679/:1696/:1784/:1806, OtpSmsController.php:54-71, 94, 127-136, 359-373, 433-457, 479-480, 630, 656. R2 says "about 26"; count is 24. |
| P76 | Verified | Verified | Keep run 2 | AuthController.php:466 Invalid username 401, :476 blocked 401, :481 Invalid password 401. R1 shows only blocked. |
| P77 | Verified | Verified | Keep run 2 | AuthController.php:1652-1668 validation fail returns 404; :1679 unknown user 404. R1 "—" omits status. |
| P78 | Verified | Verified | Keep run 2 | SignUpController.php:708-712 rules; failures return 400 (:775-:790). R1 "—" omits status. |
| P79 | Verified | Verified | Keep run 2 | OtpSmsController.php:479-480 use $request->validate (no explicit status in code). R2 is honest and cites both lines. |
| P80 | Verified | Verified | Keep run 2 | SignUpController.php:220 (18) and :226 (100) both 400. |
| P81 | Verified | n/a | Keep run 1 | R1 §4 acceptance criteria do list more messages per endpoint (internal pointer holds). |
| P82 | Verified | Verified | Keep run 2 | api.php:968, :971, :972, :975 are inside the auth.token group (api.php:907); :1636, :1639 have no middleware. |
| P83 | Verified | Verified | Merge both | OtpSmsController.php:79, :381, :612 (5 min), :136 "Expired OTP" (R1); no attempt counter anywhere in the file (R2). |
| P84 | Verified | Verified | Keep run 2 | SignUpController.php:708 (digit), :908 (min 6); UpdatePasswordController.php:24, :38; AuthController.php:480-481 Hash::check (cite is 1 line off). |
| P85 | n/a | Verified | Add from run 2 | SignUpController.php:1033 (email), :1055 + sendNewSigupMessageOnWhatsapp (WhatsApp) in SignUpV2; :590 (older SignUp email), :668 (Samvit call). |
| P86 | Verified | Verified | Keep run 2 | Frontend resources/lang/en has auth, pagination, passwords, validation; resources/lang/en_patient.json exists. |
| P87 | Not provable | Verified | Keep run 2 | R1 cites nothing for "the map found…". R2 cites facts.md, which has no timeout or limit entry. Note: Backend:app/Http/Kernel.php:48 sets throttle 100000,1 on the api group (practically no limit). |
| P88 | Verified | Verified | Wording only | staging-delta.md exists in atreya-docs/nt/auth/; link style differs only. |
| P89 | n/a | Verified | Add from run 2 | SignUpController.php:1085 UserNotificationService addSingleUserFirebaseNotification, title "Account Created". |
| P90 | Verified | Verified | Keep run 2 | SignUpController.php:491, :539 are the only uploadFileToS3 calls (older SignUp); SignUpV2 (:701-1122) has none and uses placeholders; AuthController.php:139-141 builds URL only. |
| P91 | Verified | Verified | Keep run 2 | SignUpController.php:662-668 is in older SignUp; no Samvit call in SignUpV2. |
| P92 | Mismatch | Verified | Needs confirmation | R1 says "message text only" but AuthController.php:1710 (email) and :1740 (WhatsApp) show the sending code; R1's cite :1751 is only a response message. R2 matches: OtpSmsController.php:409, :89. Provider is not provable from the code read. Conflict row. |
| P93 | Verified | Verified | Wording only | login_bloc.dart:173, :196; AuthController.php:1862 stores fcm_token (R1's extra cite is valid and worth keeping). |
| P94 | Verified | Verified | Keep run 2 | R1 has 10 questions, R2 has 13; R2 covers all R1 topics. |
| P95 | Verified | Verified | Keep run 2 | api.php:903 allRoles route; AuthController.php:461 whereNotIn role_id [3,5]. |
| P96 | Verified | Verified | Keep run 2 | api.php:753 checkGeoIPValidity; App login_bloc.dart:125, :375 call it before navigation. |
| P97 | Verified | Verified | Keep run 2 | api.php:737, :744 under middleware api; AuthController.php:798-803 loginOtpBasedUser looks up the user by id with no OTP check. |
| P98 | Verified | Verified | Keep run 2 | OtpSmsController.php:489-496 use MasterWhitelist (fixed numbers/emails and OTP live in App/Support/MasterWhitelist.php, not in the controller); no attempt counter. |
| P99 | Verified | Verified | Keep run 2 | Frontend routes/web.php:341-342 logout routes use LoginController; Frontend SignUpController.php:71 only caller of /signup. |
| P100 | n/a | Verified | Add from run 2 | AuthController.php:1652 (username only), :1682-1693 (immediate reset, fixed prefix plus 4 random digits). |
| P101 | n/a | Verified | Add from run 2 | UpdatePasswordController.php:24 message; :28-34 handler reads the message array; status unconfirmed from static reading. Premise right. |
| P102 | n/a | Verified | Add from run 2 | SignUpController.php:1033, :1055 (SignUpV2), :668 (older SignUp to Samvit). |
| P103 | Verified | Verified | Keep run 2 | facts.md:273-276 (no migration columns for the three tables); AuthController.php:459, :485, :493, :1862 (P73). |
| P104 | Verified | Verified | Keep run 2 | R2 Q12 premise holds: SignUpV2 stores no file to S3 (placeholders in :701-1122) and only SignUp uploads (:491, :539). Samvit now Q10. |
| P105 | Verified | Verified | Merge both | diagrams/ has all five .drawio files; er.spec.json has 11 nodes. R2 folder note is right (rerun/diagrams holds only seq-AUTH-R02). |
