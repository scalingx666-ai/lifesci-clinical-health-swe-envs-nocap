# Issue

**Title:** fix(backend): convert Apple Health XML values to series units

## Description

Apple Health XML exports write each value in the user's display unit (km, lb, mmol/L, °F, kJ…), but the import stored the raw number under the series' fixed unit. As a result, glucose from mmol/L users, distance from metric users and body weight or temperature from imperial users were stored wrong. This adds a shared unit conversion layer and routes XML ingestion through it.

## Changes

- Add a shared unit conversion module covering length, mass, volume, energy, speed, temperature and blood glucose. It parses provider unit strings, including Apple's molar-mass glucose unit, and converts values to the unit each series is stored in.
- XML import now converts every record to its series unit using the record's `unit` attribute. Workout energy statistics are converted to kcal.
- ~~A value whose unit is missing, unknown or measures a different quantity is kept as-is and counted. Each import logs one summary warning, and the counts are also returned in the upload task result.~~
- _(Changed during review by Sebastian Kalisz:)_ A record in a unit that is unknown or measures a different quantity is skipped, under the skip reason `unconvertible_unit:<series>:<unit>`, instead of being stored in the wrong unit; workout energy in such a unit is left unset. A value without a unit is kept as it is.
- HealthKit's `%` values, 0-1 fractions, are scaled to the 0-100 that percent series hold.
- Series that hold temperature differences, and blood alcohol content, are excluded from conversion. A conversion formula would corrupt them.
- The SDK import now takes its glucose, hydration and calorie factors from the shared module. Its behavior is unchanged.

## Testing

Tested on a real Apple Health export: the ~1.1 GB sample from https://www.kaggle.com/competitions/kaggle-pog-series-s01e04/data. The conversion worked:

- 2,770,120 records and 1,387 workouts parsed, none skipped.
- The export uses US units, which are now converted to the series units. For example: `mi` to `m`
- Parse time is 60 s for the whole file, against 55 s with conversion disabled.

## Existing data

No backfill: the original unit is not stored, so already-imported values can't be converted reliably.

_(Added during review by Sebastian Kalisz:)_ Percentages are the exception: every `%` value the XML import stored is a fraction. A data migration, `scale_apple_xml_percentages`, scales the stored blood oxygen, body fat and walking percentages (double support, asymmetry, steadiness) of Apple Health XML sources to 0-100, for values of at most 1, in one statement through the per-source index, and queues their days for the rollup. A walking percentage under 1% imported by the fixed code before the migration has run would be scaled twice; that window is the deploy.

## Breaking change

_(Added during review by Sebastian Kalisz:)_ Apple Health XML imports store values in the series unit instead of the export's display unit, so a re-import of the same file gives different values (glucose in mg/dL instead of mmol/L, distance in meters instead of km or miles). Records in a unit that can't be converted are no longer stored and show up as skipped. Stored XML percentages move from 0-1 to 0-100; other stored XML values stay as they are, in whatever unit they were exported.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Health data imported from Apple Health XML and supported SDK sources now uses consistent units for measurements such as blood glucose, hydration, energy, and workout energy.
  * Percentage samples from Apple Health XML are correctly scaled, including previously imported values.
  * Records with unsupported units are skipped rather than reported with misleading values; unitless values remain unchanged.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `815c8a42cccb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.