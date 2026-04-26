# Operational Baseline

## Status

Governance and CI baseline added for the Python/FastAPI retrieval backend.

## Classification

Application repository: Python/FastAPI/Poetry retrieval backend.

## Completed

- Classified repository as a Python/FastAPI/Poetry application.
- Added Python CI workflow using Poetry, pytest and `poetry check`.
- Added Dependabot for Python dependencies and GitHub Actions.
- Added `SECURITY.md` focused on OpenAI keys, bearer tokens, datastores, endpoints, uploads and logs.
- Hardened pull request template for backend/security review.
- Added bug report issue template for reproducible retrieval backend failures.

## Remaining validation

- Run GitHub Actions or wait for the next push.
- If CI fails due to missing environment variables, add safe test defaults or split syntax/package validation from integration tests.
- Review whether this fork should stay active or track upstream.

## Security notes

- Do not commit OpenAI API keys, bearer tokens, vector database credentials or cloud secrets.
- Keep real secrets in deployment secrets or GitHub Actions secrets.
- Treat retrieval data as sensitive when it includes personal, legal, business or private documents.
