# Importing Data

Data is imported from a `vault.json` file. Go to **Import Data** in the sidebar.

## Full Import

Imports all data from the vault.json: persons, contracts, contacts, departments, and all reference data.

1. Click **Browse** and select your `vault.json` file
2. Choose a **Primary Manager Logic**:
   - **From JSON** — Use manager values as-is from the file
   - **Contract-Based** — Use the primary contract's manager
   - **Department-Based** — Use the department's manager
3. Optionally enable **Anonymize data before import** (see [Anonymization](anonymization.md))
4. Click **Import**

### When Database Has Existing Data

If the database already has data, you'll be asked to choose:

| Option | Description |
|--------|-------------|
| **Backup and Overwrite** | Creates a timestamped backup, then replaces all data |
| **Overwrite Without Backup** | Deletes all data and imports fresh |
| **Cancel** | Aborts the import |

## Import Company Data

Imports only reference data (departments, locations, employers, cost centers, teams, divisions, titles, organizations) and custom field schemas. No persons or contracts are imported.

This is useful when you want to set up the organizational structure before importing persons.

## Import with Selection

Imports all company data plus only the persons you select.

1. Select your `vault.json` file
2. Click **Import with Selection**
3. A popup appears with all persons from the file:
   - Use the **search box** to filter by name or external ID
   - Check/uncheck persons to select them
   - Use **Select All** or **Deselect All** for convenience
4. Choose import options:
   - **Also import referenced managers (cascade)** — Recursively imports persons who are referenced as managers by your selected persons
   - **Clear manager references for persons not imported** — Sets manager references to NULL if the referenced person was not imported
5. Click **Import Selected**

### How Cascade Import Works

When cascade is enabled:
1. Start with your selected persons
2. For each person, look up their manager references (primary manager + contract managers)
3. If a referenced manager is not already selected, add them
4. Repeat recursively until no new managers are found
5. Import the expanded set

Circular references are handled automatically (person A → manager B → manager A stops the loop).

## Import Results

After import, a results grid shows counts for all imported data types:

- Persons, Contracts, Contacts
- Departments (+ auto-created)
- Organizations, Locations, Employers
- Cost Centers, Cost Bearers, Teams, Divisions, Titles
- Custom Field Schemas (Persons/Contracts)
- Empty Manager GUIDs Fixed
