# Issue

**Title:** catalog: split activity distance the way LOINC does (running/swimming/walking/exercise)

## Description

## The case that exposed it

PHIA asks: *"What is the total distance I walked in the last 21 days?"* — published answer **0**. The agent answered **20,991.8 m**, and it was not hallucinating: that is a real reading in the record.

The user's exercise table has eleven rows:

| activity | rows | distance |
|---|---:|---:|
| Treadmill | 1 | **20,991.8 m** |
| Run | 2 | **12,195.1 m** |
| Outdoor Bike | 7 | 0 |
| Aerobic Workout | 1 | 0 |
| **Walking** | **0** | **0** |

No walking at all. So why did a treadmill run end up answering a walking question? Because the catalogue gave it nowhere else to go.

## What LOINC says

LOINC names these separately, and only one of the six was in the catalogue:

| LOINC | component | catalogue before |
|---|---|---|
| 93818-3 | Cycling distance | `CYCLING_DISTANCE` |
| **93817-5** | **Running distance** | — |
| **93816-7** | **Swimming distance** | — |
| **41953-1** | **Walking distance** | — |
| **55412-1** | **Exercise distance** | — |
| 112427-0 | Distance walking **or running** | `DISTANCE` — display "Distance" |

`DISTANCE` carried the *walking-or-running* code under the generic name "Distance". Anything a source labelled "distance" without an activity could only land there, and once it did, "how far did I walk" and "how far did I run" read the same series.

The comment in the row already said `Walking or exercise distance` — the intent was generic, the code was not.

## The change

Four catalogue rows, nothing else:

```
RUNNING_DISTANCE   93817-5   Running Distance
SWIMMING_DISTANCE  93816-7   Swimming Distance
WALKING_DISTANCE   41953-1   Walking Distance
EXERCISE_DISTANCE  55412-1   Exercise Distance
```

All four codes are already in the shipped axis table and resolve by name (`resolve("Running distance") == 93817-5`), so this is catalogue data — no bundle rebuild, no resolver change.

`DISTANCE` itself stays as it was: it is a real indicator, used by device sources that report distance without an activity, and changing what an existing indicator means would rewrite stored series. The new rows give converters somewhere correct to file an activity they *do* know.

## What it fixes and what it does not

Fixed: a converter that knows the activity (Apple workout type, PHIA `activityName`, Garmin/Fitbit activity logs) can now file treadmill distance as running and walking as walking, so activity-specific questions stop reading one shared series.

Not fixed: PHIA's converter still does not carry `activityName` at all, so the evaluation corpus continues to collapse the eleven rows into one series. That is the next change, and this PR is its prerequisite — there was no correct target code to file a run into until now.

## Verification

- **947 passed**, 114 skipped, 12 xfailed
- `ruff check mirobody` → clean
- The four new rows load and expose `loinc` 93817-5 / 93816-7 / 41953-1 / 55412-1

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e9cd9aeef59d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.