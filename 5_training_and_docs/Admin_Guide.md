# BI Reset Admin Guide

This guide is for administrators of the BI Reset platform. It covers user management, data source configuration, and other administrative tasks.

## 1. User Management

As an administrator, you can manage users within your tenant.

### 1.1. Inviting Users

1.  Navigate to the **Admin** section and select **Users**.
2.  Click the **Invite User** button.
3.  Enter the user's email address and select a role (Admin, Editor, or Viewer).
4.  The user will receive an email invitation to join the platform.

### 1.2. Managing User Roles

You can change a user's role at any time from the **Users** page. Simply find the user in the list and select a new role from the dropdown menu.

## 2. Data Source Management

You are responsible for connecting BI Reset to your company's data sources.

1.  Navigate to the **Admin** section and select **Data Sources**.
2.  Click **New Data Source**.
3.  Select the type of data source you want to connect to (e.g., Zoho, SAP Business One, PostgreSQL).
4.  Enter the required connection details (e.g., server address, username, password, API key). All credentials are encrypted.
5.  Click **Save**. The system will test the connection and then begin the initial data sync.

## 3. Semantic Layer

While the initial setup of the semantic layer is a technical task performed during the platform's implementation, administrators can manage certain aspects of it.

-   **Hiding Fields**: You can hide sensitive or irrelevant fields from business users in the Metabase admin settings.
-   **Renaming Fields**: You can change the display name of fields to be more user-friendly (e.g., renaming `cust_id` to `Customer ID`).

## 4. Security & Access Control

-   **Workspaces**: You can create different workspaces to organize reports and dashboards (e.g., by department). You can then grant users access to specific workspaces.
-   **Row-Level Security (RLS)**: RLS is configured at the database level to restrict user access to specific rows of data. This is typically set up during the initial implementation, but you can work with your technical team to adjust the policies if needed.
