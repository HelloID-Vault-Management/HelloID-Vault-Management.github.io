# Managing Contracts

Contracts are managed from two places: the **Contracts** view and the person detail **Contracts** tab.

## Adding a Contract

1. Select a person (either from Persons view or Contracts view)
2. Click **Add Contract**
3. Fill in the form:

| Field | Description |
|-------|-------------|
| **External ID** | Auto-generated as `{PersonID}~{GUID}` |
| **Start Date** | Contract start (defaults to today) |
| **End Date** | Contract end (leave empty for open-ended) |
| **Type Code** | E.g., "1" |
| **Type Description** | E.g., "Personeelslid" |
| **FTE** | Full-time equivalent (e.g., 1.0, 0.8) |
| **Hours Per Week** | Working hours per week |
| **Percentage** | Employment percentage |
| **Sequence** | Contract sequence number |
| **Manager** | Click **Search** to find and select a manager |
| **Department** | Dropdown (filtered by source) |
| **Location** | Dropdown |
| **Employer** | Dropdown |
| **Title** | Dropdown |
| **Cost Center** | Dropdown |
| **Cost Bearer** | Dropdown |
| **Team** | Dropdown |
| **Division** | Dropdown |
| **Organization** | Dropdown |

4. Click **Save**

## Editing a Contract

1. Go to the person's **Contracts** tab, or use the **Contracts** view
2. Double-click a contract or right-click > **Edit**
3. Modify the fields
4. Click **Save**

## Viewing Contract Details (JSON)

1. In the Contracts view, **double-click** any contract row
2. A window opens showing the contract data formatted as JSON
3. This matches the vault.json structure, including:
   - Context, External ID, Start/End Date
   - Type, Details (FTE, hours, percentage, sequence)
   - Location, Cost Center, Cost Bearer, Employer
   - Manager (with email from contacts)
   - Team, Department, Division, Title, Organization
   - Custom fields (as a `"custom": {}` object)

## Searching and Filtering Contracts

### Quick Search

Use the search box at the top to search across all fields.

### Advanced Search

1. Click **Advanced Search**
2. Add filter rows:
   - Select a **Field** (e.g., Department, FTE, Start Date)
   - Select an **Operator** (equals, contains, greater than, etc.)
   - Enter a **Value**
3. Add multiple filters as needed
4. Click **Apply Filters**

### Column Visibility

1. Click **Columns**
2. Check/uncheck columns to show/hide
3. 37+ columns available including all reference data fields
4. Use **Select All** or **Hide Empty Columns** for quick adjustments

### Status Filters

- **All** — Show all contracts
- **Past** — Contracts with end date before today
- **Active** — Contracts currently active (start ≤ today, end ≥ today or null)
- **Future** — Contracts with start date after today

## Deleting a Contract

1. Right-click a contract row
2. Select **Delete**
3. Confirm the deletion
