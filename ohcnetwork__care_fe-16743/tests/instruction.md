# Issue

**Title:** Consolidate agentic PR reviewers and auto-retry transient 429 failures

## Description

## Proposed Changes

On 2026-08-20 a Copilot rate limit window failed every agentic run in this repo for 45 minutes. Nothing was actually broken: run `32344080781` was re-run by hand and attempt 2 passed. The repo has been accumulating auto-filed `[aw] ... failed` issues from these (#16731, #16732, #16705, #16706, #16670, #16708), so this PR addresses both the cost pressure that triggers the limit and the lack of automatic recovery when it is hit.

**1. Drop the Grumpy PR Reviewer, keep CARE PR Reviewer**

Two agentic reviewers fired on every `pull_request_target`, both on `claude-opus-5`, both authenticating through the same Copilot PAT. Compared head to head on the same diff (#16613) they produced roughly 40% duplicate findings at 259 vs 124 AIC.

Grumpy was the one to cut:

- It is stateless, so it re-reviewed the whole diff on every push and re-raised findings as fresh comments instead of converging. CARE tracks its own prior findings, verifies fixes at the head SHA, resolves threads, and answers @-mentions.
- Its checklist is generic (code smells, naming, duplication) and duplicates Copilot, CodeRabbit and Greptile, which already review these PRs. CARE's lenses encode actual care_fe rules (i18next keys, `query()`/`mutate()` wrappers, shadcn/CAREUI reuse, `useBreakpoints`, the `min-w-0`/`min-h-0` scroll trap, 320px viewport, 44px touch targets).
- It had no draft filter, no bot filter, no `noop` and no round cap, so it posted full reviews on lockfile-only Renovate diffs. In the 07:00 to 07:45 outage window: 7 Grumpy runs vs 1 CARE run.

Three things it genuinely did better were ported into CARE rather than lost:

- **Silent failure paths.** Its highest value finding on #16613 was two mutations with `onSuccess` and no `onError`, which CARE missed entirely. Lens 1 now checks failure handling explicitly, graded by what the user sees when a request rejects.
- **`APPROVE`.** A clean PR now gets a green check instead of a neutral comment. Safe because this is not a required check and `github-actions[bot]` cannot satisfy a required-review gate. `REQUEST_CHANGES` stays disallowed.
- **Concreteness.** The Tone section now asks for the failure and its consequence up front. The specificity, not the persona.

**2. Auto-retry runs that fail on transient inference errors**

Two layers, covering different outage lengths:

- **In-job** (`care-review.md`): the harness defaults space its four attempts only ~35s apart, so a run exhausts them in ~8 minutes, usually before a rate limit window clears. Widened to 15s/30s/60s/120s over five attempts (~12 minutes), still inside the 20 minute job timeout. Free when the model answers, since the delays only elapse on a retry path.
- **Out-of-job** (`retry-agentic-runs.yml`): a `workflow_run` watcher that re-runs failed jobs when the failure looks transient, backing off ~10 then ~20 minutes. Covers all three agentic workflows.

The classifier is the part worth reviewing closely. It is deliberately narrow in both directions and was checked against real logs:

| Test case | Result |
| --- | --- |
| The two real 2026-08-20 429 logs | transient, retries |
| Two most recent non-429 failures (real `gh pr checkout` errors) | unrecognised, does not retry |

Two non-obvious details that the first draft got wrong:

- Permanent failures must match the harness `is<X>=true` flags, **not** the bare output names. gh-aw prints `Set output 'invocation_cap_exceeded'` on every run regardless of value, so matching the bare name classified every failure as permanent, including the 429s this is meant to catch. This is also why #16742 (`exceeded daily AI credits budget`) correctly does not retry.
- Generic network strings (`socket hang up`, `ECONNRESET`) are excluded from the transient set. The MCP gateway logs `socket hang up` on its first health probe in runs that go on to succeed, so matching it would retry genuine failures containing a recovered blip.

Loop protection is `run_attempt < 3`, since a re-run emits another `workflow_run: completed` event. The watcher also skips runs superseded by a newer run on the same branch, so it never spends credits reviewing a diff that has already been replaced.

### Notes for reviewers

- `workflow_run` only fires for the copy on the default branch, so the watcher does nothing until this lands on `develop`.
- The watcher sleeps to back off, which holds a runner. Free on this public repo but not free of concurrency, which is why the delays are modest and the in-job layer absorbs short spikes without a rerun round trip.
- This treats the symptom. The root cause is that inference authenticates through a single user's `COPILOT_GITHUB_TOKEN`, and Copilot rate limits are scoped per user, so every agentic run in the repo shares one person's ceiling. `permissions: copilot-requests: write` moves this to org billing and removes the shared bottleneck, but it needs an org admin to enable centralized Copilot CLI billing first, so it is deliberately not in this PR.
- There is no JIRA ticket for this work, so the PR Title JIRA Validation check is expected to fail.

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

N/A for this change: it touches only `.github/` CI configuration and ships no application code, UI text, or user facing behaviour. Validation was `gh aw compile` (0 warnings), `actionlint` on the new workflow (clean), and replaying the classifier against real failure logs as described above.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

- **Workflow Improvements**
  - Automated reviews can now approve pull requests when defined criteria are met.
  - Comments from additional automated tools are filtered for clearer results.
  - Eligible temporary failures in automated checks can be retried automatically.
  - Review findings now emphasize concrete failures and affected-user impact.

- **Documentation**
  - Added guidance for identifying silent failures, including missing feedback and misleading loading or success states.

- **Removed**
  - Retired the outdated automated reviewer workflow and its associated review agent.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e41471c20c49`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.