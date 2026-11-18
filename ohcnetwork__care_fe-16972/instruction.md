# Issue

**Title:** Let extension fields choose their column in supply delivery tables

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/104
<!-- entire-trail-link-end -->

## Proposed Changes

Extension fields can now choose where their column appears in the supply delivery tables. Until now, every extension field landed in one block at the end.

- **Schema hint:** a field sets `x-ui.placement.after` to an anchor, for example `"placement": {"after": "pack_quantity"}`.
  - The anchors for each entity are listed in `ExtensionAnchors` (`src/Utils/schema/types.ts`).
  - `sale` and `purchase` mean "after the whole column group".
- **Rendering:** `groupFieldsByAnchor` (`src/hooks/useExtensions.tsx`) groups the fields by anchor once per table. The add-delivery form header, its rows, and the deliveries table each render a group right after its column.
- **Fallback:** a field without a placement, with an unknown anchor, or anchored to a column the table doesn't show stays at the end, before Actions.
  - Internal transfers hide Pack size, Pack qty and Purchase, so fields anchored there fall back the same way.
  - Existing schemas render exactly as before.
  - In the add form, `discount` uses the Tax slot because that cell holds both the tax and discount selectors.
- **Header/row alignment fix:** the add-form header used the `supply_delivery_table` context to pick its columns, while the rows used `supply_delivery_form`. Both now use the same grouping.
- **Hidden/const fields:** these no longer get an empty labelled column. Their hidden inputs now render inside the row's Actions cell.
- **Other extension screens** (account, payment reconciliation, delivery order, patient) are unchanged and ignore the hint until they opt in.

Companion plugin change: ohcnetwork/care_odoo_be#33. It puts Free quantity after Pack qty and Purchase Discount after the Purchase columns. The two PRs can merge in either order.

**Care Apps heads-up:** `SmartExternalDeliveryRow` now takes `extensionColumns` instead of `processedExtensions`. This only matters if an app overrides that component.

### Testing

- `tsc`, ESLint and knip pass.
- Tested against a local backend running care_odoo, with `GET /api/v1/extensions/` intercepted to add the placement hints:
  - **With hints:** the add form and the deliveries table show Free quantity after Pack qty and Purchase Discount after the Purchase columns. Header leaf columns match row cells, and the inputs stay bound to `items.N.extensions.<extension>.<field>`.
  - **No hints:** the layout is identical to develop.
  - **Unknown anchor:** the field goes to the end.
  - **`discount` anchor:** the field lands after Tax in the add form and after Disc. in the deliveries table.
  - **Internal-transfer table:** fields anchored to hidden columns go to the end.
  - **Field blacklisted only for `supply_delivery_table`:** the deliveries table hides it, and the add form stays aligned.

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * Supply-delivery extension fields can now appear beside their configured columns in delivery forms and inventory tables, with unanchored fields shown at the end.
  * Extension fields can be hidden from table columns while remaining available to forms.
* **Bug Fixes**
  * Invalid column placement hints are no longer applied, preventing malformed settings from affecting field display.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0faab2333a80`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.