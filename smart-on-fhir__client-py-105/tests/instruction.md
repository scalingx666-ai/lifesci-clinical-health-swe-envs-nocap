# Issue

**Title:** Fix create() method for Bundle type transaction/batch

## Description

Supersedes #54, 

I'm not sure this is much of an improvement on #54 . I've added a createUrl() method as @p2 suggested. This might not have been what was intended. To me it would make sense for createUrl() to return relativeBase() in fhirabstractresource.py and for the Bundle class to override this. To do that I'd need some help working that into the resource template / generate_models script.

I would also add some tests but I need some help working out how to run the tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b4da2bdc3bf0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.