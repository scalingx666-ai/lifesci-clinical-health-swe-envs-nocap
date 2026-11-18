# Issue

**Title:** Save transfer options to server settings

## Description

. It turns out that the various changes to the server settings made it so that transfer options were not written back to server.xml at all, so this PR mostly creates the necessary methods for this and adds tests.

---


While working on this, I realized that the mechanism to introduce default transfer syntaxes is in effect regardless of whether an empty transfer syntax list (`<transfer-syntaxes/>`) or no list is provided in an SOP class. This means that in order for Dicoogle to be able to reject SOP classes, we need to clear the list of default transfer syntaxes. Fixing this behavior would have required updating Jackson, so I left that alone.

---

### Test plan

Use the Dicoogle UI to change the accepted transfer syntaxes of one or more SOP classes (). After doing so, inspect `confs/server.xml` to see that the changes were applied there shortly after.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f18b919f81ac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.