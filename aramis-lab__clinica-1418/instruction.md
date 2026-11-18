# Issue

**Title:** [FIX] `Center_Nifti` should run by default on T1

## Description

Adresses part of #1413

The modalities to center were set as described in the documentation. By default, `center_nifti` will only process T1w images. It is possible to change this by using the `--modality` option and you can process several modalities at the same time. 

Modalities are not restricted to a set of known modalities on our side to give the user more freedom. That means the user could enter `-m TOTO` if they wanted to, however the implementation is at the moment not very robust. **This can be changed.**


For follow-up PR : 
- Review the CI data et non regression tests to handle more cases (command line tested?)
- Review logic to check for files since split in 2 functions. Might be more practical to move the logic for it to be tested and completed (issue if output folder does not exist yet).
- Check behavior for writing over
- Review threshold logic (see discussion below)

### What is left to discuss : 

From the documentation, this tool is used in clinica if the data should at some point be processed by SPM (hence the discussion from #1412 on T1-Freesurfer). As of now, `center-nifti` processes by default only files that are more than 50 mm away from the center. The threshold was empirically established specifically for SPM by previous users. It is definitely not intuitive if someone uses `center-nifti` for any other purpose than SPM processing. We could : 
- get rid of the threshold altogether and process all images (🥇 in my opinion)
- change the default behavior to processing all images and use an option to accelerate the processing by allowing the user to choose the treshold

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d379ae6a87fa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.