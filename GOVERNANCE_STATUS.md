# Governance Status

## Repository

```text
jymmyjr/chatgpt-retrieval-plugin
```

## Classification

```text
Application repository — Python / FastAPI / Poetry retrieval backend
```

## Current operational state

This repository is governed and protected for dependency/security maintenance.

The current open dependency PRs must not be merged individually while they remain in a conflicting or unverified state.

## Open dependency/security PRs

```text
#1 lxml 4.9.4 -> 6.1.0
#2 python-dotenv 0.21.1 -> 1.2.2
#3 gitpython 3.1.40 -> 3.1.47
```

Observed connector state:

```text
mergeable: false
CI/status: not exposed through connector
```

## Decision

```text
Do not merge the individual Dependabot PRs one by one.
Use a consolidated Poetry dependency update.
Validate before merge.
No automatic merge is enabled.
```

## Manual validation workflow

Workflow:

```text
.github/workflows/dependency-update-validation.yml
```

GitHub UI path:

```text
GitHub -> chatgpt-retrieval-plugin -> Actions -> Dependency Update Validation -> Run workflow
```

Purpose:

```text
Test consolidated update without committing, pushing or merging.
```

It runs:

```text
poetry install --with dev
poetry check
pytest
poetry update lxml python-dotenv gitpython
poetry check
pytest
```

Artifact:

```text
dependency-update-diff.txt
```

## Manual PR-preparation workflow

Workflow:

```text
.github/workflows/prepare-consolidated-dependency-update.yml
```

GitHub UI path:

```text
GitHub -> chatgpt-retrieval-plugin -> Actions -> Prepare Consolidated Dependency Update -> Run workflow
```

Purpose:

```text
Test consolidated update and create/update a consolidated PR if validation passes and dependency files changed.
```

It can create/update:

```text
branch: chore/consolidated-poetry-security-update
PR title: Consolidate Poetry security dependency updates
artifact: dependency-update-diff.txt
```

It does not merge automatically.

## Required review before final merge

Before merging any consolidated dependency PR, review:

```text
dependency-update-diff.txt
pyproject.toml
poetry.lock
CI status
pytest result
poetry check result
secret exposure risk
runtime compatibility risk
```

## Guardrails

Do not commit:

```text
OPENAI_API_KEY
bearer tokens
vector database credentials
Redis credentials
Postgres credentials
Azure credentials
Pinecone / Weaviate / Qdrant / Milvus / Supabase secrets
.env files with real values
private endpoint URLs with embedded credentials
```

Do not do:

```text
Do not merge PR #1 individually.
Do not merge PR #2 individually.
Do not merge PR #3 individually.
Do not ignore dependency-update-diff.txt.
Do not merge if pytest fails.
Do not merge if poetry check fails.
Do not merge if pyproject.toml constraints changed unexpectedly.
Do not merge if poetry.lock introduces unrelated dependency churn.
```

## Related governance files

```text
OPERATIONAL_BASELINE.md
DEPENDENCY_SECURITY_UPDATE_PLAN.md
SECURITY.md
.github/CODEOWNERS
.github/pull_request_template.md
.github/dependabot.yml
```

## Final current state

```text
Governance: applied
Dependency PRs: open
Individual merge: blocked
Consolidated validation workflow: ready
Consolidated PR-preparation workflow: ready
Next material action: run Prepare Consolidated Dependency Update from GitHub Actions
```
