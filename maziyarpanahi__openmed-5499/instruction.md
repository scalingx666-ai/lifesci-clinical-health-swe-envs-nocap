# Issue

**Title:** fix: reject non-JSON request media types at the privacy proxy

## Description

# Pull Request

## Description
Validate the request `Content-Type` header on the privacy proxy chat completion routes (`/v1/chat/completions` and `/chat/completions`) before reading or parsing the request body. Requests with non-JSON or missing media types now return HTTP 415 with `reason: "unsupported_content_type"` through the existing PHI-safe error payload without invoking the transport or echoing request text.

## Type of Change
- [x] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- Reused `_normalize_content_type` from `openmed.service.privacy_proxy.outbound` in `chat_completions` (`openmed/service/privacy_proxy/app.py`) to validate the `Content-Type` header before calling `await request.json()`.
- Added optional `status_code` override support to `PrivacyProxyError` so `PrivacyProxyRequestError(reason_code="unsupported_content_type", status_code=415)` returns HTTP 415 via `_error_response`.
- Added unit tests in `tests/unit/service/privacy_proxy/test_app.py` covering `application/json; charset=utf-8`, `text/plain` with a JSON payload, and a missing `Content-Type` header.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [x] I have tested this change with different models/inputs

Validation commands executed locally:
``bash
uv run --with pytest --with fastapi --with httpx pytest tests/unit/service/privacy_proxy/test_app.py -q
uv run --with pytest --with fastapi --with httpx pytest tests/unit/service/privacy_proxy/ -q
uv run --with ruff ruff check openmed/service/privacy_proxy/app.py tests/unit/service/privacy_proxy/test_app.py
uv run --with ruff ruff format --check openmed/service/privacy_proxy/app.py tests/unit/service/privacy_proxy/test_app.py
uv run python scripts/security/check_effect_paths.py --check
uv run --with mypy --with fastapi mypy openmed/service/privacy_proxy/app.py
``

## Documentation
- [ ] I have updated the documentation accordingly
- [ ] I have added docstrings to new functions/classes
- [ ] I have updated the CHANGELOG.md

## Code Quality
- [x] I ran `make format`, `make lint`, and `make format-check`
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Checklist
- [x] I have read the [contributing guide](https://github.com/maziyarpanahi/openmed/blob/master/CONTRIBUTING.md), [Code of Conduct](https://github.com/maziyarpanahi/openmed/blob/master/CODE_OF_CONDUCT.md), and [maintainer guide](https://github.com/maziyarpanahi/openmed/blob/master/MAINTAINERS.md)
- [x] My commits have clear, descriptive messages
- [x] I have squashed/organized my commits appropriately

## Related Issues

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e2323288ec5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.