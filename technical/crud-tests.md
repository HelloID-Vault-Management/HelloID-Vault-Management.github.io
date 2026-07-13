# CRUD Tests

## Overview

Unit tests verify create, read, update, delete, and search operations for PersonRepository and ContractRepository.

## Test Files

- `tests/HelloID.Vault.Tests.Unit/PersonRepositoryCrudTests.cs` — 11 tests
- `tests/HelloID.Vault.Tests.Unit/ContractRepositoryCrudTests.cs` — 10 tests

## Test Infrastructure

- Uses `TestSqliteConnectionFactory` (test-only, no WAL mode) defined in PersonRepositoryCrudTests.cs
- File-based SQLite DBs created in `bin/.../test_databases/` with GUID filenames
- Each test class gets its own DB instance, cleaned up via IDisposable
- Simplified schema (source_system, persons, contracts only — no views)

## Person Tests (11)

| Category | Test |
|----------|------|
| Create | InsertAsync_CreatesPerson_ReturnsRowsAffected |
| Read | GetByIdAsync_ReturnsPerson_WhenExists |
| Read | GetByIdAsync_ReturnsNull_WhenNotExists |
| Update | UpdateAsync_UpdatesDisplayName_Succeeds |
| Update | UpdateAsync_WithValidManager_Succeeds |
| Update | UpdateAsync_WithStaleManager_DoesNotThrow |
| Update | UpdateAsync_WithNullManager_Succeeds |
| Delete | DeleteAsync_RemovesPerson_WhenExists |
| Delete | DeleteAsync_ReturnsZero_WhenNotExists |
| Search | SearchAsync_ReturnsMatchingPersons |
| Search | SearchAsync_ReturnsEmpty_WhenNoMatch |
| Search | SearchAsync_MatchesByExternalId |

## Contract Tests (10)

| Category | Test |
|----------|------|
| Create | InsertAsync_CreatesContract_ReturnsContractId |
| Read | GetByIdAsync_ReturnsContract_WhenExists |
| Read | GetByIdAsync_ReturnsNull_WhenNotExists |
| Update | UpdateAsync_UpdatesFields_Succeeds |
| Update | UpdateAsync_WithValidManager_Succeeds |
| Update | UpdateAsync_WithStaleManager_DoesNotThrow |
| Update | UpdateAsync_WithNullManager_Succeeds |
| Delete | DeleteAsync_RemovesContract_WhenExists |
| Delete | DeleteAsync_ReturnsZero_WhenNotExists |

## Key Test

`UpdateAsync_WithStaleManager_DoesNotThrow` verifies that saving a non-existent manager ID doesn't throw an FK error. This is the core consistency guarantee across SQLite, Turso, and PostgreSQL — all three disable FK constraints during updates.

## Running Tests

```bash
# Run CRUD tests only
dotnet test tests/HelloID.Vault.Tests.Unit/ --filter "PersonRepositoryCrudTests|ContractRepositoryCrudTests"

# Run all unit tests
dotnet test tests/HelloID.Vault.Tests.Unit/
```

## Results

- 21/21 CRUD tests pass
- 58/59 total unit tests pass (1 pre-existing failure: `CustomFieldRepositoryTests.VerifyPostgreSQLSqlContainsToJsonb` — requires real PostgreSQL connection)
