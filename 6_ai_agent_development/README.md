# AI Agent Development Guides

This directory contains detailed technical specifications and guides for AI development agents. The purpose of these documents is to provide the agents with all the information they need to implement the BI Reset platform.

## Guiding Principles for AI Agents

-   **Adhere to Specifications**: All development must strictly follow the requirements and architectural patterns outlined in these documents.
-   **Write Clean, Testable Code**: All code should be well-documented, and every component must be accompanied by unit and integration tests.
-   **Follow the Tech Stack**: Use only the approved technologies and libraries from the prescribed technology stack.
-   **Commit Frequently**: Commit your work to Git frequently with clear, descriptive commit messages.
-   **Report Issues Clearly**: If you encounter an ambiguity or a problem, create a detailed GitHub Issue and await guidance from a human supervisor.

## Development Workflow

1.  **Receive a Task**: A human supervisor will assign you a task by creating a GitHub Issue with a detailed description and a link to the relevant specification document in this directory.
2.  **Understand the Requirements**: Thoroughly review the linked specification to understand the task.
3.  **Implement the Feature**: Write the code to implement the feature, including all necessary tests.
4.  **Create a Pull Request**: Once the implementation is complete and all tests are passing, create a pull request against the `main` branch.
5.  **Await Review**: A human supervisor will review your pull request. You may be asked to make changes.
6.  **Merge**: Once approved, the pull request will be merged.

## Table of Contents

-   [**01_Backend_Setup.md**](./01_Backend_Setup.md): Guide for setting up the Supabase backend, including database schema, RLS policies, and storage.
-   [**02_Frontend_Setup.md**](./02_Frontend_Setup.md): Guide for initializing the Refine frontend with the Metronic template.
-   [**03_Data_Integration_Pipeline.md**](./03_Data_Integration_Pipeline.md): Specifications for building the ELT pipeline with Airbyte and dbt.
-   [**04_LLM_Orchestration_Layer.md**](./04_LLM_Orchestration_Layer.md): Detailed design for the AI-powered query engine.
-   [**05_Metabase_Integration.md**](./05_Metabase_Integration.md): Instructions for embedding and securing the Metabase frontend.
