# Project Plan & Schedule

**Project**: BI Reset
**Version**: 1.0
**Date**: December 12, 2025

## 1. Project Summary

This document outlines the high-level plan and schedule for the development of the BI Reset Minimum Viable Product (MVP). The project is expected to take **6 months** to complete, following the recommended Hybrid Architecture path.

## 2. Project Phases & Timeline

| Phase | Duration | Key Activities |
| :--- | :--- | :--- |
| **Phase 1: Foundation** | 4 Weeks | - Set up Supabase, Snowflake, and Airbyte.<br>- Deploy Metabase.<br>- Initialize Refine frontend with Metronic template.<br>- Configure multi-tenancy and auth. |
| **Phase 2: Data Integration** | 6 Weeks | - Build Zoho and SAP B1 connectors in Airbyte.<br>- Develop dbt models for data transformation.<br>- Establish semantic layer in Metabase. |
| **Phase 3: AI & Core Logic** | 4 Weeks | - Build LLM orchestration layer.<br>- Implement natural language to SQL functionality.<br>- Integrate AI layer with the backend. |
| **Phase 4: UI & Embedding** | 6 Weeks | - Develop custom UI components in Refine.<br>- Embed Metabase for report building.<br>- Implement dashboard and export features. |
| **Phase 5: Testing & Deployment** | 4 Weeks | - Conduct end-to-end testing (security, performance, UAT).<br>- Finalize documentation.<br>- Deploy to production. |

## 3. High-Level Schedule (Gantt Chart)

```
Month 1: [#### Phase 1: Foundation ####]
Month 2: [###### Phase 2: Data Integration ######]
Month 3: [###### Phase 2 ######][#### Phase 3: AI & Core Logic ####]
Month 4: [###### Phase 4: UI & Embedding ######]
Month 5: [###### Phase 4 ######][#### Phase 5: Testing & Deployment ####]
Month 6: [#### Phase 5 ####][ MVP Launch ]
```

## 4. Resource Allocation

- **Human Resources**: 1 Project Manager, 2 Supervisors.
- **AI Resources**: A team of AI development agents (e.g., Google Antigravity).
- **Technology Resources**: Subscriptions/access to Supabase, Snowflake, Vercel, Metabase Pro, OpenAI API, and GitHub.

## 5. Milestones

- **End of Month 1**: Foundational infrastructure is deployed and operational.
- **End of Month 3**: Data from Zoho and SAP is successfully integrated into the data warehouse, and the AI core logic is prototyped.
- **End of Month 5**: All features are code-complete, and the platform enters the final testing phase.
- **End of Month 6**: MVP is launched to pilot users.
