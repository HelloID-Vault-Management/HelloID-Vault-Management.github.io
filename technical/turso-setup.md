# Turso Setup

## What is Turso?

Turso is a cloud-hosted SQLite database accessible via HTTP API. It's ideal for scenarios where you need cloud database access without running a PostgreSQL server.

## Creating a Turso Account

1. Go to [turso.tech](https://turso.tech)
2. Sign up (GitHub login supported)
3. Note your **Organization Slug** (visible in the dashboard URL)

## Creating a Database via the Application

1. Go to **Database Management** in the application sidebar
2. Select **Turso** as the database type
3. In the **Auto-Create Database** section:
   - Enter your **Platform API Token** (Turso dashboard > Settings > API Tokens)
   - Enter your **Organization Slug**
   - Enter a **Database Name** (e.g., `vaultdb`)
4. Click **Create New Database**
5. The application:
   - Creates the database on Turso
   - Waits for it to be ready (up to 5 retries)
   - Fetches the database URL and auth token
   - Tests the connection
6. Click **Save Settings**

## Creating a Database via Turso CLI

```bash
# Install Turso CLI
curl -sSfL https://get.tur.so/install.sh | bash

# Login
turso auth login

# Create database
turso db create vaultdb

# Get URL
turso db show vaultdb --url

# Create auth token
turso db tokens create vaultdb
```

Then enter the URL and token in the application settings.

## Using an Existing Database

1. Enter the **Database URL** (e.g., `libsql://vaultdb-myorg.aws-eu-west-1.turso.io`)
2. Enter the **Auth Token**
3. Click **Test Connection**
4. Click **Save Settings**

## Zombie Database Recovery

Sometimes a Turso database entry exists in the platform but the actual database namespace has been deleted (e.g., from a failed operation). The application detects this:

1. When you click **Create New Database** and the database name already exists
2. The application fetches fresh credentials and tests the connection
3. If the connection fails (404 "Namespace doesn't exist"):
   - The application offers to **delete and recreate** the database
   - Creates a fresh database with the same name
   - Waits for it to be ready

## Upload Retry Logic

When importing to Turso, the application creates a temporary SQLite database locally, then uploads it to Turso. The upload endpoint may not be immediately ready for newly created databases. The application retries:

- **Full import:** 3 attempts with 3-second delays
- **Auto-create:** 5 attempts with 3-second delays
- **Company-only import:** 3 attempts with 3-second delays

## URL Format

The application normalizes Turso URLs:
- `libsql://vaultdb-myorg.turso.io` → `https://vaultdb-myorg.turso.io`
- `https://vaultdb-myorg.turso.io` → unchanged
- `vaultdb-myorg.turso.io` → `https://vaultdb-myorg.turso.io`

The pipeline endpoint is at `{normalized_url}/v2/pipeline`.
