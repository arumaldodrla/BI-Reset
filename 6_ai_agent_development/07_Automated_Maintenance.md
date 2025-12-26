# AI Agent Guide: Automated Maintenance & Self-Revision System

**Objective**: To implement the automated weekly self-revision system using GitHub Actions and a dedicated AI maintenance agent.

---

## 1. GitHub Actions Workflow

Create a new workflow file at `.github/workflows/weekly-maintenance.yml`.

```yaml
name: Weekly Codebase Maintenance

on:
  schedule:
    # Runs every Sunday at 00:00 UTC
    - cron: '0 0 * * 0'
  workflow_dispatch: # Allows manual triggering

jobs:
  maintenance:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
          cache: 'pnpm'

      - name: Install dependencies
        run: pnpm install

      - name: Invoke Maintenance AI Agent
        id: maintenance-agent
        uses: your-custom-ai-agent-action@v1 # This will be a custom action you build
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          # Add any other inputs the agent needs, like API keys for analysis tools

      - name: Log Maintenance Summary
        run: echo "${{ steps.maintenance-agent.outputs.summary }}"
```

## 2. Maintenance AI Agent Logic

The core of this system is the "Maintenance AI Agent," which will be implemented as a custom GitHub Action (e.g., a Docker container or a TypeScript action). This agent will perform the following steps when invoked.

### Step 2.1: Dependency & Vulnerability Scan

-   **Run Scans**: The agent will execute the following commands in the `bi-reset-frontend` directory:
    -   `pnpm outdated --json > outdated.json` to get a machine-readable list of outdated dependencies.
    -   `pnpm audit --json > audit.json` to get a machine-readable list of security vulnerabilities.

### Step 2.2: Analyze Scan Results

-   **Parse JSON**: The agent will parse `outdated.json` and `audit.json`.
-   **Categorize Updates**: It will categorize each outdated dependency:
    -   **Minor/Patch**: If the update is a patch or minor version change (e.g., `1.2.3` -> `1.2.4` or `1.2.3` -> `1.3.0`). These are considered low-risk.
    -   **Major**: If the update is a major version change (e.g., `1.2.3` -> `2.0.0`). These are high-risk and may contain breaking changes.
-   **Categorize Vulnerabilities**: It will categorize vulnerabilities by severity (`low`, `moderate`, `high`, `critical`).

### Step 2.3: Automated Action

-   **For Minor/Patch Updates**: The agent will automatically:
    1.  Create a new branch (e.g., `chore/update-deps-YYYY-MM-DD`).
    2.  Run `pnpm update <package-name>` for each low-risk dependency.
    3.  Commit the changes with a conventional commit message (e.g., `chore(deps): update lodash to 4.17.21`).
    4.  Create a pull request against the `develop` branch.
    5.  If the CI tests (unit tests, linting) pass on the PR, the agent will automatically merge it.

-   **For Major Updates or High/Critical Vulnerabilities**: The agent will:
    1.  Create a new GitHub Issue with a detailed report, including the package name, current version, latest version, and a link to the release notes or vulnerability report.
    2.  Create a draft pull request with the attempted update.
    3.  Assign the issue and the PR to the designated human supervisor for manual review.

### Step 2.4: Code Quality Analysis (Optional Enhancement)

-   The agent can be extended to integrate with a static analysis tool like SonarCloud.
-   It would fetch the latest analysis report via the SonarCloud API.
-   If new "code smells" or bugs are detected, it would create a GitHub Issue with the details, assigning it to the appropriate development agent or human supervisor.

## 3. Reporting

-   At the end of the workflow, the agent will generate a summary of its actions (e.g., "Auto-merged 3 dependency updates. Created 1 issue for a major version update.").
-   This summary will be output from the custom action and logged in the GitHub Actions run, making it easy for the human team to review the week's automated maintenance activities.
