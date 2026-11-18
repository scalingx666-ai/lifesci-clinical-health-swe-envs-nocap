# Issue

**Title:** Add table based transitions to Java Graphviz rendering.

## Description

This PR adds the ability to render table based transitions to the `./gradlew graphviz` task.

The labeling follows the same standard as the Module Builder.

Example rendering:
<img width="736" alt="image" src="https://user-images.githubusercontent.com/1054765/159060507-c99ae7ad-25c7-4ac6-91a6-e444fd549b40.png">

This PR does not address the preexisting overflow/word-wrap issue displayed in the example above.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63421913bbba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.