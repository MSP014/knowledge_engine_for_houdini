# ADR 004: Technology Stack (Override)

## Status

Accepted

## Context

While referencing the "Nvidia Showreel Case 01" standards (which mandate Python 3.10), KEH operates as a standalone backend service. We prioritize performance and modern language features over legacy compatibility with Omniverse Kit's internal Python.

## Decision

### 1. Python Version

* **Version**: **Python 3.11**
* **Rationale**: Significant performance improvements over 3.10; better Type Hinting support.
* **Environment**: Development is strictly confined to the `keh-env` Anaconda environment.

### 2. Database

* **Vector Engine**: **Qdrant**
* **Deployment**: Docker Container.
* **Rationale**: Rust-based, high performance, excellent Python client, supports hybrid search (dense + sparse).

### 3. Orchestration & Transformation ("The Factory")

* **Task Queue**: **Celery**
* **Broker**: **Redis** (Docker)
* **Rationale**: Asynchronous processing is required for heavy ingestion and vectorization tasks to avoid freezing the UI.

### 4. Knowledge Graph

* **Graph Engine**: **Neo4j** (Docker)
* **Rationale**: Required for storing strict hierarchical relationships (SOP/DOP/VOP) and node interconnections that Vector search effectively misses.

### 5. User Interface ("The Bridge")

* **Framework**: **PySide6** (Qt for Python)
* **Integration**: Embedded directly into Houdini as a Python Panel.
* **Rationale**: Native look and feel, direct access to `hou` module.

### 6. AI & Logic ("The Brain")

* **Orchestrator**: **LangChain**
* **LLM Provider**: **OpenAI** / **Groq** (External API)
* **Monitoring**: **psutil**, **pynvml** (for Hardware Telemetry).

### 7. Containerization

* **Platform**: Docker / Docker Compose.
* **Usage**: Hosting the Qdrant service and potentially the API layer in the future.

## Consequences

* **Positive**: Access to modern Python features and speed buffers.
* **Negative**: Code cannot be directly copy-pasted into an Omniverse Extension (Python 3.10) without modification, but KEH is designed as an external tool, so this is acceptable.
