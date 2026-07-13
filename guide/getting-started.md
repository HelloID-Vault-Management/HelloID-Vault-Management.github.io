# Getting Started

## Prerequisites

- Windows 10/11 with .NET 8.0 Desktop Runtime
- OR build from source with .NET 8.0 SDK

## Installation

### Option 1: Download Release

1. Go to [Releases](https://github.com/mc303/HelloID.Vault.Management/releases)
2. Download the latest ZIP for your architecture (x64 or x86)
3. Extract and run `HelloID.Vault.Management.exe`

### Option 2: Build from Source

```bash
git clone https://github.com/mc303/HelloID.Vault.Management.git
cd HelloID.Vault.Management
dotnet build HelloID.Vault.Management.sln
dotnet run --project src/HelloID.Vault.Management/HelloID.Vault.Management.csproj
```

## First Run

1. The application starts with **SQLite** as the default database type
2. A local database file is created automatically on first import
3. Go to **Database Management** in the sidebar to configure a different database
4. Go to **Import Data** to import your `vault.json` file

## Next Steps

- [Database Setup](database-setup.md) — Configure SQLite, Turso, or Supabase
- [Importing Data](importing-data.md) — Import and anonymize your data
- [Managing Persons](managing-persons.md) — Add, edit, and manage persons
