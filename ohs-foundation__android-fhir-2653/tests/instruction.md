# Issue

**Title:** Enable Magic Links to auto-link any links in docs (even if not <...>)

## Description

This will fix e.g. the currently missing links on hyperlinks on https://google.github.io/android-fhir/contrib/git/#further-resources (and similar future occurrences).

Inspired by e.g. https://github.com/enola-dev/enola/blob/df45649e225e57131d3fe433577e3748bb46a8f5/mkdocs.yaml#L151.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `535b8a3a297e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.