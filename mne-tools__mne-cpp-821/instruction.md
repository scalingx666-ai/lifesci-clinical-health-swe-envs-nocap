# Issue

**Title:** WIP [ENH,MAINT] HPI Coil Presets

## Description

- Add GUI for selecting HPI coil presets.
- Load presets from file.
- Some light refactoring to separate the parsing of digitizer data and displaying that data in the gui.

I ended up hijacking the existing json file that every mne scan plugin has and used it as the dev/enduser editable preset file. It gets coped to the plugin folder at build time.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `22e2cdf92d8c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.