# Issue

**Title:** Add Tukey fences and batch-aware outlier removal

## Description

#### AI assistance

I wrote the code and used Claude Opus to review and suggest revisions. I then reviewed the changes myself.

#### What does this implement/fix?

Previously, z-scoring was used for outlier removal. However, this approach assumes that the data are approximately Gaussian distributed. This assumption often does not hold for neuroscience data (which is one of the motivations for using SHASH).

This revision supports both z-scoring and the Tukey fences method. Tukey fences is a non-parametric approach and doe not require the data to follow a normal distribution.

Secondly, site differences were previously not accounted for during outlier removal. This fork provides an option for the user to pass a list of batch effects, which are then used to group the data before performing outlier removal.

Lastly, I have tried to maintain backward compatibility with the existing implementation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fbf1be46b7a3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.