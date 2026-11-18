# Issue

**Title:** DicomStorage handling priority improvement

## Description

This PR provides several enhancements to the archive's DICOM storage implementation, the major one being a better criteria when entry fetching for indexing.

The problem with the old algorithm is that it was not anti-symmetrical (`a < b` did not necessarily mean that `!(b < a)`), which could bring odd outcomes and starve other entries. Instead, the comparison function was rewritten to have two criteria, in this order:

- whether the calling AE title is listed as a priority AE title;
- the earliest sequence number, counted by the DicomStorage instance.

Also other changes:

- remove unused things, such as old methods and variable declarations
   - While there may be interest in bringing back the thread pool eventually, we should not allocate resources which are never used, much less threads.
 - refactor log lines

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5a7a9ed6f29d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.