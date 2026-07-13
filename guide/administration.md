# Administration

The Administration menu contains three tools.

## Custom Fields

Manage custom field schemas for persons and contracts.

### Viewing Custom Fields

1. Go to **Administration > Custom Fields**
2. View all custom field definitions in the DataGrid
3. Filter by table: **All / Persons / Contracts**
4. Use the search box to find specific fields

### Adding a Custom Field

1. Click **Add**
2. Select table: **persons** or **contracts**
3. Enter **Field Key** (the JSON property name, e.g., `employeeCode`)
4. Enter **Display Name** (shown in UI, e.g., `Employee Code`)
5. Set **Sort Order** (for display ordering)
6. Optionally enter **Help Text**
7. Click **Save**

### Editing/Deleting

- Right-click > **Edit** to modify
- Right-click > **Delete** to remove

Custom field values are stored as JSON in the `custom_fields` column and displayed in the contract JSON view.

## Primary Contract Configuration

Configure which contract is considered the "primary" contract for each person.

### How It Works

When a person has multiple contracts, the primary contract is determined by priority rules:
1. **Contract Status** — Active > Future > Past > No Dates (always first priority)
2. **Configured fields** — Additional fields like FTE, Sequence, Start Date, etc.

### Configuring Rules

1. Go to **Administration > Primary Contract**
2. The default field is **Contract Status** (cannot be removed)
3. Add fields from the dropdown (FTE, Hours Per Week, Sequence, Start Date, End Date)
4. For each field:
   - Toggle **Ascending** or **Descending** sort
   - Check **Active** to include in priority
   - Use **Move Up/Down** to reorder
5. Click **Save**
6. Click **Update Contract Cache** to recalculate all contract statuses

### Preview

Click **Preview** to see how the configured rules affect actual data. This shows a sample of persons and which contract is selected as primary for each.

## Primary Manager Administration

Calculate and refresh the primary manager for all persons.

### Viewing Statistics

- **Total Persons** / **With Manager** / **Without Manager**
- **Source Distribution**: Contract-Based, Department-Based, From JSON

### Refresh All Primary Managers

1. Choose logic: **Contract-Based** or **Department-Based**
2. Click **Refresh All Primary Managers**
3. This overwrites all existing primary manager values

> **Warning:** This operation overwrites all existing primary manager values. Use with caution.

### Recalculate Using Primary Contract Rules

Click **Recalculate Using Primary Contract Rules** to apply the configured Primary Contract priority rules to determine each person's primary manager.

This uses the primary contract (determined by the rules configured in Primary Contract Configuration) and extracts the manager from that contract.
