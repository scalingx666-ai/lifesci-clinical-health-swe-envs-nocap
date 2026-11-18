# Issue

**Title:** Templates and Keep modules

## Description

This PR supports two "new" categories of modules:

## Templates
Templates are snippets of modules intended to help authors create a new module quickly. A corresponding change to the module builder () adds the ability to load these templates. After submitting this PR I will put together some documentation on how to use these to create a new module.

## Keep Modules
Keep modules have been supported for a while; this PR adds a set of built-in keep modules and updates the `-k` flag to support either arbitrary paths or these built-in ones. We had two already `must_have_cabg.json` and `must_have_cardiac_surgery.json` which I moved from the repo root to this new directory so any existing scripts that reference them can still work without changes. This should work both running via gradle/run_synthea or as a JAR file.


Tech Notes:
 - I migrated `Module.fixPathFromJar` into the Utilities class since I was using it in App as well now
 - Changed `Generator.keepPatientsModulePath` from File to Path since you can't reference files in a zip/jar as a File

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `85673dfd1503`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.