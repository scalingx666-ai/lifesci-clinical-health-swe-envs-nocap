# Issue

**Title:** docs: add TypeScript REST client example with stubbed fetch tests

## Description

# Pull Request

## Description
Add a runnable example for the TypeScript REST client that de-identifies one note through an injected `fetch` and handles `OpenMedApiError` by its controlled `code`, plus offline tests that drive it with a stubbed `fetch`. The client itself is unchanged.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [x] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- `clients/typescript/examples/deidentify.mjs` (new): exports `run({ fetch, baseUrl, text })`, calls `deidentify`, and on `OpenMedApiError` returns `{ ok: false, code, status, retry }`, where `retry` is decided from the code only (`rate_limited`, `service_busy`, `timeout`). Other errors (for example transport failures) are rethrown. Running the file directly targets `OPENMED_BASE_URL` (default `http://localhost:8080`) and prints only counts and codes, never the note.
- `clients/typescript/tests/example.test.mjs` (new): 6 offline tests with synthetic stub responses: success (also checks URL, method and request body), `validation_error`, the three retryable codes, a negative control where message and code disagree in both directions, a non-envelope error body falling back to `http_error`, and a rethrown transport failure.
- `clients/typescript/README.md`: new Example section linking the example and its validation commands.
- `CHANGELOG.md`: entry under Unreleased / Added.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [x] I have tested this change with different models/inputs

Python 3.12 environment from `uv sync --frozen --extra dev --python 3.12`.

```sh
cd clients/typescript && npm run build && node --test tests/example.test.mjs
# 6 passed

UV_NO_SYNC=1 make lint format-check type-check
(cd clients/typescript && npm run build && npm run typecheck && node --test 'tests/*.test.mjs')
# 118 passed (112 existing + 6 new)
.venv/bin/python -m pytest tests/ -q -n 4
# 29768 passed, 243 skipped (same totals on unchanged master 74561086)

pre-commit run --files CHANGELOG.md clients/typescript/README.md clients/typescript/examples/deidentify.mjs clients/typescript/tests/example.test.mjs
python scripts/release/check_repo_policy.py --commits origin/master HEAD
# all passed
```

Negative control: temporarily changing the example to decide `retry` from `error.message` instead of `error.code` makes 2 of the 6 tests fail. I also ran the example file directly against a local synthetic HTTP stub: it printed `redacted 1 entities` for a success and returned `validation_error` / 422 for a blank note.

## Documentation
- [x] I have updated the documentation accordingly
- [ ] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Code Quality
- [x] I ran `make format`, `make lint`, and `make format-check`
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

(`make lint`, `make format-check` and `make type-check` were run; no Python files changed. No Swift changes.)

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Checklist
- [x] I have read the [contributing guide](https://github.com/maziyarpanahi/openmed/blob/master/CONTRIBUTING.md), [Code of Conduct](https://github.com/maziyarpanahi/openmed/blob/master/CODE_OF_CONDUCT.md), and [maintainer guide](https://github.com/maziyarpanahi/openmed/blob/master/MAINTAINERS.md)
- [x] My commits have clear, descriptive messages
- [x] I have squashed/organized my commits appropriately

## Related Issues

## Screenshots/Examples

| Before | After |
| --- | --- |
| ![before](https://raw.githubusercontent.com/shu-chen-dot-ca/openmed/22bade69fb1cb2e01589766df141716b1ad2e1bd/draft_089b08/ev_76c557.jpg) | ![after](https://raw.githubusercontent.com/shu-chen-dot-ca/openmed/22bade69fb1cb2e01589766df141716b1ad2e1bd/draft_089b08/ev_75a25e.jpg) |

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b5bf9fc0c9c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.