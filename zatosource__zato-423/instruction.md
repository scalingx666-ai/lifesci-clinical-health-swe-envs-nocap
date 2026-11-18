# Issue

**Title:** Ignore Zato token if whole line is commented out.

## Description

The load balancer did not start any more after I had changed a line in the config, and left the original there, commented out. The problem was that Zato's config parser also tried to parse the commented out line. This patch fixed the problem.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `86b0aeb8435b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.