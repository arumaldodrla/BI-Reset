# AI Agent Guide: LLM Orchestration Layer

**Objective**: To design and build the service that translates a user's natural language question into a SQL query that can be executed against the Snowflake data warehouse.

This is the most complex and critical component of the BI Reset platform.

## 1. Architecture

-   The LLM Orchestration Layer will be a Vercel Serverless Function written in TypeScript.
-   It will use the LangChain.js library to manage the interaction with the LLM.
-   It will expose a single API endpoint that accepts a natural language question and returns a SQL query.

## 2. High-Level Workflow

1.  Receive a natural language question from the BI Reset API.
2.  Fetch metadata about the available tables and columns from the semantic layer stored in the Supabase database.
3.  Construct a detailed, few-shot prompt that includes:
    -   The user's question.
    -   The database schema (table names, column names, data types).
    -   Examples of similar questions and their corresponding SQL queries.
4.  Send the prompt to the LLM (OpenAI's GPT-4).
5.  Receive the generated SQL query from the LLM.
6.  **Validate the SQL**: Perform a basic validation to ensure the SQL is syntactically correct and does not contain any destructive commands (e.g., `DROP`, `DELETE`).
7.  Return the validated SQL query to the BI Reset API.

## 3. Semantic Layer

-   A `semantic_layer` table will be created in Supabase to store metadata about the tables in the Snowflake `analytics` schema.
-   This table will include:
    -   `table_name`: The name of the table in Snowflake.
    -   `column_name`: The name of the column.
    -   `description`: A human-readable description of the column's meaning (e.g., "The total revenue from the sale").
    -   `is_dimension`: A boolean indicating if the column is a dimension (for grouping).
    -   `is_measure`: A boolean indicating if the column is a measure (for aggregation).

## 4. Prompt Engineering

-   The quality of the generated SQL depends heavily on the prompt. The prompt must be carefully engineered to provide the LLM with as much context as possible.
-   The prompt should instruct the LLM to only use tables and columns from the provided schema and to always generate a valid Snowflake SQL query.

## 5. Error Handling & Fallbacks

-   If the LLM returns an invalid SQL query, the orchestration layer should attempt to fix it or ask the user to rephrase their question.
-   If the LLM is unable to generate a query, it should return a message to the user explaining that it could not understand the request.
