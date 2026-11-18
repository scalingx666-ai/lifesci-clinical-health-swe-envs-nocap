# Issue

**Title:** Release bug fixes faster, without having to wait for feature releases

## Description

We have come up with a plan to release bug fixes faster, without having to wait for feature releases that take a long time.

We introduce what is called backporting, see our strategy in the wiki:
- https://github.com/predictive-clinical-neuroscience/PCNtoolkit/wiki/GitHub-workflow
- https://github.com/predictive-clinical-neuroscience/PCNtoolkit/wiki/How-to-make-a-release
- https://github.com/predictive-clinical-neuroscience/PCNtoolkit/wiki/Copying-bug-fixes-from-dev-to-master-(backporting)

below you see the new "backport" branch:
<img width="369" height="409" alt="image" src="https://github.com/user-attachments/assets/76134acd-98fa-4610-95ad-69299b9c889b" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `249bdde5928f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.