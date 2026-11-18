# Issue

**Title:** fix(server): allow membership access policies from linked projects

## Description

ProjectMembership access policies may now come from a linked project, following the normal linked project export rules. AccessPolicy is exempt from the rule that keeps project admin resource types in the current project.

readMembershipReference now reads through a Repository scoped to the membership's project (and its linked projects, when allowed), instead of re-implementing the project checks against a system repository.

Access policies without a project are no longer accepted at login or in invites.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `67418132c867`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.