# ADR 002: QA & Security Protocols

## Status

Accepted

## Context

The "Top Mode" rigor demands that the code is not only functional but robust, secure, and clean. "Works on my machine" is unacceptable. We must enforce quality checks automatically.

## Decision

We enforce a "Shift Left" strategy using `pre-commit` hooks.

### 1. Guardrails (Pre-commit)

* **Linting**:
  * `black`: Uncompromising code formatting.
  * `flake8`: Logic and style error checking.
  * `isort`: Import sorting.
* **Security**:
  * `bandit`: Static analysis for security issues (e.g., hardcoded passwords).
  * `pip-audit`: Checks dependencies for known vulnerabilities.
* **Hygiene**:
  * `check-added-large-files`: Prevent committing heavy binary assets.

### 2. Secrets Management

* **Isolation**: All sensitive data (e.g., JIRA tokens, Qdrant keys) MUST be stored in a `.env` file.
* **Prohibition**: The `.env` file must be included in `.gitignore` and never committed.

### 3. Testing Policy

* `pytest` must pass locally before any push.
* All core logic (ingestion, retrieval) must be covered by unit tests.

## Consequences

* **Positive**: Prevents technical debt accumulation and credential leaks.
* **Negative**: Requires discipline to fix linting errors before every commit.
