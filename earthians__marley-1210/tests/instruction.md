# Issue

**Title:** fix: render observation note/findings as HTML and fix multi-note save (backport #1207)

## Description

- Note, findings and interpretation fields were declared as plain Text fields but populated with rich HTML from a Text Editor field, so raw markup showed up instead of rendered content. Switched them to HTML fieldtype and styled to match the surrounding observation card.

Before:
<img width="1902" height="898" alt="Screenshot from 2026-09-11 15-44-08-1" src="https://github.com/user-attachments/assets/a447816e-b23a-4ff9-b74c-245d64eaad19" />

After:
<img width="1918" height="907" alt="Screenshot from 2026-09-12 09-54-41" src="https://github.com/user-attachments/assets/409eeedf-ab3a-4845-b01d-eb6cf7b29155" />

- Also fixed add_note() only queuing a note for saving when the shared results array was completely empty, which silently dropped notes added to any observation after the first one in the same save.<hr>This is an automatic backport of pull request #1207 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e1e0e22b8cb6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.