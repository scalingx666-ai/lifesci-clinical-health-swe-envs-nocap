# Issue

**Title:** feat(schemas): add reviewer disagreement report JSON Schema

## Description

# Pull Request

## Description
Adds a packaged JSON Schema for `ReviewerDisagreementReport`, so consumers can validate a report and verify that no reviewer or case identifiers slipped into it.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [x] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- Add `openmed/core/schemas/json/reviewer_disagreement_report.schema.json` matching `ReviewerDisagreementReport.to_dict()`: all seven report keys required, `additionalProperties: false` at the report, published-rate, and per-reason levels, `schema_version` pinned to `openmed.reviewer_disagreement.v1`, `minimum_cell_size` >= 2, rates bounded to [0, 1] with nullable numerator/denominator/rate for suppressed cells, and the reason field restricted to the `DisagreementReason` values.
- Add `tests/unit/eval/test_reviewer_disagreement_schema.py`: the schema passes `validator_for(schema).check_schema`, a synthetic report built with `reviewer_disagreement_report()` validates, and reports carrying an extra `reviewer_id`, `case_id`, or `decision` key fail validation.
- Report behaviour is unchanged; this is schema and tests only.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [ ] I have tested this change with different models/inputs

Commands run:
- `.venv/bin/python -m pytest tests/unit/eval/test_reviewer_disagreement_schema.py tests/unit/eval/test_reviewer_disagreement.py -q` — 12 passed.
- `.venv/bin/python -m pytest tests/unit/core -q -k schema` — 60 passed (packaged-schema loading and versioning suites with the new schema present).

## Documentation
- [ ] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [ ] I have updated the CHANGELOG.md

No documentation changes needed: the schema is self-describing and follows the existing packaged-schema conventions.

## Code Quality
- [x] I ran `make format`, `make lint`, and `make format-check`
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

Validated with the scoped equivalent, `pre-commit run --files openmed/core/schemas/json/reviewer_disagreement_report.schema.json tests/unit/eval/test_reviewer_disagreement_schema.py` — all applicable hooks passed. No Swift files touched.

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Checklist
- [x] I have read the [contributing guide](https://github.com/maziyarpanahi/openmed/blob/master/CONTRIBUTING.md), [Code of Conduct](https://github.com/maziyarpanahi/openmed/blob/master/CODE_OF_CONDUCT.md), and [maintainer guide](https://github.com/maziyarpanahi/openmed/blob/master/MAINTAINERS.md)
- [x] My commits have clear, descriptive messages
- [x] I have squashed/organized my commits appropriately

## Related Issues

## Screenshots/Examples
Not applicable (schema and tests only).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b5bf9fc0c9c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.