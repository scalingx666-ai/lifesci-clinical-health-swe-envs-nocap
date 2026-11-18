# Issue

**Title:** (Docs) Document Provider Workflows

## Description

Provider's documentation still lists messaging, labs, and medications as coming soon, although these workflows are implemented. Add task-oriented guides and link them from the Provider landing page.

- Explain prerequisites, everyday actions, status meanings, and troubleshooting for each workflow.
- Name the Orders guide **Orders (Labs & Imaging)** and preserve the application's current navigation and form labels in instructions.
- Cover imaging facility and study selection, appointment coordination, requisitions, returned report documents, and supported attachment mappings. Explain the current limitation for reports containing only `DiagnosticReport.conclusion` and link to the separate DICOM viewer guide.
- Add a shared lab/imaging workflow diagram. Highlight that **Completed** includes preliminary and partial reports and that acknowledgement and follow-up need their own workflow.
- Clarify external message delivery, whole-cart medication checkout, and synchronization with the prescribing service.
- Use the current Hugo layout, shortcodes, and generated sidebar ordering. Add a CI check comparing the Orders guide title, index link, and navigation instruction with the Provider tab label in source.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `431a751d3d38`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.