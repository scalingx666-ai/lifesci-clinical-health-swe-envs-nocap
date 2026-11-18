# Issue

**Title:** fix: source-grounded trend view with explicit coverage

## Description

First/last readings can conceal a series' movement, and a matching number alone can attach a citation to the wrong claim. This adds a source-grounded `view="trend"` and validates automatic citations against the metric, statistic, unit, date and signed change being stated. It includes and replaces #180.

- Compute observed-day third means, delta, relative delta, elapsed-calendar-day slope, direction and shape in the existing pure kernel query module. Preserve small-scale precision; normalize safe multiplicative units and abstain on incompatible/offset units. Relative cutoff tolerance keeps g/L and ng/L representations consistent.
- Preserve series identity, source warnings and coverage. More than 400 input days is explicitly partial; unsupported reported/nonnumeric data and insufficient inputs keep a reason. Compact and REST output retain statistics, units and shape.
- Trend citation definitions identify the actual daily span. Resolution reuses daily authority, reads amendments/erasure live and preserves person/conversation isolation. Derived values are never stored.
- Change/endpoint grammar keeps metric binding active. Explicit positive/negative signs, including Unicode minus, retain their meaning. Statistic operators are parsed outside the metric name, preserving Vitamin D and mean corpuscular volume readings. Units pass through the shared normalizer, and explicit incompatible or unknown units remain uncited. Named stats and correct changes/endpoints stay citable.

The 2% threshold and prominence rule describe change rather than clinical significance. Thirds count observed numeric days; gaps are not imputed. Citation matching establishes source attribution rather than clinical correctness.

Validation on `6b766d19`:
- Citation/trend controls: 106 passed.
- App suite: 1048 passed, 111 skipped, 12 strict xfails.
- Clean minimal suite: 611 passed, 174 skipped, 12 strict xfails.
- Ruff, compileall, six import contracts, bare library imports, source PHI baseline and comment style passed.
- Final-head GitHub CI is green.

Combined with #183 `ccaaf45f`: app 1096 passed / 111 skipped / 12 strict xfails; minimal 611 / 175 / 12. All nine additional review reproductions now pass. Combined lint/compile/import/PHI gates pass and the merge is conflict-free. The temporary local merge was aborted after verification; no GitHub merge was performed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95a342531e1d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.