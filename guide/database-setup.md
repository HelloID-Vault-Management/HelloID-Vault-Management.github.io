# Database Setup

The application supports three database types. Go to **Database Management** in the sidebar to configure your database.

## SQLite (Local)

SQLite is the default database type. No server or account is needed.

1. Select **SQLite** as the database type
2. Choose a database file path (or browse for an existing `.db` file)
3. Click **Save Settings**

The database file and schema are created automatically on first import.

## Supabase (PostgreSQL)

Supabase provides a cloud-hosted PostgreSQL database.

1. Create a project at [supabase.com](https://supabase.com)
2. Go to **Settings > Database** in your Supabase project
3. Copy the connection string
4. In the application, select **Supabase** as the database type
5. Paste the connection string into the **Connection String** field
   - You can use either the key-value format or a `postgresql://` URI
6. Optionally enter your Supabase Project URL
7. Click **Test Connection** to verify
8. Click **Save Settings**

The schema is created automatically on first import.

## Turso (Cloud SQLite)

Turso provides cloud-hosted SQLite databases accessible via HTTP API.

### Create a New Database

1. Create an account at [turso.tech](https://turso.tech)
2. In the application, select **Turso** as the database type
3. Go to the **Auto-Create Database** section
4. Enter your Turso **Platform API Token** (from Turso dashboard > Settings)
5. Enter your **Organization Slug** (e.g., `myorg`)
6. Enter a **Database Name** (e.g., `vaultdb`)
7. Click **Create New Database**
8. The application creates the database and fetches the URL and auth token automatically
9. Click **Save Settings**

### Use an Existing Database

1. Enter the **Database URL** (e.g., `libsql://vaultdb-myorg.aws-eu-west-1.turso.io`)
2. Enter the **Auth Token** (from Turso dashboard > your database > Settings > Tokens)
3. Click **Test Connection** to verify
4. Click **Save Settings**

### Zombie Database Recovery

If a Turso database entry exists but the actual database namespace has been deleted (e.g., from a previous failed operation), the application detects this and offers to **delete and recreate** the database automatically.

## Switching Database Types

> **Warning:** Switching database types requires an application restart. Data is NOT migrated between database types — you need to re-import your data.
