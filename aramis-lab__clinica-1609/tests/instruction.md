# Issue

**Title:** [REF] Support spm25 for `pet-surface`

## Description

This PR modifies the script used in the pet-surface pipeline to allow for SPM25 usage. The pipeline would need further refactoring (separating tasks from pipeline, proper use of nipype interfaces, clean up calls for spm/matlab command...) but that can be addressed in another PR if need be.

What has been done : 
- Remove parts that were used by the set-up MATLAB + SPM
- Complete the parts that are used by the set-up MCR + SPM standalone. These existed but were not functional, as they were probably never tested.
- Some cleaning of useless cprints
- Code refactoring

RQ : `pet-surface-longitudinal` does not need additional modifications (though it is weird it works manually on CI but not with the non-regression workflow)

Todo : test on Mac

Tested on : Linux / CI machine1

Follow up : 
- For unification purposes with other PET pipelines PR#1237 should be completed afterwards.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dd390459b62b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.