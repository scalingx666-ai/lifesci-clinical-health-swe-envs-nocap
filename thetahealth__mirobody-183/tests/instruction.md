# Issue

**Title:** fix: discriminating capability probes with auditable grading

## Description

Capability probes need independently correct gold and grading that cannot be passed by a constant answer, an empty cite or a differently formatted wrong unit. This adds a compact source-derived diagnostic with separate C3 window, C4 aggregate, C6 provenance and C7 absence results. It includes and replaces #181.

- Read the generator's actual flat device records in the planned account time zone. Retain disjoint windows only when source-derived answers differ beyond combined tolerances. Default: two metrics and at most 19 questions per person. Flat/ambiguous sources are omitted with reasons.
- Establish absence against loaded documents, short device series and journal mentions. Reject contradictory absence plus a numeric reading. Exclude mixed units, duplicate-day ambiguity and windows overlapping document readings; sleep uses the existing interval oracle.
- Exclude dates/citation IDs from numerical extraction and reject ambiguous values. Explicit incompatible units fail inside parentheses, brackets, quotes, backticks, nested wrappers and surrounding whitespace; UCUM's own brackets remain meaningful. Reuse citation tracing to reject empty, invented and numerically unsupported references.
- Verify pinned corpus and completed account provenance before model calls. Save complete questions, source hashes, window points, answers and tool evidence. Keep incomplete/failed/unattempted runs in their selected denominators and stop after an incomplete turn. `--dry-run` constructs the set without account or model access.

Validation on `ccaaf45f`:
- Probe controls: 48 passed, including 17 format/UCUM controls.
- App suite: 1009 passed, 107 skipped, 12 strict xfails.
- Clean minimal suite: 530 passed, 171 skipped, 12 strict xfails.
- Ruff, compileall, six import contracts, bare library imports, source PHI baseline and comment style passed.
- Final-head GitHub CI is green: Python 3.12/3.13, Windows benchmark and Linux/macOS/Windows imports. Both replacement PRs report CLEAN / MERGEABLE.

Combined with #182 `6b766d19`: app 1096 passed / 111 skipped / 12 strict xfails; minimal 611 / 175 / 12. All nine additional review reproductions now pass; the merge is conflict-free. No combined merge commit or GitHub merge was retained.

This is a compact record-access diagnostic. C6 checks numeric traceability; clinical interpretation and independent held-out performance need separate evaluation. No new model quality score is claimed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95a342531e1d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.