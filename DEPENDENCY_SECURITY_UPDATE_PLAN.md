# Dependency security update plan

## Objective

Track the controlled remediation path for currently open Dependabot security/dependency PRs.

## Current open Dependabot PRs

```text
#1 lxml 4.9.4 -> 6.1.0
#2 python-dotenv 0.21.1 -> 1.2.2
#3 gitpython 3.1.40 -> 3.1.47
```

## Current connector state

The PRs are reported as:

```text
mergeable: false
CI/status: not exposed through connector
```

Because all three PRs affect Poetry dependency resolution and/or `poetry.lock`, they should not be merged individually while conflicts or mergeability uncertainty remain.

## Risk classification

| Dependency | Current update | Risk | Reason |
|---|---|---:|---|
| `lxml` | `4.9.4 -> 6.1.0` | High | Security-related XML parsing fixes and dependency drift |
| `gitpython` | `3.1.40 -> 3.1.47` | High | Security advisory fixes in GitPython release path |
| `python-dotenv` | `0.21.1 -> 1.2.2` | Medium | Behavior changes around env-file mutation and symlink handling; lockfile drift control needed |

## Decision

Do not merge the three Dependabot PRs individually while they are reported as `mergeable=false`.

Use a single consolidated Poetry update instead.

## Manual validation workflow

A non-committing validation workflow is available:

```text
.github/workflows/dependency-update-validation.yml
```

Execution path:

```text
GitHub -> chatgpt-retrieval-plugin -> Actions -> Dependency Update Validation -> Run workflow
```

This workflow:

```text
checks out main
sets up Python 3.10
installs Poetry
installs current dependencies
runs poetry check
runs pytest before update
runs poetry update lxml python-dotenv gitpython
runs poetry check after update
runs pytest after update
uploads dependency-update-diff artifact
```

It does not commit, merge or push changes.

Expected artifact:

```text
dependency-update-diff.txt
```

## Manual PR preparation workflow

A separate controlled workflow can prepare the consolidated PR after validation:

```text
.github/workflows/prepare-consolidated-dependency-update.yml
```

Execution path:

```text
GitHub -> chatgpt-retrieval-plugin -> Actions -> Prepare Consolidated Dependency Update -> Run workflow
```

This workflow:

```text
checks out main
sets up Python 3.10
installs Poetry
installs current dependencies
runs poetry check and pytest before update
runs poetry update lxml python-dotenv gitpython
runs poetry check and pytest after update
uploads dependency-update-diff artifact
creates/updates branch chore/consolidated-poetry-security-update only if a diff exists
creates/updates a PR titled Consolidate Poetry security dependency updates
```

It does not merge the PR automatically.

## Controlled update path

Run from repository root:

```bash
poetry update lxml python-dotenv gitpython
poetry check
pytest
```

If integration tests require live secrets, datastores, OpenAI API keys, bearer tokens, or external services, split validation into safe local checks:

```bash
poetry check
python -m compileall server local_server datastore models services tests
pytest -q tests --ignore integration tests that require live services
```

## Required review before merge

- Confirm `pyproject.toml` constraints remain intentional.
- Confirm `poetry.lock` is regenerated once, not through conflicting dependency PRs.
- Confirm no secrets, API keys, bearer tokens, datastore credentials or private endpoints are introduced.
- Confirm Python CI passes.
- Confirm application import/startup remains valid where feasible.
- Confirm security update PRs are closed or superseded after the consolidated merge.
- Review `dependency-update-diff.txt` from the validation or PR-preparation workflow when available.

## Repository security guardrails

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

## Current recommendation

Run the manual dependency validation workflow first. If it passes, run the PR-preparation workflow or prepare a consolidated update branch manually. Then review the generated PR and close or supersede the individual Dependabot PRs only after CI and diff review pass.
