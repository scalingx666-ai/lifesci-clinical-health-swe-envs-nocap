# Issue

**Title:** Integrate CodeRx MDT emergency_inhaler submodule into asthma module

## Description

Created a `emergency_inhaler` submodule following the CodeRx Medication Diversification Tool (MDT) tip sheet at https://coderx.io/projects/medication-diversification#tip-sheet.

Integrated the submodule into Synthea.

Ran a population of 5000 patients in Synthea and examined the CSV output to verify the diversity of emergency inhaler medications having REASONDESCRIPTION "Asthma" / "Childhood Asthma" has increased from one to many.

Attaching the log file output [log 20221101-201924.txt](https://github.com/synthetichealth/synthea/files/9915346/log.20221101-201924.txt) from the [CodeRx Medication Diversification Tool (MDT)](https://github.com/coderxio/medication-diversification) - it helps summarize the expected distributions of medication products at a population level and also provides a snapshot of the settings used to create this MDT submodule.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `30383d0d8cef`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.