# Issue

**Title:** feat: hide duplicate workouts in portal and MCP

## Description

## Final scope

> _Added during review by Sebastian Kalisz._

The backend part of this PR (a priority filter for workouts) overlaps with #2020, now merged: `GET /events/workouts` and `/events/workouts/totals` take `source_selection=per_session` with the same 50% overlap rule. This PR now keeps what main did not have yet:

- Portal: a "Show duplicates / Hide duplicates" control on the workouts page (`?top=1`), applied by the backend to the list, its paging and the totals.
- MCP: `get_workouts` asks for `source_selection=per_session`, so an AI client does not count a workout imported from two providers twice.
- API tests that the list and the totals drop the same lower-priority copy.

The original description below is kept for history.

~~Settings -> Priorities only applied to sleep and the summaries, so a workout that reached us from two providers (a Strava ride that Apple Health also imported) was listed, counted and summed twice.~~

~~Backend: GET /events/workouts and /events/workouts/totals take an opt-in filter_by_priority (default false). A workout is dropped when another workout of the same user, from a source ranked strictly higher (provider, then device type, then device_model, as for sleep), overlaps at least 50% of its duration. Workouts nothing overlaps are kept, back-to-back sessions are not merged, and equally-ranked sources never hide each other. Type and source filters are left out of the comparison, so a copy labelled differently by a higher source (cycling vs indoor_cycling) is still recognised. The source ranking SQL is shared with the sleep query.~~

~~MCP: get_workouts asks for filter_by_priority=true, so an AI client no longer doubles counts, duration and calories. Timeseries are left alone because of the tie-breaking issue in #1704.~~

~~Frontend: a "Show duplicates / Hide duplicates" control on the workouts page, driven by ?top=1 like the sleep page, applied to the list, its pagination and the totals.~~

~~~~

<!--

Don't describe the diff - we can read that. Tell us what we can't read: why this
approach, what you ruled out, what you checked, what you're still unsure about.

Use whatever tools help you write it, but do the editing yourself. AI writes far more
than it needs to - cut it down to the few sentences that actually say something.
-->

## What does this change?

<!-- A sentence or two. -->

## Why?

<!-- What problem does this solve, and for whom? If you considered another approach, tell us why you didn't take it. -->

Related issue: #

## How did you test this?

<!--
Be concrete: the commands you ran, the flow you clicked through, the data you looked at.
Best formats: before/after request + response, a table with numbers, a screenshot for
docs/UI. Say what you did NOT test. Examples: contributing/pull-requests.md#showing-that-it-works

If your change touches a provider integration, we need to know it was tested against
a real account and real API responses.

Paste the proof where you can - a log excerpt, a screenshot, a sample response - with
all secrets and sensitive personal data removed.
-->

## AI usage

<!-- Which tools and models you used, and roughly what for. "None" is a perfectly good answer. -->

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Added a “Hide duplicates” option on the workouts page. When enabled, the list and workout totals show only the highest-priority source for each session; turning it off shows records from all sources.
  * The selection is reflected in the page URL and applies to both workout lists and totals.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6101cbf66f89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.