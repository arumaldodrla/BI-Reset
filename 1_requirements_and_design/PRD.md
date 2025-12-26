# Product Requirements Document (PRD)

**Project**: BI Reset
**Version**: 1.0
**Date**: December 12, 2025

## 1. Introduction

This Product Requirements Document (PRD) defines the vision, features, and scope for BI Reset. It serves as the guiding document for the project team—including project managers, designers, AI development agents, and quality assurance—to ensure alignment on what is being built and for whom.

## 2. Product Vision & Strategy

BI Reset will democratize data analytics for small and medium-sized enterprises (SMEs) by delivering a powerful, intuitive, and affordable BI solution. The product strategy is centered on three key differentiators:

- **AI-First Experience**: Making natural language the primary means of data interaction.
- **Seamless Multi-Source Integration**: Eliminating data silos by enabling easy connection to and analysis of data from disparate systems.
- **Self-Service Analytics**: Empowering non-technical users to answer their own data questions without relying on data analysts.
- **Simple UX, Powerful Engine**: Delivering a user experience that is clean, intuitive, and requires minimal training, while the underlying platform provides complex, powerful, and feature-rich analytics capabilities.

## 3. Target Audience & User Personas

- **Primary Persona: The Business Decision-Maker (e.g., CEO, Head of Sales, Operations Manager)
  - **Summary**: A non-technical leader who needs high-level, accurate data to make strategic decisions.**
  - **Needs**: High-level dashboards, KPI tracking, ability to ask strategic questions of the data.
  - **Pain Points**: Lack of a unified view of the business, dependence on technical teams for reports, slow access to data.

- **Secondary Persona: The Data-Savvy Business User (e.g., Business Analyst, Marketing Analyst)
  - **Summary**: A hands-on user who is comfortable with data and needs to perform ad-hoc analysis and create custom reports.**
  - **Needs**: Ability to create custom reports, perform ad-hoc analysis, and blend data from different sources.
  - **Pain Points**: Existing tools are too complex, data is not easily accessible, manual data blending in spreadsheets is error-prone.

- **Tertiary Persona: The Administrator (e.g., IT Manager, System Admin)
  - **Summary**: Responsible for the technical management of the platform, including user access, data security, and system integrations.**
  - **Needs**: Easy user management, data source configuration, security and access control.
  - **Pain Points**: Managing multiple BI tools, ensuring data security and compliance, high licensing costs.

## 4. Product Features

### 4.1. P0 - Must-Have Features

| Feature ID | Feature Name | Description | User Stories |
| :--- | :--- | :--- | :--- |
| F01 | **AI-Driven Report Creation** | Users can type questions in natural language (e.g., "What were our top 10 products by revenue in Q3?") and receive a generated chart or table. | As a CEO, I want to ask for my key metrics in plain English so I can get quick answers without needing a data analyst. |
| F02 | **Multi-Source Data Connectivity** | The platform must connect to multiple data sources simultaneously, with initial priority on Zoho (CRM, Books) and SAP Business One. | As a Business Analyst, I want to connect to both our CRM and ERP systems so I can analyze the entire customer lifecycle from lead to invoice. |
| F03 | **Cross-Source Data Joining** | Data from different sources must be joinable within a unified semantic layer. | As an Operations Manager, I want to join sales data from our CRM with inventory data from our ERP to understand stock turnover rates. |
| F04 | **Visual Report Builder** | A drag-and-drop interface for creating reports, including charts (bar, line, pie), tables, and pivot tables. | As a Marketing Analyst, I want to build a custom report by dragging and dropping fields so I can visualize campaign performance. |
| F05 | **Interactive Dashboards** | Users can combine multiple reports and KPIs into a single dashboard with global filters and drill-down capabilities. | As a Head of Sales, I want to create a dashboard that shows my team's performance at a glance, with the ability to filter by region and salesperson. |
| F06 | **Secure Multi-Tenancy** | The platform must support multiple customer tenants, with strict data isolation between them. Each tenant can have multiple workspaces. | As an Administrator, I want to create separate, isolated environments for each of our clients to ensure their data is secure. |
| F07 | **User & Access Management** | Admins can invite users, assign roles (Admin, Editor, Viewer), and control access to data sources, reports, and dashboards. | As an Administrator, I want to grant read-only access to our executive team so they can view dashboards but not edit them. |

### 4.2. P1 - Should-Have Features

| Feature ID | Feature Name | Description | User Stories |
| :--- | :--- | :--- | :--- |
| F08 | **Data Export** | Users can export reports and dashboards to common formats, including CSV, XLSX, and PDF. | As a Business Analyst, I want to export a report to Excel so I can perform further analysis or share it with stakeholders. |
| F09 | **Dashboard Embedding** | Dashboards can be securely embedded in other applications using iframes or a JavaScript SDK. | As a Product Manager, I want to embed a customer usage dashboard directly into our internal admin panel. |
| F10 | **API Access** | A RESTful API for programmatic interaction with the platform (e.g., managing users, triggering data syncs, querying reports). | As a Developer, I want to use an API to automatically create new user accounts when they sign up for our main application. |
| F11 | **Internationalization (i18n)** | The user interface must support multiple languages. The initial launch will include English (default) and Spanish. The architecture must support adding new languages easily with AI-assisted translation. | As a user in Mexico, I want to use the platform in Spanish so I can understand all the features and options. |

| F12 | **Automated Self-Maintenance** | The platform will include a weekly process to self-review its codebase, identify potential bugs or areas for minor improvement, and automatically apply patches. Major updates will be flagged for human review. | As an Administrator, I want the system to handle routine maintenance automatically so I can focus on strategic tasks. |

### 4.3. P2 - Could-Have Features (Future Scope)

| Feature ID | Feature Name | Description |
| :--- | :--- | :--- |
| F11 | **Scheduled Reports & Alerts** | Automatically send reports via email or Slack on a schedule or when certain data thresholds are met. |
| F12 | **Advanced Chart Types** | Support for more complex visualizations like heatmaps, treemaps, and geospatial maps. |
| F13 | **Community Connector Marketplace** | Allow third-party developers to build and share their own data source connectors. |

## 5. Non-Functional Requirements

- **Performance**: Queries should return results within 10 seconds for typical use cases. Dashboards should load in under 5 seconds.
- **Scalability**: The platform must be able to support hundreds of concurrent users and data volumes up to several terabytes.
- **Security**: All data must be encrypted at rest and in transit. The platform must comply with GDPR and CCPA standards.
- **Reliability**: The system should have an uptime of 99.9%.
- **Usability**: The user interface should be intuitive and require minimal training for non-technical users.

## 6. Assumptions & Dependencies

- **Core Principle**: The project will be developed **100% by AI agents** using frameworks like Google Antigravity, with supervision from a non-technical human team. All documentation and specifications are written to support this model.
- **Assumption**: The hybrid architecture (Metabase + data warehouse) is the chosen path.
- **Dependency**: Access to a cloud data warehouse (e.g., Snowflake) is required for the multi-source join functionality.
- **Dependency**: Access to OpenAI (or a similar LLM) API is required for the AI-powered query feature.

