# Issue

**Title:** OBPIH-7757 Fix dashboard

## Description

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:** https://pihemr.atlassian.net/browse/OBPIH-7757?atlOrigin=eyJpIjoiMTIxMzE4ZTIzODlkNGM3Nzg4ZjZlMzkzOGZlYTQ4MDciLCJwIjoiaiJ9

**Description:**
- Replaced react-sortable-hoc with @dnd-kit/react
- Added SortableCard, a dashboard-scoped wrapper that calls useSortable and passes sortableRef/handleRef to the card
- Kept archiving by dropping a tile at the bottom of the screen
- The cause of all widgets loading was the missing route match (now provided by withRouter)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1241e491e15d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.