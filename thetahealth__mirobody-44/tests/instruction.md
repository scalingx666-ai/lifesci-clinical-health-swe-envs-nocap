# Issue

**Title:** Release 1.2.2: units engine backflow and Collect-constant convergence

## Description

## What's in 1.2.2

### Units engine

- **`indicator.fhir.units.pick_display_unit`** (new) — pick the unit a merged
  series displays in: most readings wins, ties go to the latest measurement.
  One indicator must render as one series in one unit; this is the tie-break
  callers were each reimplementing.
- **`parse_value_unit` respects the author's whitespace boundary (Path B0).**
  The whitespace collapse used to glue a numeric value onto a digit-leading
  count unit: `240 10⁹/L` became `240109/L` and parsed as value 240109,
  unit `/L` — a platelet count corrupted by three orders of magnitude. The
  first token is now tried as the whole value and the remainder as the whole
  unit before any collapsing.
- **The pulse Collect tables no longer carry conversion constants of their
  own.** `pulse.standardize.units` had drifted from the UCUM engine it
  shadows: lb was `2.20462` there vs the exact `2.2046226…` (`[lb_av]` =
  453.59237 g), glucose said `18.0182` vs the engine's `18.016` (C6H12O6 =
  180.16 g/mol). Imperial factors and the glucose / cholesterol /
  triglyceride molar masses now derive from `indicator.fhir.units.convert`
  at import. Device-only vocabulary (temperature affine, psi, rmssd, spo2
  aliases) stays local because the engine deliberately declines it.
- **`families.py` gains `[in_i]`/`[ft_i]` rows.** `scale()` gates on
  `UCUM_FAMILY`, and only the international spellings have `_BASE` atoms —
  without the rows the exact ft/in definitions were unreachable by any
  caller.
- **`mirobody/test_units.py`** ships the guardrails in-tree: Path B0 platelet
  vectors, the `pick_display_unit` tie-break, a zero-drift walk of the whole
  Collect table against the engine, and the substance factors pinned to
  `MOLAR_MASS`.

### Agent

- The note announcing this turn's uploads to the model is built from the
  mount itself rather than from the request, so it cannot name a path the
  mount does not serve ( / #42; details in the CHANGELOG).

### Docs / release

- Version 1.2.2. The four READMEs drop the run-from-source warning that
  publishing 1.2.1 made obsolete.

## Verification

- 206 shipped tests green (including the new `test_units.py`); full local
  suite 835 green.
- `lint-imports`: both contracts kept (engine stays framework-free).
- `python -m build` + `scripts/check_wheel_data.py`: all 5 engine data
  bundles present and real, no build-time-only artifacts shipped.

## Known follow-up (deliberately not in this PR)

`[in_us]`/`[ft_us]` — what the everyday `ft`/`in` aliases resolve to — still
have no `_BASE` atom, so imperial length stays atomic for those spellings.
Giving them exact survey definitions (or retargeting the aliases to the
international units) is a behavior change that deserves its own review.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `559c6dc557b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.