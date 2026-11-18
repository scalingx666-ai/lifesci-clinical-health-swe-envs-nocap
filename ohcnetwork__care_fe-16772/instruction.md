# Issue

**Title:** [ENG-990] Refactor dispense order view's footer to a component

## Description

> [!NOTE]
> Ticket: **[`CIMPL-259`](https://openhealthcarenetwork.atlassian.net/browse/CIMPL-259) / [`ENG-990`](https://openhealthcarenetwork.atlassian.net/browse/ENG-990)**

Dispense oder view's footer code just moved to a component. This enables plugs to override this component.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Added a sticky action bar for pharmacy dispense orders.
  * Added actions for holding, resuming, completing, returning medications, printing, navigating to the pharmacy, and marking orders as entered in error or abandoned.
  * Added confirmation safeguards for cancellations involving issued or balanced invoices.

* **Bug Fixes**
  * Added a warning when preparation cannot be resumed after an invoice is fully paid.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `038a33ff9de1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.