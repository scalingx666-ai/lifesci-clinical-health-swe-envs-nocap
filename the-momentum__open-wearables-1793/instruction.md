# Issue

**Title:** fix: generate meals from presets and the seed form

## Description

## What does this change?

The seed form now knows about meals: there's a Meals section, and presets with meals actually generate them. Picking a preset highlights it again.

## Why?

#1692 added `generate_meals` and `meal_config` to the seed profile, but the form didn't have them. Comparing the form against a preset never matched, so no preset was ever shown as selected, and the request left meals out, so "Nutrition Focused" and "Comprehensive" seeded without them.

`MealConfig` also gets `date_range_months` like the other configs. The meal window was a fixed 6 months, so it ignored the window picked in the form.

## How did you test this?

Clicked through the presets on Settings → Seed Data: each one is highlighted after picking it, and editing a field switches to "Custom". Generated "Nutrition Focused" and checked that meals show up on the user's Meals tab.

Before:

https://github.com/user-attachments/assets/f0f82815-a2c2-4acb-aaf7-b837c2ec66df

After:

https://github.com/user-attachments/assets/93757912-59d3-4a3f-9d48-b5595f8e37f4

Added:

<img width="1135" height="698" alt="image" src="https://github.com/user-attachments/assets/1ad048b6-37fa-46b9-95d1-5ddef800b65a" />

## AI usage

Claude Code (Claude Opus) for finding the cause and writing the fix.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Added meal generation options, including an on/off toggle, meal count, and calorie range.
  * Meal generation can be selected on its own and is available for Apple Health connections.
  * Added a configurable meal date range of 1–24 months, defaulting to six months. Explicit start and end dates override the selected range.
  * Meal summaries now show the configured count and calorie range when meal generation is enabled.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `38f36d0cdfc9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.