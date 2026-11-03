# Doc check: atreya-docs/nt/dashboard/BRD.md (with PRD.md)

Checked 2026-11-03 by atreya:doc-checker (fresh context) against the stamped commits. Did not open facts.md or _map json; PRD section 7 columns and TO FILL rows not checked.

Summary: about 115 claims · 98 verified · 5 mismatch · 4 not provable · 0 secret risk

## Mismatch
1. PRD s2: "29 of 30" web routes under the middleware group; only 28 (update_kyc has none, switchToAdminToDoctor is in nt_admin_authentication). web.php:109,156,304,355
2. PRD s6/R04/R05: welcome-tour "App (4 screens)"; the App references tours in ~22 files.
3. PRD s6/R06: getAccountData "App (4 screens)"; called in 20 App files.
4. PRD R09: api_repository.dart:1225 is saveReportLanguages, getLanguages is 1206, clinic calls 2209/2216.
5. BRD s1/BR-03: "by week, month or year"; actual buckets are 7 daily / 4 weekly / 12 monthly (AuthController.php:2276-2297).

## Not provable
1. BRD s12 item 8, PRD R12 AC and s13 item 4: splash conditions are in splash_screen.dart:47-90 (stale question); only what GeoRestricted blocks is open.
2. getUserStatsData "not called": no code citation (no references in App lib/ or Frontend).
3. PRD s7 per-table columns: fact-pack content, not verified.
4. BRD out-of-scope member progress/report/queries pages: handler bodies not read (honest TO CONFIRM).

## Secret risk
None.

Summary: 98 Verified · 5 Mismatch · 4 Not provable · 0 Secret risk
