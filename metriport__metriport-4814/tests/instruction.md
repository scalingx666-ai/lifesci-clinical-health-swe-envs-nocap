# Issue

**Title:** remove webhook feature flag for webhook sender

## Description

_[Release PRs:]_

Issues:

- https://linear.app/metriport/issue/ENG-000

### Dependencies
None

### Description
Remove webhook feature flag.
All cxs should receive webhooks from the webhook sender.

### Testing
Staging
- [x] add a cx into the list of cxs for that feature flag in staging. Deploy, see if anything goes wrong 👍 
- [x] Send a msg to mllp server -> webhooksender


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **New Features**
  * AI Briefs are now automatically saved to secure cloud storage for improved availability and retention; upload issues are contained and won’t interrupt workflows.
  * Added an option to refresh consolidated patient data using the most recent AI-generated summary.

* **Refactor**
  * HL7 notification webhooks no longer depend on a feature flag; when settings are configured, notifications (including discharge Slack alerts) are sent, improving consistency.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `048103b29e6e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.