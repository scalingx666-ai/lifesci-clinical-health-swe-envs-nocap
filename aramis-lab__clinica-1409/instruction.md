# Issue

**Title:** PET-linear: apply transform fix

## Description

When applying the nonlinear registration T1 to MNI, the reverse_forward_transforms should be used instead of the forward_transforms. 

As the registration is non-linear, the transformation should be applied in the correct order. 

The forward_transforms output is a list containing the transformation in natural order: the first element should be applied first, and the last element should be applied last. However, the ApplyTransform applies lists of transformations in reverse order (the last transformation in the list is applied first). Thus, the "reverse_forward_transforms" output from ANTS registration should be used.

source: https://nipype.readthedocs.io/en/latest/api/generated/nipype.interfaces.ants.html#registration

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `80530a58a0dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.