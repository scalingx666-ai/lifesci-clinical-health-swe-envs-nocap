# Issue

**Title:** OBPIH-8070 Fix small issues from React upgrade

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-8070?atlOrigin=eyJpIjoiZTI3M2Y0OWI1N2JjNGNjYWI5MDJmMGYzYWIwZGU0ZDkiLCJwIjoiaiJ9

**Description:**
Fixed bugs:
- React Router 7 applies navigate() as a low-priority React update, while the wizard's nextPage() was a normal update. The next page rendered first, before the URL had the ID
- react-confirm-alert 2.6.1 -> 3.0.6
- Fixed cycle count tabs (It now reads window.location.search)
- Combined shipment and invoice item modals gave every item the same sortOrder
- The outbound Add Items offline draft stored line items without their error status

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a79026fe5a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.