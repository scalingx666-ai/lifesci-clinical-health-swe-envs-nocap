# Issue

**Title:** Generate API docs site during build

## Description

Part of #2232.

Enabled by #2463, this generates the Kotlin API docs on https://google.github.io/android-fhir/ during the CI build. (They were "static" before, and just deployed from what was in the `docs/` directory, with this, they are "built". This is the 1st step towards generating more documentation during the build in a future next step.)

Originally raised as #2483, but that PR for some strange reason didn't update even though I (force) pushed new commit.

@williamito or @santosh-pingle or @MJ1998 or @jingtang10  OK for you?

~Includes #2463, but just for testing; when this works, I'll merge that, and then rebase this to not include that anymore.~

~I'm marking this one as draft as I'm still testing this - please do not merge as long as it's in Draft.~

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9519473fb802`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.