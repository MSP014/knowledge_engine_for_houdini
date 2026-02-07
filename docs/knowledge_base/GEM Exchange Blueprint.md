# [Blueprint] KEH-GEM-[INDEX]: [Objective Name]

> **Target:** Antigravity Hector (Execution)
> **Source:** Gemini Hector (Strategy)
> **Context:** [Link to Jira Task or ADR]

## 1. Context & Preamble

* **Goal:** concise description of what we are building.
* **Constraints:** specific limitations (e.g., "No external libs", "Strictly use `pathlib`").
* **Required Context:** List files Antigravity *must* read before coding (e.g., `src/keh/core/schema.py`).

## 2. Architectural Logic (The "Why" & "How")

* **Pattern:** Define the pattern (e.g., Factory, Strategy).
* **Data Flow:** Input -> Processing -> Output.
* **Zero-Hallucination:** Explicitly state which local corpus files back this logic.
* **Pseudocode (Optional):**

    ```python
    # Logic flow visualization
    ```

## 3. Implementation Directive (The "What")

* **File Operations:**
  * `[CREATE] path/to/new_file.py`
  * `[MODIFY] path/to/existing_file.py`: Description of change.
* **Code Structure / Signatures:**

    ```python
    def expected_function(arg: Type) -> ReturnType:
        ...
    ```

* **Dependencies:** List new `pip-tools` requirements if any.

## 4. Validation (Definition of Done)

* **Command:** `pytest tests/path/to/test.py`
* **Quality Gate:** `flake8` and `bandit` must pass.
* **Manual Verify:** "Check that generated JSON contains key 'XYZ'".

## 5. Q&A / Edge Cases

* *What if X happens?* -> Handle by Y.
