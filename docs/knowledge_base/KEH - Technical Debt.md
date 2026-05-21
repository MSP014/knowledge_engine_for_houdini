# KEH Technical Debt

This document tracks intentional architectural shortcuts, outdated dependencies, and security exceptions within the Knowledge Engine for Houdini (KEH). All items here must eventually be resolved to meet "Top Mode" (NVIDIA-grade) engineering standards.

## [SECURITY] Pip 25.3 Vulnerability (CVE-2026-1703 & CVE-2026-3219)

- **Status:** Mitigation Enforced (Upstream Lock)
- **Severity:** High (Security) / Critical (Dependency Chain)
- **Description:**
  - `keh-env` is running `pip 25.3`, which is flagged for **CVE-2026-1703** and **CVE-2026-3219**.
  - **Constraint:** We cannot upgrade to `pip 26.0+` because it breaks `pip-tools` (current version used for dependency management).
- **Action Plan:**
  - [x] **DO NOT UPGRADE PIP** until `pip-tools` releases a compatible fix.
  - [ ] **Weekly check for `pip-tools` updates** (Last Check: 2026-05-04).
    - *Rule: If the current date is more than 7 days past the Last Check date, run `pip index versions pip-tools`. If no update >= 26.0 compatibility is available, update the Last Check date here to today.*
  - [ ] Once fixed, upgrade `pip` and `pip-tools` simultaneously.
  - [ ] **Cleanup**: After successful upgrade, remove `--ignore-vuln CVE-2026-1703` and `--ignore-vuln CVE-2026-3219` from `.pre-commit-config.yaml`.

## [SECURITY] Black 26.1.0 Vulnerability (CVE-2026-32274)

- **Status:** Mitigation Deferred (Blocked by Upstream `pip-tools` Lock)
- **Severity:** High (Security) / Low Risk (Local Context)
- **Description:**
  - `black 26.1.0` is flagged for **CVE-2026-32274**.
  - **Constraint:** Fixed in `26.3.1`, but we cannot upgrade cleanly because it requires `pip-compile` (which is broken by `pip-tools` incompatibility with `pip 26.0+`).
- **Action Plan:**
  - [ ] **Weekly check for `black` updates** (Last Check: 2026-05-04).
    - *Rule: If the current date is more than 7 days past the Last Check date, run `pip index versions black`. If an update >= 26.3.1 is available AND `pip-tools` issue is resolved, proceed to upgrade.*
  - [ ] Defer upgrade until `pip-tools` is fixed.
  - [ ] Once `pip-tools` is fixed, regenerate `requirements-dev.txt` pulling `black >= 26.3.1`.
  - [ ] **Cleanup**: After successful upgrade, remove `--ignore-vuln CVE-2026-32274` from `.pre-commit-config.yaml`.

## [SECURITY] Pytest (CVE-2025-71176), Requests (CVE-2026-25645), etc.

- **Status:** Mitigation Deferred (Blocked by Upstream `pip-tools` Lock)
- **Severity:** Medium
- **Description:**
  - Multiple vulnerabilities discovered in `pytest`, `requests`, `python-dotenv`, and `pygments`.
  - **Identified CVEs**: `CVE-2025-71176`, `CVE-2026-25645`, `CVE-2026-28684`, `CVE-2026-4539`.
  - **Constraint:** Cannot upgrade packages cleanly because `pip-compile` is broken due to `pip-tools` incompatibility with `pip 26.0+`.
- **Action Plan:**
  - [ ] Defer upgrade until `pip-tools` is fixed.
  - [ ] Once `pip-tools` is fixed, regenerate requirements files to pull secure versions.
  - [ ] **Cleanup**: After successful upgrade, remove related `--ignore-vuln` flags from `.pre-commit-config.yaml`.

## Future Architectural Enhancements

- **Hardcoded Environment Logic in Hooks**:
  - **Status:** Resolved (2026-05-04)
  - **Description:** Pre-commit hooks previously relied on absolute user-specific paths to the `keh-env` interpreter.
  - **Action Taken:** Migrated to `conda run -n keh-env` in `.pre-commit-config.yaml` to ensure portability across different workstations.
- **Corpus Versioning Isolation**:
  - **Status:** Planned
  - **Description:** Currently, the directory structure for extracted documentation is being finalized. We need to ensure rigid build version isolation (e.g., `v21.0.596`) to prevent data mixing.
  - **Action Required:** Implement automated version detection in the ingestion pipeline and enforce directory naming conventions.
