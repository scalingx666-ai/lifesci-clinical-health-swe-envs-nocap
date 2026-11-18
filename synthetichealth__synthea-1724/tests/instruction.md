# Issue

**Title:** Skip lab panels already recorded in the same encounter

## Description

Part of #1552 (the same-code part of it).

## Problem

When a submodule joins an encounter and records the same lab panel the host module also records, Synthea emits the panel twice at the same instant. Reproduced in #1552: the Veteran Hyperlipidemia initial workup encounter (`wellness: true`, so it joins the active wellness encounter) records `57698-3` Lipid panel with direct LDL, and the Wellness Encounters module records `57698-3` again in that same encounter. Downstream systems reject duplicate panels, so the import fails.

Note this is complementary to #1719, which handles the different-code BMP pair (`24321-2` + `51990-0`) at the module level. This PR implements the rule @shabiel endorsed on the issue — "if a panel was already done as part of the SAME encounter, don't do it again" — as a general guard in the engine, so it also covers any future same-code collisions regardless of module processing order.

## Solution

`State.DiagnosticReport.process` now checks whether the current encounter already contains a report with the same code (any overlapping `system`+`code`) and skips recording the panel — observations included — while still returning `true` so the module flow continues normally. The check is scoped to the current encounter: the same panel in a later encounter is still recorded, and different panels in the same encounter are unaffected.

## Tests

New `StateTest.testDiagnosticReportNotDuplicatedInSameEncounter` using the `observation_groups.json` fixture:

- records a metabolic panel once -> 1 report
- records the same panel again in the same encounter -> still 1 report, no extra observations (fails on pristine master: `expected:<1> but was:<2>`)
- records a different panel in the same encounter -> 2 reports
- records the same panel in a later encounter -> recorded again

Sandbox note: Gradle/Maven Central are unreachable from my environment, so I verified by compiling the patched `State.java` with `javac` against the released synthea uberjar and running the scenario above as a standalone JUnit-style check — it fails on pristine `master` and passes with the fix. Please let CI run the full suite.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9d07a6eef91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.