# Issue

**Title:** fix(backend): google provider split survives a retry after the seed ran

## Description

## What does this change?

`split_google_provider.py` now folds the legacy `google` row onto `google_health` when that row already exists (provider_settings and provider_priority), instead of a plain rename. With no target row it renames as before.

## Why?

app.sh runs the split before the seeds, which is right for the first start. But a failed split is non-fatal (`|| echo "will retry on next startup"`), so `init_provider_settings.py` and `init_provider_priorities.py` go on and create `google_health` rows. From then on every retry renames onto an existing pkey, raises `duplicate key ... provider_settings_pkey` and rolls back the whole split, user_connection included. The leftover `google` connections make `sync_all_users` die on `ValueError: Unknown provider: google`, so the retry the script promises can never succeed.

We hit it on our fork (our init script seeded first), one OAuth connection stayed on `google` and the hourly sync crashed until we patched this. The legacy row wins over the seeded one because the seed only holds defaults.

## How did you test this?

- New `tests/scripts/test_split_google_provider.py`: plain rename, retry with seeded target rows (connection moves, settings + priority folded), idempotent second run
- Without the fix the retry tests fail with `UniqueViolation: duplicate key value violates unique constraint "provider_settings_pkey"`
- Full backend suite: 3050 passed, 2 skipped. ruff check, ruff format --check, ty check clean
- Same fix is in our fork since 0.9.3; the prod row itself we fixed by hand before patching, after checking the collision in a rolled-back transaction

## AI usage

Prepared with Claude Code (Opus), reviewed by me.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Preserved Google Health settings and priority when provider records are migrated, including when a migration is retried.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a8c59af9c14a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.