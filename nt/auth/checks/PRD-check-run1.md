# Doc check: atreya-docs/nt/auth/PRD.md

Checked 2026-10-26 by the doc-checker (fresh context, read-only) against commits
Ashoka-World-Backend 8dfbb37, Nadi-Tarangini-App 0b7deec, Nadi-Tarangini-Frontend e8a9742.

Summary: ~150 claims · ~142 verified · 3 mismatch · 5 not provable · 0 secret risk

Coverage: all §4 messages, HTTP codes and field rules; all §6 route lines,
controllers and middleware; §2/§3 citations; §8 rows. Not checked: §7 column lists,
§5 file paths beyond existence.

## Mismatch
| # | Claim | What the code shows | Source | Resolution |
|---|---|---|---|---|
| 1 | AUTH-R06 required fields list | `address_line_1` is also required; `country_code` is `required_with:mobile_no` | `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:717`, `Ashoka-World-Backend:app/Http/Controllers/SignUpController.php:722` | Fixed in AUTH-R06 |
| 2 | §1 "Five backend routes are not called" | §6 marks six (incl. `POST signup`, called only from an unrouted controller) | PRD §6 | Fixed in §1 |
| 3 | §12 S3 at `AuthController.php:139` | Line 139 is commented out | `Ashoka-World-Backend:app/Http/Controllers/AuthController.php:139` | Citation removed |

## Not provable
| # | Claim | Why | Resolution |
|---|---|---|---|
| 1 | §12 Firebase at `AuthController.php:1852`, `loginController.php:325` | Method signatures only | Re-cited: App `login_bloc.dart:173`, `:196` (FirebaseMessaging) |
| 2 | §12 WhatsApp/email at `AuthController.php:1751` | A message string, not delivery code | Wording now says "messages mention"; provider stays §13 Q9 |
| 3 | §3 J1 page links | No citation | Cited `login.blade.php:181`, `:279` |
| 4 | §3 J5 tab links | No citation | Cited `tabs.blade.php:27`, `:53` |
| 5 | §9 "No limits or timeouts visible" | OTPs are cached for 5 minutes | §9, AUTH-R02/R03 and §13 Q5 updated (`OtpSmsController.php:79`, `:381`, `:612`) |

## Secret risk
None.

## Verified (sample)
- AUTH-R01: all 400/401/500 messages at `AuthController.php` 429-528; `v2/loginValidation` has no middleware (`api.php:1639`, `v2` group).
- AUTH-R02/R03: every send/verify message and code in `OtpSmsController.php` 54-197 and 359-457.
- AUTH-R04/R05: `loginOtpBasedUser` 401s (806, 814); forgotPassword rule (1652), 404 (1679), 422 (1696), channel messages (1751/1762/1773), no-contact (1784).
- AUTH-R06-R09, R11: sign-up v2 rules (706-712) and errors (766, 825, 832, 838); availability checks (182-301); verification OTP rules (479-480, 630) and messages (500, 564, 656, 666); change-password messages (24-64); reference lists (1130, 1353).
- §6: all 25 route lines, controllers and middleware groups match.
- §3/§5: every cited Frontend and App call line resolves to the stated endpoint; all screen files exist.
- Drift: §8 firstname/lastname row cited the lastname line only; now cites both.
