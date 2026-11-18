# Issue

**Title:** RELEASE ENG-1123 + ENG-1133

## Description

Issues:

- https://linear.app/metriport/issue/ENG-1123
- https://linear.app/metriport/issue/ENG-1133

### Dependencies

None

### Description

- 
- 
- 

### Testing

Check each PR.

### Release Plan

- :warning: Points to `master`
- [ ] Merge this


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Webhook meta can include an optional requestId for per-request correlation of async flows.
  * Diagnostic report output now includes status and code fields and adjusts embedded content encoding.

* **Documentation**
  * Medical API docs and examples updated to show requestId across webhook types and realtime patient notifications.

* **Samples**
  * Sample app paginates patient listing (count: 10) and adds an IS_PROD env flag.

* **Chores**
  * Analytics now logs patients missing consolidated data and their count.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f760a58ca2ba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.