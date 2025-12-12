# Product Requirements Document (PRD)

**Project**: BI Reset
**Version**: 1.0
**Date**: December 12, 2025

## 1. Introduction

This document outlines the product requirements for BI Reset, an AI-first, multi-source business intelligence platform. The target audience for this document includes project managers, designers, developers (including AI agents), and QA teams.

## 2. Product Vision & Strategy

BI Reset aims to democratize data analytics for small to medium-sized enterprises (SMEs) by providing a powerful, intuitive, and affordable BI solution. Our strategy is to differentiate through:

- **AI-First Experience**: Making natural language the primary means of data interaction.
- **Seamless Multi-Source Integration**: Eliminating data silos by enabling easy connection to and analysis of data from disparate systems.
- **Self-Service Analytics**: Empowering non-technical users to answer their own data questions without relying on data analysts.

## 3. Target Audience & User Personas

- **Primary Persona: The Business Decision-Maker (e.g., CEO, Head of Sales, Operations Manager)**
  - **Needs**: High-level dashboards, KPI tracking, ability to ask strategic questions of the data.
  - **Pain Points**: Lack of a unified view of the business, dependence on technical teams for reports, slow access to data.

- **Secondary Persona: The Data-Savvy Business User (e.g., Business Analyst, Marketing Analyst)**
  - **Needs**: Ability to create custom reports, perform ad-hoc analysis, and blend data from different sources.
  - **Pain Points**: Existing tools are too complex, data is not easily accessible, manual data blending in spreadsheets is error-prone.

- **Tertiary Persona: The Administrator (e.g., IT Manager, System Admin)**
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

- **Assumption**: The project will be developed entirely by AI agents, supervised by a human project manager.
- **Assumption**: The hybrid architecture (Metabase + data warehouse) is the chosen path.
- **Dependency**: Access to a cloud data warehouse (e.g., Snowflake) is required for the multi-source join functionality.
- **Dependency**: Access to OpenAI (or a similar LLM) API is required for the AI-powered query feature.

