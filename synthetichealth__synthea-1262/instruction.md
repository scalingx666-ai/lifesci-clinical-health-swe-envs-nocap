# Issue

**Title:** Additional reproducibility fixes, plus a "single person seed" feature

## Description

Fixes two additional instances where running with the same settings may produce different results, and adds a new feature to assist in debugging.

1. Fixes the issue seen here:  where the records were identical up to a point, then diverged. The issue appears to be with age calculation, specifically if you're unlucky a person's age in months can be different for a given timestep based on the time zone. The change here makes it so that all age calculations are done in UTC. (This does introduce the possibility of age-based events happening up to 12 hours before they would be expected to, or one full timestep later, but in context I don't think that's a big deal)
While there I also cached the birthdate as a LocalDate object, because in normal usage it will never change. (We do have some tests where we change the birthdate on a Person object unfortunately)

2. Changes Person.getSymptoms() from returning a Set to returning a sorted List. This is extremely minor as it's only ever used in the ClinicalNoteExporter, but the Set version can result in a different order of symptoms between runs.

3. Adds a new -ps for a single person seed, to assist in debugging. Now when you have a patient record you want to replicate, you don't have to re-run the entire population it was part of. Note this will silently override the -p setting. I can add a warning message or exception if people think that's useful.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `40cb89b520c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.