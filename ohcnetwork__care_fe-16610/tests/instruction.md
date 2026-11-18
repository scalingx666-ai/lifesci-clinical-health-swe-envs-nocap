# Issue

**Title:** fix: allow clicking the dropdown caret icon in Autocomplete

## Description

## Description

.

The `CaretSortIcon` (dropdown arrow) in the shared `Autocomplete` component is absolutely positioned on top of the trigger `Button`, but it is rendered as a sibling of the `Popover`/`Drawer`, not as a descendant of the `Button` itself. Because of that, clicks landing directly on the icon never reach the `Button` click handling, so dropdowns built on `Autocomplete` (e.g. the medication request frequency dropdown) could not be opened by clicking the arrow icon, even though clicking elsewhere on the field worked fine.

This affects both the desktop (`Popover`) and mobile (`Drawer`) branches of `Autocomplete`, including the `shortcutId` badge variant.

## Fix

Add `pointer-events-none` to the icon (and its wrapper, for the shortcut-badge case) so clicks pass through to the underlying trigger button instead of being swallowed by the icon element. This matches how equivalent icons are already handled elsewhere in the codebase (e.g. `select.tsx`, `dialog.tsx`).

## Testing

- Verified `pointer-events-none` is an established Tailwind utility already used across `src/components/ui/*` in this codebase.
- Change is scoped to className additions only, no structural or behavioral changes to component logic.

## Screenshots

Not attached, this is a click-target fix with no visual change (icon appearance and position are unchanged, only its click-through behavior changes).

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Bug Fixes**
  * Improved autocomplete interaction by ensuring caret icons do not intercept clicks or pointer events.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c22b5c208a59`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.