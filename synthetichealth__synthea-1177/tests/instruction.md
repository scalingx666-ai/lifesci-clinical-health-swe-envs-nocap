# Issue

**Title:** DME Data Ratio Changes

## Description

Adjustments to DME Data Ratios; .

The following adjustments are approximations based on observed claims data:

- Adds DME states back into metabolic syndrome care module.
  - Blood glucose monitors, calibration solution, testing strips, lancets.
- Adds Oxygen concentrators and portable concentrators into COPD with "DeviceEnd" states.
- Adds additional DME supplies to Sleep Apnea, regular supplies at Wellness visits, and device replacement every 5 years.
  - masks, respiratory humidifiers, air filters, tubing
- Skilled nursing facility
  - wheelchairs
- Added crutches and wheelchairs for broken ankles and hips.
- Added osteoporosis as a fall risk.
- Assign wheelchair or walker for osteoarthritis
- Total joint replacement resolves DME for 99%
- Assigns wheelchairs for some COPD patients who use oxygen
- Assigns beds and other items to some hospice patients
- Adjusts the DME warning messages to be less obnoxious.

Other high-impact changes that are not included: DME charges related to medication administration.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a2e87dcb629`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.