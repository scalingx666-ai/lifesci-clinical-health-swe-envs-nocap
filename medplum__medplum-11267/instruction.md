# Issue

**Title:** [React] AsyncAutocomplete and its wrappers take an aria-label

## Description

Lets `AsyncAutocomplete`, `ResourceInput`, and `MultiResourceInput` name their search field with `aria-label`, for fields shown without a visible label.

Until now, callers had two ways to do that, and neither worked. A visually hidden `label` still takes a line of space above the input, because Mantine draws the `<label>` as an inline-block. An `aria-label` compiled, since TypeScript doesn't check hyphenated JSX attributes a component doesn't declare. But it fell  into `...rest` and went to `Combobox`, which renders no element of its own, so it never reached the input.

- `aria-label` is now a declared prop on all three, and goes on the search field. Its tsdoc notes that the field, and so the name, is hidden while disabled or at `maxValues`. For `ResourceInput`, that's whenever a resource is chosen.
- `SearchFilterValueInput`'s `ariaLabel` is renamed to `aria-label` to match, along with its one caller, `SearchFilterPopover`. The component isn't exported, so no public API changes. The popover tests now find value fields by name.
- `ServiceFacilitiesField` names its input with `aria-label` when linked facilities sit under its heading. That replaces the stylesheet that made its hidden label a block.

This prepares for the SchedulingWorkspace calendar pickers, which name their search fields this way.

Not covered here: `SearchFilterValueInput` still doesn't name its reference, date-time, or quantity inputs, and the legacy `SearchFilterEditor` and `SearchFilterValueDialog` don't name their value inputs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8c3c4daf609a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.