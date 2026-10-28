# Test accounts found in code (read-only)

- Date: 2026-10-26
- Why: hard-coded test accounts with a fixed OTP work on every environment that
  runs this code, production included. Escalate together with the Razorpay key.
- Values are never shown here: only file, line and account type. QA never uses
  these accounts (references/qa-scope-rules.md); it uses the staging login from
  the plugin settings only.
- Status: **Needs confirmation**: owner to decide whether each one may stay in
  production code.

| Repo | Commit scanned |
|---|---|
| Ashoka-World-Backend | `8dfbb37db7d71a400b3656bd50fbed6173908a24` |
| Nadi-Tarangini-Frontend | `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d` |
| Nadi-Tarangini-App | `0b7deec6de2b0b8b4f05eab4be8c8430523829bf` |

## Accounts

| # | Where (definition) | Account type | What the code does with it |
|---|---|---|---|
| 1 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:76` | 2 mobile numbers (+91), inline in `sendOtp` | Login OTP by mobile: these numbers get a fixed OTP (`:77`) and no message is sent (`:81`). Not in MasterWhitelist (different numbers). |
| 2 | `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:378` | 2 email addresses, inline in `sendEmailOtp` | Login OTP by email: fixed OTP (`:379`), no email sent (`:383`). Same addresses as #4. |
| 3 | `Ashoka-World-Backend:app/Support/MasterWhitelist.php:11` | 2 mobile numbers (country code + number) | "Master whitelist": fixed OTP for verification OTPs (`OtpSmsController.php:494`, `:496`), and exempt from the "number already registered" check (see Uses). |
| 4 | `Ashoka-World-Backend:app/Support/MasterWhitelist.php:20` | 2 email addresses | Same as #3 for email. Same addresses as #2. |
| 5 | `Ashoka-World-Backend:app/Support/MasterWhitelist.php:56` | fixed OTP value (shared) | The one OTP every whitelisted entry receives; the inline lists (#1, #2) use the same value. |

### Uses of the master whitelist (#3, #4)

| Where | Effect |
|---|---|
| `Ashoka-World-Backend:app/Http/Controllers/OtpSmsController.php:494` | verification OTP: whitelisted mobile/email gets the fixed OTP (`:496`) |
| `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:821` | sign-up: a whitelisted mobile may register again (duplicate check skipped) |
| `Ashoka-World-Backend:app/Http/Controllers/DoctorController.php:449` | same exemption in DoctorController |
| `Ashoka-World-Backend:app/Services/NTAdmin/UserManagementService.php:200` | NT admin user management: duplicate-mobile check skipped (also `:792`, `:909`) |
| `Ashoka-World-Backend:app/Services/NTAdmin/UserManagementService.php:207` | NT admin user management: duplicate-email check skipped (also `:916`) |

## Related, not accounts in code
- `Ashoka-World-Backend:app/Models/WhitelistedMobilenoTuryaa.php:17`: table
  `whitelisted_mobileno_turyaa` holds whitelisted Turyaa mobile numbers in the
  database. Values are not in code; what they are allowed to do is not checked here.

## Searched, nothing found
- Backend `app/` and `routes/`, Frontend `app/` and `routes/`, App `lib/`, for:
  a fixed OTP literal; inline mobile/email lists compared in OTP code;
  names like whitelist, test/dummy user/mobile/email, bypass/static/fixed OTP,
  demo user/account.
- Excluded on reading: `dummy_user` (a patient_prakruti value filtered out in
  Admin reports) and `dummy.jpg` / `dummy_clinic_logo.png` (default images).
- Not searched: database contents, config files outside `app/`, git history.

## Needs confirmation
1. **Owner:** may these test accounts and the fixed OTP stay in production code?
   If yes, who controls the mailboxes and numbers?
2. **Dev:** why are there two lists (#1 inline, #3 MasterWhitelist) with
   different mobile numbers? Should `sendOtp` use MasterWhitelist?
3. **Dev:** what may numbers in `whitelisted_mobileno_turyaa` do?
