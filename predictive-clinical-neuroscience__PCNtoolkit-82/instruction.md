# Issue

**Title:** Added SHASHo, SHASHo2, SHASHb support for hbr

## Description

- Added PyMC3 implementation for SHASH, SHASHo, SHASHo2, and SHASHb. 
- Added support for SHASH* likelihoods in hbr
- Changed to a new keyword system
- Added some parameter classes in the hbr method
- Added get_map function to the HBR class
- Added support for more priors to from_posterior

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c8e4f5c933bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.