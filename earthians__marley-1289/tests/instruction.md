# Issue

**Title:** fix(sample collection): multi-level panel tree support and checkbox cascade fix (backport #1248)

## Description

- Checkbox fix: selecting a nested component (e.g. a leaf inside a panel) no longer force-selects its parent panel and sibling components. Also fixed a follow-up case where selecting one of several same-colored standalone samples incorrectly cascaded into an unrelated panel's own components.
- Multi-level panel support: the sample tree now correctly renders, selects, and collects panel templates nested at any depth (e.g. a package containing a sub-panel containing individual tests), not just one level.
- Fixed two related data bugs this exposed:
  - Invoicing or creating a Sample Collection for a multi-level template (via Sales Invoice or Service Request) could create a duplicate, orphaned parent Observation for an intermediate panel (e.g. a "Lipid Profile" sub-panel under a "Package 1" template) in addition to the correctly-chained one — the duplicate would also surface on the Diagnostic Report as a second entry for the same panel.
  - `has_direct_leaf_component()` only checked direct children, so a  template whose only content was a nested sub-panel (no leaf directly on it) would get no Sample Collection row created at all. Made it recursive.

<img width="1900" height="876" alt="Screenshot from 2026-10-05 12-58-21" src="https://github.com/user-attachments/assets/d312ce54-b6f8-4b4b-b801-68194687e8a7" />
In the above image shows the patient choosen the Package 1 and URINE MICROALBUMIN observation templates<hr>This is an automatic backport of pull request #1248 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3a88966cdde4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.