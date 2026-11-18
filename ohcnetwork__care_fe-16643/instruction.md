# Issue

**Title:** 🧹 Remove stale diagnosis__* i18n keys

## Description

## Description

Removes five orphaned translation keys from `public/locale/en.json`:

- `diagnosis__confirmed`
- `diagnosis__differential`
- `diagnosis__principal`
- `diagnosis__provisional`
- `diagnosis__unconfirmed`

These keys have zero literal and zero dynamic (template-literal) references anywhere in `src/`, `tests/`, or `plugins/`. They were found to be dead while writing user-facing documentation for the Condition module.

Only `public/locale/en.json` was touched. Non-English locale files are managed via Crowdin and are intentionally left untouched.

Note: the `Diagnosis_{category}__title` keys (used for dynamic category titles) are still in active use and were intentionally left in place.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Style**
  * Removed unused English translations for several diagnosis statuses.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `26e1f50433e3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.