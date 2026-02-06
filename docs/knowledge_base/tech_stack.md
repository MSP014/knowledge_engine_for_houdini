# Technology Stack & Architecture

## Core Runtime

* **Python 3.11**: Primary development language. Chosen for performance (vs 3.10) and advanced typing features.
  * **Environment**: `keh-env` (Anaconda).
* **Pydantic V2**: Data validation and schema serialization.

## Data Storage

* **Qdrant**: High-performance Vector Database (Rust-based).
  * **Deployment**: Docker Container (Official Image).
  * **Interface**: `qdrant-client` (gRPC/HTTP).
* **FileSystem (Corpus)**:
  * Raw HTML/JSON extracted from Houdini Help.
  * Processed Markdown/JSON for indexing.

## Infrastructure

* **Docker & Docker Compose**: Service orchestration (Qdrant, potentially API).
* **Git**: Version control with strict `.gitignore` for corpus/assets.

## Development Tools

* **Linting/Formatting**: `black`, `flake8`, `isort`.
* **Security**: `bandit`, `pip-audit`.
* **Testing**: `pytest`.
* **Dependency Management**: `pip-tools` (`requirements.in` -> `requirements.txt`).
