# BI Reset: AI-First Business Intelligence Platform

> **Stop Guessing. Start Asking.**

**BI Reset** is an AI-first business intelligence (BI) platform designed for multi-source data analytics. It empowers users to ask questions in natural language, build complex reports with a drag-and-drop interface, and securely manage data across heterogeneous systems.

This repository contains the complete technical, project, and marketing documentation for BI Reset, optimized for development by AI agents using frameworks like Google Antigravity.

---

## Quick Links

| For Whom? | Start Here |
| :--- | :--- |
| **AI Development Agents** | [AI Agent Development Guides](./6_ai_agent_development/README.md) |
| **Human Supervisors** | [Project Summary](./PROJECT_SUMMARY.md) |
| **Marketing Team** | [Marketing Overview](./0_initiation_and_commercial/Marketing_Overview.md) |
| **New Contributors** | [Contributing Guidelines](./CONTRIBUTING.md) |

---

## Table of Contents

- [1. The Problem We Solve](#1-the-problem-we-solve)
- [2. Our Solution](#2-our-solution)
- [3. Technology Stack](#3-technology-stack)
- [4. Documentation Index](#4-documentation-index)
- [5. Getting Started for AI Agents](#5-getting-started-for-ai-agents)
- [6. License](#6-license)

---

## 1. The Problem We Solve

Modern businesses are drowning in data yet starving for wisdom. They operate on a complex web of disconnected applications—a CRM for sales, an ERP for inventory, accounting software for finance—and each system is a silo. This fragmentation leads to:

-   **No Single Source of Truth**: Decision-makers stitch together conflicting reports, leading to poor strategic choices.
-   **Inability to Ask Critical Questions**: Answering a simple question like, "Which campaigns bring our most profitable customers?" takes weeks.
-   **BI Tools Built for Experts**: Traditional BI platforms are powerful but complex, expensive, and require specialized skills.

For more detail, see the [Product Vision & Problem Statement](./0_initiation_and_commercial/Product_Vision_and_Problem_Statement.md).

## 2. Our Solution

BI Reset is built on three foundational pillars:

1.  **Unify Your Data**: Connect to all your critical business systems (Zoho, SAP, databases, spreadsheets) and pull them into a single, unified source of truth.
2.  **Ask Anything in English**: Our AI-powered chat interface lets you ask questions in plain English and receive instant, accurate visualizations.
3.  **Democratize Insights**: A user-friendly drag-and-drop builder empowers everyone on your team to explore data and find their own insights.

## 3. Technology Stack

| Layer | Technology |
| :--- | :--- |
| **Frontend** | Refine (React), Tailwind CSS, Metronic Admin Template |
| **Backend** | Supabase (PostgreSQL, Auth, Storage) |
| **Hosting** | Vercel (Frontend), Supabase (Backend) |
| **Data Warehouse** | Snowflake |
| **ELT Pipeline** | Airbyte |
| **BI Engine** | Metabase (Open Source) |
| **AI/LLM** | OpenAI (GPT-4), LangChain |

For exact versions and dependencies, see the [Technology & Version Specifications](./1_requirements_and_design/Technology_and_Version_Specifications.md).

---

## 4. Documentation Index

This repository is organized into the following directories. Each section contains documents for a specific phase of the project lifecycle.

### Initiation & Commercial (`0_initiation_and_commercial/`)

These documents establish the strategic foundation for the project.

| Document | Description |
| :--- | :--- |
| [Product Vision & Problem Statement](./0_initiation_and_commercial/Product_Vision_and_Problem_Statement.md) | The "why" behind BI Reset. Defines the problem, solution, and vision. |
| [Business Case & Feasibility Summary](./0_initiation_and_commercial/Business_Case_and_Feasibility_Summary.md) | Justification for the project, including technical and financial feasibility. |
| [Marketing Overview](./0_initiation_and_commercial/Marketing_Overview.md) | Key messaging, value propositions, and competitive positioning for marketing. |

### Requirements & Design (`1_requirements_and_design/`)

These documents define *what* is being built and *how* it is designed.

| Document | Description |
| :--- | :--- |
| [Product Requirements Document (PRD)](./1_requirements_and_design/PRD.md) | Features, user stories, and scope for the product. |
| [System Requirements Specification (SRS)](./1_requirements_and_design/SRS.md) | Detailed functional and non-functional requirements. |
| [Architecture Overview](./1_requirements_and_design/Architecture_Overview.md) | System design, component breakdown, data flows, and **database schema**. |
| [Technology & Version Specifications](./1_requirements_and_design/Technology_and_Version_Specifications.md) | Pinned versions for all technologies and dependencies. |
| [UX Guidelines & Key Screens](./1_requirements_and_design/UX_Guidelines_and_Key_Screens.md) | Design principles and wireframes for the user interface. |

### Project & Change Management (`2_project_and_change_management/`)

These documents govern how the project is managed.

| Document | Description |
| :--- | :--- |
| [Project Charter](./2_project_and_change_management/Project_Charter.md) | Formal authorization, scope, and stakeholders. |
| [Project Plan & Schedule](./2_project_and_change_management/Project_Plan_and_Schedule.md) | High-level timeline, phases, and milestones. |

### Build & QA (`3_build_and_qa/`)

These documents define how quality is assured.

| Document | Description |
| :--- | :--- |
| [Test Strategy & Test Plan](./3_build_and_qa/Test_Strategy_and_Test_Plan.md) | Testing levels, types, and procedures. |

### Deployment & Ops (`4_deployment_and_ops/`)

These documents govern how the platform is deployed and operated.

| Document | Description |
| :--- | :--- |
| [Deployment Plan & Go-Live Criteria](./4_deployment_and_ops/Deployment_Plan_and_Go_Live_Criteria.md) | Deployment strategy, checklist, and go-live requirements. |
| [Support & SLA](./4_deployment_and_ops/Support_and_SLA.md) | Support channels, service level agreements, and uptime guarantees. |

### Training & Docs (`5_training_and_docs/`)

These are the end-user and administrator guides.

| Document | Description |
| :--- | :--- |
| [Documentation Plan](./5_training_and_docs/Documentation_Plan.md) | Overview of the documentation strategy. |
| [User Guide](./5_training_and_docs/User_Guide.md) | Instructions for end-users on how to use the platform. |
| [Admin Guide](./5_training_and_docs/Admin_Guide.md) | Instructions for administrators on managing the platform. |

### AI Agent Development (`6_ai_agent_development/`)

These are the detailed technical specifications for AI development agents.

| Document | Description |
| :--- | :--- |
| [AI Agent README](./6_ai_agent_development/README.md) | Workflow, principles, and table of contents for AI agents. |
| [01: Backend Setup](./6_ai_agent_development/01_Backend_Setup.md) | Supabase setup, database schema, and RLS policies. |
| [02: Frontend Setup](./6_ai_agent_development/02_Frontend_Setup.md) | Refine and Metronic integration. |
| [03: Data Integration Pipeline](./6_ai_agent_development/03_Data_Integration_Pipeline.md) | Airbyte and dbt configuration. |
| [04: LLM Orchestration Layer](./6_ai_agent_development/04_LLM_Orchestration_Layer.md) | Design for the AI-powered query engine. |
| [05: Metabase Integration](./6_ai_agent_development/05_Metabase_Integration.md) | Secure embedding and multi-tenancy in Metabase. |

---

## 5. Getting Started for AI Agents

AI agents should begin by reviewing the core documentation in the following order:

1.  **[Product Requirements Document (PRD)](./1_requirements_and_design/PRD.md)**: Understand *what* needs to be built and for whom.
2.  **[System Requirements Specification (SRS)](./1_requirements_and_design/SRS.md)**: Review the detailed functional and non-functional requirements.
3.  **[Architecture Overview](./1_requirements_and_design/Architecture_Overview.md)**: Understand the system design, data flows, and **database schema**.
4.  **[Technology & Version Specifications](./1_requirements_and_design/Technology_and_Version_Specifications.md)**: Confirm the exact versions of all technologies to use.
5.  **[AI Agent Development Guides](./6_ai_agent_development/)**: Access step-by-step implementation guides for each module.

All development tasks should be based on the specifications within the `6_ai_agent_development` directory.

---

## 6. License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.
