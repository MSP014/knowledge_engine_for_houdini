# ADR 005: Corpus Hydration & Data Isolation

## Status

Accepted

## Context

The Knowledge Engine relies on parsing a massive corpus of Houdini Help files (HTML/JSON). These files are proprietary to SideFX and legally/technically unsuitable for storage in the Git repository.

## Decision

### 1. The `corpus/` Directory

* We establish a dedicated `corpus/` directory at the project root.
* This directory serves as the "Work Bench" for ingestion.
* **Structure**:
  * `corpus/raw/`: Original documentation files (User provided). **Hydration Target**.
  * `corpus/processed/`: Normalized Markdown/JSON ready for indexing.

### 2. Git Exclusion

* **Rule**: The contents of `corpus/` are strictly ignored via `.gitignore`.
* **Exception**: `.gitkeep` files are maintained in `raw/` and `processed/` to preserve the folder structure.

### 3. Hydration Protocol

* The user is responsible for populating `corpus/raw/` with the target Houdini documentation.
* The system must validate the existence of data in this folder before attempting ingestion.

## Consequences

* **Positive**: Keeps the Git repository lightweight; respects SideFX IP compliance.
* **Negative**: Fresh clones of the repo are "empty" and require manual data setup (hydration) before they are functional.
