# Issue

**Title:** Fix StackOverflowError and users settings folder issues

## Description

This PR introduces fixes to two distinct bugs related to the ExportToCSV modal.
The export of the Search Result to a CSV is originating a StackOverflow exception in the PluginController. This is caused because the queryAll method is invoking itself infinitely. This was fixed by getting the list of providers and query each one.

The second part fixes the saving of presets into files. Changes introduced in #388 creates a file named "users" in the dicoogle folder. This name was used to organize and store preset data - was previously saved in users/<username>/presets/<presetname>. This PR changes the saving directory name to userdata/<username/presets/<presetname>. I also abolish the dependencies of apache StringUtils.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9bf18f5a9ce9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.