# Issue

**Title:** Add grumpy-reviewer agentic PR-review workflow

## Description

## What this does

Adds a [GitHub Agentic Workflow (gh-aw)](https://github.com/github/gh-aw) that runs a **grumpy senior code reviewer** on pull requests and leaves grumpy-but-constructive **inline review comments** on the PR's changed lines. Tone and reviewing standards are delegated to the imported `grumpy-reviewer` agent (taken verbatim from `github/gh-aw`).

### When it runs
- **Automatically on every PR**: `opened`, `reopened`, and `synchronize` (new commits pushed).
- **Manual runs**: `workflow_dispatch`.
- Guarded with `if: ${{ github.repository == 'ohcnetwork/care_fe' }}` so it only runs on the upstream repo (like `daily-playwright-improver.md`).

### Community / fork PR support
Uses `pull_request_target` (matching `thank-you-note.md`) so the Copilot engine credentials are available even for fork PRs — a plain `pull_request` trigger from a fork does **not** expose secrets/the Copilot token. `roles: all` is set so external contributors' PRs are actually reviewed (the default role gate would otherwise skip non-write contributors).

This is safe because of gh-aw's **safe-outputs** model: the agent job runs **read-only** (`permissions: read-all`) and can only emit structured review comments that separate, permission-scoped jobs apply. The base repo and the PR head are checked out (the imported `grumpy-reviewer` agent uses `read`/`search` local-file tools, so the changed files must be on disk), but the agent **never executes untrusted PR code** — it only reads files and calls the GitHub MCP + Copilot inference inside gh-aw's network-firewalled sandbox. Because it's a `pull_request_target` workflow that checks out PR content, the compiler emits an advisory *"pwn request"* warning; it's accepted here because no untrusted code is run and every write is confined to the isolated safe-output jobs. All repo/PR content is treated as untrusted input in the prompt.

### Authentication (PAT)
The Copilot engine authenticates inference with a **`COPILOT_GITHUB_TOKEN`** repository Actions secret. This must be a **fine-grained PAT** with:
- **Account permissions → Copilot Requests: Read** (the only permission needed — no repo scopes)
- an owner account that holds an **active Copilot license**

Reading the PR diff and posting review comments do **not** use this PAT — those run on the built-in Actions `GITHUB_TOKEN`; gh-aw injects the needed write scopes (`pull-requests: write`) into the separate safe-output jobs while the agent job stays read-only (`permissions: read-all`).

> Alternative (not used here): if the org enables centralized Copilot billing, `permissions: copilot-requests: write` lets it run on the Actions token with no PAT.

### Configuration
- `permissions: read-all`
- `imports: [ .github/agents/grumpy-reviewer.agent.md ]`
- `tools.github.toolsets: [default]`
- checkout enabled (base ref + PR head) — required so the imported agent can read changed files locally
- `safe-outputs`:
  - `create-pull-request-review-comment` (max 10, focused on changed lines)
  - `submit-pull-request-review` (max 1, `COMMENT` event — non-blocking consolidated summary)
  - `missing-tool: create-issue: true`
- Default engine (copilot) — `engine:` omitted, matching the other workflows.

## Files
- `.github/agents/grumpy-reviewer.agent.md` — reviewer persona (imported verbatim).
- `.github/workflows/grumpy-reviewer.md` — the workflow source.
- `.github/workflows/grumpy-reviewer.lock.yml` — compiled output (`gh aw compile`, v0.80.9).
- `.github/aw/actions-lock.json` — additive pin for the `setup` action the new lock references (does not touch existing pins).

Validated via `gh aw compile` (0 errors; 1 advisory `pull_request_target`+checkout *"pwn request"* warning, addressed above). No app build/test run — this is workflow config only.

## Testing
Exercised with `gh aw trial` against a temporary private host repo (simulating `github.repository = ohcnetwork/care_fe`, triggered with a real PR context). Verified:
- **Compiles and installs** with the imported agent resolved; the lock is in sync with the source.
- **Activation gate passes** — setup, agentic run-info, daily-usage cache, and token-guardrail steps all succeed.
- In the compiled `agent` job, the **base repo is checked out first** (`actions/checkout`, `persist-credentials: false`) and the **PR head is fetched after**, so the PR-branch `git fetch` runs inside a valid git repo. This fixes an earlier `fatal: not a git repository` failure that was caused by `checkout: false`.

The only step that can't be exercised without credentials is **Copilot inference**: gh-aw validates `COPILOT_GITHUB_TOKEN` up front and stops the run if it's unset (`Error: None of the following secrets are set: COPILOT_GITHUB_TOKEN`). A full end-to-end trial — where the agent posts grumpy review comments, captured as safe-outputs without touching the real PR — just needs that secret set on the trial/host repo.

## Follow-up / requirement
Set the **`COPILOT_GITHUB_TOKEN`** repo secret (fine-grained PAT, Copilot Requests: Read, Copilot-licensed owner) on `ohcnetwork/care_fe` before this can post reviews. If it isn't configured yet, add it as a follow-up.

<!-- This is an auto-generated comment: release notes by coderabbit.ai --

## Summary by CodeRabbit

## Release Notes

* **New Features**
  * Added an automated code review agent that provides constructive feedback on pull requests, focusing on security and correctness.
  * Reviews analyze changed lines, limit inline comments, and provide a consolidated, non-blocking result.

* **Chores**
  * Added workflow support for reviews on pull request updates and manual runs.
  * Added safeguards for bounded outputs, validation, and usage limits.
  * Added pinned workflow action versions for reliable execution.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7f945410634c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.