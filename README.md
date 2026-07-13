# HelloID Vault Management

HelloID Vault Management is a WPF desktop application for anonymizing and managing HR data used by HelloID connectors.

## Features

### Data Management
- **Persons** — Full CRUD with search, status filters, and custom fields
- **Contracts** — Full CRUD with advanced search, 37+ columns, and JSON view
- **Contacts** — Personal and business contacts per person
- **Reference Data** — Departments, Locations, Employers, Cost Centers, Cost Bearers, Teams, Divisions, Titles, Organizations

### Database Support
- **SQLite** — Local file-based database (default)
- **Turso** — Cloud-hosted SQLite via HTTP API
- **Supabase** — Cloud-hosted PostgreSQL

### Import
- **Full Import** — Import all data from vault.json
- **Company Data Import** — Import only reference data + custom field schemas
- **Import with Selection** — Select specific persons to import, with cascade manager support
- **Anonymization** — Replace real data with realistic European names before import

### Performance
- PostgreSQL COPY bulk insert (142s to 14s for 700+ persons)
- Cached FK validation (14,000 queries to 10)
- Temp table + COPY + JOIN UPDATE for custom fields

### Administration
- Custom field schema management
- Primary contract priority rules configuration
- Primary manager recalculation (contract-based or department-based)

## Quick Links

- [Getting Started](guide/getting-started.md)
- [Database Setup](guide/database-setup.md)
- [Importing Data](guide/importing-data.md)
- [Anonymization](guide/anonymization.md)

## Local Preview

To preview this documentation site locally:

```bash
npm i -g docsify-cli
docsify serve docs
```

Then open http://localhost:3000
