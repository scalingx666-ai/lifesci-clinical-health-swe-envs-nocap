# Issue

**Title:** feat(web): add Node.js de-identification example

## Description

# Pull Request

## Description
Adds a runnable Node.js example for the `openmed` npm package: it de-identifies a synthetic note and prints the redacted text and span labels, giving web/Node users the end-to-end script the package previously lacked.

## Type of Change
- [ ] Bug fix (non-breaking change which fixes an issue)
- [x] New feature (non-breaking change which adds functionality)
- [ ] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [ ] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- Add `examples/web/node_deidentify.mjs` exporting `run({ pipeline })`: it de-identifies a synthetic note, prints the redacted text and span labels (never the original identifier values), and returns the full result. When run directly it loads the default model with `loadOnnxModel`, with a comment noting the one-time model download; tests always inject a stub pipeline.
- Add `tests/web/test_examples_node.spec.ts` calling `run()` with a stub pipeline and asserting the redacted output, the span labels, and that no original identifier values appear in the printed output.
- Register the new spec in `test:node` in `js/openmedkit-web/package.json`.
- Link the example from `js/openmedkit-web/README.md` with build/run instructions.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [ ] I have tested this change with different models/inputs

Commands run (in `js/openmedkit-web`):
- `npm ci` then `npm test` (build + typecheck + `test:node`) — 35 passed, including the new example test.
- `npm run test:node` re-run — the new test is `ok 1 - node deidentify example redacts a synthetic note with a stub pipeline`.

## Documentation
- [x] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [ ] I have updated the CHANGELOG.md

README gains a short "Node.js Example" section; the example file itself is commented for readers copying it into their own project.

## Code Quality
- [x] I ran `make format`, `make lint`, and `make format-check`
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

Validated with `pre-commit run --files examples/web/node_deidentify.mjs tests/web/test_examples_node.spec.ts js/openmedkit-web/package.json js/openmedkit-web/README.md` plus the package's own `npm test` (tsup build and `tsc --noEmit` included). No Swift files touched.

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Checklist
- [x] I have read the [contributing guide](https://github.com/maziyarpanahi/openmed/blob/master/CONTRIBUTING.md), [Code of Conduct](https://github.com/maziyarpanahi/openmed/blob/master/CODE_OF_CONDUCT.md), and [maintainer guide](https://github.com/maziyarpanahi/openmed/blob/master/MAINTAINERS.md)
- [x] My commits have clear, descriptive messages
- [x] I have squashed/organized my commits appropriately

## Related Issues

## Screenshots/Examples
```text
Patient [PERSON], DOB [DATE_OF_BIRTH], email [EMAIL].
PERSON, DATE_OF_BIRTH, EMAIL
```
(from the stub-pipeline test; a direct run with the real model prints the same shape)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b5bf9fc0c9c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.