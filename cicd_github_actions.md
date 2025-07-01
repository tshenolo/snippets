# CI/CD (GitHub Actions) Cheatsheet

*   **Core Concepts**: Automation of build, test, and deployment pipelines.
*   **Workflow Syntax (YAML files in `.github/workflows/`)**:
    *   `name`: Workflow name displayed on GitHub.
    *   `on`: Triggers for the workflow.
        *   Events: `push`, `pull_request`, `schedule`, `workflow_dispatch`.
        *   Filters: `branches`, `tags`, `paths`.
    *   `jobs`: Contains one or more jobs that run in parallel by default (can be sequential).
        *   `<job_id>`: Unique identifier for the job.
        *   `runs-on`: Type of runner (e.g., `ubuntu-latest`, `windows-latest`, `macos-latest`, self-hosted).
        *   `steps`: Sequence of tasks within a job.
            *   `name`: Name of the step.
            *   `uses`: Action to use (e.g., `actions/checkout@v3`, `actions/setup-node@v3`).
            *   `run`: Command-line programs to execute.
            *   `with`: Input parameters for an action.
            *   `env`: Environment variables for the step.
    *   `env`: Environment variables for the entire workflow or specific jobs.
*   **Actions**: Reusable units of code (e.g., checking out code, setting up Node.js, building Docker images).
*   **Triggers**:
    *   Push to a branch: `on: push: branches: [ main ]`
    *   Pull request to a branch: `on: pull_request: branches: [ main ]`
    *   Scheduled run: `on: schedule: - cron: '0 * * * *'` (hourly)
    *   Manual trigger: `on: workflow_dispatch`
*   **Jobs**:
    *   Dependencies: `needs: <job_id>` to run jobs sequentially.
    *   Strategy Matrix: `strategy: matrix: node-version: [16, 18, 20]` to run a job multiple times with different configurations.
*   **Secrets**: Storing sensitive data (`secrets.GITHUB_TOKEN`, custom secrets).
*   **Artifacts**: Storing files produced by a job (`actions/upload-artifact`, `actions/download-artifact`).
*   **Example Workflow Snippet (Build and Test Node.js app)**:
    ```yaml
    name: Node.js CI
    on: [push, pull_request]
    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v3
        - name: Use Node.js
          uses: actions/setup-node@v3
          with:
            node-version: '18'
        - run: npm ci
        - run: npm run build --if-present
        - run: npm test
    ```
