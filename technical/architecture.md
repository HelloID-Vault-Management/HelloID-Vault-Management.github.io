# Architecture

## Project Structure

```
src/
├── HelloID.Vault.Core/          # Models, DTOs, Filters, Interfaces
├── HelloID.Vault.Data/          # Repositories, Database, Connection
├── HelloID.Vault.Services/      # Business logic, Import, Anonymization
└── HelloID.Vault.Management/    # WPF UI (Views, ViewModels, Controls)
```

## Database Support

| Database | Driver | Connection |
|----------|--------|------------|
| SQLite | Microsoft.Data.Sqlite | Local file |
| Turso | ITursoClient (HTTP API) | libsql:// URL + auth token |
| Supabase | Npgsql | PostgreSQL connection string |

## Key Patterns

- **MVVM** with CommunityToolkit.Mvvm (`[ObservableProperty]`, `[RelayCommand]`)
- **Repository pattern** with Dapper (SQLite/PostgreSQL) and TursoClient (Turso)
- **Strategy pattern** for import (`BaseImportStrategy`, `SqliteImportStrategy`, `PostgresManagedImportStrategy`)
- **Factory pattern** for database connections (`IDatabaseConnectionFactory`)
- **Dependency injection** via `Microsoft.Extensions.DependencyInjection`

## Import Pipeline

```
vault.json → Deserialize → ReferenceDataCollector → Import Strategy → Database
                ↓                    ↓                      ↓
          VaultRoot          Collects lookup         SQLite/Turso/PostgreSQL
          (persons,          tables, departments     strategy-specific insert
           contracts,        from contracts
           contacts)
```

## FK Constraint Handling

All database types disable FK constraints during updates for consistency:

| Database | Method |
|----------|--------|
| SQLite | `CreateConnection(enforceForeignKeys: false)` |
| Turso | `PRAGMA foreign_keys = OFF/ON` |
| PostgreSQL | `DEFERRABLE INITIALLY DEFERRED` + pre-validation |
