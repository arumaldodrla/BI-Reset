# AI Agent Guide: Metabase Integration

**Objective**: To securely embed the Metabase frontend into the BI Reset UI and configure it for multi-tenancy.

## 1. Deploy Metabase

-   Deploy a self-hosted instance of Metabase (Open Source) on a cloud server. The Pro plan is recommended for production to enable white-labeling and advanced embedding features.
-   Connect the Metabase instance to the Snowflake data warehouse.

## 2. Secure Embedding

-   Metabase embedding will be done using a **signed JWT**. This ensures that users can only see the data they are authorized to see.
-   The BI Reset backend will be responsible for generating the signed JWT.

**Workflow**:

1.  A user in the BI Reset UI attempts to access an embedded Metabase dashboard.
2.  The BI Reset frontend makes a request to the BI Reset backend for a Metabase embedding URL.
3.  The backend generates a JWT that includes:
    -   The user's ID.
    -   The `tenant_id` and `workspace_id` to filter data.
    -   The ID of the dashboard or report to be embedded.
4.  The backend signs the JWT with the Metabase embedding secret key.
5.  The backend returns the signed embedding URL to the frontend.
6.  The frontend renders the Metabase dashboard in an iframe using the provided URL.

## 3. Multi-Tenancy in Metabase

-   While Supabase RLS handles data isolation at the backend level, we will use Metabase's sandboxing feature to enforce multi-tenancy at the visualization layer.
-   A Metabase sandbox will be created for each tenant.
-   The signed JWT will include a parameter that maps the user to their corresponding Metabase sandbox, ensuring they can only access data associated with their tenant.

## 4. White-Labeling

-   If using the Metabase Pro plan, use the white-labeling feature to customize the appearance of the embedded Metabase interface to match the BI Reset branding (e.g., remove the "Powered by Metabase" logo, change colors).
