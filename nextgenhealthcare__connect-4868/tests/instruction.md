# Issue

**Title:** Add default impl for getObjectsForSwaggerExamples in ServicePlugin

## Description

The ServicePlugin interface included an additional method since version 3.9.0 in commit  causing any classes implementing this interface to require updating. This broke multiple 3rd-party plugins which otherwise should have been able to be compiled against newer mirth versions.

I can only assume that this change was to facilitate a commercial plugin, because all of the open-source implementations contain an auto-generated method stub which returns null.

In order to avoid breakage with other plugins and to reduce overall code size, this PR provides a default implementation for the method which returns null and removes all of the now unnecessary method stubs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3d7cac8a3db5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.