# Issue

**Title:** TRUNK-6864: Publish master images from GitHub Actions

## Description

Ticket: https://openmrs.atlassian.net/browse/TRUNK-6864

## Why

The master images haven't been published since Bamboo stopped: `nightly` and `3.0.x` were last updated on 2026-06-01, and `dev` on 2026-07-17. Maven SNAPSHOTs already deploy from `build.yaml`.

## What

**`build.yaml`**
- Adds a `publish-images` job. After the build matrix passes, on pushes to master in openmrs/openmrs-core, it pushes the same tags Bamboo did:
  - `dev` and `dev-eclipse-temurin-21`,
  - `nightly` and `nightly-eclipse-temurin-21`,
  - the version line tag (`3.0.x` for 3.0.0-SNAPSHOT) and `3.0.x-eclipse-temurin-21`.
- The JDK is set explicitly rather than taken from the Dockerfile default, so the `-eclipse-temurin-21` tags stay accurate.
- Like 2.8.x, it publishes only for a SNAPSHOT version and only from the branch tip. It is skipped on pull requests.
- Corrects the `deploy-snapshot` comment, which described the 2.x JDK 8 baseline.

**`release.yaml`**
- Master's copy is inert on master itself, but it is what a 3.0.x branch would inherit. Its variant job built Corretto 8/11/17 images, which can't build a Java 21 codebase.
- The release images are now built on Temurin 21 and also tagged `-eclipse-temurin-21`, as Bamboo did for master. The variant job is removed.
- The release job sets up JDK 21 instead of 17.
- All the pinned actions are still used by the release job, so Dependabot coverage is unchanged.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `42277bf371b1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.