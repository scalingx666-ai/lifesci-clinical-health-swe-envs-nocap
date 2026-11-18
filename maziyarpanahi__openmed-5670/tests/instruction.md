# Issue

**Title:** feat(mlx): give MapleResponseError stable reason codes

## Description

## Description
Gives `MapleResponseError` a stable, machine-readable `code` so callers can turn a Maple validation failure into an abstention without matching English message text.

## Type of Change
- [x] New feature (non-breaking change which adds functionality)
- [x] Test addition/improvement

## Changes Made
- Adds `MAPLE_RESPONSE_ERROR_CODES`, a closed frozenset (exported from `openmed.mlx.maple`), and a keyword-only `code` argument and attribute on `MapleResponseError`. An unknown or missing code falls back to `invalid_response`, so existing `MapleResponseError("...")` callers keep working.
- Every `MapleResponseError(` raise site in `openmed/mlx/maple.py` passes a literal code, for example `empty_response`, `non_text_response`, `unfinished_reasoning`, `invalid_json`, `trailing_text`, `non_object_json`, `invalid_keys`, `invalid_span`, `unmatched_span`, `invalid_label`, `label_not_allowed`, `invalid_relation`, `unknown_relation_endpoint` or `invalid_uncertainty`. Messages and parsing behaviour are unchanged.
- No code is ever built from model output.
- Adds a CHANGELOG (Unreleased / Added) entry and a short section with an example in `docs/maple-on-device.md`.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes

New tests in `tests/unit/mlx/test_maple.py`:
- Each code is triggered from a synthetic parser or runtime path, and every code except the fallback is shown to be reachable.
- An AST check confirms that every `MapleResponseError(...)` call passes a literal `code=` from the closed set.
- A sentinel check confirms that model output never leaks into a code.
- The fallback behaviour is tested.

```
.venv/bin/python -m pytest tests/unit/mlx/test_maple.py -q   # 42 passed
.venv/bin/python -m pytest tests/unit/mlx -q                 # 204 passed, 14 skipped
ruff check / ruff format --check on the changed files        # clean
```

## Documentation
- [x] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Dependencies
- [x] I have not added any new dependencies

## Related Issues

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f83eb05b74f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.