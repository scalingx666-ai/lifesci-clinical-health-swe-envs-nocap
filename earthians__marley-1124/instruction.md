# Issue

**Title:** fix(medication): auto fetch linked item details in medication  linked item table (backport #1119)

## Description

Issue:
Selecting an existing Item in the linked_items child table of the Medication form did not auto-populate dependent fields like item_group, brand, manufacturer, description.

PR description:
This change fixes the Medication Linked Item child table so selecting an Item correctly pulls related values from the linked Item master.

Changes made:
Added fetch_from for item_group
Added fetch_from for brand
Added fetch_from for manufacturer ( will be fetched if the manufacturer is added in the item manufacturer form and set it as default)
Added fetch_from for description

The child table fields were missing fetch_from mappings, so Frappe had no field-level instructions to copy values from the selected Item. With these mappings in place, the form now auto-fills the expected details when an item is selected.
<hr>This is an automatic backport of pull request #1119 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `56b7df675bb7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.