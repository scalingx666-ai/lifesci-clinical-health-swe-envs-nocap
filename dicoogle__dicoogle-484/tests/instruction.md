# Issue

**Title:** Form event handler for 'plugin-load'

## Description

Handles `plugin-load` in `pluginForm.jsx` to resend `result-selection-ready` event and data.

## Description
Certain web plugins would get the `result-selection-ready` event from the webapp before initializing their listeners/handlers.

This PR adds a handler for the `plugin-load` event that plugins automatically emit, to send back a `result-selection-ready` event (with the data from `ResultsSelected.get()`).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ec06522cc722`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.