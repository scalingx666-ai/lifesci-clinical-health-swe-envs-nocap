# Issue

**Title:** Remove insecure built-in defaults from eval signing, Android hashing and corpus loading

## Description

# Pull Request

## Description
Three places in OpenMed fell back to a secret that is published in the source. As a result, their output proves nothing, or can be reversed by anyone who reads the code. This PR removes all three defaults. Each is a deliberate break, so it targets v4.0.

**Merge after the v3.3.0 tag.** Master is still the 3.3 line until then.

1. **Eval report signing.** `run_relation_suite`, `run_suite(suite="relations")` and `run_federated_leakage_eval` fell back to `openmed-relation-scorecard-local-key` / `openmed-federated-eval-local-key`. Anyone could forge a scorecard or leakage report that verifies.
2. **Android `HASH` replacements.** `DeidentifyEngine` keyed its HMAC with the published `openmed-android-deidentify-v1` salt. With that key, digests of guessable identifiers (MRNs, phone numbers, dates) can be reversed offline by brute force.
3. **Biomedical NER corpus loading.** The public corpus loaders passed `trust_remote_code=True`, so a change to an upstream dataset repository could run code on the evaluator's machine.

## Type of Change
- [x] Bug fix (non-breaking change which fixes an issue)
- [ ] New feature (non-breaking change which adds functionality)
- [x] Breaking change (fix or feature that would cause existing functionality to not work as expected)
- [x] Documentation update
- [ ] Code refactoring
- [ ] Performance improvement
- [x] Test addition/improvement

## Changes Made
- `openmed/eval/harness.py`: both built-in keys are removed. A new `_resolve_report_signing_key` uses `signing_key` first, then `OPENMED_RELATION_SCORECARD_KEY` / `OPENMED_FEDERATED_EVAL_KEY`, and otherwise raises `ValueError` naming both. It runs before any fixture is scored or the detector subprocess starts, so a missing key writes no output file. Empty keys are rejected. `sign()`, `verify()` and the report formats are unchanged.
- `android/.../deid/DeidentifyEngine.kt`: without `hashSalt`, each engine generates a random 32-byte key from `SecureRandom`. Digests repeat within one engine but differ between engines and app launches. Callers who need stable pseudonyms pass their own secret key. The KDoc explains how to store it.
- `openmed/eval/datasets/biomedical_ner.py`: JNLPBA, Species-800 and BC2GM load Parquet pinned to a commit on each repository's `refs/convert/parquet` branch, through the packaged `parquet` builder. BC5CDR and NCBI Disease are published only as loading scripts, which `datasets` 4 and later already refuse. They now raise a clear `RuntimeError` asking for a local export. `BiomedicalNerSource` drops `trust_remote_code` and gains `revision` and `data_dir`. Suite metadata records the pinned revision.
- Docs: `docs/eval-harness.md` documents the key requirement. The CHANGELOG has three **Breaking** entries under `Security`.

## Testing
- [x] I have added tests that prove my fix is effective or that my feature works
- [x] New and existing unit tests pass locally with my changes
- [ ] I have tested this change with different models/inputs

New tests (synthetic and offline):
- `tests/unit/eval/test_report_signing_keys.py` checks the following:
  - With no key, both harnesses fail before the runner or detector starts, and no scorecard file is written.
  - Empty keys are rejected.
  - The environment key is used, and an explicit key wins over it.
  - Reports no longer verify under the old published strings.
- `tests/unit/eval/test_biomedical_ner_remote_sources.py` checks the following:
  - No source carries `trust_remote_code`, and every revision is a full commit SHA.
  - Pinned sources call `load_dataset("parquet", data_files=...)` at that commit.
  - `data_dir` overrides the config name.
  - Script-only corpora fail before `datasets` is called.
  - Metadata records the revision.
- `DeidentifyEngineTest.kt`: default engines use independent random keys, and the default key is not the legacy salt.

Results:
- `.venv/bin/python -m pytest tests/unit/eval -q -m "not slow and not fuzz"` with both key variables unset: 2641 passed, 13 skipped.
- `tests/unit/test_model_registry.py`, `tests/unit/clinical/validation/test_validation_study.py` and `tests/unit/release`: 297 passed.
- After the final rebase onto `174fd485c` (#5552), the targeted signing, corpus, federated and relation test files were rerun: 24 passed.
- `./gradlew :openmedkit:testDebugUnitTest --tests 'com.openmed.openmedkit.deid.DeidentifyEngineTest'`: 10/10 passed.
- One `test_public_api_compat.py` run failed once while a Gradle build was running alongside it. It passed on every rerun, on this branch and on master (42 passed). It doesn't touch these files.

## Documentation
- [x] I have updated the documentation accordingly
- [x] I have added docstrings to new functions/classes
- [x] I have updated the CHANGELOG.md

## Code Quality
- [x] I ran `make format`, `make lint`, and `make format-check`
- [ ] For Swift/OpenMedKit changes, I ran `make format-swift` and `make lint-swift`
- [x] I have performed a self-review of my own code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] My changes generate no new warnings

Ruff format and lint pass on the touched Python files. `scripts/release/check_repo_policy.py --commits origin/master HEAD` passes (4 commits).

## Dependencies
- [x] I have not added any new dependencies
- [ ] OR I have added new dependencies and they are justified because: ____

## Checklist
- [x] I have read the [contributing guide](https://github.com/maziyarpanahi/openmed/blob/master/CONTRIBUTING.md), [Code of Conduct](https://github.com/maziyarpanahi/openmed/blob/master/CODE_OF_CONDUCT.md), and [maintainer guide](https://github.com/maziyarpanahi/openmed/blob/master/MAINTAINERS.md)
- [x] My commits have clear, descriptive messages
- [x] I have squashed/organized my commits appropriately

One commit per default, plus the changelog commit, so each break can be reviewed alone.

## Related Issues

Related:
- #4794 (v6.0): the Python core's `method="hash"` is still unsalted SHA-256. This PR does not change it.
- #4888 (v5.2): pins the SHIELD sample revision and records dataset revisions in reports. This PR pins only the biomedical NER corpora.
- Migration guide: there is no `docs/migration/3.3-to-4.0.md` on master yet. Two open v4.0 branches add it (#4864 and the #4266 branch). To avoid an add/add conflict, the migration notes live in the CHANGELOG entries for now and should move into that guide once it lands.

## Screenshots/Examples
```python
from openmed.eval import run_relation_suite

run_relation_suite(model_name="m", runner=runner)
# ValueError: relation scorecard signing requires a key: pass signing_key or
# set OPENMED_RELATION_SCORECARD_KEY; OpenMed has no built-in signing key
```

| Surface | Before | After |
| --- | --- | --- |
| Relation scorecard, no key | signed with a published key | `ValueError` before any fixture runs |
| Federated leakage report, no key | signed with a published key | `ValueError` before the detector starts |
| Android `HASH`, no `hashSalt` | HMAC with `openmed-android-deidentify-v1` | HMAC with a random per-engine 32-byte key |
| JNLPBA / Species-800 / BC2GM | `trust_remote_code=True`, unpinned | commit-pinned Parquet, no dataset code |
| BC5CDR / NCBI Disease | loading script | needs a local export (clear error) |

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `174fd485c153`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.