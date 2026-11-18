# Issue

**Title:** [ENG-707]: Default account close reason to completed for settled accounts

## Description

### Proposed Changes

Adjusts the close-account dialog in `AccountShow` so that the close reason defaults sensibly to the account's balance:

- **Zero balance (settled account):** the reason defaults to **Closed Completed**.
- **Non-zero balance:** unchanged — defaults to **Closed Bad Debt** with the existing option order.

The default is computed in the existing `useEffect` that seeds `closeAccountStatus.reason`, so it applies to every entry point that opens the dialog (the "Settle & Close" button, the mobile dropdown item, and the billing-lifecycle stepper). Closed accounts continue to show their actual billing status.

Ticket: **ENG-707**

### Notes

- Scope is intentionally minimal — a single default/ordering tweak in `AccountShow.tsx`.
- Playwright E2E coverage was scoped out for this UI-only default change at the task owner's direction.

@ohcnetwork/care-fe-code-reviewers


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * The close-account dialog now selects a default reason based on the account’s availability, billing status, and balance.
  * Unavailable accounts default to the bad-debt reason. Accounts with billing already closed use their current billing status.
  * Accounts with a zero balance default to completed, while accounts with a remaining balance default to bad debt.
  * These defaults are applied consistently whether the dialog is opened from the primary button, dropdown, or billing lifecycle stepper.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c9519b7f3f50`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.