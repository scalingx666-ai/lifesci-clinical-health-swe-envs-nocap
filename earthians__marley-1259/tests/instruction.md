# Issue

**Title:** feat: migrate healthcare desk navigation to Sidebar/Dock system

## Description

Migrates the healthcare app's desk navigation away from the deprecated `Workspace Sidebar`/`Desktop Icon` doctypes to Frappe new `Sidebar`/`Dock` system, matching the pattern erpnext uses for its own modules.

- Adds 8 separate `Sidebar` fixtures under the `Healthcare` module (Healthcare, Diagnostics, Inpatient, Insurance, Outpatient,
  Emergency, Rehabilitation, Healthcare Setup), each with its own section-specific items.
- Adds a `Dock` fixture so each section gets its own icon in the navigation rail, rather than one combined icon.
- Fixes a routing/highlighting bug this split exposes: Frappe's `resolve_sidebar()` attributes every workspace of a module to every sidebar sharing that module (it assumes one sidebar per module). With 8 sidebars under one module, this caused wrong icon highlighting, a 2-click lag before the sidebar updated, and random wrong URL shell-prefixing.

https://github.com/user-attachments/assets/487ac86e-5eee-4718-bbda-1dc25701b412

no-docs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `148dcca71c8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.