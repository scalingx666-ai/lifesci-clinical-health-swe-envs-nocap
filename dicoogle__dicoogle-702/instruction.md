# Issue

**Title:** Optimize task management page

## Description

### Summary

- Restrain task status view to showing the 200 most recent tasks, so that the page can still open fine on long-running Dicoogle instances without saturating the browser.
- Show how many tasks are presented and the number of tasks not shown in the header above the task list.
- Update task status style so that each task is more compact.

See screenshot.

![Screenshot 2024-10-24 095303](https://github.com/user-attachments/assets/98e263dd-4d79-438b-a216-3fe94068f8b7)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `390ab782fe83`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.