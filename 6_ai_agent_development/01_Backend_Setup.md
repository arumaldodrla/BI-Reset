# AI Agent Guide: Backend Setup

**Objective**: To set up the Supabase backend, including the complete database schema, multi-tenancy via Row-Level Security (RLS), and authentication.

---

## 1. Prerequisites

Before starting, ensure you have the following:

-   A Supabase account and a new project created.
-   The Supabase project URL and `anon` key.
-   Access to the Supabase SQL Editor.

## 2. Initialize Supabase Project

Navigate to the Supabase dashboard for your project and enable the following extensions via the SQL Editor:

```sql
-- Enable UUID generation
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";

-- Enable audit logging (optional but recommended)
CREATE EXTENSION IF NOT EXISTS "pgaudit";

-- Enable query statistics (optional but recommended)
CREATE EXTENSION IF NOT EXISTS "pg_stat_statements";
```

## 3. Database Schema

Execute the following SQL statements in the Supabase SQL Editor to create the complete database schema. This schema is designed for multi-tenancy, with all core tables linked to a `tenant_id`.

### 3.1. `tenants` Table

Stores information about each customer organization.

```sql
CREATE TABLE public.tenants (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    name TEXT NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

COMMENT ON TABLE public.tenants IS 'Stores customer tenant organizations.';
```

### 3.2. `profiles` Table (User Extension)

This table extends the built-in `auth.users` table to link users to a tenant. A trigger will automatically create a profile when a new user signs up.

```sql
CREATE TABLE public.profiles (
    id UUID PRIMARY KEY REFERENCES auth.users(id) ON DELETE CASCADE,
    tenant_id UUID REFERENCES public.tenants(id) ON DELETE SET NULL,
    full_name TEXT,
    avatar_url TEXT,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

COMMENT ON TABLE public.profiles IS 'Extends auth.users with tenant association and profile data.';

-- Function to create a profile on user signup
CREATE OR REPLACE FUNCTION public.handle_new_user()
RETURNS TRIGGER AS $$
BEGIN
    INSERT INTO public.profiles (id, full_name, avatar_url)
    VALUES (NEW.id, NEW.raw_user_meta_data->>'full_name', NEW.raw_user_meta_data->>'avatar_url');
    RETURN NEW;
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;

-- Trigger to call the function on new user creation
CREATE TRIGGER on_auth_user_created
    AFTER INSERT ON auth.users
    FOR EACH ROW EXECUTE FUNCTION public.handle_new_user();
```

### 3.3. `workspaces` Table

A tenant can have multiple workspaces to isolate projects or departments.

```sql
CREATE TABLE public.workspaces (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    tenant_id UUID NOT NULL REFERENCES public.tenants(id) ON DELETE CASCADE,
    name TEXT NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

COMMENT ON TABLE public.workspaces IS 'Logical containers for data sources and reports within a tenant.';
```

### 3.4. `workspace_members` Table

A join table to manage user roles within workspaces.

```sql
CREATE TYPE public.workspace_role AS ENUM ('admin', 'editor', 'viewer');

CREATE TABLE public.workspace_members (
    workspace_id UUID NOT NULL REFERENCES public.workspaces(id) ON DELETE CASCADE,
    user_id UUID NOT NULL REFERENCES public.profiles(id) ON DELETE CASCADE,
    role public.workspace_role NOT NULL DEFAULT 'viewer',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    PRIMARY KEY (workspace_id, user_id)
);

COMMENT ON TABLE public.workspace_members IS 'Manages user membership and roles within workspaces.';
```

### 3.5. `data_sources` Table

Stores connection information for each data source configured in a workspace.

```sql
CREATE TYPE public.data_source_type AS ENUM ('zoho_crm', 'zoho_books', 'sap_b1', 'postgresql', 'csv');
CREATE TYPE public.data_source_status AS ENUM ('pending', 'connected', 'syncing', 'error');

CREATE TABLE public.data_sources (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    workspace_id UUID NOT NULL REFERENCES public.workspaces(id) ON DELETE CASCADE,
    name TEXT NOT NULL,
    type public.data_source_type NOT NULL,
    -- Credentials are stored encrypted. Use Supabase Vault in production.
    credentials_encrypted TEXT,
    status public.data_source_status NOT NULL DEFAULT 'pending',
    last_synced_at TIMESTAMP WITH TIME ZONE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

COMMENT ON TABLE public.data_sources IS 'Stores configuration for connected data sources.';
```

### 3.6. `semantic_layer_columns` Table

Stores the business-friendly metadata for columns that the LLM will use to generate queries.

```sql
CREATE TABLE public.semantic_layer_columns (
    id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
    data_source_id UUID NOT NULL REFERENCES public.data_sources(id) ON DELETE CASCADE,
    table_name TEXT NOT NULL,
    column_name TEXT NOT NULL,
    display_name TEXT,
    description TEXT,
    is_dimension BOOLEAN NOT NULL DEFAULT FALSE,
    is_measure BOOLEAN NOT NULL DEFAULT FALSE,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT NOW(),
    UNIQUE (data_source_id, table_name, column_name)
);

COMMENT ON TABLE public.semantic_layer_columns IS 'Metadata for the semantic layer, used by the LLM for query generation.';
```

## 4. Multi-Tenancy & Row-Level Security (RLS)

Enable RLS on all tables and create policies to ensure data isolation between tenants. Users can only access data belonging to their own tenant.

```sql
-- Enable RLS on all tables
ALTER TABLE public.tenants ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.profiles ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.workspaces ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.workspace_members ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.data_sources ENABLE ROW LEVEL SECURITY;
ALTER TABLE public.semantic_layer_columns ENABLE ROW LEVEL SECURITY;

-- Helper function to get the current user's tenant_id
CREATE OR REPLACE FUNCTION public.get_my_tenant_id()
RETURNS UUID AS $$
    SELECT tenant_id FROM public.profiles WHERE id = auth.uid();
$$ LANGUAGE sql SECURITY DEFINER STABLE;

-- RLS Policy for tenants: Users can only see their own tenant.
CREATE POLICY "Users can view their own tenant" ON public.tenants
    FOR SELECT USING (id = public.get_my_tenant_id());

-- RLS Policy for profiles: Users can only see profiles in their tenant.
CREATE POLICY "Users can view profiles in their tenant" ON public.profiles
    FOR SELECT USING (tenant_id = public.get_my_tenant_id());
CREATE POLICY "Users can update their own profile" ON public.profiles
    FOR UPDATE USING (id = auth.uid());

-- RLS Policy for workspaces: Users can only see workspaces in their tenant.
CREATE POLICY "Users can view workspaces in their tenant" ON public.workspaces
    FOR SELECT USING (tenant_id = public.get_my_tenant_id());

-- RLS Policy for workspace_members: Users can only see members in their tenant's workspaces.
CREATE POLICY "Users can view workspace members in their tenant" ON public.workspace_members
    FOR SELECT USING (
        workspace_id IN (SELECT id FROM public.workspaces WHERE tenant_id = public.get_my_tenant_id())
    );

-- RLS Policy for data_sources: Users can only see data sources in their tenant's workspaces.
CREATE POLICY "Users can view data sources in their tenant" ON public.data_sources
    FOR SELECT USING (
        workspace_id IN (SELECT id FROM public.workspaces WHERE tenant_id = public.get_my_tenant_id())
    );

-- RLS Policy for semantic_layer_columns: Users can only see columns for their tenant's data sources.
CREATE POLICY "Users can view semantic layer columns in their tenant" ON public.semantic_layer_columns
    FOR SELECT USING (
        data_source_id IN (
            SELECT ds.id FROM public.data_sources ds
            JOIN public.workspaces w ON ds.workspace_id = w.id
            WHERE w.tenant_id = public.get_my_tenant_id()
        )
    );
```

## 5. Authentication

In the Supabase dashboard, navigate to **Authentication > Providers** and enable the following:

-   **Email**: Enable email/password sign-up.
-   **Google**: Configure with your Google Cloud OAuth credentials.
-   **GitHub**: Configure with your GitHub OAuth App credentials.

## 6. Storage

In the Supabase dashboard, navigate to **Storage** and create a new bucket:

-   **Bucket Name**: `uploads`
-   **Public**: No (private bucket)

Then, apply an RLS policy to the bucket to ensure users can only upload to a folder corresponding to their `tenant_id`. This can be done via the Supabase dashboard or SQL.
