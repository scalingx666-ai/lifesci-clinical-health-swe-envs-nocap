# Issue

**Title:** chore: route Entire agent checkpoints to a dedicated repository

## Description

Routes Entire agent checkpoints to `ohcnetwork/care_fe-checkpoints` instead of a branch in this repo, which is the tool's default. Checkpoints contain verbatim agent session transcripts, so they should not live in a public repo. Also enables Entire's PII redaction layer, which is off by default.

Git hooks are not committed — contributors who want Entire run `entire enable`. Contributors without the CLI are unaffected.

For reviewers: `"enabled": true` means contributors who already have the Entire CLI installed will start capturing sessions on this repo.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added configuration for remote checkpointing with Git-based session synchronization and publishing.
  * Enabled automated redaction for email, phone, and address.
  * Introduced workflow hook integrations for common tools (GitHub, Codex, Cursor, and OpenCode), including context-aware one-time prompt augmentation during sessions.
* **Chores**
  * Updated local ignore rules to exclude temporary and runtime/state files.
  * Updated linting to skip auto-generated hook/plugin configuration directories.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17a1384e4cba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.