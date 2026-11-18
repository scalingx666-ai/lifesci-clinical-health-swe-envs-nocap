# Issue

**Title:** Remove aclmanager

## Description

Dicoogle was holding remnants of a DICOM ACL mechanism which filtered C-Find requests by the title of the AE which provided the DICOM objects. At this time, support for this filter would require a very custom indexer plugin and it is very unlikely that anyone is still depending on it (still I would appreciate a confirmation from @bastiao).



### Summary

- Remove uses of ACL manager
- Remove dependency aclmanager from core
- Add dependency jdom2 to core, in its latest version 2.0.6.1
   - It was a transitive dependency that we were still depending on.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c728ffaca8ef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.