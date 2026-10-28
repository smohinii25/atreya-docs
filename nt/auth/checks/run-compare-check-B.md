# Run-compare check: B1–B50
Paths: BE = Ashoka-World-Backend, FE = Nadi-Tarangini-Frontend, APP = Nadi-Tarangini-App. Controllers under app/Http/Controllers.

| # | Run 1 | Run 2 | Decision | Evidence (short; cite Repo:path:line; no values) |
|---|---|---|---|---|
| B1 | n/a | Verified | Add from run 2 | atreya-docs/not-in-use.md line 63: auth 5 of 25 routes unused (login, logout, validateCorporateCode, checkusernameormobileno, getdetailsbymobileno). |
| B2 | Verified | Verified | Keep run 2 | BE:AuthController.php:1684 generates a new password; :1751 "Password sent to whatsapp/email". R2 is the more precise. |
| B3 | Verified | Verified | Merge both | Each run cites its own PRD; atreya-docs/modules.yaml and _map/_modules/auth/facts.md both exist. |
| B4 | n/a | Verified | Add from run 2 | FE:routes/web.php:328 (sign-up-college) and :329 (sign-up-admin) are GET page routes. |
| B5 | Verified | Verified | Keep run 2 | FE:DashboardController.php:1374 and :1404 both post to loginOtpBasedUser for the switch (R2 superset). |
| B6 | Verified | Verified | Merge both | APP:login_with_otp.dart:163 sends role "2" to /reportScreenPatient; facts.md:178 lists that target. |
| B7 | Verified | Verified | Keep run 2 | BE:AuthController.php:1784 "contact customer care"; this is the AUTH-R05 branch (PRD R05 source list). |
| B8 | Not provable | Not provable | Needs confirmation | Pointers to §12 Q2 only; code has role handlers (AuthController.php:1155 to 1484) but no role list, so neither sentence is checkable as written. |
| B9 | n/a | Verified | Add from run 2 | BE:SignUpController.php:1353 (salutation types) and :1130 (currency types), AUTH-R11. |
| B10 | Verified | Verified | Merge both | atreya-docs/modules.yaml:1412 module id payments exists; R2 "other modules" also true. |
| B11 | Verified | Verified | Keep run 2 | not-in-use.md:63 lists the 5; FE:SignUpController.php:71 calls old `signup`, FE routes/web.php:319-324 commented out (no page route); BE routes/api.php:741. |
| B12 | n/a | Verified | Add from run 2 | not-in-use.md:63 (auth 5 of 25); PRD rerun §1 states it; AUTH-R01 to R11 exist in rerun PRD. |
| B13 | Verified | Verified | Keep run 2 | BE:AuthController.php:1684 sets new password; :1710 email, :1740 WhatsApp. |
| B14 | Verified | Verified | Keep run 2 | BE:AuthController.php:466 (unknown), :476 (blocked), :481 (wrong password); editFcmToken api.php:971 (device); updatepassword api.php:975; account creation in SignUpController.php:701+. |
| B15 | Verified | Verified | Keep run 2 | Both PRDs have journeys J1 to J5 (PRD.md:43,86; rerun/PRD.md:31,52); AUTH-R01..R10 exist. R2 superset. |
| B16 | Verified | Verified | Needs confirmation | Conflict (rule sourced differently). Both lines are real blocked checks: BE:AuthController.php:476 in loginValidation (R01), :814 in loginOtpBasedUser (R04). Rule holds for both flows. |
| B17 | Verified | Verified | Merge both | BE:AuthController.php:415 is the required-fields validator; :429 is the "Both username and password are required" refusal. |
| B18 | n/a | Verified | Add from run 2 | BE:AuthController.php:466 "Invalid username", :481 "Invalid password" (both 401). |
| B19 | Verified | Verified | Keep run 2 | BE:OtpSmsController.php:79 (5 min cache), :136 "Expired OTP"; AUTH-R08 verify code also 5 min (:496, :612). |
| B20 | Verified | Verified | Keep run 2 | BE:OtpSmsController.php:54 invalid length, :57 country code mismatch. |
| B21 | Verified | Verified | Keep run 2 | BE:SignUpController.php:708 digit rule; UpdatePasswordController.php:16 current required, :38 min 6, :56 must differ. |
| B22 | Verified | Verified | Keep run 2 | BE:UpdatePasswordController.php:16 current_password required; R2 merges it into the change-password rule. |
| B23 | n/a | Verified | Add from run 2 | BE:SignUpController.php:832 "Invalid salutation type"; :838 gender fit check. |
| B24 | n/a | Verified | Add from run 2 | BE:AuthController.php:1652 only user_name required; :1684 new password set. |
| B25 | n/a | Verified | Add from run 2 | BE:AuthController.php:1784 NT_1016 "contact customer care" with DB::rollBack in the same branch. |
| B26 | Mismatch | Mismatch | Needs confirmation | Rule tables hold 10 rows in run 1 BRD and 14 rows in run 2 BRD, not 9 and 13 (count of §6 table rows). |
| B27 | Verified | Verified | Keep run 2 | BE:AuthController.php:1684/:1751; run 2 says "new" password, which matches. |
| B28 | Verified | Verified | Keep run 2 | AUTH-R06 sign-up (SignUpController.php:701); AUTH-R11 reference lists for the form (:1353, :1130). |
| B29 | Verified | Verified | Merge both | FE:DashboardController.php:1374/:1404 re-login through loginOtpBasedUser as another user id; "account" and "view" both fit. |
| B30 | Verified | Verified | Keep run 2 | §9 tables hold 4 and 7 rows; every run 1 row is also in run 2. |
| B31 | n/a | Verified | Add from run 2 | BE:SignUpController.php:1085-1088 addSingleUserFirebaseNotification, title "Account Created". |
| B32 | n/a | Verified | Add from run 2 | BE:OtpSmsController.php:89 otpSmsService->sendOtp. |
| B33 | Verified | Verified | Keep run 2 | BE:AuthController.php:1751 message; OtpSmsController.php:409 send_email; AuthController.php:1710 email body; :1740 sendForgotPasswordOnWhatsapp. |
| B34 | Verified | Verified | Keep run 2 | BE:SignUpController.php:491 uploadFileToS3 (profile pictures; in older SignUp, SignUpV2 has no S3 call); AuthController.php:139 S3BucketUrlService in sign-in code. |
| B35 | Verified | Verified | Keep run 2 | BE:SignUpController.php:662 is inside older SignUp (V2 starts :701, no Samvit call); it posts the plain password. |
| B36 | Verified | Verified | Keep run 2 | APP:login_bloc.dart:173 subscribeToTopic, :196 getToken. |
| B37 | Verified | Verified | Keep run 2 | FE:resources/lang holds only en/ and en_patient.json; qa-scope-rules.md:19 lists the 7 languages. |
| B38 | Verified | n/a | Keep run 1 | PRD.md:238 and :355 (§13 Q6) and not-in-use.md:63 support the assumption; run 2 moved it to §1/§4. |
| B39 | n/a | Verified | Add from run 2 | BE:routes/api.php:744 (signupV2) and :1636 (v2/signup) both map to SignUpController@SignUpV2. |
| B40 | n/a | Verified | Add from run 2 | atreya-docs/environments.md: Status TO FILL, all refs TO FILL. |
| B41 | n/a | n/a | Wording only | Success measures, no code; same intent (TO CONFIRM), run 2 adds two questions. |
| B42 | n/a | n/a | Wording only | Counts are true (9 and 12); the extra questions are checked in B43 to B49. |
| B43 | Verified | Verified | Keep run 2 | Premises true: APP:login_with_otp.dart:163 patient screen; FE:routes/web.php:328, :329 admin and college pages exist. |
| B44 | Verified | Verified | Keep run 2 | BE:OtpSmsController.php:79 5 min; fixed test numbers :75-76 and test emails :377-378 give a fixed code. |
| B45 | Verified | Verified | Keep run 2 | not-in-use.md:63 (5 routes); older register called only from FE:SignUpController.php:71, which has no route (routes/web.php:319-324 commented). |
| B46 | Verified | Verified | Keep run 2 | BE:SignUpController.php:662-669 sends the original password to Samvit Chakra in older SignUp only. |
| B47 | Verified | Verified | Keep run 2 | S3 at SignUpController.php:491, AuthController.php:139; SMS OtpSmsController.php:89; WhatsApp AuthController.php:1740; email :1710. |
| B48 | n/a | Verified | Add from run 2 | BE:routes/api.php:739 loginOtpBasedUser and :1639 v2/loginValidation sit outside auth.token; AuthController.php:798 reads `id` from request without code check. |
| B49 | n/a | Verified | Add from run 2 | BE:AuthController.php:1652 only user_name; :1684 builds "atreya" plus rand(1000, 9999) and replaces the password. |
| B50 | Verified | Verified | Wording only | Age rule exists only in older SignUp (BE:SignUpController.php:220, :226); SignUpV2 has none. Premise right in both runs. |
