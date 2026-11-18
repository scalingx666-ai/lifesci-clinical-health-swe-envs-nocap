# Issue

**Title:** ENG-1270: fix(infra): add permissions for structured data bucket

## Description

Issues:

- https://linear.app/metriport/issue/ENG-1270

### Dependencies

- Upstream: None
- Downstream: None

### Description

Adds permissions for Lambdas to access the S3 bucket, which is necessary for consolidated ingestion. I assembled the previous PR by picking out pieces of another PR, and forgot to move over the Lambda nested stack update.

### Testing

- Local
  - [x] `cdk diff`
- Staging
  - [x] check consolidated bucket can be accessed 
- Production
  - [ ] check consolidated bucket access

### Release Plan

- [ ] Merge this

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added optional structured data bucket support for serverless functions: when configured, functions receive read access and an environment variable pointing to the bucket so they can access structured data.
  * Deployment wiring now exposes the bucket name to relevant functions automatically when provided.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24424cfc41c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.