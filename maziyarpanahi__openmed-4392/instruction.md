# Issue

**Title:** Withhold provisional speech until local PHI decisions resolve

## Description

## Description

Provisional speech stays in bounded local memory until its pending context is finalized and local PHI screening resolves identifiers. Releases preserve negation and original transcript lineage, redact known spans, and fail closed on unresolved identifiers, stale screening results, buffer overflow or expired deadlines.

## Dependency and merge order

This branch builds on #4388 (transcript revision lineage), which includes latest master `29ffa70050cc7729a0051be419a1b090699a5ed1`. It targets master so the required CI matrix runs. The current cumulative diff includes #4388; this feature is the separate commit `21fb22a5b3d664b68af2b25e44f302e476c881ed`. Merge #4388 first, then refresh this branch and revalidate before merging. The dependency's code is reused, not independently reimplemented.

## Type of Change

- [x] New feature
- [x] Documentation and tests

## Changes Made

- Add a bounded trailing-segment buffer that owns protected text and delegates edits/finalization to the existing revision ledger.
- Bind each local screening response to the full pending context, exact revisions, policy and detector artifact; omissions or stale responses never imply safety.
- Require finalized context and resolved PHI before releasing the ordered prefix. Preserve known redactions when earlier context leaves and merge overlapping spans before rendering.
- Keep source-to-output mappings and content-free lineage for redacted outputs.
- Enforce latency before and after screening/rendering without resetting the clock on revisions. Overflow, expired deadlines and invalid clocks discard all pending text.
- Add controlled diagnostics and classify the local ledger edit and screening-request callbacks in the existing effect inventory.

## Testing

Dependency head: `eacb4021a9b1081165ec1086ec77705c7bd51abe`.
Reviewed head: `21fb22a5b3d664b68af2b25e44f302e476c881ed`.

- `python -m pytest tests/unit/multimodal/streaming -q`: 168 passed, including 25 withholding controls.
- `python -m pytest tests/ -q -n 10`: 24,614 passed, 158 skipped; 11,361 subtests passed, 89 warnings.
- `make format lint format-check type-check brand-check`: passed.
- `python -m mypy openmed/multimodal/streaming/privacy --follow-imports=silent`: passed.
- `python scripts/release/check_public_api.py`: passed.
- Strict MkDocs build and executable guide example: passed.
- Scoped pre-commit, Bandit and secret scanning: passed.
- Complete incoming commit-attribution checks against both master and the dependency branch: passed.
- Hosted checks are pending on the pushed head.

## Documentation

Published guide, public docstrings, navigation, publication classification and Unreleased changelog included. The guide explains explicit idle ticking, cooperative execution limits, detector ownership, bounded lookahead and protected output handling. Synthetic fixtures test the withholding behavior; detector recall and clinical workflows require independent qualification.

## Dependencies

No new packages, models, datasets or remote services. Uses the existing transcript-lineage implementation from #4388 and an injected local PHI detector.

## Checklist

- [x] Scoped implementation and self-review complete
- [x] Local validation and failure controls passed
- [x] Documentation and changelog updated
- [x] Privacy-safe diagnostics and synthetic fixtures
- [x] Incoming commit attribution verified

## Related Issues

Depends on #4388

## Example

A synthetic identifier followed by “has no allergy” stays withheld while provisional. After finalization and a matching detector decision, the released text is “[REDACTED] has no allergy”, with mappings back to original finalized offsets. An expired deadline returns no text, including when screening or rendering consumed the remaining budget.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3eaca3c3d363`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.