# Issue

**Title:** Update toml dependencies

## Description

#### Reference issue (if any)

 

#### What does this implement/fix?

We removed unused dependencies and decided to keep upper bounds only for the bayesian stat libraries that has caused breaking issues before. For the rest of the dependencies we are not adding upper bounds because:
- Upper bounds restrict users (eg if we cap numpy but the user needs a newer numpy for *another package in the same venv* then they can't work with this other package)
- The stable scientific-Python core (numpy, scipy, pandas, etc.) has long deprecation windows and rarely breaks on a major bump.
- It is better to be reactive (eg weekly CI against the latest dependencies, then cap only when a real break appears) instead of defensive (eg force upper bounds to all deps)
- Older releases of pcntoolkit may break when new versions of its dependencies are released, but we assume most users install the *latest pcntoolkit release*

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea81c1e0c1dd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.