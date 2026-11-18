# Issue

**Title:** feat(backend): return one OW health score per day by source priority

## Description

> ⚠️ **Breaking change:** `GET /health-scores` returns at most one OW score (`provider = internal`) per category and day instead of all of them, and the unique key of `health_score` gains `data_source_id`.

## What does this change?

- OW scores of different sources can be stored side by side: the unique key includes `data_source_id` (`NULLS NOT DISTINCT`, so provider scores, which have no source, still deduplicate).
- `/health-scores` returns one OW score per category and day, from the highest-priority source (the ranking the summaries use). Within one source the longest sleep wins over an unflagged nap, and a score without a source comes last. Provider scores are unchanged.
- Each score has a `source`, as in `/summaries` and `/events`.

## Why?

OW scores are computed per source. Clients get one per day, from the same source the summaries use, and the per-source scores stay in the database. The old key treated scores of two sources at the same time as duplicates.

Computing the scores per source, each with its own history, belongs to the Health Scores module, where OW scores are moving; this PR prepares the storage and the API for it.

Related issue: #983

## Upgrading

- **API clients:** expect one OW score per category and day; `source` tells which data source it came from. There is no parameter to get the others.
- **Self-hosted instances:** nothing to do. The migration runs on startup, builds the new key concurrently (writes aren't blocked) and changes no data. Downgrading fails if two sources have an OW score at the same time by then; delete one of them first.

## How did you test this?

- Repository, service and API tests for the selection, `source`, the new key and duplicate handling.
- Migration: upgrade, `alembic check`, downgrade and upgrade again on a local database.
- Local instance seeded with scores from three sources over several days, checked through the API and in the database.

## AI usage

Claude Code was used to propose and implement the change, help with testing and analyze potential issues with the migration.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Health score responses now include optional source details, such as provider, device type, and device model.
  * For each category and day, the API returns one internally computed score from the highest-priority source. For multiple sleep scores from that source, it selects the longest sleep.
* **Documentation**
  * Updated guidance explains source priority, date-range behavior, and how provider-reported scores are handled.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6cf6d14a31e4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.