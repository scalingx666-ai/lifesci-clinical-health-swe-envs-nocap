# Issue

**Title:** chore: add backward compatibility review rules to CodeRabbit

## Description

## What does this change?

Adds backward compatibility review rules to `.coderabbit.yaml`, so CodeRabbit flags changes that could break existing instances or their clients and asks for intentional breaks to be called out in the PR description. Also moves the existing docs rule out of `reviews.instructions`, which CodeRabbit doesn't support, so it was silently ignored.

## Why?

Open Wearables is self-hosted. Instances upgrade on their own schedule, and we don't control their API clients, mobile SDK builds, webhook consumers or `.env` files. So far nothing in the review setup checks for this.

The rules only cover the places where a change reaches outside the instance: "External" routers (not "Internal" ones - the dashboard ships with the backend), mobile SDK payloads, outgoing webhook payloads, provider webhook and OAuth callback URLs, env vars, migrations and the deploy files. Celery task renames get a softer rule: tasks still queued during an upgrade get dropped, but that's an upgrade hazard rather than a breaking change, so it doesn't require a note in the PR description.

## How did you test this?

We'll see how CodeRabbit applies these rules on the next PRs.

## AI usage

Claude Code (Opus) found compatibility-sensitive places in the repo I hadn't thought of and wrote the rules.


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Chores**
  * Updated review guidance to check compatibility risks across APIs, schemas, integrations, mobile SDK payloads, migrations, and deployment configuration.
  * Reviewers are prompted to identify breaking changes and check for compatible alternatives, documentation, affected clients, and upgrade steps.
  * No changes to app functionality or user-facing behavior.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2d02da01b3e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.