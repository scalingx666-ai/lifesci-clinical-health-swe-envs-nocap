# Issue

**Title:** readme: print the BUNDLE_VERSION the package actually reports

## Description

The four READMEs showed

```
>>> import mirobody; mirobody.BUNDLE_VERSION
'loinc-2.82+2026.08.28-050559ecc200'
```

and the package reports `loinc-2.82+2026.08.28-af2524b7a285`. The digest was
current when that section was drafted in #45; the bundle was restamped
afterwards and the prose was not re-checked.

It is the **only** interactive example the READMEs carry, and nothing guarded
its output — `test_readme_numbers.py` covers every other exact number in those
files. A reader pasting the one line we invite them to paste got a different
string back, from the paragraph whose whole point is that the corpus version is
a fact the package states rather than a comment that can drift.

The digest is a hash over the bundle's own members, so it must change whenever
the bundle does. The new test makes that a required edit here instead of a
wrong line in the README; it fails on the stale value, verified by putting it
back.

Found while checking this repo's public surface against the GitHubDaily article
going out today, which uses the README as its screenshots.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `519b92bca8d0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.