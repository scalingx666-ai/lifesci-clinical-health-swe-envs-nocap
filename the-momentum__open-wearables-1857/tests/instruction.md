# Issue

**Title:** docs: warn that seed data doesn't reflect real data volumes

## Description

## What does this change?

Adds a warning on the Seed Data settings page and in the [Seed Data Generator](https://openwearables.io/docs/developer-portal/settings/seed-data-generator) docs that seeded data doesn't match real device volumes or sampling frequency.

## Why?

We got a question on Discord about whether the seed generator gives you typical Apple Health quantities. It doesn't, the generator was built for testing the UI and API, not for estimating data size. We never mentioned that anywhere, and the docs actually called it "realistic data", so I changed that to "test data" too.

## How did you test this?

Checked both pages locally (dashboard + `mint dev`):

<img width="2880" height="2000" alt="seed-data-warning-docs" src="https://github.com/user-attachments/assets/1ade3b30-7226-4ba8-9fdc-83da0aade447" />

<img width="2880" height="2000" alt="seed-data-warning" src="https://github.com/user-attachments/assets/8fe538d5-bfe8-4573-9ee8-5b4c7f57343b" />



## AI usage

Claude Code (Claude Opus 5.5), helped with the wording and took the screenshots.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

## Summary by CodeRabbit

* **Documentation**
  * Clarified that generated seed data is for testing and does not represent real device volumes or sampling frequency.
  * Added a warning not to use seed data to estimate real-user data generation.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8fdab1c5911d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.