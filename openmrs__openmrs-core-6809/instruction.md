# Issue

**Title:** TRUNK-6864: Remove the Bamboo spec from 2.8.x

## Description

Ticket: https://openmrs.atlassian.net/browse/TRUNK-6864

. Builds, SNAPSHOT deploys, image publishing and releases for 2.8.x all run in GitHub Actions, and the Bamboo plan is disabled, so this deletes `bamboo-specs/bamboo.yml`. It also rewords two workflow comments that pointed at that file.

Deleting the spec does not delete the plan in Bamboo. That still needs doing by hand.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa795cd4d088`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.