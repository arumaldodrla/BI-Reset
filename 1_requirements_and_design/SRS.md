# System Requirements Specification (SRS)

**Project**: BI Reset
**Version**: 1.0
**Date**: December 12, 2025

## 1. Introduction

This document provides a detailed description of the system requirements for the BI Reset platform. It is intended for the development team (including AI agents), architects, and QA engineers.

## 2. System Overview

BI Reset is a web-based, multi-tenant, AI-powered business intelligence platform. It follows a hybrid architecture, leveraging Metabase for visualization and a custom backend built on Supabase and Snowflake for data integration and AI processing. The system is designed to be accessed via a modern web browser.

## 3. Functional Requirements

### 3.1. User Authentication & Authorization

- **SYS-001**: The system shall use Supabase Auth for user authentication.
- **SYS-002**: Users shall be able to register and log in using email/password and OAuth providers (Google, GitHub).
- **SYS-003**: The system shall support the following user roles:
  - **Admin**: Full control over the tenant, including user management, data source configuration, and billing.
  - **Editor**: Can create, edit, and delete reports and dashboards within their assigned workspaces.
  - **Viewer**: Can view reports and dashboards they have been given access to, but cannot edit or create them.
- **SYS-004**: Access control shall be enforced using Supabase Row-Level Security (RLS) to ensure data isolation between tenants and workspaces.

### 3.2. Data Source Management

- **SYS-005**: Admins shall be able to add, edit, and remove data source connections through the UI.
- **SYS-006**: The system shall initially support the following data sources:
  - Zoho (CRM, Books, Inventory)
  - SAP Business One
  - PostgreSQL
  - CSV uploads
- **SYS-007**: Connection credentials shall be securely encrypted at rest in the Supabase database.
- **SYS-008**: The system shall use an ELT pipeline (Airbyte) to extract data from sources and load it into a Snowflake data warehouse.
- **SYS-009**: Data syncs shall be configurable to run on a schedule (e.g., hourly, daily).

### 3.3. AI-Powered Querying (Metabot equivalent)

- **SYS-010**: The system shall provide a chat interface for users to ask questions in natural language.
- **SYS-011**: The system shall use an LLM (e.g., GPT-4) via an orchestration layer (LangChain) to convert natural language questions into SQL queries.
- **SYS-012**: The generated SQL queries shall be executed against the Snowflake data warehouse.
- **SYS-013**: The system shall automatically select the best visualization type (e.g., bar chart, line chart, table) for the query results.
- **SYS-014**: The AI layer must be aware of the semantic layer to generate accurate queries based on business terms.

### 3.4. Reporting & Dashboards (Metabase Layer)

- **SYS-015**: The system shall embed the Metabase interface for report and dashboard creation.
- **SYS-016**: Users with Editor roles shall be able to create reports using Metabase's visual query builder.
- **SYS-017**: Users shall be able to create dashboards by arranging multiple reports on a grid.
- **SYS-018**: Dashboards shall support interactive filters that apply to all reports on the dashboard.
- **SYS-019**: Users shall be able to export reports to CSV, XLSX, and JSON formats.
- **SYS-020**: Users shall be able to download entire dashboards as PDFs.

## 4. Non-Functional Requirements

- **PERF-001**: Median API response time for backend operations shall be under 200ms.
- **PERF-002**: P95 query execution time for standard reports shall be under 15 seconds.
- **PERF-003**: Dashboard load time shall be under 5 seconds for a dashboard with up to 10 reports.
- **SEC-001**: All network traffic shall be encrypted using TLS 1.2 or higher.
- **SEC-002**: All sensitive data at rest (e.g., credentials, user data) shall be encrypted using AES-256.
- **SEC-003**: The system shall be protected against common web vulnerabilities (OWASP Top 10), including SQL injection, XSS, and CSRF.
- **SCALE-001**: The backend shall be able to scale horizontally to handle at least 1,000 concurrent users.
- **SCALE-002**: The data pipeline shall be able to process up to 1TB of new data per day.
- **AVAIL-001**: The platform shall have a minimum uptime of 99.9%.
- **COMP-001**: The platform must be designed to be compliant with GDPR and CCPA regulations regarding data privacy and user rights (e.g., data export, account deletion).

## 5. System Interfaces

- **UI**: A responsive web interface accessible via modern browsers (Chrome, Firefox, Safari, Edge).
- **API**: A RESTful API for programmatic access to system resources. The API shall be secured using JWTs provided by Supabase Auth.
- **Data Source APIs**: The system will interface with the REST/OData APIs of Zoho and SAP Business One, as well as standard database connection protocols.

