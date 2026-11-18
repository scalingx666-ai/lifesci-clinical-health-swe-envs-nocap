# Issue

**Title:** fix(healthcare): prevent false "Not Saved" state in Diagnostic Report after Frappe update (backport #1042)

## Description

Issue:-
After upgrading to the latest Frappe/ERPNext version, opening an already approved Diagnostic Report was showing the form in an unsaved state even though no user changes had been made.

Testing
1. Opening an approved Diagnostic Report after the Frappe/ERPNext update
2. Confirming the form no longer shows a false "Not Saved" indicator on load
3. Verifying that actual user edits still mark the form as unsaved

<img width="1128" height="313" alt="image" src="https://github.com/user-attachments/assets/cc7adec3-44c0-418e-98be-120006f9cc3c" />

This was causing confusion because:
- the report status was already approved
- no visible data was changed by the user
- the form header still showed "Not Saved"

Root Cause:-
The Diagnostic Report observation widget renders result fields using a custom FieldGroup-based UI.
In newer Frappe versions, field initialization/default hydration during render can trigger the custom result field change handler. That handler was directly calling frm.dirty(), which marked the document as unsaved during initial render instead of only during actual user edits.

As a result, simply loading the Diagnostic Report UI could incorrectly set the form to a dirty state.

Fix
After upgrading to newer Frappe/ERPNext versions, the Observation Widget's result field change event could be triggered during field initialization and value hydration. Since the handler directly called frm.dirty(), approved Diagnostic Reports were incorrectly marked as Not Saved immediately after loading.

This fix adds a render-time guard to ignore change events fired during field initialization. As a result:

  - Initial observation value hydration no longer marks the form as unsaved.
  - Actual user modifications continue to mark the form dirty as expected.
  - The behavior remains consistent and compatible across newer Frappe version

Files Changed
- healthcare/public/js/observation_widget.js

Notes
After pulling this change, run:
bench build --app healthcare<hr>This is an automatic backport of pull request #1042 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f2130f6c7d1b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.