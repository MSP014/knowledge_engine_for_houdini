# Technical Debt: Pip Version Lock

**Status:** Active
**Created:** 2026-02-06
**Related Issue:** `pip-tools` incompatibility with `pip >= 26.0`

## Problem

We are forced to pin `pip==25.3` (vulnerable to CVE-2026-1703) because `pip-tools v7.5.2` crashes on `pip 26.0+` (AttributeError: 'PackageFinder').

## Mitigation

* **Action**: `pip` is pinned to 25.3.
* **Security**: Added to `pip-audit` ignore list in `.pre-commit-config.yaml`.
* **Risk**: Low (Developers only).

## Resolution Trigger

We need to wait for a `pip-tools` release that supports `pip 26.0`.

**Check Frequency**: Weekly (Every Monday).
**Estimated ETA**: Late Feb 2026 (Based on historical quarterly lag).

## Action Plan

1. Check release: `pip index versions pip-tools`
2. If new version > 7.5.2 exists:
    * Upgrade pip: `pip install --upgrade pip`
    * Upgrade pip-tools: `pip install --upgrade pip-tools`
    * Test compilation: `pip-compile requirements.in`
    * If success: Remove ignore entry from `.pre-commit-config.yaml`.
