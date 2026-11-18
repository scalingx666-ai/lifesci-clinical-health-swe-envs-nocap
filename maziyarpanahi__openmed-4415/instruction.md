# Issue

**Title:** feat: export provider capability matrix schema

## Description

## Description
Export a strict, self-contained Draft 2020-12 schema for the actual JSON records emitted by the provider capability matrix. Deployment tooling can validate the five content-free cell fields and their allowed outcome/reason combinations without loading providers or resolving remote schemas.

## Type of Change
- [x] New feature
- [x] Tests and documentation

## Changes Made
- Add fresh mapping and byte-stable JSON schema exports with fragment-local references.
- Share identifier/version grammars, record limits and outcome/reason options with the Python runtime contract.
- Close cell objects; reject extra metadata, endpoint/model paths, malformed values, trailing newlines, unknown outcomes and contradictory reasons.
- Add source drift controls and an executable guide with navigation, publication registration and changelog updates.

## Dependencies and merge order
This branch preserves Rudy Celekli's original #4159 capability-matrix commit and integrates it onto current master. Merge #4159 first, then refresh and revalidate this PR. The original contributor branch remains unchanged. The maintainer follow-up centralizes existing contract rules for schema export and makes a local type annotation explicit; it does not change matrix outcomes.

The branch also carries the independently validated scanner-install and documentation-search accessibility repairs used by the other v3.3 implementation PRs. No package dependencies or lockfile changes.

## Testing
- [x] **88 focused tests passed** on Python 3.12 and the frozen Python 3.11 environment.
- [x] Full suite: **25,650 passed, 155 skipped, 11,361 subtests passed**, 81 warnings, 210.73 seconds.
- [x] `make format lint format-check type-check` and explicit mypy on both matrix modules.
- [x] Draft 2020-12 metaschema validation, real matrix output, blocked external resolution and schema/runtime boundary parity.
- [x] Exported identifier patterns also passed positive/negative controls in an ECMA-262 runtime.
- [x] Strict `make docs-build`, executable guide, routes, feeds and publication metadata.
- [x] Documentation controls passed in Chromium, Firefox and WebKit.
- [x] Wheel and sdist source bytes verified; `twine check` passed.
- [x] API compatibility, dependency-license policy, actionlint, pre-commit security/secret checks and all five incoming commits' attribution policy passed.

## Documentation and limits
- [x] Public docstrings, guide and changelog updated.

JSON Schema rejects identical duplicate records. Uniqueness of a provider/profile pair with differing other fields remains a Python renderer check, because standard `uniqueItems` cannot express uniqueness over a subset of fields. The guide documents this boundary, canonical ordering, and the difference between structural validity and real provider qualification.

## Related Issues

Related to #3095, #4159

## Example
```python
from jsonschema import Draft202012Validator
from openmed.multimodal.capability_matrix_schema import build_capability_matrix_schema

schema = build_capability_matrix_schema()
Draft202012Validator.check_schema(schema)
Draft202012Validator(schema).validate([])
```

The exporter makes no network calls, discovers no providers and loads no models.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2f70a60d8377`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.