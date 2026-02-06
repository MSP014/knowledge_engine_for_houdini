# ADR 003: Dependency Management

## Status

Accepted (Implementation Pending Command)

## Context

To ensure reproducibility across environments (Dev, CI, Production), a simple `pip freeze` is insufficient as it does not separate direct dependencies from transitive ones.

## Decision

We will use `pip-tools` for deterministic dependency management.

### 1. Workflow

1. **Source of Truth**: `requirements.in`. This file lists *only* the top-level libraries we explicitly use (e.g., `qdrant-client`, `beautifulsoup4`).
2. **Compilation**: We generate `requirements.txt` using `pip-compile`.
    * Command: `pip-compile requirements.in`
3. **Installation**: We sync the environment using `pip-sync` (or `pip install -r requirements.txt`).

### 2. Lockfile Policy

* `requirements.txt` is treated as a lockfile containing exact versions and hashes.
* It must be committed to Git.
* It is strictly Read-Only for humans; do not edit it manually.

## Consequences

* **Positive**: Precise control over dependency tree; easy vulnerability scanning.
* **Negative**: Extra step (`pip-compile`) required when adding new libraries.
