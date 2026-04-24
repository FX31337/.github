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

### [Cogni AI Agent](cogni-ai-agent.yml)

Integration with the [Cogni AI Agent](https://github.com/Cogni-AI-OU/cogni-ai-agent-action)
to assist with repository tasks via issue/PR comments and manual triggers.

- **Trigger:** `issues`, `issue_comment`, `pull_request`, `pull_request_review_comment`, and `workflow_dispatch`.

## Documentation

- [Agent Directives](AGENTS.md)
