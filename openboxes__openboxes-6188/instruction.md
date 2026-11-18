# Issue

**Title:** #6186 Support multiple local development environments simultaneously

## Description

**Link to GitHub issue or Jira ticket** 
#6186 

**Description** 
Lays the groundwork for multiple local development environments using git worktrees and direnv. 

* Ignore .envrc and add .envrc.example with per-environment settings (server port, debug port, server URL, datasource URL) so each clone/worktree can run side by side without collisions.
* Generate git.properties with the git CLI when building inside a worktree. JGit 5.x (forced for Java 8 compatibility) cannot read linked worktrees, so the gradle-git-properties task is skipped there. This keeps Spring Boot's GitProperties bean populated for the footer, admin settings, and API build info.
* Guard SentryServletContextListener against a missing git.properties (e.g. source builds without .git) instead of failing on an ambiguous Properties.load(null) call.

Documentation on how to configure and use git worktrees, direnv will be created in a separate PR to the Contributor Guide shortly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b500f168d7a5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.