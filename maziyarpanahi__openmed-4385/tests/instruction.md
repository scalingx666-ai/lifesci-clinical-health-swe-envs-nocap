# Issue

**Title:** feat: preserve source-linked fused image-text evidence

## Description

## Description

Preserve separate pixel, page-geometry, OCR, metadata and normalized-fact origins when building fused claims. Every claim receives its source citations and an explicit cited, review-required or unsupported state. Invalid derivations and declared conflicts propagate through the graph; a valid parallel source cannot clear a problematic branch.

## Type of Change

- [x] New feature
- [x] Test addition/improvement
- [x] Documentation update

## Changes Made

- Add a bounded, immutable evidence graph with typed derivation edges, half-open source regions and OCR offsets, opaque references and deterministic JSON.
- Reject malformed shapes, duplicate or dangling references, inconsistent page geometry and cycles. Keep unsupported modality jumps and coordinate mismatches visible as review findings.
- Add synthetic controls and a published guide. Python scope follows #2796; OpenMedKit parity remains tracked by #3679.

## Testing

Validated head: `9cd40a77cb88439c4b4a988667e6d4523882604f`, based on master `29ffa70050cc7729a0051be419a1b090699a5ed1`.

- `.venv/bin/python -m pytest tests/unit/multimodal/evidence/test_fused_graph.py -q`: 39 passed.
- `.venv/bin/python -m pytest tests/ -q -n 10 --durations=10`: 24,595 passed, 158 skipped; 11,361 subtests passed, 74 warnings. The initial sandboxed attempt denied local sockets and subprocess operations; the complete rerun with the required local permissions passed.
- `make format`, `make lint`, `make format-check`, `make type-check`: passed using the existing locked development environment.
- Explicit mypy check of `openmed/multimodal/evidence`: passed.
- Public API compatibility, strict `make docs-build`, scoped pre-commit hooks including the secret scan, and incoming commit-attribution audit: passed.
- Hosted checks are pending and will be monitored on this exact head.

## Documentation

- [x] Guide, API docstrings, navigation, publication manifest and Unreleased changelog updated.
- [x] Example preserves coordinates and separate evidence origins without source values.

## Dependencies

No new dependencies, model downloads or restricted datasets. The graph has no file or network operations. A citation is a structural provenance result, not clinical verification or permission to release sensitive content.

## Checklist

- [x] Read repository contribution and maintainer guidance.
- [x] Scoped implementation and synthetic tests reviewed.
- [x] Owner-authored commit passed the repository attribution policy.

## Related Issues

## Example

An OCR-derived fact and an independently sourced metadata fact can support the same claim while retaining distinct ancestry. Declaring a conflict between them changes that claim to `review_required` without deleting either source or its coordinates.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29ffa70050cc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.