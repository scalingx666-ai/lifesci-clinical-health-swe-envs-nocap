# Issue

**Title:** [ENG-882] Gate empty-state Create Encounter button by can_create_encounter permission

## Description

## Problem

The empty-state "Create Encounter" button in `EncounterHistory.tsx` rendered unconditionally. The other 3 encounter creation entry points check `can_create_encounter` before render:
- Patient home page
- Appointment "Start Consultation"
- Appointment "Create Planned Encounter"

## Fix

Gate the button on `canCreateEncounter`, read from the **facility** permissions through `useCurrentFacilitySilently()`.

The patient response is the wrong source. `PatientPermissionsMixin` in the backend returns only `PATIENT` and `FACILITY` context permissions, but `can_create_encounter` has the `ENCOUNTER` context. The facility response carries it, which is why the other entry points use `facility.permissions`.

## Test

Added `tests/facility/patient/patientDetails/encounters/encounterHistoryPermission.spec.ts`. It uses real data and real roles, with no request stubs:
- Creates a patient with no encounter through the API, so the empty state renders.
- Gives `care-nurse` and `care-staff` a role on the geo organization of the patient, so both can view the patient.
- The Nurse role has `can_create_encounter`. The Staff role does not. Both roles have `can_list_patients`, so both see the encounters tab.

Also added the `care-staff` storage state (`tests/setup/staff.setup.ts`) and documented it in `tests/PLAYWRIGHT_GUIDE.md` and `CLAUDE.md`.

Verified against the local care backend:
- With the fix: both tests pass.
- With the fix reverted: the "hides the button" test fails.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

## Summary by CodeRabbit

* **Bug Fixes**
  * The Create Encounter action is now shown only to users with permission to create encounters.
  * Users can continue viewing encounter history according to their existing patient-access permissions.
  * Staff without encounter-creation permission no longer see the creation action in the empty encounter-history state.

* **Tests**
  * Added coverage to verify encounter-creation visibility for different permission levels.

* **Documentation**
  * Added guidance for local development, testing, authentication, and verification workflows.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5878887e115`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.