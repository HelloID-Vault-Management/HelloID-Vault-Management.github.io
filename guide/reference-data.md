# Reference Data

Reference data represents the organizational structure. All reference data views follow the same pattern: a searchable DataGrid with Add, Edit, and Delete actions.

## Reference Data Types

| Type | Description | Key Fields |
|------|-------------|------------|
| **Departments** | Organizational departments | External ID, Display Name, Code, Parent, Manager, Source |
| **Locations** | Physical locations / offices | External ID, Code, Name, Source |
| **Cost Centers** | Financial cost centers | External ID, Code, Name, Source |
| **Cost Bearers** | Financial cost bearers | External ID, Code, Name, Source |
| **Employers** | Legal employers | External ID, Code, Name, Source |
| **Teams** | Teams within the organization | External ID, Code, Name, Source |
| **Divisions** | Organizational divisions | External ID, Code, Name, Source |
| **Titles** | Job titles | External ID, Code, Name, Source |
| **Organizations** | Top-level organizations | External ID, Code, Name, Source |
| **Source Systems** | Data source systems | System ID, Display Name, Identification Key |

## Adding Reference Data

1. Navigate to the reference data type (e.g., Departments)
2. Click **Add**
3. Fill in the fields:
   - **External ID** — Unique identifier within the source
   - **Code** — Short code
   - **Name** — Display name
   - **Source** — Which source system this belongs to
4. Click **Save**

## Editing Reference Data

1. Double-click an item or right-click > **Edit**
2. Modify the fields
3. Click **Save**

## Deleting Reference Data

1. Right-click an item
2. Select **Delete**
3. Confirm the deletion

## Source Systems

Source Systems is a special reference data type that tracks data provenance. Each source system has:
- **System ID** — Unique identifier (GUID)
- **Display Name** — Human-readable name
- **Identification Key** — Additional identifier

The Source Systems view shows usage statistics (how many persons/contracts reference each source system) and can identify unused systems.
