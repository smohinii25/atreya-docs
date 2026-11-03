# Doc check: atreya-docs/nt/dashboard/PRD.md

Checked 2026-11-03 by atreya:doc-checker (fresh context) against commits Ashoka-World-Backend 8dfbb37d, Nadi-Tarangini-App 0b7deec6, Nadi-Tarangini-Frontend e8a9742b. Not checked: mobile navigation targets beyond splash; web welcome-tour proxy internals; section 7 column lists (taken from facts.md).

Summary: ~85 claims · 74 verified · 5 mismatch · 6 not provable · 0 secret risk

## Mismatch
1. R08 / §5: `invoice/{invoiceId}` makes no backend call; it reads `Session::get('all_current_transactions')`, renders `profile.invoice` when found and `errors.404` only when not found. (DashboardController.php:1156-1177)
2. §9: "No OTP logic ..." is wrong: `GET update_kyc` (`updateKycDetails`) also posts to `loginOtpBasedUser`, has no auth middleware, and redirects to dashboard if `kyc_updated` is 1. (DashboardController.php:667-679; routes/web.php:304)
3. §6: "GET/POST welcome-tour (360/361)": line 361 is `POST welcome-tour/complete`.
4. §1: `nadi_status = 1` cited at AuthController.php:2060; it is at lines 2091, 2183, 2201.
5. R01: `monthly_counts` is a top-level sibling of `data`, not inside it. (AuthController.php:2111-2123)

## Not provable
1. Dashboard screen navigation targets cited to the whole file.
2. GeoRestrictedScreen "has no outgoing navigation" (no citation).
3. `locality_info` is_default/timezone column names come from facts.md only (timezone use also at AuthController.php:1976, 2252).
4. Web welcome-tour proxy routes belong to same flow (handlers at DashboardController.php:823, 880, 1002 not read; covered by §13 item 5).
5. "All backend routes sit behind auth.token" cited at api.php:949; group starts at routes/api.php:907.
6. "Only English language files in web" copied from facts.md.

## Secret risk
None in the PRD. Side note outside the doc: UserStatsController.php:157-161 hard-codes Google Chat webhook URLs with key/token values (not repeated here, not in the PRD).

Summary: Verified 74 / Mismatch 5 / Not provable 6 / Secret risk 0
