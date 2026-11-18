# Issue

**Title:** Modified search result onChanged binds to be regular w/ event stop propagation.

## Description

Modifies `onChanged` behavior to resolve webmove plugin's current issue of receiving duplicate data.

## Description
Dicoogle has `handleSelect` methods for its search result views wherein these are bound to the `onChanged` event. What would happen is that these methods would be triggered when clicking the checkbox **and** immediately after in a rerendering of the page after the click, which would add duplicated entries in the data to be moved. 

This PR modifies the binds to be regular method usage, and includes the addition of a parameter for the event to run the `stopPropagation()` method, resolving the duplicated method call.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b4be3f1bc336`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.