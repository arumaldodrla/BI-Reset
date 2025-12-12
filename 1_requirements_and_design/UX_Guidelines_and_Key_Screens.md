# UX Guidelines & Key Screens

**Project**: BI Reset
**Version**: 1.0
**Date**: December 12, 2025

## 1. UX Principles

- **Simplicity & Clarity**: The UI should be clean, uncluttered, and intuitive. Avoid jargon and complex configurations wherever possible.
- **AI-First, Human-Friendly**: While AI is the core engine, the user should always feel in control. Provide clear feedback and allow for manual overrides.
- **Consistency**: Maintain a consistent design language across the entire platform, leveraging the Metronic template as a base.
- **Efficiency**: Design workflows to minimize clicks and streamline common tasks like creating reports and adding filters.

## 2. Visual Design & Branding

- **Color Palette**: Primary colors should be professional and accessible. Use the default Metronic color scheme as a starting point, with the ability to customize for white-labeling.
- **Typography**: Use clear, legible fonts. The default font family from the Metronic template (e.g., Inter, Poppins) is approved.
- **Iconography**: Use a consistent set of icons, preferably from a single library like Font Awesome, which is integrated with Metronic.

## 3. Key Screens & Wireframes

This section provides conceptual wireframes for the key screens of the BI Reset application. These are not final designs but serve as a guide for the AI development agents.

### 3.1. Login Screen

- **Description**: A clean, simple login page.
- **Components**:
  - Email and password fields.
  - "Sign In" button.
  - Links for "Forgot Password?" and "Sign Up".
  - OAuth buttons for Google and GitHub.

```
+---------------------------------------+
|                                       |
|               BI Reset                |
|                                       |
|  Email: [_________________________]   |
|                                       |
|  Password: [______________________]   |
|                                       |
|              [ Sign In ]              |
|                                       |
|      --- Or sign in with ---          |
|                                       |
|      [ Google ]  [ GitHub ]           |
|                                       |
|  Forgot Password?  |  Sign Up         |
+---------------------------------------+
```

### 3.2. Main Dashboard / Home Screen

- **Description**: The landing page after login, showing a user's favorite dashboards and recent reports.
- **Components**:
  - Main navigation sidebar (Dashboards, Reports, AI Chat, Admin).
  - Search bar.
  - A grid of dashboard/report cards.

```
+--------------------------------------------------------------------+
| [Nav] |  Search: [________________________________]   [User Profile] |
|-------+------------------------------------------------------------|
|       |                                                            |
| Dash..|  My Dashboards                                             |
|       |                                                            |
| Rep...|  +-----------+  +-----------+  +-----------+               |
|       |  | Dash 1    |  | Dash 2    |  | Dash 3    |               |
| AI....|  +-----------+  +-----------+  +-----------+               |
|       |                                                            |
| Admin |  Recent Reports                                            |
|       |                                                            |
|       |  - Report A                                                |
|       |  - Report B                                                |
+--------------------------------------------------------------------+
```

### 3.3. AI Chat Interface

- **Description**: The primary interface for the AI-powered query engine.
- **Components**:
  - Chat history panel.
  - Text input for natural language queries.
  - A display area where the generated chart or table appears.
  - Options to save the generated report or ask a follow-up question.

```
+--------------------------------------------------------------------+
| [Nav] |  AI Analyst                                                  |
|-------+------------------------------------------------------------|
|       |                                                            |
|       |  [Chat History]  |  User: Show me sales by country.         |
|       |                  |                                          |
|       |                  |  AI: Here are your sales by country:     |
|       |                  |                                          |
|       |                  |  +-----------------------------------+   |
|       |                  |  |        [ Bar Chart ]          |   |
|       |                  |  +-----------------------------------+   |
|       |                  |                                          |
|       |                  |  [__________________________________]    |
|       |                  |  Type your question...                   |
+--------------------------------------------------------------------+
```

### 3.4. Report Builder (Embedded Metabase)

- **Description**: The embedded Metabase interface for creating and editing reports.
- **Components**: This will be the standard Metabase query builder UI, which includes:
  - Data source and table selector.
  - Field selection for measures and dimensions.
  - Filtering, summarizing, and sorting options.
  - Visualization type selector.

### 3.5. Admin - Data Sources

- **Description**: A page for administrators to manage data source connections.
- **Components**:
  - A list of existing data sources.
  - A "New Data Source" button.
  - A form for adding a new data source, with fields for name, type, and credentials.

```
+--------------------------------------------------------------------+
| [Nav] |  Admin > Data Sources                                      |
|-------+------------------------------------------------------------|
|       |                                                            |
|       |  [+ New Data Source]                                       |
|       |                                                            |
|       |  - Zoho CRM (Connected)         [ Edit ] [ Delete ]        |
|       |  - SAP Business One (Connected) [ Edit ] [ Delete ]        |
|       |  - PostgreSQL (Connected)       [ Edit ] [ Delete ]        |
|       |                                                            |
+--------------------------------------------------------------------+
```
