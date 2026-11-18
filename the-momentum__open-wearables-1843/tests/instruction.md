# Issue

**Title:** chore: limit CodeRabbit docs requests to user-facing changes

## Description

## What does this change?

Narrows the CodeRabbit rule that asks for a `docs/` update. It now fires only for changes an integrator or operator can see or has to act on, and explicitly skips internal mechanisms. The `backend/app/schemas/**` rule and the docs step in `AGENTS.md`, which CodeRabbit also reads, get the same scope.

## Why?

"Provider integrations or data schemas" matches almost every backend PR, so most of these requests get rejected. CodeRabbit records a learning each time, but the learning is tied to one file, so the same request comes back on the next PR.

Docs requests on code changes from the last two weeks:

| PR | request | outcome |
|---|---|---|
| #1814 | Garmin token refresh before deregistration | rejected, internal |
| #1822 | when stale Garmin deregistration pings are ignored | rejected, internal bug fix |
| #1817 | deployment docs for the Google data migration | rejected, nothing for operators to do |
| #1722 | Nightly Recharge backfill policy | answered in the PR description |
| #1731 | pull eligibility rule, Redis keys for sync runs | ignored, merged without docs |
| #1841 | `refresh_token` table not in docs | API unchanged, table isn't documented |
| #1809 | webhook payload cleanup on user deletion | added to `webhooks.mdx` |
| #1746, #1729 | provider data coverage | provider pages updated |

The new wording keeps the last two kinds of requests and drops the rest.

## How did you test this?

Went through the requests above against the new wording: #1809, #1746 and #1729 still match (webhook delivery, provider data), the other six fall under the listed exclusions.

## AI usage

Claude Code (Claude Opus) to collect the CodeRabbit threads and draft the rule; I reviewed the wording.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Documentation**
  * Documentation checks now focus on changes visible to integrators or operators, including API behavior, provider data coverage, settings, deployments, upgrades, and API-visible schema or enum changes. Internal mechanisms and fixes restoring expected behavior are excluded. Data-model and schema documentation is required only for changes to content those pages already cover. Generated API-reference pages remain exempt from endpoint-change updates.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `456b82502fea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.