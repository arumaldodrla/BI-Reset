# AI Agent Guide: Backend Setup

**Objective**: To set up the Supabase backend, including the database schema, multi-tenancy, and authentication.

## 1. Initialize Supabase Project

-   Create a new Supabase project.
-   Enable the following Supabase extensions: `pgaudit`, `pg_stat_statements`.

## 2. Database Schema

Create the following tables in the `public` schema. All tables must include a `tenant_id` column for multi-tenancy.

### `tenants`

| Column | Type | Constraints |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `uuid_generate_v4()` |
| `name` | `text` | Not Null |

### `users`

-   This table is automatically created by Supabase Auth. You will need to add a `tenant_id` column to it.

### `workspaces`

| Column | Type | Constraints |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `uuid_generate_v4()` |
| `tenant_id` | `uuid` | Foreign Key -> `tenants.id` |
| `name` | `text` | Not Null |

### `data_sources`

| Column | Type | Constraints |
| :--- | :--- | :--- |
| `id` | `uuid` | Primary Key, Default: `uuid_generate_v4()` |
| `workspace_id` | `uuid` | Foreign Key -> `workspaces.id` |
| `name` | `text` | Not Null |
| `type` | `text` | e.g., 'zoho', 'sap_b1' |
| `credentials` | `text` | Encrypted |

## 3. Multi-Tenancy & RLS

-   Enable Row-Level Security (RLS) on all tables.
-   Create a policy on each table that restricts access to rows matching the user's `tenant_id`.

**Example RLS Policy for `workspaces`**:

```sql
CREATE POLICY "Enable access for users based on tenant_id" ON "public"."workspaces"
AS PERMISSIVE FOR ALL
TO public
USING ( (auth.uid() IN ( SELECT users.id
   FROM users
  WHERE (users.tenant_id = workspaces.tenant_id))) );
```

## 4. Authentication

-   Configure Supabase Auth to use email/password authentication.
-   Enable OAuth providers for Google and GitHub.

## 5. Storage

-   Create a Supabase Storage bucket named `uploads`.
-   Configure RLS policies on the bucket to ensure users can only upload to a folder corresponding to their `tenant_id`.
