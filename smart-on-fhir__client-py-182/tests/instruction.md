# Issue

**Title:** build: drop support for Python 3.8, add CI checks for 3.13

## Description

3.8 recently went end-of-life and 3.13 was released.
- Testing 3.13 is a no-brainer, especially since it removes a bunch of deprecated modules that we want to be sure we aren't using.
- Removing 3.8 makes our life easier and is in line with our recent removal of python2 and <3.8 as python versions go end-of-life. Previous releases of fhirclient will still be pip-installable for 3.8.

The [funnest new thing in 3.9](https://docs.python.org/3/whatsnew/3.9.html) that we might consider using more heavily is "type hinting generics in standard collections".

i.e. saying list[str] instead of List[str]

But the current code base doesn't have much hinting at all, so no changes needed yet. But we can use that going forward.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63b408168aa5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.