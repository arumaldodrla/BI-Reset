# Technology & Version Specifications

**Project**: BI Reset
**Version**: 1.0
**Date**: December 12, 2025

## 1. Introduction

To ensure consistency, prevent version conflicts, and provide a stable development environment for all AI agents, this document specifies the exact versions of all core technologies, frameworks, and libraries to be used in the BI Reset project. AI agents **must** adhere to these specifications.

## 2. Core Technology Stack

| Layer | Technology | Version | Notes |
| :--- | :--- | :--- | :--- |
| **Frontend** | React | `18.2.0` | Core UI library. |
| | Refine | `4.40.0` | Framework for data-intensive apps. |
| | Tailwind CSS | `3.3.3` | Utility-first CSS framework. |
| | Metronic | `8.1.8` | Admin template (React version). |
| | TypeScript | `5.1.6` | Language for frontend and backend. |
| **Backend** | Supabase | `1.110.1` | Backend-as-a-Service platform. |
| | PostgreSQL | `15.1` | Underlying database for Supabase. |
| | Vercel | `32.2.5` | Hosting for frontend and serverless functions. |
| **Data & AI** | Snowflake | - | Cloud Data Warehouse (use latest stable). |
| | Airbyte | `0.50.31` | ELT data pipeline (open-source version). |
| | Metabase | `0.47.2` | BI Engine (Pro plan recommended). |
| | LangChain.js | `0.0.197` | LLM orchestration framework. |
| | OpenAI API | `v1` | For accessing GPT-4. |

## 3. Frontend Dependency Management

-   The frontend application, located in the `bi-reset-frontend` directory, will manage its dependencies using `pnpm` and a `package.json` file.
-   AI agents must use the `--save-exact` flag when adding new dependencies to ensure that the exact version is pinned in `package.json`.

**Example `package.json` structure**:

```json
{
  "name": "bi-reset-frontend",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@refinedev/core": "4.40.0",
    "@refinedev/react": "4.40.0",
    "@refinedev/supabase": "5.6.0",
    "@supabase/supabase-js": "2.38.4",
    "react": "18.2.0",
    "react-dom": "18.2.0",
    "tailwindcss": "3.3.3",
    "typescript": "5.1.6"
  }
}
```

## 4. Backend & Infrastructure

-   **Supabase**: The version is managed by the Supabase cloud platform. All development should be against the specified version `1.110.1`.
-   **Snowflake**: As a managed service, the latest stable version should be used.
-   **Airbyte & Metabase**: When self-hosting the open-source versions, the exact versions specified above must be used. This can be achieved by pulling the specific Docker image tag (e.g., `airbyte/source-zoho-crm:0.1.13`).

## 5. Version Control

-   All code and documentation will be managed in the `arumaldodrla/BI-Reset` GitHub repository.
-   The `main` branch is protected. All changes must be made via pull requests from feature branches.
-   AI agents must create feature branches named `feature/<issue-number>-<short-description>`.
