# Knowledge Engine for Houdini (KEH)

> **Status**: Setup Phase

<!-- -->

> [!WARNING]
> **Work in Progress:** This project is currently under active development. Some modules, links and files may be placeholders.

A specialized RAG-based system designed to index, structure, and retrieve SideFX Houdini documentation.

## 🏗 Architecture (Src Layout)

```text
src/
    keh/                # Main Package
        core/           # Orchestration
        ingestion/      # Houdini Help Parsers
        storage/        # Qdrant Adapters
        retrieval/      # Semantic Search
docs/
    adr/                # Architectural Decision Records
    knowledge_base/     # Operational Guides
corpus/                 # (GitIgnored) Raw & Processed Data
```

## 🛠 Technology Stack (See ADR 004)

* **Language**: Python 3.11 (Managed via `keh-env`)
* **Vector DB**: Qdrant (Docker)
* **Dependency Management**: `pip-tools`
* **Quality Assurance**: `black`, `flake8`, `bandit`, `pytest`

## 🚀 Getting Started

1. **Environment**:

    ```bash
    conda activate keh-env
    pip install pip-tools
    pip-sync
    ```

2. **Hydration**:
    * Populate `corpus/raw/` with Houdini Help files (See `docs/adr/005-corpus-hydration.md`).

## 📜 Protocols

* **Development**: All code must reside in `src/keh`.
* **Commit Messages**: British English, Imperative Mood.
* **Safety**: "Zero-Hallucination" citations required for all outputs.

## Changelog

### Week of 2026-02-02 (Setup & Hardening)

* **Project Launch**: Effective Start Date: **2026-02-06**
* **Jira**:
  * Created project board.
  * Main task **KEH-1** ("Initializing the Project") completed (100% Done); 4h 30m logged.
* **Architecture**:
  * Defined stack (Python, Qdrant, Docker) and "Evidence-based answers" strategy.
  * Deployed Src Layout (`src/`, `tests/`, `tools/`) and documentation folders (`docs/adr`, `docs/knowledge_base`).
* **Environment & DevOps**:
  * Created dedicated Anaconda environment (`keh-env`).
  * Repository initialized and pushed to server.
  * Deployed public **Readme-driven repository** on GitHub.
* **QA & Security**:
  * Integrated Pre-commit hooks and dependency management via `pip-tools`.
  * Implemented `pip-audit` for vulnerability monitoring (noting pip 25.3 Technical Debt).
