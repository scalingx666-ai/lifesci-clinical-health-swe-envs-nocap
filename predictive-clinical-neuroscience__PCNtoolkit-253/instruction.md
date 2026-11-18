# Issue

**Title:** Proposed adjustments after testing in Meganorm project

## Description

I am trying to use the refactored version for the Meganorm project. I encountered some issues and tried to fix them. 

* Added code to handle situations where the required directories (`results/` and `plots/`) do not exist yet.
When I ran it initially, saving evaluation metrics resulted in an error because the needed directories did not exist and where not automatically created (like they were before I think). To prevent this error, I added code to ensure these directories are created if missing, which allowed the evaluation metrics to be saved.

* Models where not saved when savemodel was set to True, I added code that explicitly saves the models after fitting 

* In the original version of the PCNtoolkit, Nan values were handled automatically. This is not the case anymore and it results in an error. After discussion with Mosi I added an option to delete rows in the data where covariates, response variables or batch effects have Nan values. 

* Covariate_ranges where not saved to the normative_model.json but are necessary for (eg.) the plot_centile function. Added code that saves them to_dict


(My apologies for the messy commits, I adjust every time I encounter an error while testing)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a1f3105f275`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.