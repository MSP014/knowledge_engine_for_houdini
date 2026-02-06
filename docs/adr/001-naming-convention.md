# ADR 001: Naming Convention & Standards

## Status

Accepted

## Context

To ensure the Knowledge Engine for Houdini (KEH) remains a pristine, well-engineered artifact, we require strict naming conventions and language protocols that align with the "Elite Mode" engagement rigor.

## Decision

### 1. Repository Naming

* **Repository Name**: `knowledge_engine_for_houdini`
* **Remote URL**: `https://github.com/MSP014/knowledge_engine_for_houdini.git`

### 2. Directory Structure

We adhere to a standard Python package layout:

* `docs/`: Architecture Decision Records (ADR) and Specifications.
* `src/`: Source code container (Src Layout).
  * `keh/`: Main Python package.
    * `core/`: Orchestration logic.
    * `ingestion/`: Parsers for Houdini Help.
    * `storage/`: Vector DB interface (Qdrant).
    * `retrieval/`: Search & Ranking logic.
* `tests/`: Pytest suite.
* `corpus/`: Data storage (GitIgnored).
* `.agent/`: AI context and workflows.

### 3. Language Standards

* **Documentation & Commits**: ALL persistent artifacts (docs, docstrings, commit messages) must be in **British English** (en-GB).
  * *Example*: "Initialise repository", not "Initialize repository".
  * *Example*: "Optimise ingestion", not "Optimize ingestion".
* **Chat Interaction**: Strictly **Russian**.

### 4. Git Workflow

* **Branches**: `feature/description` or `fix/issue-id`.
* **Commit Messages**: Imperative mood (e.g., "Add Qdrant client", not "Added Qdrant client").

## Consequences

* **Positive**: Professional, international-standard codebase suitable for a Technical Artist portfolio.
* **Negative**: Requires constant attention to "s vs z" spelling differences (British vs American).
