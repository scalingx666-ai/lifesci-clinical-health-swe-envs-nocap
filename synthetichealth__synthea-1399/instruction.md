# Issue

**Title:** Module cleanup

## Description

This PR cleans up a few items that pop up pretty often in generated records and look odd:

1. There are several ConditionOnsets that do not have a corresponding ConditionEnd and are left open forever, even though they are acute conditions which are addressed in the module:
   - Appendicitis & rupture of appendix
   - Opioid addiction: Drug overdose (note there are a few other conditions in this module which don't get ended, like "Impacted molars", "Chronic pain", and migraine, which are not really treated so I'm ok leaving them open)
   - Miscarriage (added a "history of miscarriage" condition)
   - Covid19 outcomes: Hypoxemia (seems like this was just missed in the long list of conditions, I don't see anything in the old notes for why this one specifically should stay open)
2. Prediabetes can be diagnosed after diabetes, and based on medication impacts it happens often, so that's no longer possible
3. A couple modules include "patient transfer" as a condition where it really doesn't fit. There's already a Procedure for the transfer so I just removed the Condition.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e8a047a6179a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.