# Issue

**Title:** fix(inpatient record): confirm patient identity before discharging (backport #1256)

## Description

Clicking "Discharge" on an Inpatient Record triggers an immediate, irreversible discharge - no confirmation of any kind. In a hospital with multiple patients admitted at once, a misclick or selecting the wrong record discharges the patient instantly, with no chance to catch the mistake first.

## Fix

Added a `frappe.confirm` prompt before the discharge call goes through, showing enough to positively identify the patient:

- Patient name, always
- Patient ID - only when it differs from the name, to avoid redundant noise
- Gender and age (from DOB), when available

The message adapts to how much there is to confirm: a single extra detail reads inline ("You are about to discharge **Lisa** (Gender: Female)."), multiple details render as a small table, and a clear "This action cannot be undone" warning is always shown.
<img width="1917" height="510" alt="Screenshot from 2026-10-07 10-52-12" src="https://github.com/user-attachments/assets/89e39112-75c0-433c-968b-89fc0f4f6ed2" />
<img width="1917" height="510" alt="Screenshot from 2026-10-07 10-52-26" src="https://github.com/user-attachments/assets/adb6ab3e-749d-4b36-8534-8c65d7b08528" />
<hr>This is an automatic backport of pull request #1256 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2acfe477bc10`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.