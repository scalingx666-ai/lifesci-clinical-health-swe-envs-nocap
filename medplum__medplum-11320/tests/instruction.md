# Issue

**Title:** Remove admin acesspolicy reconciliation

## Description

Removes `reconcileDefaultAccessPolicy`. Changing a membership's `admin` flag no longer changes its access policy. The policy Medplum enforces is always the one stored on the membership.

## Changes

- `getAccessPolicyForLogin` builds the policy from the membership as stored. It no longer swaps the Practitioner and Admin defaults in memory on each request.
- `POST /admin/projects/:projectId/members/:membershipId` saves the membership as sent.
- Docs: "Switching a user to (or from) admin" now says to set `accessPolicy` yourself when promoting or demoting.

## Behavior change

Introduced in #9724 (v5.1.25). Existing memberships whose `admin` flag doesn't match their default policy will see their access change. This happens when `admin` was changed through a FHIR `PUT`, which is how the app saves edits.

- `admin: true` with the Practitioner default: loses write access to the Practitioner read-only types (MedicationKnowledge, PlanDefinition, ActivityDefinition, ObservationDefinition, ValueSet, StructureDefinition, CodeSystem).
- `admin: false` with the Admin default: gains write access to those types. Project admin resource types are still blocked.

No migration. To keep a user's current access, their `accessPolicy` must be explicitly edited.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `30a026170081`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.