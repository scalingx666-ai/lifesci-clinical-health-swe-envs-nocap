# Issue

**Title:** [ENG-613] Added expiry date to supply delivery table

## Description

## Changes

Added expiry date to supply delivery table

_Tests skipped — trivial change._

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added an **Expiry** column to the Supply Delivery table.
  * Each delivery row now shows the relevant expiry date formatted as **dd/MM/yyyy**.
  * When an expiry date isn’t available, the table displays **“–”** instead.
  * Improved product links to support navigation for both internal and external products.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dea49853619e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.