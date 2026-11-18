# Issue

**Title:** perf: compress undo snapshots with LZ4 level 1 instead of 5

## Description

## What

One-line change to `_blosc2_cparams`: `clevel` 5 → 1 (plus a comment recording why).

## Why

The undo snapshot compresses the full interactions tensor after every prediction. That tensor is overwhelmingly zeros, so LZ4's search depth buys nothing:

| clevel | compress time (2.9 GB, 8×694×512×512 fp16, 8 threads) | compressed size |
|---|---|---|
| 5 (current) | 271 ms | 0.4 MB |
| 1 (this PR) | 80 ms | 0.4 MB |

(Benchmarked with the exact cparams this method returns — LZ4, NOFILTER — on a tensor with a realistic nonzero region; sizes were byte-identical.)

The snapshot is submitted asynchronously and deliberately overlaps user think-time, which works well — until a fast follow-up interaction lands inside the compression burst and contends with it. In our deployment (nnInteractive sessions behind a FastAPI server, multiple users) this showed up as an intermittent ~330 ms of added latency on rapid consecutive prompts, measured from the client as time-to-first-byte minus server-side compute. A ~3.4× shorter burst shrinks that collision window proportionally, at zero cost in snapshot size or undo behavior.

## Related finding (not in this diff)

If you ever consider deprioritizing the snapshot thread instead: nice-then-restore does not survive containers — Docker's default seccomp/cap profile drops `CAP_SYS_NICE`, so restoring priority fails with `EPERM` even as in-container root. A permanently self-niced dedicated thread works (that's what we run alongside this change), but it's deployment-sensitive, so we're only upstreaming the universally-safe clevel change.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bbe12fdccc87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.