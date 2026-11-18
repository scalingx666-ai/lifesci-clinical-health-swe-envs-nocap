# Issue

**Title:** Blood pressure model with medication impacts

## Description

One more PR bringing features over from `cabg_cardio_gmf_htn_trial`. This PR reworks the Blood Pressure model to account for hypertension medications having impact. Ultimately I think this kind of thing could be reworked to medications having impact on arbitrary vital signs, but this is a first step.

Medications are defined in file `src/main/resources/htn_drugs.csv` with, as of this writing, more columns and codes than are required, so I may pare that down from what we had previously. Most important are the "code" and "impact minimum" and "impact maximum" columns, which are the RxNorm code and the expected range in mmHg of impact on blood pressure the medication is expected to have. As of now all drugs have impact range -11.5 to -16.29.

The basic approach of the model is:
 - determine baseline blood pressure
 - take into account medications
 - take into account lifestyle changes (CarePlans)

This model caches a number of things to ensure consistency, so that an individual's BP doesn't fluctuate wildly:
 - the final value at a given time, so that subsequent calls at the same timestamp don't have to recalculate
 - the individual's baseline blood pressure depending on hypertension status
 - the impact each drug has on blood pressure for that individual

Note one downside of this change is that in order to get realistic results at the aggregate level, we had to remove the "trending" aspect of the BloodPressureValueGenerator. We can try to reintegrate that but it will take more time and analysis.

Also note that this doesn't take into account the "titration" concept that was introduced in the htn_trial branch, as that concept was not fully fleshed out and very hackish. It worked for a research effort but it's not ready for master.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13151f3b36cf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.