# Issue

**Title:** feat: add synthetic HL7 and CDA document generation

## Description

## Description
Add deterministic, offline synthetic HL7 v2 messages and CDA/C-CDA documents with truth manifests and leakage-evaluation harnesses. This integrates Pardeep Singh's reviewed PRs #4216 and #4241 in one master commit.

## Type of Change
- [x] New feature
- [x] Documentation update

## Changes Made
- Generate bounded, configurable synthetic messages/documents and track direct identifiers, dates and linked values.
- Evaluate parser/redaction results with value-free diagnostics and structural checks.
- Preserve current master fixes, put release notes under Unreleased, and clarify that HL7 manifest offsets count Python string code points.

## Testing
- [x] Combined rehearsal: 20,775 passed, 177 skipped, 11,209 subtests.
- [x] Focused generators/parsers: 134 passed, 19 subtests.
- [x] Canonical formatting/lint, strict documentation build, artifact budgets and marketing/clinical analytics checks.
- [x] Exact final head `103a89461666c0f2a515f6906c033de1719d2aca`: 20,775 passed, 177 skipped, 11,209 subtests in 168.54s. Formatting/lint, strict docs, all 3 browser budget/analytics checks, wheel/sdist builds and packaged-source verification passed. Hosted checks have no failures; remaining queued/running jobs are covered by the local full suite for this change.

## Documentation and Dependencies
- [x] Generator guides, API docstrings, getting-started links and changelog updated.
- [x] No new dependencies.

## Related Issues

The scope is synthetic generation, truth manifests and evaluation; changes to clinical redaction rules remain separate.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5f25ae504a89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.