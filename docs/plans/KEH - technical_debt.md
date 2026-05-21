# KEH Technical Debt Register

## Unresolved Technical Debts

_No open technical debts at the moment._

## Resolved Technical Debts

### pip-tools / pip 26 compatibility debt

- **Status:** Resolved
- **Opened:** 2026-02-06
- **Resolved:** 2026-05-21
- **Context:** `pip-tools v7.5.2` had compatibility issues with `pip 26.0+`, which forced a temporary workflow constraint.
- **Resolution:** Updated the locked dev dependency to `pip-tools==7.5.3` in `requirements-dev.txt`.
- **Verification:** `pip-compile` completed successfully in `keh-env`, and `pytest` passed (`1 passed`).
