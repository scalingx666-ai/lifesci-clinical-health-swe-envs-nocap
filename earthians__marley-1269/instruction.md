# Issue

**Title:** fix(observation): render imaging result as text editor (backport #1243)

## Description

Issue description:
Imaging Observation results were saved as rich text HTML, but when the Observation Template had no permitted data type, the standalone Observation form rendered the Result field as a plain input, causing raw HTML tags to appear.

Fix applied / changes made:
Updated the Observation form result-control selection logic to render the Result field as a Text Editor whenever the Observation category is Imaging, otherwise continuing to use the permitted data type mapping.

Before fix:
<img width="729" height="552" alt="image" src="https://github.com/user-attachments/assets/ac835efd-7a12-4479-99ca-c9658df83be9" />

After fix:
<img width="1062" height="611" alt="image" src="https://github.com/user-attachments/assets/82d015d2-75cb-41d1-a66d-2eab5f3a8d66" />

Logic applied:
If observation_category is Imaging, use Text Editor for Result because imaging findings are stored as rich text; for all other observations, keep using permitted_data_type to choose the correct control.
<hr>This is an automatic backport of pull request #1243 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `131eb3667cab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.