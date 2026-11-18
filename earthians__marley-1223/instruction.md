# Issue

**Title:** fix: appointment creation from referral service request

## Description

Issue description:

  When a Patient Appointment is created from a Service Request generated through the “Refer Patient” flow, the mapper
  was copying same-named fields from Service Request to Patient Appointment.

  This caused two issues:

  - Service Request source is a Select field with values like Direct, but Patient Appointment source is a Link to UTM
    Source.

  - Because Direct was copied into the appointment Link field, saving the appointment failed with: Could not find
    Source: Direct.

  - The appointment practitioner was mapped from referred_to_practitioner, but the display name needed to be aligned
    with that target practitioner during mapping.

  Fix applied:

  - Added source to field_no_map in make_appointment, so Service Request source is not copied into Patient Appointment
    source.

  - Updated set_missing_values to fetch both department and practitioner_name from the referred practitioner.
  - Added a deterministic unit test covering appointment creation from a Service Request with source = "Direct".

  Flow after change:

  1. Patient Encounter creates a referral Service Request.
  2. Service Request keeps its own source, for example Direct.
  3. User clicks Create Appointment from the Service Request.
  4. Mapper creates Patient Appointment.
  5. referred_to_practitioner maps to appointment practitioner.
  6. Appointment department and practitioner_name are fetched from that referred practitioner.
  7. Service Request source is not copied to Patient Appointment.
  8. Appointment saves without Could not find Source: Direct.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6e5711c3830d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.