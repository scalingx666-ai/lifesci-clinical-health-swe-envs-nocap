# Issue

**Title:** Implement Longitudinal Modelling (zdiff and zgain)

## Description

#### AI assistance

If you used AI to help prepare this pull request, please describe how.
- "I prompted Claude Opus 4.8 to plan and implement the code, then refined it
  manually until I was satisfied."


#### Reference issue (if any)

 #477 #460 

#### What does this implement/fix?

Implements longitudinal modelling. The core of this architectural design is the longitudinal score. Every new longitudinal model should have a score (= a number that tell us how much a subject follows the expected longitudinal trajectory). The rest of the details can be implemented flexibly on top of this architecture.

we follow the user API design 

#### To reproduce

In this PR there will be a longitudinal_model notebook to run and check everything

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3eac2b693e49`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.