# Doc check: atreya-docs/nt/nt-admin/PRD.md (atreya:doc-checker, fresh context)
Checked 2026-11-03 against Ashoka-World-Backend 8dfbb37, Nadi-Tarangini-Frontend e8a9742. Spot-checked, not every line.

## Mismatch (all fixed in the PRD afterwards)
1. §8 and Q8 said addUser validation HTTP status was not shown; AddUserRequest::failedValidation returns 400 (`Ashoka-World-Backend:app/Http/Requests/NTAdmin/UserManagement/AddUserRequest.php:113-130`). Fixed.
2. "44 web routes / All 44 use nt_admin_authentication": the web.php group (routes/web.php:109-166) also holds CustomizeController getCategoryWiseCustomizeQuestions(+List) and DashboardController switchToAdminToDoctor. Reworded.
3. R14 omitted the 400 error branch of add-self-admin (`Ashoka-World-Backend:app/Http/Controllers/NTUser/AdminManagementController.php:36-57`). Added; Q8 now asks about it.

## Not provable
1. Role meanings: already in §13 Q1.
2. "App has no admin screen / calls only three APIs" is a negative claim: reworded to "fact pack lists".
3. 500 `errors` field: line 147 not opened; same pattern confirmed at UserManagementController.php:210.
4. Language files "only en": not re-checked by the checker.

## Secret risk
None found.

Summary: about 75 claim groups checked · 65 verified · 3 mismatch · 5 not provable · 0 secret risk
