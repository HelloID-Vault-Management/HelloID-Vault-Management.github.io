# Managing Persons

Go to **Persons** in the sidebar.

## Browsing Persons

- The left panel shows a searchable list of persons
- The right panel shows details for the selected person
- Use the search box to find persons by name, external ID, or UUID
- Filter by status: **All / Past / Active / Future**

## Person Detail View

The person detail view has three tabs:

| Tab | Content |
|-----|---------|
| **Information** (Ctrl+1) | General info, personal details, name, contact info, primary contract, custom fields |
| **Contracts** (Ctrl+2) | List of contracts with add/edit/delete |
| **Contacts** (Ctrl+3) | Personal and business contacts |

## Adding a Person

1. Click **Add Person** in the person detail panel
2. Fill in the form:
   - **Display name** (required)
   - **External ID** — Employee number or identifier
   - **Username** — Login name
   - **Source** (required) — Which system this person comes from
   - **Gender** — M, F, or X
   - **Manager** — Click **Search** to find and select a manager
   - Name details, birth date, marital status, etc.
3. Click **Save**

## Editing a Person

1. Select a person from the list
2. Click **Edit Person** in the detail panel
3. Modify the fields
4. Click **Save**

## Deleting a Person

1. Select a person from the list
2. Click **Delete Person**
3. Confirm the deletion

> **Note:** Deleting a person also deletes their contracts and contacts (cascade delete).

## Manager Search

The manager field uses a read-only TextBox with a **Search** button:

1. Click **Search** to open the popup
2. Type at least 2 characters (name, external ID, or username)
3. Search runs automatically after 300ms debounce
4. **Double-click** a result or select + press **Enter**
5. The selected manager's name appears in the read-only TextBox
6. Click **Clear** to remove the manager

### Stale Manager References

If a person has a manager reference to someone not in the database (e.g., from a partial import), the manager field appears empty when editing. Saving the person clears the stale reference automatically.
