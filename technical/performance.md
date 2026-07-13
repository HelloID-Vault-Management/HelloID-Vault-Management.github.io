# PostgreSQL Performance Optimization

## Problem

Full import to Supabase (PostgreSQL) took **142 seconds** for ~700 persons with ~1400 contracts.

## Root Cause

The import was making ~20,350 individual database round-trips to Supabase:
- 14,000 FK validation queries (10 per contract)
- 2,100 person/contract/contact individual INSERTs
- 2,500 custom field individual UPDATEs
- 150 reference data INSERTs

At ~10ms RTT per query to Supabase, this resulted in ~200 seconds of pure network overhead.

## Optimizations Applied

### 1. FK Validation Cache (142s → 73s)

**Before:** 10 `SELECT EXISTS` queries per contract (14,000 total)

**After:** Load all valid reference IDs into HashSets once at the start (10 queries total), then validate in-memory.

```
FkValidationCache:
  - PersonIds (HashSet<string>)
  - TitleKeys (HashSet<string>)  
  - LocationKeys, EmployerKeys, DepartmentKeys, etc.
```

### 2. Npgsql COPY Bulk Insert (73s → 14s)

**Before:** Individual `INSERT` statements via Dapper (N round-trips)

**After:** PostgreSQL `COPY FROM STDIN (FORMAT BINARY)` via `NpgsqlConnection.BeginBinaryImport()` (1 round-trip per table)

Used for:
- Persons (~700 rows → 1 round-trip)
- Contracts (~1400 rows → 1 round-trip)
- Contacts (~1400 rows → 1 round-trip)

### 3. Temp Table + COPY + JOIN UPDATE

For custom field UPDATEs (can't use COPY directly since they're UPDATEs, not INSERTs):

1. `CREATE TEMP TABLE tmp_person_cf (external_id TEXT, custom_fields JSONB)`
2. `COPY tmp_person_cf FROM STDIN (FORMAT BINARY)` — bulk insert all updates
3. `UPDATE persons SET custom_fields = tmp.custom_fields FROM tmp_person_cf tmp WHERE persons.external_id = tmp.external_id` — single join update

### 4. Reference Data Batching

Batched all 8 lookup table inserts via `Dapper.ExecuteAsync(sql, IEnumerable<T>)` — one round-trip per table instead of N per row.

## Result

| Metric | Before | After |
|--------|--------|-------|
| Round-trips | ~20,350 | ~22 |
| Import time | 142s | 14s |
| Improvement | — | 10x |

## Implementation

See `src/HelloID.Vault.Services/Import/Utilities/PostgresBulkInsertHelper.cs` for the COPY implementation. The helper automatically falls back to Dapper batch insert for non-PostgreSQL connections (SQLite, Turso).
