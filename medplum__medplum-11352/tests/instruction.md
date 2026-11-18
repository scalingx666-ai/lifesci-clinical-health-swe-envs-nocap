# Issue

**Title:** (Docs) Add Advanced Questionnaire and Persistence Guides

## Description

Implementers currently need to read component code and tests to assemble calculated, conditional, multi-page questionnaires and a durable save/resume workflow. These guides connect those capabilities in one activity-log example, with the renderer's supported features and limitations stated explicitly.

## Changes

- Add **Advanced Questionnaire Authoring**: a runnable preview, calculated answers, expression-based conditions, page groups, repeating-item guidance, and an SDC compatibility table.
- Add **Saving and Resuming Questionnaire Responses**: publish a definition, create or reuse an assigned response, retain context, validate completion across pages, save with version checking, resume editing, and coordinate downstream processing.
- Explain how to revise definitions while keeping existing responses usable.
- Include five TypeScript/React example files directly in the docs, two Mermaid diagrams, numbered walkthroughs, and expandable longer examples.
- Link both guides from the questionnaire overview, modeling guide, and sidebar.

This change adds documentation and example code. It does not change the form renderer or claim full SDC support.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e6ea6a28f985`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.