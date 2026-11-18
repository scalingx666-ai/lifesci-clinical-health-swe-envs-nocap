# Issue

**Title:** [SchedulingConfigWorkspace] Add Schedule.comment editor

## Description

This field appears in Schedule selection in `<SchedulingWorkspace>`, and we're often defaulting it to some values that are duplicative of other information we already show, such as the name of the Actor attached to the schedule.

I think that in the long term we may want to distinguish the more generic concept of "Schedule.name" (which is an R5 field that maybe we should start allowing in an extension like `http://hl7.org/fhir/5.0/StructureDefinition/extension-Schedule.name`?). For now, we can offer SchedulingConfig users the ability to customize or remove those details on a per-schedule basis.

<img width="1911" height="1141" alt="Schedule Comment Field" src="https://github.com/user-attachments/assets/3851217d-f452-43fe-bf0e-29e5935f61e0" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6c86f9e1f93`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.