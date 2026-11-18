# Issue

**Title:** Add local review for multimodal evidence

## Description

## Description

.

Add a reusable OpenMedKit view for local review of conflicting visual values, ambiguous handwriting and uncertain speaker roles. It displays the caller's bounded source material and returns an explicit accept, reject or defer decision bound to the evidence revision and displayed content.

This PR includes the shared multimodal contract prerequisite from #4425; merge that prerequisite first. The issue-specific change is limited to the review component, synthetic fixtures/tests, documentation and the Swift fixture workflow trigger.

## Type of Change

- [x] New feature
- [x] Documentation update
- [x] Test addition/improvement

## Changes Made

- Resolve protected text and immutable image crops through caller-owned local handles. Check revision, source binding and ordered alternative references before display and again before every decision.
- Require source presentation before enabling choices, explicit selection before acceptance, and finalized transcript evidence before accepting a speaker interpretation. Clear stale, missing, hidden or revoked content; prevent replay.
- Route native buttons, accessibility activation and focused keyboard shortcuts through the same checks. Preserve watchOS compilation by registering shortcuts only on supported platforms.
- Add four synthetic preview fixtures and 14 focused controls. Decisions contain references/digests, never protected source values, and cannot finalize a note automatically.

## Testing

- [x] `make format-swift` and `make lint-swift`.
- [x] `swift test --disable-automatic-resolution` in `swift/OpenMedKit`: 174 tests, 17 skipped, zero failures.
- [x] The root Swift package suite: 167 tests, 14 skipped, zero failures.
- [x] Focused `MultimodalReviewTests` with network access denied: 14 passed.
- [x] Native synthetic iOS/macOS fixture exercise: source presentation, explicit acceptance, keyboard acceptance/rejection, accessibility deferral, stale/missing holds, and revision changes after selection.
- [x] Source type-checks against iOS 17, watchOS 10 and visionOS 1 deployment targets using their simulator SDKs.
- [x] Full offline Python regression suite: 25,940 passed, 155 skipped; 11,361 subtests passed.
- [x] `make docs-build`, scoped pre-commit hooks, `actionlint .github/workflows/swift-test.yml`, isolated `uv sync --frozen --extra dev --extra hf`, package build and `twine check`.
- [x] Full incoming-commit attribution policy.

## Documentation and Dependencies

- [x] Added `docs/multimodal/local-review.md`, navigation/publication entries, public API documentation and an unreleased changelog entry.
- [x] No new package dependencies.
- [x] Self-review completed; no unrelated formatting changes.

## Examples and Limits

Synthetic handwriting shows the source crop `12 ?` with `12 mg` and `17 mg` alternatives. Selecting an alternative and accepting returns its opaque reference. Changing the revision before acceptance instead displays “The evidence changed” and returns no decision. A speaker can be deferred without choosing any role.

The application remains responsible for authenticating the supplied crop/text, retaining local custody and rechecking the decision at use time. Presentation is not proof of human comprehension, and the returned decision is not an authenticated review-authority receipt. The component performs no network access, logging, persistence, inference or automatic clinical finalization.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `86f538dd2529`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.