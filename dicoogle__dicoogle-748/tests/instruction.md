# Issue

**Title:** Adjust WebUIPluginManager and WebUIPluginTest for test reliability

## Description

We have encountered an odd scenario where the JDK would try to retrieve the web UI plugin directory incorrectly in the tests, resulting in false positives. This form should be more resilient.

### Summary

- Replace `assert`s with hard checks which throw exceptions in `WebUIPluginManager#load`
- Tweak test1 dir resource retrieval in `WebUIPluginTest#loadTest1`, adding a fallback to webui plugin path resolution

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1fc8c21beee3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.