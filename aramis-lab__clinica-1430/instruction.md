# Issue

**Title:** [ENH] Improve the `crop_nifti`

## Description

Following #1426, this PR proposes to improve the `crop_nifti` function.

Currently the function behaves in a very specific way, by cropping the provided image with a hardcoded bounding box that we defined for a specific use case (T1 images with MNI reference template). Therefore, I think the name is misleading and we could make use of a more generic function.

This PR proposes to make `crop_nifti` more generic by letting users provide both the bounding box and the reference image. If no bounding box is provided, then no cropping is performed. If no reference image is provided, the input image is used as a reference. In other words `crop_nifti(img)` with no other argument is the identity function.

The old `crop_nifti` has been renamed `crop_nifti_using_t1_mni_template` and is nothing more than a partial function on the new `crop_nifti`, calling it with the MNI_BBOX and the MNI cropped template. 

Implementation details: I introduced two classes called `NiftiImage` and `NiftiImage3D` which behave as wrappers around a path to a nifti image. I'm still unsure whether we should keep them or not, but I think it could help us reduce boilerplate code we have in various places to check that a nifti is 3D, or that a nifti file exists, and so on.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0321fd402a0b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.