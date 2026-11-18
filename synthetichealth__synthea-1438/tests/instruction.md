# Issue

**Title:** Module Metrics

## Description

This branch revamps the module, state, and transition metrics.

Previously, use of the `generate.track_detailed_transition_metrics` property outputted metrics to system out. Using this feature roughly quadrupled the runtime.

This change outputs the metrics as JSON (`./output/metrics/**`), one file per module. Using this feature will roughly double the runtime.

Sample output looks something like this for each state, where the name of the state (e.g., `Chance_of_Stroke` matches a state name in the corresponding GMF module):

```json
  "Chance_of_Stroke": {
    "entered": 58987,
    "duration": 152635104000000,
    "population": 101,
    "current": 100,
    "destinations": {
      "Stroke": 1,
      "Chance_of_Stroke": 58886
    }
  }
```

Field | Description
-----|-----
`entered` | Count, how many times this state was entered.
`duration` | Sum of time (milliseconds) spent in this state.
`population` | Count, how many unique individuals entered this state (this count is not reliable for submodules).
`current` | Count, how many individuals are currently in this state at simulation end.
`destinations` | Map of states and counts that processing transitioned to.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `94ca67dcab48`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.