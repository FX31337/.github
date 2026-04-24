# GitHub Actions Workflows

This directory contains GitHub Actions workflows for the repository.

## Workflows

### [Check](check.yml)

Automated checks for code quality and documentation consistency.

- **Trigger:** `push`, `pull_request`, weekly `schedule`, `workflow_call`, and `workflow_dispatch`.
- **Jobs:**
  - `actionlint`: Validates GitHub Actions workflow files.
  - `link-checker`: Checks for broken links in Markdown files using [lychee](https://github.com/lycheeverse/lychee).
  - `pre-commit`: Runs various hooks defined in `.pre-commit-config.yaml`.

### [Development Containers (CI)](devcontainer-ci.yml)

Builds and tests the project's development container.

- **Trigger:** `push` and `pull_request` on `.devcontainer/**` paths, weekly `schedule`, and `workflow_call`.
- **Jobs:**
  - `devcontainer-build`: Builds the container image and runs verification tests.

### [Cogni AI Agent](cogni-ai-agent.yml)

Integration with the [Cogni AI Agent](https://github.com/Cogni-AI-OU/cogni-ai-agent-action)
to assist with repository tasks via issue/PR comments and manual triggers.

- **Trigger:** `issues`, `issue_comment`, `pull_request`, `pull_request_review_comment`, and `workflow_dispatch`.

## Documentation

- [Agent Directives](AGENTS.md)
