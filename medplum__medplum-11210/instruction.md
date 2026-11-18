# Issue

**Title:** [SchedulingWorkspace] Slide the time finder in and out

## Description

This animation makes the transition feel less jarring.

- Time finder pane animates in/out with a 100ms slide
- Selecting an entry now auto-closes (with the slide animation)
- Selecting an entry briefly highlights the time field that was changed by the selection
- Reopening the pane keeps the currently selection option highlighted

Based on work originally done in the `kevin-calendar-explorations` branch.

https://github.com/user-attachments/assets/1e71135c-e22f-4662-a51a-3b4afd2dd5e7

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b314add34aef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.