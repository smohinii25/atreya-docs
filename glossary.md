# Glossary

Status: **Draft** · 2026-10-26 · candidate terms found in code (file and folder
names, model and method names). Every meaning is **TO CONFIRM** by the product
owner; nothing here is a definition yet.

| Term | Where seen (file) | Meaning |
|---|---|---|
| Nadi Tarangini (NT) | Ashoka-World-Backend `app/Services/NadiTaranginiV3.php`; repo names | TO CONFIRM |
| Nadi | Ashoka-World-Backend `app/Http/Controllers/NadiReportController.php`; Nadi-Tarangini-App `lib/doctor_dashboard/nadi_flow_new/` | TO CONFIRM |
| Prakruti / Prakriti (two spellings in code) | Ashoka-World-Backend `app/Http/Controllers/PrakrutiController.php`, `app/Models/NadiParikshaModels/NpPrakritiQuestion.php` | TO CONFIRM (and which spelling is official) |
| Vikruti | Nadi-Tarangini-Frontend `app/Http/Controllers/VikrutiController.php`; Ashoka-World-Backend `app/Models/TuryaaModels/VikrutiDescription.php` | TO CONFIRM |
| Prahar | Ashoka-World-Backend `app/Http/Controllers/MedicalReportSaveController.php:4471` (`find_prahar_new1`), `app/Http/Controllers/External/ExternalUserController.php:1911` (`getCurrentPrahar`) | TO CONFIRM |
| Swasthya Darshika | Ashoka-World-Backend `app/Models/SwasthyaReportData.php`, `app/Http/Controllers/GenerateSwasthyaLambda.php` | TO CONFIRM |
| Arogya Darshika | Ashoka-World-Backend `app/Models/ArogyaDarshikaData.php` | TO CONFIRM |
| Rutucharya | Ashoka-World-Backend `app/Models/RutucharyaPeriodsDates.php`; Nadi-Tarangini-Frontend `app/Http/Controllers/DownloadRutucharyaController.php` | TO CONFIRM |
| Dinacharya | Ashoka-World-Backend `app/Http/Controllers/DinacharyaController.php` | TO CONFIRM |
| Aniruddha (rule list) | Ashoka-World-Backend `app/Models/AniruddhaRuleList.php` (research dashboard) | TO CONFIRM |
| Pudi | Ashoka-World-Backend `app/Http/Controllers/PudiController.php` (medical inventory) | TO CONFIRM |
| Samvit Chakra | Nadi-Tarangini-Frontend `resources/views/payments/samvit_checkout.blade.php` (payment bridge) | TO CONFIRM |
| Guna | Ashoka-World-Backend `app/Http/Controllers/Guna/` (unassigned routes `guna/*`) | TO CONFIRM (legacy product?) |
| Badmin | Ashoka-World-Backend `app/Http/Controllers/Guna/BadminFunctionsController.php` | TO CONFIRM |
| Jiva | Ashoka-World-Backend `database/migrations/2026_05_08_104955_add_jiva_consent_status_to_np_analysis_data.php`; routes `nt-jiva/*` | TO CONFIRM |
| NT Lite | Nadi-Tarangini-Frontend `app/Http/Controllers/NtLiteDashboardController.php`, `resources/views/auth/nt-lite/` | TO CONFIRM |
| Ashoka (dashboard) | Ashoka-World-Backend `app/Http/Controllers/Admin/AshokaAuthController.php`; routes `ashokaDashboard/*` | TO CONFIRM |
| Nadi Pariksha | Ashoka-World-Backend `app/Http/Controllers/NadiPariksha/` | TO CONFIRM |
| Turyaa | Ashoka-World-Backend `app/Http/Controllers/Turyaa/` | TO CONFIRM |
| Coach | Ashoka-World-Backend `app/Http/Controllers/Turyaa/CoachController.php`, `app/Http/Controllers/NadiPariksha/CoachDashboardController.php` | TO CONFIRM (same role in both products?) |
| Cohort | Ashoka-World-Backend `app/Http/Controllers/NadiPariksha/NpCohortManagement.php` | TO CONFIRM |
| Patanjali report | Ashoka-World-Backend `app/Services/patanjaliReport.php` | TO CONFIRM |
| SPA report | Ashoka-World-Backend `app/Http/Controllers/SpaReportController.php` | TO CONFIRM |
| Nakshatra | Ashoka-World-Backend `app/Models/NakshatraResult.php` | TO CONFIRM |
| HRV | Ashoka-World-Backend `app/Models/HrvResult.php`, `app/Http/Controllers/PatientDetailsController.php:1469` (`get_hrv_output`) | TO CONFIRM |
| Vata / Pitta / Kapha | Nadi-Tarangini-App `assets/patient_module/kapha_vata.webp`; Ashoka-World-Backend `resources/views/research_dashboard_vata.blade.php` | TO CONFIRM |
| Mark on image | Ashoka-World-Backend `app/Models/MarkOnImage.php`; Nadi-Tarangini-Frontend `app/Http/Controllers/MarkOnImageController.php` | TO CONFIRM |
| Tongue analysis | Ashoka-World-Backend `database/migrations/2025_05_16_173030_tongue_analysis_data.php` | TO CONFIRM |
| Wellness tracking | Ashoka-World-Backend `app/Http/Controllers/Turyaa/WellnessController.php` | TO CONFIRM |
| Knowledge data | Ashoka-World-Backend `app/Models/TuryaaModels/KnowledgeData.php` | TO CONFIRM |
| PG device | Ashoka-World-Backend `app/Models/PgDeviceList.php`, `app/Models/PgDeviceMapping.php` | TO CONFIRM (what "PG" stands for) |
| ENACH / e-mandate | Ashoka-World-Backend `app/Http/Controllers/ENACH/ENACHController.php`, `app/Models/EnachMandate.php` | TO CONFIRM |
| KYC | Nadi-Tarangini-App `lib/doctor_dashboard/kyc/`; Nadi-Tarangini-Frontend `public/js/myaccount/updateKyc.js` | TO CONFIRM |
| Medical ID / visit | Ashoka-World-Backend `app/Http/Controllers/Client/VisitManagementController.php`; route `reception-api/report/getNewMedicalId` | TO CONFIRM |
