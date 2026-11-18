# Issue

**Title:** TRUNK-6864: Publish 2.9.x images from GitHub Actions

## Description

Ticket: https://openmrs.atlassian.net/browse/TRUNK-6864

## Why

The `openmrs/openmrs-core:2.9.x` images were last updated on 2026-08-17. Bamboo had stopped publishing them before the spec was removed on 2026-10-16, and nothing in GitHub Actions replaced it. Maven SNAPSHOTs already deploy from `build.yaml`.

## What

Adds a `publish-images` job to `build.yaml`, the same as 2.8.x's from #6795 apart from the branch allowlist. After the build matrix passes, on pushes to 2.9.x in openmrs/openmrs-core, it pushes:

- `2.9.x` and `2.9.x-dev` on JDK 8, the same default `release.yaml` uses,
- `2.9.x[-dev]-amazoncorretto-{11,17,21}`,
- `-amazoncorretto-8` aliases for the default images, as on 2.8.x.

Each image job publishes only for a SNAPSHOT version and only if the commit is still the branch tip, so a re-run of an older build can't overwrite newer images. The job is skipped on pull requests, so it first runs on merge.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9a855a825d20`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.