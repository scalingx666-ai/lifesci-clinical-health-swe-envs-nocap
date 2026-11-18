# Issue

**Title:** perf(units): speed up unit normalization -- 5.8% less time

## Description

## TL;DR
Skip cleanup for exact built-in-string alias hits and use ASCII and translation paths in `_clean`.
Optimize `normalize_unit` on the LOINC traversal from `test_the_unit_gate_admits_the_units_loinc_declares`, with additional public-API probes.
`normalize__clean_time_ratio`: **0.942128 (5.8% less wall time)**, the median of three independent paired re-scores.
Median timed sample: **920.946 ms → 866.290 ms**, with three complete workload traversals per sample.
Validation: `pytest -q` reports **958 passed, 110 skipped, 12 xfailed**; the requested regression subset reports **305 passed**; all three paired re-scores pass.

## What this changes

`_clean` previously folded every character in Python, including inputs already present in the cleaned alias table. Exact built-in-string alias hits now return before cleanup. ASCII strings skip NFKC, which leaves them unchanged, and avoid unnecessary space/tab replacements. Other inputs retain NFKC followed by stripping and use `str.translate` for symbol folding.

The shortcuts are restricted to built-in strings so subclasses retain the original normalization path. Case sensitivity, Unicode folds, annotations, power-of-ten refusal, and value-prefix fallbacks keep their existing behavior. The change is confined to `_clean` and `normalize_unit`, without dependencies or additional caches.

## Which benchmark it moves

The frozen workload reproduces `mirobody/tests/test_engine_coverage.py::test_the_unit_gate_admits_the_units_loinc_declares`: all bundled LOINC declared units, row/property lookups, normalization, unit-family checks, and the BMI reading check. It adds alias, Unicode, whitespace, invalid-input, quantity-parsing and scan probes, comparing complete outputs with an independent pristine-baseline oracle. The reported timings cover this workload, rather than timing the pytest process or `_clean` alone.

Baseline: `95a342531e1d86e0b25d76242b0cd1b5e221a234`. Each of three independent re-scores used nine alternating baseline/candidate pairs, fresh processes and seeded inputs, three traversals per timed sample, and an isolated CPU core under `osspr-bench`. Imports and resolver construction were warmed outside measurement. Python 3.12.13 on Linux; parent-clock wall time.

| Re-score | Baseline ms/sample | Candidate ms/sample | Paired time ratio | Relative IQR |
| --- | ---: | ---: | ---: | ---: |
| 1 | 931.435 | 873.145 | 0.934745 | 2.96% |
| 2 | 918.348 | 866.290 | 0.943313 | 2.36% |
| 3 | 920.946 | 865.070 | 0.942128 | 1.41% |

The ratio is the median of each run's paired candidate/baseline ratios, followed by the median across the three runs. Absolute before/after numbers are separate medians of the three run medians. Every re-score is below the frozen 0.95 cutoff, and every relative IQR is below 5%. No coverage or wrong-rate improvement is claimed.

Twelve distinct candidates passed the frozen evaluator and additional behavior checks. The selected source is Weco Observe step 11, unchanged from its recorded snapshot. One re-score attempt was rejected before timing because lint-generated cache files were present in the test copy; the remaining measurements used a fresh baseline copy with the identical patch. The rejected attempt is retained in the local evidence.

## Which gate you ran

- [x] `pytest -q` (full local suite, both roots): 958 passed, 110 skipped, 12 xfailed.
- [ ] `pytest -q mirobody` (not run separately; included in the full suite).
- [x] `lint-imports`: 6 contracts kept, 0 broken, against the patched checkout.
- [ ] `uvx ruff check mirobody examples` (used the environment's `ruff` executable instead).
- [ ] `python -m benchmarks.run_eval` (the private `eval/testset.jsonl` is not shipped in this checkout).

Additional checks, all passing:

- `pytest -q mirobody/tests/test_engine_coverage.py mirobody/tests/test_security_gates.py tests/agent/test_local_eval_contract.py benchmarks/genomics/test_review_regressions.py`: 305 passed, 5 subtests passed.
- `ruff check mirobody examples`: no findings; `python -m compileall -q mirobody`: passed.
- `python -c "import mirobody.kernel.meds, mirobody.kernel.query"`: passed.
- `python -m unittest discover -s benchmarks/genomics -p 'test_*.py'`: 37 tests, 2 skipped; health-records equivalent: 3 tests passed.
- A local differential check compared `_clean` with baseline on every Unicode code point alone and inside a unit-like string, plus 10,000 mixed sequences: 2,238,224 matches. Thirty public-input cases also checked string-subclass behavior. These checks are retained with the delivery evidence.

Tests ran on the patched source checkout, with source imports verified. Database and unavailable Docker cases remain skipped; no live-database end-to-end run was performed.

## AI assistance

This PR was prepared with AI assistance from Aiden. Candidates were tracked with Weco Observe.

Weco share link: https://dashboard.weco.ai/share/3xv-DVLeRRTiOLJcRN_jghJ1I4PeUPnM

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2bd7db2449d1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.