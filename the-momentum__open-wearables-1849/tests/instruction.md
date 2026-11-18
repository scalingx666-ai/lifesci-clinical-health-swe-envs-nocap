# Issue

**Title:** chore(backend): keep config/.env out of the Docker image

## Description

## What does this change?

`backend/.dockerignore` now excludes `config/.env` and `config/.env.*` (except `.env.example`), the same way `frontend/.dockerignore` already does.

## Why?

The backend Dockerfile does `COPY . .`, so any local build (including `docker compose build`) bakes the developer's `config/.env` with real secrets into the image. One manual `docker push` of such an image would publish them. The images on Docker Hub are built in CI from a clean checkout, so they don't contain it - I checked the current `otel-log-export`, `arm-test`, `frontendv2-beta` and `0.7` tags and each one only has `.env.example`.

Local dev is not affected: compose passes the values through `env_file`, and the watch `sync+restart` still copies `.env` into the container when it changes.

## How did you test this?

Built a throwaway image (`COPY . /ctx`) from `backend/` with a dummy `config/.env` and `config/.env.local`, then listed `/ctx/config`:

```
before: .env  .env.example  .env.local
after:  .env.example
```

Also built the real backend image with a dummy `config/.env` present: it builds, `/root_project/config` only has `.env.example`, and settings load once `SECRET_KEY` is passed as an env var, which is how the CI images run too.

## AI usage

Claude Code (Opus 5.5) for checking the published images and running the before/after build.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Chores**
  * Docker builds now exclude environment configuration files while retaining the example configuration file.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b22796b92893`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.