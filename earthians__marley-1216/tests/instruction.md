# Issue

**Title:** test: add regression tests for therapy session practitioner fallback (backport #1214)

## Description

## Summary
PR #1174 (already merged to `develop`) fixed `make_therapy_session()` so the practitioner is resolved from the source Service Request or Therapy Plan when not passed explicitly. It shipped without test coverage for that fallback - flagged by review on the version-16-hotfix backport (#1211).

This adds the missing coverage directly against `develop`.

## Changes
- `test_practitioner_from_service_request`: creates a Patient Encounter with a therapy line, submits it, and calls `make_therapy_session()` with only `service_request` set - asserts the practitioner comes from the Service
  Request.
- `test_practitioner_from_therapy_plan`: calls `make_therapy_session()` with only `therapy_plan` set (no matching Service Request) - asserts the practitioner comes from the Therapy Plan.
- `test_explicit_practitioner_takes_priority`: passes a practitioner explicitly, different from the plan's - asserts it wins over both fallbacks.<hr>This is an automatic backport of pull request #1214 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7f439f4491e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.