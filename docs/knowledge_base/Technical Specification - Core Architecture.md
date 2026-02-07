# Technical Specification: Core Architecture (KEH)

**Version:** 1.0.0
**Status:** Approved
**Date:** 2026-02-07

## 1. Executive Summary

The Knowledge Engine for Houdini (KEH) is a localized, evidence-based retrieval augmented generation (RAG) system designed to answer technical queries about Houdini v21.0.596. It prioritizes **accuracy over creativity**, enforcing a "Zero-Hallucination" policy through a rigorous Cognitive Feedback Loop.

The system is architected as a set of 5 isolated functional contours, orchestrated to transform raw HTML documentation into a queryable semantic graph.

## 2. High-Level Architecture (C4 Container)

**[View Full C4 Container Diagram](../c4_diagrams/KEH%20-%20C4%20Diagram%20-%2002%20Container%20Level%20-%20en.md)**

(See external file for the authoritative diagram source to ensure Single Source of Truth)

## 3. Modular Decomposition (The 5 Contours)

### 3.1. Input Contour (Ingestion)

**Role:** Raw Material Acquisition.

* **Help Extractor:** Located in `src/keh/ingestion/`. Responsible for copying documentation from the User's Houdini installation and normalizing directory structures.
* **Local Raw Corpus:** A strictly defined filesystem area for normalized HTML/JSON assets.

### 3.2. Transformation Contour (The Factory)

**Role:** Processing and Enrichment.

* **Data Orchestrator:** Powered by Celery/Redis. Manages the pipeline queues.
* **Vector Factory:** Splits text into semantic chunks for Qdrant.
* **Graph Factory:** Extracts node relationships (SOP/DOP links) for Neo4j.

### 3.3. Analytical Contour (The Brain)

**Role:** Synthesis and Validation.

* **KnowledgeEngineCore:** The LLM driver (LangChain). Generates draft answers.
* **Reference Checker (GATEKEEPER):**
  * **CRITICAL:** Acts as the **Final Gatekeeper**.
  * **Function:** Audits every citation in the draft answer against the `Local Raw Corpus`.
  * **Logic:** If a path does not exist, the answer is rejected and returned to the Core for regeneration. **No answer leaves this contour without specific Reference Checker approval.**

### 3.4. Communication Contour (The Bridge)

**Role:** User Interface.

* **kehHoudiniPanel:** A PySide6 panel embedded in Houdini.
* **Gap:** The IPC mechanism between the Panel (Python 3.10/System) and the Core (Python 3.11/KEH-Env) is currently **To Be Decided** (REST vs Shared Memory vs Socket).

### 3.5. Service Contour (Infrastructure)

**Role:** Observability and Management.

* **Resource Manager:** Monitors VRAM/RAM to prevent crashes during rendering.
* **Telemetry:** Broadcasts system health at user-defined $2^n$ intervals (4s, 8s, 16s, 32s).
* **Single Source of Truth (SSOT):** MySQL stores all configuration and logs.

## 4. Operational Policies

### 4.1. Zero-Context Policy

If Semantic Search (Qdrant) and Structural Search (Graph) fail to return relevant context with a high confidence score (>0.75), the system must return a hardcoded fallback: *"No info found in documentation"*. Hallucinated "guesses" are strictly forbidden.

### 4.2. VRAM Safety

The Resource Manager has the authority to kill or offload LLM processes if VRAM usage approaches the "Render Danger Zone" (defined in settings). Offloading targets include CPU-quantized models or external APIs.
