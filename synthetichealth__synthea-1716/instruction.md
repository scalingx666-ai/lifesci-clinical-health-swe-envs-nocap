# Issue

**Title:** Report a clear error when the requested state is not in the demographics

## Description

## Problem

When the state on the command line is not in the demographics file (a typo, or `xxx`), `Location` loads an empty set of demographics without complaint, and the run fails later in an unrelated place. On current `master`:

```
$ java -jar build/libs/synthea-with-dependencies.jar -p 1 xxx
Exception in thread "main" java.lang.RuntimeException: Poverty Eligibility File 'payers/eligibility_input_files/medicaid_income_eligibilities.csv' does not contain state 'xxx'.
	at org.mitre.synthea.world.agents.behaviors.planeligibility.PovertyMultiplierFileEligibility.buildPovertyMultiplierEligibility(PovertyMultiplierFileEligibility.java:92)
	...
	at org.mitre.synthea.engine.Generator.<init>(Generator.java:265)
	at App.main(App.java:284)
```

`Location` already checks the city the same way (`The city X was not found in the demographics file for state Y.`), but not the state.

## Solution

`Location(String state, String city)` now throws `The state X was not found in the demographics file.` when the demographics have no rows for the state, before the city check. It goes through the same `catch` as the city check, so the error surfaces the same way.

With the fix, the same command stops at the first thing that is wrong:

```
$ java -jar build/libs/synthea-with-dependencies.jar -p 1 xxx
ERROR: unable to load demographics
java.lang.Exception: The state xxx was not found in the demographics file.
	at org.mitre.synthea.world.geography.Location.<init>(Location.java:88)
	at org.mitre.synthea.engine.Generator.init(Generator.java:285)
	...
Caused by: java.lang.Exception: The state xxx was not found in the demographics file.
```

## Tests

`LocationTest.testStateThatDoesNotExist` builds a `Location` for a state that does not exist and checks the message.

- On `master` it fails: `AssertionError: Expected an error for a state missing from the demographics file` (no error is raised).
- With the fix it passes, and so does the rest of `LocationTest` (20 tests).
- The full `./gradlew test` suite passes locally (JDK 21), and checkstyle reports no warnings on the changed files.

---

_This PR was written by Claude Code (AI assistant) on behalf of @namespaceMarcello, who directs this work._

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d9d07a6eef91`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.