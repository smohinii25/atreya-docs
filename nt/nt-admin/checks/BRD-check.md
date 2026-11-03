# Doc check: atreya-docs/nt/nt-admin/BRD.md (atreya:doc-checker, fresh context)
Checked 2026-11-03 against Ashoka-World-Backend 8dfbb37, Nadi-Tarangini-Frontend e8a9742.

## Mismatch (fixed in the BRD afterwards)
1. §6 said every admin service rejects a request without the user id; updateUserStatus, getAllRoles, getUserDetails, getUserWiseActiveClinicDetails do not read the header (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/UserManagementController.php:121-150`, `:152-183`, `:257-289`, `:430-462`). Reworded.
2. §6 said a feature-details request needs a valid medical visit; the medical id is optional and checked only when supplied (`Ashoka-World-Backend:app/Http/Controllers/NTAdmin/FeaturesController.php:164-192`). Reworded; PRD R16 got the same note.

## Not provable (addressed)
1. §3 "doctors and clinic staff": changed to "Mobile app users" and cited api_repository.dart:63, :2038, :2396.
2. §5 step 1: added AdminDashboardController.php:24, :41 citations.
3. §5 steps 2, 5, 6 rest on R-numbers and the fact pack (left as is).

## Secret risk
None found.

Summary: about 45 claims · 36 verified · 2 mismatch · 3 not provable · 0 secret risk
