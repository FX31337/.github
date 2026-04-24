# AGENTS.md (workflows)

## Setup & Environment Invariants

- **Secrets**: `OPENCODE_API_KEY` is mandatory for all agent-based workflows.
- **Python Runtime**: Standardized on Python 3.12 via `actions/setup-python`.
- **Caching**:
  - Python user site (`~/.local`) cached against `.devcontainer/requirements.txt`.
  - `pre-commit` hooks cached against `.pre-commit-config.yaml`.

## Key Workflows & Agent Context

### Cogni AI Agent (`cogni-ai-agent.yml`)

- **Role**: Specialized autonomous issue resolution and PR review.
- **Triggers**: Issue/PR comments, `workflow_dispatch`.
- **Tooling**: Utilizes `Cogni-AI-OU/cogni-ai-agent-action`.
- **Shell Permissions**:
  - `allow`: `ansible*`, `git*`, `gh*`, `pre-commit*`, `vim*`, `ex*`, `jq*`.
  - `deny`: default `*` catch-all.

### Copilot Setup Steps (`copilot-setup-steps.yml`)

- **Role**: Environment preparation for agents.
- **Function**: Installs dependencies from `.devcontainer/requirements.txt` and ensures `~/.local/bin` is on `GITHUB_PATH`.

### Check Workflow (`check.yml`)

- **Role**: Quality gate for agent-produced code.
- **Invariants**:
  - MUST run `actionlint` for workflow validation.
  - MUST run `pre-commit` for linting/formatting.
  - MUST run `link-checker` (Lychee) for documentation.

### Development Containers CI (`devcontainer-ci.yml`)

- **Role**: Automated build and validation of dev environments.
- **Function**: GHCR login, container build/test, and validation of `required_commands` and `required_python_packages`.
- **Integration**: Reusable via `workflow_call`.

## Agent Directives (Workflow Operations)

- **MUST** prioritize native agent tools (`Glob`, `Read`, `Grep`, `Edit`, `Write`) over shell equivalents.
- **MUST** use `gh run view <run_id> --log-failed` for diagnosing CI failures.
- **NEVER** force-push to protected branches; agents operate on feature branches.
- **NEVER** bypass pre-commit hooks unless explicitly instructed for environment-specific debugging.

## Verification Gates

- **actionlint**: All workflow changes MUST be validated via `actionlint`.
- **pre-commit**: All code changes MUST pass local `pre-commit run -a` before pushing.

## Troubleshooting

> Duplicate header: "Authorization" error

- Root-cause: `persist-credentials: true` in `actions/checkout`.
- Fix: Set `persist-credentials: false`.
