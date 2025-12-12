_to_write="# AI Agent Guide: Data Integration Pipeline

**Objective**: To build the ELT (Extract, Load, Transform) pipeline that moves data from source systems into the Snowflake data warehouse.

## 1. Set Up Airbyte

-   Deploy an instance of Airbyte (Open Source) on a cloud server (e.g., AWS EC2, DigitalOcean Droplet).
-   Configure the Airbyte instance to be accessible via a secure URL.

## 2. Configure Connectors

### 2.1. Source Connectors

-   Within Airbyte, set up the following source connectors:
    -   **Zoho CRM**: Authenticate using OAuth.
    -   **Zoho Books**: Authenticate using OAuth.
    -   **SAP Business One**: Authenticate using the Service Layer API credentials.
    -   **PostgreSQL**: Connect to any required PostgreSQL databases.

### 2.2. Destination Connector

-   Set up a Snowflake destination connector in Airbyte. This will require the Snowflake account URL, username, password, and warehouse details.

## 3. Create Connections & Transformation

-   Create an Airbyte connection for each data source, linking it to the Snowflake destination.
-   **Sync Frequency**: Configure the connections to sync data on a daily schedule.
-   **Normalization**: Use Airbyte's built-in normalization to create raw tables in Snowflake (e.g., in a `raw_data` schema).
-   **(Optional but Recommended) dbt Transformation**: After the raw data is loaded into Snowflake, use dbt (Data Build Tool) to run transformation models. These models will:
    -   Clean and cast data types.
    -   Join tables from different sources (e.g., joining Zoho CRM data with SAP invoice data).
    -   Create aggregated, analysis-ready tables in a separate `analytics` schema.

## 4. Data Monitoring & Alerting

-   Set up monitoring to track the health of the Airbyte syncs.
-   Configure alerts (e.g., via Slack or email) to notify the human supervisors if a sync fails.
"
