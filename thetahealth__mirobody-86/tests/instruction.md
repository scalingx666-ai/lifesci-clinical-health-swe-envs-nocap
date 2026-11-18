# Issue

**Title:** release: cut 1.5.0

## Description

Bumps the version literal to 1.5.0, closes the CHANGELOG section, and clears
three references to `mirobody/indicator/` that 1.5.0 deleted. One of them
would have failed the release.

## The one that blocked the release

`.github/workflows/pypi-release.yml`'s ② `[parse]` gate ran
`import mirobody.indicator`. Against a 1.5.0 wheel that is
`ModuleNotFoundError`, and the step has no `continue-on-error`, so a tag would
have built the artifacts, failed the gate, and published nothing. It imports
`mirobody.translate` now. Verified both ways: the old line fails on the built
wheel, the new one passes.

## The CHANGELOG's measured claim

It said coverage holds at 0.963 and wrong-rate falls 0.035 to 0.025 on the
6,780 inside the cut. Re-run on this tree with `benchmarks/run_eval.py
--no-embed`:

| | was written | measured |
|---|---|---|
| in-cut n | 6,780 | 6,992 |
| in-cut coverage | 0.963 | 0.950 |
| in-cut wrong-rate | 0.025 | 0.025 |

0.963 is the pre-cut OVERALL figure, recorded by every run from 2026-08-31 to
09-18; `run_eval.py`'s own `scope_of` puts `checkup` + `clinical-extended`
(3,401 + 3,591 = 6,992) inside the cut. The wrong-rate was right. The section
now states both scopes: overall 0.963 to 0.916 and 0.032 to 0.030, in-cut
0.950 and 0.025, and says the resolver abstains on 273 of the 362 outside.

The run reproduces the 1.5.0 branch's own 2026-09-20 results exactly, so this
corrects the prose, not the resolver.

## The other two

`MANIFEST.in` excluded eleven paths under `mirobody/indicator/` as the sdist
half of `_BUILD_ONLY_CODE`, which `build_backend.py` emptied in 1.5.0. The
build printed a warning per line; those eleven are gone. `config.llm.yaml`
told the reader to re-embed with `python -m mirobody.indicator embed`, a
command that does not exist.

## Verified

- `pytest -q` 1,987 passed, 4 skipped; `pytest -q mirobody` 69 passed
- `ruff`, `check_comment_style`, `lint-imports` (6 contracts), `stamp_bundle_version --check`
- `python -m build` then `check_wheel_data.py` on both artifacts, `twine check` both PASSED
- The three install gates from the release workflow, each in a fresh venv and
  run from outside the checkout: ① bare install reaches nothing but the stdlib
  (`deps []`), reports 1.5.0 and `loinc-2.83+2026.09.17`, resolves 718-7;
  ② `[parse]` imports with no FastAPI; ③ the server install stays
  langchain-free
- sdist install, then `mirobody resolve hemoglobin 血红蛋白` from `/tmp`

Artifacts build at 13 MB (wheel) and 14 MB (sdist). Not tagged.

Left alone: `scripts/check_comment_style.py` still lists `mirobody/indicator/`
in `SKIP_PREFIXES`, which now matches nothing. A dead skip entry only makes the
gate stricter, so it is not a defect, but it is dead.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e90f67def88`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.