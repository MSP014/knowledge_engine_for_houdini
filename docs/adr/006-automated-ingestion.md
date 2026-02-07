# ADR 006: Automated Ingestion & Configuration

## Status

Accepted (Supersedes [ADR 005](005-corpus-hydration.md))

## Context

Originally (ADR 005), we planned for the user to manually copy Houdini Help files into `corpus/raw`. This approach is fragile, error-prone, and creates friction for the user ("Hydration Step"). With the introduction of the **5-Contour Architecture** and the **Input Contour (Ingestion)**, we now have a `Help Extractor` component capable of automating this process.

## Decision

### 1. Automated Extraction

* The system will **automatically copy and normalize** documentation from the user's installed Houdini version.
* **Manual copying to `corpus/raw` is deprecated.**

### 2. Configuration via UI

* The user will provide the path to their Houdini installation (e.g., `C:\Program Files\Side Effects Software\Houdini 21.0.596`) via the **kehHoudiniPanel** (Communication Contour).
* The `Data Orchestrator` (Transformation Contour) will trigger the `Help Extractor` to populate `corpus/raw`.

### 3. Source of Truth

* The `corpus/raw` directory remains the local storage for raw HTML, but it is **read-only** for the user and **write-managed** by the system.

## Consequences

* **Positive**: Zero-setup friction for the user; guaranteed data consistency; aligns with "The Factory" automation philosophy.
* **Negative**: Requires implementation of filesystem permissions logic to ensure the `Help Extractor` can read from Program Files (usually fine in User mode, but worth noting).
