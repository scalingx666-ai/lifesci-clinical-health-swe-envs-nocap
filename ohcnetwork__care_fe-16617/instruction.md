# Issue

**Title:** Fix grumpy-reviewer checkout (PR-branch fetch fails: not a git repository)

## Description

## Problem

The `grumpy-reviewer` agentic workflow added in #16616 is **failing on every PR** it triggers on. Example runs on `develop`: , #16610, #16579 — all fail at the **Checkout PR branch** step with:

```
🔄 Checkout Strategy: git fetch refs/pull + checkout
fatal: not a git repository (or any of the parent directories): .git
Event type: pull_request_target
Error message: The process '/usr/bin/git' failed with exit code 128
```

**This is not a token problem** — the `activation` job (which validates `COPILOT_GITHUB_TOKEN`) passes in ~19s. The failure is in the `agent` job.

## Cause

#16616 shipped the workflow with `checkout: false`. That was based on the assumption that the agent reads everything through the GitHub API. But the imported `grumpy-reviewer` agent uses local-file tools (`read`/`search`), so gh-aw injects a **Checkout PR branch** step that runs `git fetch origin +refs/pull/N/head`. With `checkout: false` there is **no base `actions/checkout`**, so there is no `.git` directory and the fetch aborts with exit 128.

## Fix

Remove `checkout: false` from `.github/workflows/grumpy-reviewer.md` and recompile. The compiled `agent` job now runs the base **`Checkout repository`** (`actions/checkout`, `persist-credentials: false`) **before** the injected **`Checkout PR branch`** fetch, so the PR head is fetched into a valid git repo.

Two files change: the source `.md` (4 lines removed) and the generated `.lock.yml` (`gh aw compile`, v0.80.9).

### Security note
Enabling checkout under `pull_request_target` brings back the compiler's advisory *"pwn request"* warning. It's acceptable here: the agent job is **read-only** (`permissions: read-all`), never executes untrusted PR code (only reads files + calls the GitHub MCP / Copilot inference in gh-aw's firewalled sandbox), and every write is confined to the separate permission-scoped safe-output jobs.

## Testing

Verified end-to-end with `gh aw trial` (simulating `github.repository = ohcnetwork/care_fe`, real PR trigger context). The full run is **green**: `activation` ✓ → **`agent` ✓ (2m26s)** → `detection` ✓ → `safe_outputs` ✓. The agent checked out the PR, reviewed the changed lines, and produced grumpy-but-constructive inline review comments plus a consolidated `COMMENT` review (captured as safe-outputs, not posted to any real PR).

Compile: 0 errors, 1 advisory warning (the pwn note above). No app build/test run — workflow config only.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Chores**
  * Updated automated review workflow configuration.
  * Improved repository access and credential handling during automated checks.
  * Enabled the workflow to check out repository contents when needed.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cb27e0e30e9a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.