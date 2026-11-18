# Issue

**Title:** feat(desk-v2): add v1's Portal entry to the rail

## Description

no-docs

- Adds v1's missing Portal entry to `erpnext/rail/erpnext/erpnext.json`: a `Module` row for the Portal module, after Assets, as in v1's dock (`erpnext/dock/erpnext/erpnext.json`). Lucide icon `panels-top-left`, the v1 icon.
- The 18 sidebars (`erpnext/sidebar/module_def_*`) are unchanged. The converter (`~/wt/apps-fan/fan.py`, shared with frappe/frappe#47746, not shipped) compared every v1 sidebar with its v2 sidebar by DocType row: v2 already holds every DocType row v1 does, in v1's order and sections. Nothing to add.
- What v1 holds and v2 does not is only what v2 cannot open: Report rows (about 200), Dashboard (9), Workspace "Home" (about 14) and classic Page rows (6). They stay out.
- Modules with more than one v1 sidebar: Accounts (Accounts, Financial Reports, Invoicing, Payments), Buying, CRM, Assets, Manufacturing, Projects, Quality, Selling, Stock and Support (each with a v1 "Workspace Sidebar" beside the module sidebar), Setup (Setup, ERPNext Settings, Home). Each was compared against its module's v2 sidebar. The extra ones hold no DocType row the module's v2 sidebar lacks, so none is merged or listed in v2.
- Communication and ERPNext Integrations stay `Module` rail rows (no v2 sidebar), so their v1 DocType rows (Communication Medium, Plaid Settings) are drawn from the module's contents already.

Portal is in the resolved rail but does not draw yet: the module owns only child-table doctypes, so the renderer finds no address and skips the row (see the comment in `erpnext/tests/test_navigation.py`, updated here: it said Portal was deliberately off the rail; the owner ruled it on, 2026-11-17). v1's Portal sidebar is empty too. The row shows once the module owns a doctype.

The rail file's `modified` moves, because sync skips a record whose `modified` is unchanged and existing sites would never get the row.

## How tested
- Migrated a preview site with frappe#47746 and this branch: `resolve_navigation("erpnext")` returns the 20 rail rows plus Portal; the rail in the browser draws the same 20 (Portal skipped); the 18 sidebars are byte-identical to the base.
- `erpnext.tests.test_navigation`: 12 pass, with the rail test now expecting 21 keys (it failed in CI on the new row).

Runtime: one more rail row in the boot payload (about 0.2 KB); nothing else runs.

Desk v1: unchanged. A `Rail` record is read only by the v2 shell.

## Screenshots
No visible change (Portal is hidden while its module is empty). Stock sidebar on the branch, unchanged:

![Stock](https://raw.githubusercontent.com/shariquerik/erpnext/pr-screenshots/47735-after-erpnext-stock.png)

Refs frappe/frappe#47735

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3c1fbcd174da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.