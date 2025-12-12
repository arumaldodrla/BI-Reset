# AI Agent Guide: Frontend Setup

**Objective**: To initialize the Refine frontend application with the Metronic admin template and connect it to the Supabase backend.

## 1. Initialize Refine Application

-   Use the `create-refine-app` CLI to bootstrap a new Refine project.
-   Choose the following options:
    -   **Project Name**: `bi-reset-frontend`
    -   **UI Framework**: Tailwind CSS
    -   **Backend**: Supabase

## 2. Integrate Metronic Template

-   Purchase and download the Metronic admin template.
-   Integrate the Metronic assets (CSS, JS, fonts) into the Refine application.
-   Replace the default Refine layout with a layout based on the Metronic theme.
-   Create a custom `Layout` component that includes the Metronic sidebar, header, and footer.

## 3. Connect to Supabase

-   In the Refine application, configure the Supabase data provider with your Supabase project URL and `anon` key.
-   Set up the Supabase auth provider to handle user login, registration, and session management.

## 4. Routing

-   Set up the following routes in the application:
    -   `/login`: The login page.
    -   `/`: The main dashboard/home screen.
    -   `/ai-analyst`: The AI chat interface.
    -   `/reports`: The report builder (embedded Metabase).
    -   `/dashboards`: The dashboard viewer.
    -   `/admin/users`: User management page.
    -   `/admin/data-sources`: Data source management page.

## 5. State Management

-   Use a state management library like Zustand or Redux Toolkit to manage global application state (e.g., the current user, selected workspace).
