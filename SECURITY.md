# Security Policy

## Scope

This repository contains a FastAPI retrieval backend that may connect to OpenAI, vector databases, and external storage providers.

## Sensitive data rules

- Do not commit real API keys, bearer tokens, database passwords, private keys, or cloud credentials.
- Use `.env.example` only for placeholders.
- Store real secrets in GitHub Actions secrets, deployment provider secrets, or a dedicated secret manager.
- Rotate any credential that may have been committed, even if later removed.
- Treat retrieval data as sensitive when it contains personal, business, legal, or private documents.

## Required review areas

Before deployment or production use, review:

- authentication configuration;
- datastore authorization;
- OpenAI API key handling;
- bearer token handling;
- exposed endpoints;
- uploaded file handling;
- logs and telemetry;
- CORS and public access;
- dependency vulnerabilities.

## Reporting

Do not open public issues containing secrets, credentials, customer data, document contents, or exploit details. Use a private owner-controlled channel for sensitive reports.
