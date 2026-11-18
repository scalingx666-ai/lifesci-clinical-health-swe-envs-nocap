# Issue

**Title:** 🤖 Raises CARE PR Reviewer daily AI-credits budget to 25K

## Description

<!-- entire-trail-link-start -->
https://entire.io/gh/ohcnetwork/care_fe/trails/31
<!-- entire-trail-link-end -->

## Proposed Changes

The CARE PR Reviewer gh-aw workflow stopped mid-day after hitting the compiled-in default daily AI-credits guardrail (`vars.GH_AW_DEFAULT_MAX_DAILY_AI_CREDITS || '5000'`). The 24h window before run [35535244745](https://github.com/ohcnetwork/care_fe/actions/runs/35535244745) held **33 billed agent runs (~150 AIC each)** — ordinary review traffic on this repo, not a runaway loop (drafts and bot comments are already filtered at the trigger, and the reviewer caps itself at 6 rounds per PR).

- Add explicit `max-daily-ai-credits: 25000` to `care-review.md` frontmatter — ~5× the observed daily peak, so legitimate reviews never trip it while a genuine runaway is still capped at a bounded daily cost. Comment documents the rationale in the file's existing style.
- Recompile `care-review.lock.yml` with the exact pinned compiler (gh-aw v0.86.2 from the lock's metadata header) so the activation job's stale-lock check keeps passing. Baseline compile was verified byte-identical before editing, so the lock diff is strictly the threshold and hash:

```diff
-      GH_AW_MAX_DAILY_AI_CREDITS: ${{ vars.GH_AW_DEFAULT_MAX_DAILY_AI_CREDITS || '5000' }}
+      GH_AW_MAX_DAILY_AI_CREDITS: "25000"
```

Engine version, action SHAs, and container digests are unchanged. The guardrail resumes its intended role as a runaway backstop rather than a ration on normal traffic.

Tagging: @ohcnetwork/care-fe-code-reviewers

## Merge Checklist

- [ ] Add specs that demonstrate the bug or test the new feature.
- [ ] Update [product documentation](https://docs.ohc.network).
- [ ] Ensure that UI text is placed in I18n files.
- [ ] Prepare a screenshot or demo video for the changelog entry and attach it to the issue.
- [ ] Request peer reviews.
- [ ] Complete QA on mobile devices.
- [ ] Complete QA on desktop devices.
- [ ] Add or update Playwright tests for related changes

<!-- START COPILOT CODING AGENT SUFFIX -->

-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9138ca3d772f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.