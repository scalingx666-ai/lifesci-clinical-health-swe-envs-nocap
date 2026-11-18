# Issue

**Title:** fix(observation): allow imaging observations to select case-specific report templates (backport #1316)

## Description

Problem

Imaging Observations could not choose a case-specific Findings or Interpretation template. Both fields were read only because they had read_only: 1 and Frappe also locks fields fetched from another document. When no template was mapped, the empty read only fields could appear hidden.

After Change:-
<img width="917" height="487" alt="image" src="https://github.com/user-attachments/assets/da119d8a-a47c-4979-a2d6-392faf6aea80" />

After changing template:-
<img width="933" height="477" alt="image" src="https://github.com/user-attachments/assets/a5417c7f-d456-4675-9de6-7013e131a7c5" />

Changes made

- Removed read_only and added fetch_if_empty to both template fields. This preserves mapped defaults while allowing an override on a draft Observation.
- Added depends_on for Imaging. Previously the fields were read only across all Observation categories; without this condition, making them editable would expose template selectors on Laboratory, Vital Signs, and other Observations.
-If findings and interpretation template is mapped in observation template, then by default it will render it. If required, we can select different template based on case.
-If no finding and interpretation template is mapped in observation template, then in observation it will be empty by default, but we can select the required result and interpretation template from the selection dropdown.

- If Patient changes on a saved draft, the form now asks the clinician to save before selecting a template. It also checks Patient again when the rendered content returns.

<img width="691" height="180" alt="image" src="https://github.com/user-attachments/assets/d2d50abc-588f-40ea-a4a2-4a13937b2c0b" />

- An older request can no longer restore a template after a newer selection
<hr>This is an automatic backport of pull request #1316 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d676b81ff46b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.