# Issue

**Title:** Leave listed codes the CodeSystem doesn't have out of expansions without full-text indexing

## Description

With full-text indexing off, expandWithoutHibernateSearch added every code an include listed, so pre-expanded ValueSets stored codes the CodeSystem doesn't have, and $validate-code and :in searches treated them as members. Listed codes are now looked up in the code system version first, as the full-text path already does.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a61f73e2683e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.