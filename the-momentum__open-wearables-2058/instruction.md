# Issue

**Title:** feat: add Polar nightly recharge samples, save workout raw payloads

## Description

Polar workouts now map to specific workout types using Polar's official `detailed_sport_info` values. Most sport="OTHER" workouts used to end up as generic.

- Replaced the `(sport, detailed_sport_info)` tuple list in Polar workout type mappings with one `{detailed_sport_info: WorkoutType}` table. It covers all 175 values from the AccessLink docs appendix "Detailed sport info values in exercise entity".
- Lookup tries `detailed_sport_info` first, then sport. An unmapped OTHER still gives generic, and an unknown sport still gives other.
- Polar workout API responses are now stored as raw payloads (`api_response`), like Polar 24/7 data and other providers' workouts. Polar workouts were the one provider path that skipped this.
- Now UTC offset for sleep is correctly stored as well

_(Added during review by Sebastian Kalisz:)_

- Nightly Recharge now also stores Polar's per-sample HRV and breathing rate values (`hrv_samples`, `breathing_samples`), placed on the night's sleep start: the one fetched in the same sync, or a stored Polar night that has a `zone_offset`. Without a known sleep start only the nightly averages are stored, as before.
- Only nights processed by a sync after deploying get the samples. Polar's endpoints return the last 28 days, and stored nights from before this change have no `zone_offset`, so older nights keep the averages only; no backfill is planned.
- Each per-sample value carries the sleep start's `zone_offset`, so a sample after local midnight counts toward the right local day.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Improvements**
  * Polar workouts now recognize a broader range of activities and variants, including tennis, indoor climbing, strength training, and treadmill running.
  * Nightly recharge samples are aligned with sleep start times, including when samples cross midnight. Nightly averages remain available when sleep timing is unavailable.
  * Sleep records now reflect their local time zone.
* **Documentation**
  * Updated Polar workout coverage information to reflect the expanded activity mappings.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `27d68020f705`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.