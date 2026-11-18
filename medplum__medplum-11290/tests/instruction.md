# Issue

**Title:** fix(core): validate cron strings with the scheduler's own rules

## Description

## Summary

- Adds an `isValidCron()` FHIRPath function (Medplum extension) backed by a new `isValidCronString()` export in `@medplum/core`.
- `isValidCronString` is a dependency-free port of the parse-time validation in [cron-parser](https://github.com/harrisiirak/cron-parser) 5.10.2, the parser BullMQ schedules with. Only the validation path is ported, so core does not pick up cron-parser's luxon dependency (bundle +~4 KB minified vs. +~104 KB for the library itself). MIT notice is included in the file, following `core/src/patch/`.
- Two deliberate restrictions relative to cron-parser (`cron-validator` rejected both too, so no schedule that worked before stops working):
  - **Minute granularity:** the optional sixth (seconds) field and `@secondly` are rejected.
  - **No hashed (`H`) terms:** `H`, `H(a-b)`, and `H/n` stagger jobs that share a schedule. Staggering stays a scheduler implementation detail, which keeps the syntax `Cron` and `Bot` authors must learn small. cron-parser also draws them at random, so their validity could change between parses. Dropping them also removes the backtracking regexes Sonar flagged.
- Anything accepted is valid BullMQ `pattern` input, verified against BullMQ 6.4.0's `upsertJobScheduler` / `defaultRepeatStrategy`. Beyond cron-parser's parse checks, this rejects expressions where BullMQ would throw or silently schedule nothing:
  - the empty string (BullMQ throws on a missing pattern);
  - days of month that occur in none of the months, e.g. `0 0 31 4,6 *` (`next()` gives up and BullMQ swallows it);
  - the 5th weekday of February alone, e.g. `0 0 * 2 1#5` (recurs up to 40 years apart, past `next()`'s 10,000-step limit, so the scheduler is dropped after its first run).
- New constraints: `cron-4` on `Cron.cronString` (`isValidCron()`) and `bot-1` on `Bot.cron[x]` (`ofType(string).all(isValidCron())`).
- Server switches from `cron-validator` to the shared helper and drops the dependency. The write-time `Cron` check stays so projects with `strictMode` off still reject bad schedules.

## Behavior changes

`cron-validator` disagreed with BullMQ in both directions:

| Expression | cron-validator | BullMQ / now |
|---|---|---|
| `@daily`, `0 0 * * MON-FRI`, `0 0 L * *`, `0 0 * * 5#2` | rejected | accepted |
| `0 0 31 2 *` (Feb 31) | accepted | rejected |
| `30 * * * * *`, `@secondly` (seconds) | rejected | rejected (BullMQ would accept) |
| `H * * * *`, `0 H(0-5) * * *` (hashed) | rejected | rejected (BullMQ would accept) |

In strict-mode projects, a `Bot` with an invalid `cronString` is now rejected on write (previously it was saved and silently never scheduled). Existing Bots with invalid values will fail validation on their next update.

- Docs: new "Cron expression syntax" section in `bots/bot-cron-job.md`, with a note on the differences from cron-parser (seconds and hashed terms).

## Testing

- `cron.test.ts`: accept/reject table, each case cross-checked against cron-parser; 100% statement and branch coverage.
- Fuzzed 400k generated expressions against cron-parser: 0 disagreements (six-field expressions expected to be rejected), and ~270k expressions containing `H`: all rejected.
- BullMQ compatibility: every accepted expression from ~180k fuzzed + exhaustive rare-day schedules gets a next run from BullMQ's `defaultRepeatStrategy` across 6 start dates in UTC, America/Los_Angeles, Pacific/Chatham, and Asia/Kathmandu (0 failures); rare-day schedules also from twice-yearly starts through 2210. A real queue on local Redis schedules every accepted sample, including all nine shorthands.
- Known upstream issue, not addressed here: under `TZ=Australia/Lord_Howe` (the only 30-minute DST zone), cron-parser's `next()` fails for some schedules around its DST transitions. Medplum passes no `tz`, so this only affects servers running in that zone.
- Core fhirpath/typeschema tests, server `workers/cron.test.ts`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `13cc88b20520`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.