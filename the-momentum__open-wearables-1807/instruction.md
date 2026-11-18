# Issue

**Title:** feat(backend): add endpoints to read and set a user's personal record

## Description

## What does this change?

Adds `GET` and `PUT /api/v1/users/{user_id}/personal-record`, so an API client can read and set a user's birth date, gender and sex.

## Why?

Nothing could write `personal_record`, so every user had an empty one and the code reading it always fell back: the activity summary used a 190 bpm maximum heart rate instead of 220 - age, and the body summary returned `age: null`.

- A sub-resource rather than new fields on `PATCH /users/{user_id}`: that endpoint changes only the fields sent, while this one replaces the whole record (a field left out becomes null). Keeping them apart leaves the user endpoints as they are.
- `GET` for a user without a record returns 200 with nulls, not 404. An empty profile is a normal state; 404 stays for an unknown user.
- `PUT` is a single `INSERT ... ON CONFLICT (user_id) DO UPDATE`, so two first writes at the same time cannot collide on the unique `user_id`.
- `sex` stays a boolean column, so there is no migration. Nothing had defined what `true` meant; it is now `true` = male, `false` = female, `null` = unknown, written next to the column and in the data model docs. The API shows it as `male` / `female`.
- The future-date check raises `PydanticCustomError` rather than `ValueError`, because with `ValueError` the validation handler repeats the message in the 400 detail.

Closes: #1796

## How did you test this?

New schema, repository, service and API tests

Requests against the app in the test setup

| Request | Response |
|---|---|
| `GET` | `200 {"birth_date": null, "gender": null, "user_id": "<id>", "sex": null}` |
| `PUT {"birth_date": "1990-05-01", "gender": "female", "sex": "male"}` | `200`, same values back, stored `sex` is `true` |
| `PUT {"birth_date": "1991-01-01"}` | `200`, `gender` and `sex` now `null` |
| `PUT {"birth_date": "2999-01-01"}` | `400 {"detail": "birth_date cannot be in the future"}` |

## AI usage

Claude Code for the design discussion, tests and review.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added endpoints to retrieve and update a user’s personal record, including birth date, gender, and sex.
  * Updates replace the full record, clearing omitted fields. Future birth dates and unsupported gender or sex values are rejected.
* **Documentation**
  * Added the personal-record endpoints to the API reference and documented how sex values are represented.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b54b40bc96f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.