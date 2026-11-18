# Issue

**Title:** fix: preserve linked Item name when updating Observation Template

## Description

Issue description

Updating a billable Observation Template can unintentionally replace its linked Item's descriptive name with the Item Code. This was observed while correcting HSN/SAC values through Actions → bulk update.

The HSN/SAC update succeeds, but the same save changes the Item Name.

Example

- Observation Template: CT Head (Plain) - CTS005
- Linked Item and Item Code: R-0006
- Item Name before update: CT Head (Plain) - CTS005
- HSN/SAC before update: 999314
- HSN/SAC after update: 999316

After bulk updating the Observation Template's HSN/SAC, the linked Item  shows the correct HSN/SAC, 999316, but its Item Name becomes R-0006. The Item activity log records both changes in the same update.

Steps to reproduce

1. Open a billable Observation Template linked to an Item whose Item
   Name differs from its Item Code.
2. Ensure the Observation Template's template field, which links to
   Terms and Conditions, is empty.
3. Change the Observation Template's HSN/SAC, either by saving its form
   or through Actions → bulk update.
4. Open the linked Item and inspect its Item Name and HSN/SAC.

Actual result:-
The Item receives the new HSN/SAC, but its Item Name changes to its
Item Code.

Expected result:-

The linked Item receives the new HSN/SAC and retains the descriptive
name associated with the Observation Template.

Root cause:-
An HSN/SAC change triggers the Observation Template's on_update handler, which calls the shared update_item_and_item_price() function.

For every template other than a Lab Test Template, that function used doc.template as the Item Name. On an Observation Template, template is a separate Terms and Conditions field; the observation's descriptive name is stored in doc.observation.

When doc.template is empty, the sync assigns an empty Item Name. ERPNext's Item validation then fills the empty Item Name with the Item Code. This produces the change seen in the Item activity log.

Fix applied:-
The shared update function now selects doc.observation as the Item Name when the source document is an Observation Template. Lab Test Templates and other template types retain their previous name selection.

Because the selected name is also used when updating an existing Item Price, that path receives the correct observation name as well.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1dda18fc2c5c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.