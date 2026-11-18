# Issue

**Title:** Fix intermittent changelog-location CI failure from a SIGPIPE race

## Description

## What is wrong

The `changelog-location` check fails intermittently on PRs, with:

```
sed: couldn't flush stdout: Broken pipe
##[error]Process completed with exit code 4.
```

It reads the project version like this, under `set -euo pipefail`:

```bash
pom_version=$(sed -n 's:.*<version>\(.*\)</version>.*:\1:p' pom.xml | head -1)
```

`head -1` exits after the first line and closes the read end of the pipe. `sed` is
still holding buffered output, and its final flush at exit hits `EPIPE` — so it
prints the broken-pipe message and exits 4. `pipefail` propagates that exit status
out of the pipeline and `set -e` turns it into a failed step. Whether `head` has
already closed the pipe by the time `sed` flushes is a scheduling race, which is
what makes it intermittent rather than reliably broken.

## Why it started now

The bug has been latent since the check was added in #8033. It only bites once
`sed`'s **total** output crosses the 4096-byte stdio buffer.

Below that, `sed` buffers everything and flushes once, at exit, while `head` is
still reading — no early close, no failure. Above it, `sed` pushes out a full block
early, `head` takes its one line and exits, and the trailing flush lands on a closed
pipe.

That output is currently **4104 bytes** on `master` — eight bytes past the boundary.
The root `pom.xml` simply grew enough `<version>` tags to cross it, and the check
started flaking for every PR.

## The fix

Remove the pipe. One `sed` that quits at the first match has nothing to race against:

```bash
pom_version=$(sed -n '/<version>.*<\/version>/{s:.*<version>\(.*\)</version>.*:\1:p;q;}' pom.xml)
```

Same value (`8.13.5-SNAPSHOT`), one process, and it no longer depends on how large
`pom.xml` happens to be.

## Verification

Running the job's actual `run:` block, extracted from the parsed workflow YAML,
against the current `pom.xml`:

| step script | failures |
|---|---|
| before | **31 / 100** |
| after | **0 / 100** |

The check's own behaviour is unchanged, confirmed on all three paths:

- no changelog entry added → `nothing to check`, exit 0
- entry in the correct directory (`8_14_0`) → exit 0
- entry in a wrong directory (`8_12_0`) → `::error`, exit 1

No changelog entry is included: this changes CI only, with no user-facing effect.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1901adf7ff0d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.