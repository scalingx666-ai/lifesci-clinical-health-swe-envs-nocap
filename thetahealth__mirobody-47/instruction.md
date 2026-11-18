# Issue

**Title:** release: let a failed PyPI upload fail the release

## Description

**Blocks tagging 1.3.0.** Found while running the pre-release check.

`Publish to PyPI` still carried `continue-on-error: true` — the exact mechanism
behind both failed 1.2.1 releases:

> the upload failed → the flag swallowed it → the workflow finished **green** →
> a GitHub Release was cut for a version that did not exist → the only way
> anyone found out was querying PyPI by hand.

The fixes at the time (#37, #38) went after what made the upload *fail* (a
polluted global env, then a stale import) and left the flag that turned those
failures into *silence*. The comment at the top of the file says "Both steps
below used to carry `continue-on-error: true`", which reads like the workflow
had been cleared of it. Two steps had; the one that publishes had not.

## Changes

- **`Publish to PyPI` can fail the job.** No GitHub Release is cut for a
  version that is not on PyPI.
- **New step: `Verify the version is actually on PyPI`.** An upload exiting 0
  is twine's opinion; this asks `pypi.org/pypi/mirobody/$VERSION/json` for a
  200, polling two minutes because the index lags the upload. It turns "check
  PyPI by hand after every release, don't trust the workflow's face" from a
  habit someone has to remember into a step that fails.
- **TestPyPI keeps its flag** — that upload already ends in `|| echo`, a
  duplicate filename on a re-run is expected, and nobody installs from it.

Verified the YAML parses and that `Publish to PyPI` now resolves to
`continue-on-error=False`.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc526d43206a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.