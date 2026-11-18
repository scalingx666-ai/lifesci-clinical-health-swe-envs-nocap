# Issue

**Title:** Fix changelog-location check for release branches

## Description

#### What was done

- Changed the logic for the `changelog-location` check in Github CI, it is now derived from the target branch name instead of the root pom version:

| Target | Expected dir |
|---|---|
| `rel_X_Y` | `X_Y_0`, from the branch name. |
| `master` | The highest `X_Y_0` dir that has a `version.yaml` (created by the version-bump PR), currently `9_2_0`. |


#### Testing

Ran the extracted step script locally against:

| Scenario | Result |
|---|---|
| #8535 head into `rel_9_0`, entry in `9_0_0/` | pass (failed on CI before) |
| master + `9_2_0/` entry | pass |
| master + `8_14_0/` entry | fail, expects `9_2_0/` |
| `rel_8_8` + `8_8_0/` entry | pass |
| `rel_8_8` + `8_8_3/` entry | fail, expects `8_8_0/` |
| `rel_8_8` at `8.8.2` + backport in `8_14_0/` | skipped (pom not `-SNAPSHOT`) |

Closes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f16434b93a39`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.