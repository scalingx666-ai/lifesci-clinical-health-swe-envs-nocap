# Issue

**Title:** Manage matplotlib more flexibly

## Description

- let user have control on the figure (add custom titles, axes)
- figures now allow the user to add them in subplots
- give user flexibility to choose if they want the figure to be shown (show_figure=True or False)
- fix plt.tight_layout() bug

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c177dd5665d5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.