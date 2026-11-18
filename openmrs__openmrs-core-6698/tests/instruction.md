# Issue

**Title:** TRUNK-6839: Stop startup if anything is mounted into the folders rebuilt from the distribution

## Description

## Description of what I changed

Since TRUNK-6508, `startup-init.sh` removes and recreates the data directory's `modules/`, `owa/`, `configuration/` and `frontend/` on every start, then copies the distribution in. When one of these is a bind mount, `rm -fR` deletes the host's files first and then fails on the mount point itself ("Resource busy"), so startup stops under `set -e`. A file mounted into one of them (e.g. a single `.omod` in `modules/`) also stops startup.

Startup now checks `/proc/self/mountinfo` before deleting anything. If one of these folders is, or contains, a mount point, it stops with an error that names the matching `/openmrs/distribution` folder to mount into instead, e.g.:

```
Error: /openmrs/data/modules is, or contains, a mount point. It is rebuilt from /openmrs/distribution/openmrs_modules on every start, so mount into /openmrs/distribution/openmrs_modules instead.
```

**Rationale:** these folders are output, rebuilt from the distribution on every start, so anything mounted into them would either be deleted or would conflict with that. Rather than special-casing mounts (skipping folders, deleting around mount points, handling read-only targets), the script refuses them and points at the place that already supports it: `/openmrs/distribution` is copied in on every start, so files mounted there work as expected. Everything else is unchanged.

**Behaviour change:** a setup that mounts into one of these folders now fails at startup with the message above, instead of losing the host's files (or, on releases without TRUNK-6508, silently mixing them with the distribution's).

Not changed:
- Files placed by hand in these folders on a `/openmrs/data` volume (as the O3 configuration docs currently describe) are still removed on restart. The docs will be updated to point at `/openmrs/distribution`, as described on TRUNK-6839.
- `OMRS_HOME` containing a space already makes `startup-init.sh` fail at the server properties redirect, on master too. That's separate.

Raised in review of #6695, which will include this when it's backported to 2.8.x.

## Testing

Ran the whole `startup-init.sh` under `bash -aeu` in containers (bash 4.2, bash 5.3 with busybox awk, Debian with mawk), with stale files in each folder and a module and config in the distribution:

| Mounts | Result |
|---|---|
| none | folders cleared, only the distribution's files remain |
| host folder bind-mounted on `modules/` | stops with the error; nothing deleted, host files kept |
| single `.omod` mounted into `modules/` | stops with the error; nothing deleted |
| `configuration/addresshierarchy/` mounted | stops with the error; nothing deleted |
| `configuration/` mounted read-only | stops with the error |
| whole `/openmrs/data` as one volume | folders cleared as before |
| sibling mount on `data/modules2` | `modules/` cleared as before |
| single `.omod` mounted into `/openmrs/distribution/openmrs_modules/` | copied into `modules/` with the distribution's |
| `/proc/self/mountinfo` unreadable | stops before deleting anything |

No new variables or functions are left in the environment Tomcat inherits. I have not built the image.

## Issue I worked on

see https://issues.openmrs.org/browse/TRUNK-6839

## Checklist: I completed these to help reviewers :)

- [x] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project. (Shell script only)
- [ ] I have **added tests** to cover my changes. (No test harness exists for `startup-init.sh`; tested manually as above)
- [ ] I ran `./mvnw clean package` right before creating this pull request and added all formatting changes to my commit. (No Java changes)
- [ ] All new and existing **tests passed**.
- [x] My pull request is **based on the latest changes** of the master branch.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `453679a52fce`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.