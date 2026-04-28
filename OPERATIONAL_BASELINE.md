# Operational Baseline

## Status

Governance and CI baseline added for the Python/FastAPI retrieval backend.

## Classification

Application repository: Python/FastAPI/Poetry retrieval backend.

## Central governance reference

Portfolio-level governance is tracked in:

```text
jymmyjr/effective-meme/PORTFOLIO_GOVERNANCE.md
```

## Completed

- Classified repository as a Python/FastAPI/Poetry application.
- Added Python CI workflow using Poetry, pytest and `poetry check`.
- Added Dependabot for Python dependencies and GitHub Actions.
- Hardened Dependabot governance with target branch, timezone, labels, reviewers, assignees and grouped update policy.
- Added `SECURITY.md` focused on OpenAI keys, bearer tokens, datastores, endpoints, uploads and logs.
- Added `CODEOWNERS` for backend, Poetry, automation and sensitive retrieval areas.
- Hardened pull request template for backend/security review.
- Added Poetry/dependency lockfile governance checks to the pull request template.
- Added bug report issue template for reproducible retrieval backend failures.
- Added dependency security update plan for the open Dependabot PRs.
- Added manual non-committing dependency update validation workflow.
- Added manual consolidated dependency update PR-preparation workflow.
- Added `GOVERNANCE_STATUS.md` as the repository entry-point for current dependency governance state.

## Current dependency security queue

Open Dependabot PRs currently require consolidated handling:

```text
#1 lxml 4.9.4 -> 6.1.0
#2 python-dotenv 0.21.1 -> 1.2.2
#3 gitpython 3.1.40 -> 3.1.47
```

Connector state observed:

```text
mergeable: false
CI/status: not exposed through connector
```

Plan:

```text
DEPENDENCY_SECURITY_UPDATE_PLAN.md
```

Current status entry-point:

```text
GOVERNANCE_STATUS.md
```

Manual validation workflow:

```text
.github/workflows/dependency-update-validation.yml
```

Manual PR-preparation workflow:

```text
.github/workflows/prepare-consolidated-dependency-update.yml
```

Decision:

```text
Do not merge the three dependency PRs individually while mergeability remains false. First run the manual dependency update validation workflow. If it passes, run or prepare a single consolidated Poetry update PR and validate with CI before merge.
```

## Remaining validation

- Run `Dependency Update Validation` from GitHub Actions.
- Review `dependency-update-diff.txt` artifact.
- If validation passes, run `Prepare Consolidated Dependency Update` or prepare the consolidated PR manually.
- If CI fails due to missing environment variables, add safe test defaults or split syntax/package validation from integration tests.
- Review whether this fork should stay active or track upstream.
- Close or supersede individual Dependabot PRs only after the consolidated PR is validated and merged.

## Security notes

- Do not commit OpenAI API keys, bearer tokens, vector database credentials or cloud secrets.
- Keep real secrets in deployment secrets or GitHub Actions secrets.
- Treat retrieval data as sensitive when it includes personal, legal, business or private documents.
- Do not merge dependency updates without checking `poetry.lock`, CI and secret exposure risk.
