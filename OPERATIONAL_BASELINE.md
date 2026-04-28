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
- Added `SECURITY.md` focused on OpenAI keys, bearer tokens, datastores, endpoints, uploads and logs.
- Hardened pull request template for backend/security review.
- Added bug report issue template for reproducible retrieval backend failures.
- Added dependency security update plan for the open Dependabot PRs.

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

Decision:

```text
Do not merge the three dependency PRs individually while mergeability remains false. Prepare a single consolidated Poetry update and validate with CI.
```

## Remaining validation

- Run GitHub Actions or wait for the next push.
- If CI fails due to missing environment variables, add safe test defaults or split syntax/package validation from integration tests.
- Review whether this fork should stay active or track upstream.
- Prepare consolidated Poetry dependency update for `lxml`, `python-dotenv` and `gitpython`.

## Security notes

- Do not commit OpenAI API keys, bearer tokens, vector database credentials or cloud secrets.
- Keep real secrets in deployment secrets or GitHub Actions secrets.
- Treat retrieval data as sensitive when it includes personal, legal, business or private documents.
- Do not merge dependency updates without checking `poetry.lock`, CI and secret exposure risk.
