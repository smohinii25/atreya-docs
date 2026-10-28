# Models and tables: Nadi-Tarangini-Frontend

Built from commit `e8a9742b97e5be6d87452a6fdcfae67ee42ecb6d` by scripts/models.sh (static parse).

1 models, 4 tables (4 with migrations, 0 without: their columns are unknown from code), 1 table names inferred from class names.

## Models

| Model | Table | Relations | Source |
|---|---|---|---|
| User | `users` (inferred) |  | `app/Models/User.php` |

## Tables

| Table | Models | Columns (from migrations) | Migrations |
|---|---|---|---|
| `failed_jobs` |  | connection, exception, failed_at, id, payload, queue, uuid | 1 |
| `password_resets` |  | created_at, email, token | 1 |
| `personal_access_tokens` |  | abilities, created_at, id, last_used_at, name, token, tokenable, updated_at | 1 |
| `users` | User | created_at, email, email_verified_at, id, name, password, updated_at | 1 |
