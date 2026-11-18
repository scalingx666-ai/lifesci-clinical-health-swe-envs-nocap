# Issue

**Title:** OBPIH-8069 Add the Groovy 4 date extension modules (groovy-dateutil, …

## Description

…lper

### :sparkles: Description of Change

[//]: <> (A concise summary of what is being changed. Please provide enough context for reviewers to be able to understand the change and why it is necessary.)

**Link to GitHub issue or Jira ticket:**

**Description:**
This PR fixes the issue related to some missing methods for dates. The newer Groovy is lighter and no longer supports dates out of the box, so we have to implement a few smaller plugins to support date operations.

Marked as "do not merge", as it's targeting the migration PR, so that only changes related to that PR are visible here.

---
### :camera: Screenshots & Recordings (optional)

[//]: <> (If this PR contains a UI change, consider attaching one or more screenshots or recordings to help reviewers visualize the change. Otherwise, you can remove this section.)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `606ac243e872`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.