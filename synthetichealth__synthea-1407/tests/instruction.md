# Issue

**Title:** New script to update code displays

## Description

This PR introduces a new script to automatically update code displays when they do not match the preferred value for the code system. Originally I intended this process to be part of the Concepts java class, but writing changes back to the JSON file would have involved too much refactoring so instead I created a new JavaScript ... script.

To try to minimize the number of display changes, and standardize code displays across modules, this script takes a 2-pass approach:
1. Iterate over all the modules and keep an inventory of the codes/displays
2. Fetch the preferred display for each code. Keep a dictionary of code -> display
   i. If a module already uses the preferred display somewhere, store that
   ii. If the current display is allowed but not necessarily the preferred, store that (to reduce changes)
   iii. Otherwise, store the preferred display
3. Iterate over all the modules again and update any displays that don't match the value in the dictionary
There's also special handling for SNOMED codes to try to avoid flip-flopping between "Code" and "Code (tag)"

The modules are updated in-place and I recommend using `git add -p src/main/resources` to iterate over them and review each change separately before committing.

The script will also print errors when a code is not valid for the given system. We use some US-specific SNOMED codes which this will complain about but it will also reveal typos which I'm fixing as well.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `336e3d87866f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.