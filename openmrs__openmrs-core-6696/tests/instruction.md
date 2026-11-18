# Issue

**Title:** TRUNK-6834: Write JAVA_OPTS and CATALINA_OPTS into setenv.sh quoted

## Description

## Description of what I changed

`startup.sh` wrote `JAVA_OPTS` and `CATALINA_OPTS` into Tomcat's `setenv.sh` inside double quotes. `catalina.sh` (Tomcat 9 and 11) sources `setenv.sh` and then starts Java with `eval exec ... "$JAVA_OPTS" "$CATALINA_OPTS"`, so every option was interpreted by the shell twice: `$` was expanded, a `"` broke `setenv.sh`, `&` backgrounded Java, and quoting in `OMRS_JAVA_SERVER_OPTS` couldn't protect anything.

The values are now written single-quoted, so the `eval` is the only interpretation, as Tomcat documents for `JAVA_OPTS`. A value with special characters can be quoted in the variable, e.g. `-Dkey='a$b&c'`. Single quotes rather than `printf %q`, because `catalina.sh` runs under `/bin/sh` (dash), which can't read the `$'...'` form bash produces for some values.

**Behaviour change:** plain options and `$CATALINA_HOME`-style references work as before. Only a value escaped twice to work around the old behaviour (e.g. `\"a b\"` for a space) now reaches Java differently.

## Testing

Ran the new `setenv.sh`-writing code under `bash -aeu`, then a stand-in for `catalina.sh` under dash that sources `setenv.sh` and runs Tomcat's `eval exec` line, printing the arguments Java would get:

| `OMRS_JAVA_SERVER_OPTS` | Before | After |
|---|---|---|
| `-Dtest.value='a$HOMEb'` | `a` | `a$HOMEb` |
| `-Dtest.quote='x"y'` | `setenv.sh` syntax error | `x"y` |
| `-Dtest.space="a b"` | `a` | `a b` |
| `-Dtest.sq="it's"` | — | `it's` |
| `-Dtest.home=$CATALINA_HOME/x` | expanded | expanded |
| the default options | unchanged | unchanged |

I have not built the image or run real Tomcat. Cherry-picks cleanly onto 2.9.x and 2.8.x.

## Issue I worked on

see https://issues.openmrs.org/browse/TRUNK-6834

## Checklist: I completed these to help reviewers :)

- [x] My IDE is configured to follow the [**code style**](https://wiki.openmrs.org/display/docs/Java+Conventions) of this project. (Shell script only)
- [ ] I have **added tests** to cover my changes. (No test harness exists for `startup.sh`; tested manually as above)
- [ ] I ran `./mvnw clean package` right before creating this pull request and added all formatting changes to my commit. (No Java changes)
- [ ] All new and existing **tests passed**.
- [x] My pull request is **based on the latest changes** of the master branch.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `afdfd1a5e745`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.