# BI Reset: AI-First Business Intelligence Platform

**BI Reset** is an open-source, AI-first business intelligence (BI) platform designed for multi-source data analytics. It empowers users to ask questions in natural language, build complex reports with a drag-and-drop interface, and securely manage data across heterogeneous systems.

This repository contains the complete technical and project documentation for BI Reset, optimized for development by AI agents using frameworks like Google Antigravity.

---

## Table of Contents

- [1. Project Vision](#1-project-vision)
- [2. Core Features](#2-core-features)
- [3. Architecture Overview](#3-architecture-overview)
- [4. Technology Stack](#4-technology-stack)
- [5. Repository Structure](#5-repository-structure)
- [6. Getting Started for AI Agents](#6-getting-started-for-ai-agents)
- [7. License](#7-license)

---

## 1. Project Vision

The goal of BI Reset is to democratize data analytics by combining the power of large language models (LLMs) with a user-friendly, multi-source BI environment. The platform is designed to be:

- **AI-First**: Natural language is the primary interface for data exploration.
- **Multi-Source**: Seamlessly connect to and join data from disparate systems (ERPs, CRMs, databases, files).
- **Secure & Multi-Tenant**: Provide robust data protection, privacy, and access control for multiple customers and workspaces.
- **Extensible**: Built with an API-first design to support embedding and programmatic integration.

## 2. Core Features

- **AI-Driven Report Creation**: Users can describe their data needs in a chat interface, and the system will automatically generate the appropriate queries and visualizations.
- **Visual Drag-and-Drop Builder**: A powerful report and dashboard editor for creating custom analytics without writing code.
- **Multi-Source Connectivity**: A robust connector framework to integrate with sources like Zoho, SAP Business One, PostgreSQL, and more.
- **Semantic Layer**: A business-friendly abstraction over raw data models, enabling consistent and accurate queries.
- **Secure Multi-Tenancy**: Isolate customer data using Supabase Row-Level Security (RLS) and provide granular access controls.

## 3. Architecture Overview

BI Reset follows a hybrid architecture that leverages the strengths of a mature open-source BI tool (Metabase) for visualization while building custom components for its core value proposition.

**The architecture consists of three main layers:**

1.  **Data Integration Layer**: An ELT (Extract, Load, Transform) pipeline, powered by Airbyte, pulls data from various sources into a central data warehouse (Snowflake).
2.  **Backend & Analytics Layer**: Supabase (PostgreSQL) serves as the primary backend for user management, multi-tenancy, and storing semantic layer definitions. Metabase connects to the data warehouse to execute queries and render visualizations.
3.  **Frontend & AI Layer**: A React-based frontend built with Refine and the Metronic template provides the user interface. A custom LLM orchestration layer translates natural language prompts into SQL queries.

For a detailed breakdown, see the [Architecture Overview](./1_requirements_and_design/Architecture_Overview.md).

## 4. Technology Stack

- **Backend**: Supabase (PostgreSQL, Auth, Storage)
- **Frontend**: Refine (React), Tailwind CSS, Metronic Admin Template
- **Hosting**: Vercel (Frontend), Supabase (Backend)
- **Data Warehouse**: Snowflake
- **ELT Pipeline**: Airbyte
- **BI Engine**: Metabase (Open Source)
- **AI/LLM**: OpenAI (GPT-4), LangChain

## 5. Repository Structure

This repository is organized to support both human project managers and AI development agents. Each folder contains specific project artifacts.

```
/BI-Reset
├── .github/                    # GitHub configuration (issue templates, workflows)
├── 0_initiation_and_commercial/  # Business case, vision document
├── 1_requirements_and_design/    # PRD, SRS, architecture, UX guidelines
├── 2_project_and_change/         # Project plan, RACI matrix
├── 3_build_and_qa/               # Test strategy, QA reports
├── 4_deployment_and_ops/         # Deployment plan, SLA
├── 5_training_and_docs/          # User guides, admin guides
├── 6_ai_agent_development/       # Detailed technical specs for AI agents
└── README.md                     # This file
```

## 6. Getting Started for AI Agents

AI agents should begin by reviewing the core documentation in the following order:

1.  **[Product Requirements Document (PRD)](./1_requirements_and_design/PRD.md)**: Understand *what* needs to be built and for whom.
2.  **[System Requirements Specification (SRS)](./1_requirements_and_design/SRS.md)**: Review the detailed functional and non-functional requirements.
3.  **[Architecture Overview](./1_requirements_and_design/Architecture_Overview.md)**: Understand the system design and how the components interact.
4.  **[AI Agent Development Guides](./6_ai_agent_development/)**: Access detailed technical specifications, API contracts, and step-by-step implementation guides for each module.

All development tasks should be based on the specifications within the `6_ai_agent_development` directory.

## 7. License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.
