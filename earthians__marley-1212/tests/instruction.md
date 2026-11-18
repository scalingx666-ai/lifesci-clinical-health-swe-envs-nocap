# Issue

**Title:** fix: sanitize observation note input and fix mislabeled note heading

## Description

Addresses greptile-apps review on PR #1210 (backport of #1207, already merged to develop):

- add_note() wrote the note straight to the DB via frappe.db.set_value, bypassing Observation.sanitize_input(), so an authorized user could store event-handler markup that executes when the report is viewed. Sanitize with frappe.utils.sanitize_html() at the same write site, matching the sanitizer already used in validate().
- render_note_html() always labeled its content "Note" even when reused for Findings/Interpretation on Imaging observations. Added a label parameter and pass the correct heading at each call site.
- added missing bottom spacing on standalone observation card

Before:
<img width="1918" height="869" alt="Screenshot from 2026-09-15 11-25-32" src="https://github.com/user-attachments/assets/79c6c4c5-542f-48cf-8092-2cd36f30beb4" />

After:
<img width="1903" height="891" alt="Screenshot from 2026-09-15 11-33-16" src="https://github.com/user-attachments/assets/30dbef05-b9ae-463c-9de0-c341e40a1b33" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `357222f6b22e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.