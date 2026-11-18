# Issue

**Title:** [ENG-1227] feat: add PatientPrintPageHeader component for consistent patient information display across print previews

## Description

## Proposed Changes
single page
<img width="675" height="699" alt="image" src="https://github.com/user-attachments/assets/315013d1-c62c-4751-8d57-e019be94d323" />

multi page
<img width="675" height="699" alt="image" src="https://github.com/user-attachments/assets/fa03b532-5bb5-4b86-afa1-3b12db03b024" />



Fixes ENG-1227

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [x] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [x] Complete QA on mobile devices.
- [x] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Patient names and available official identifiers now appear in print headers for appointment, consultation, medication, prescription, billing, and diagnostic documents.
  * Headers repeat on printed pages after the first page and keep text on one line, shortening long values when needed.
  * Documents without an available patient record continue to print without a patient header.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e5ddbb04ebb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.