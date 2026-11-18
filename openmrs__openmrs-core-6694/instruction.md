# Issue

**Title:** TRUNK-6836: ProgramValidator evicts the program being saved, so saving a program from the session fails on Hibernate 7

## Description

## Description of what I changed

`ProgramValidator.validate` evicted the program it found by name whenever that program had the same uuid. When the program being saved is already in the session, `getProgramByName` returns that same instance. The validator runs from `RequiredDataAdvice` before the DAO, so it evicted the very program being saved, with its workflows. `HibernateUtil.saveOrUpdate` then merged a detached graph. On Hibernate 7, that merge either inserts a workflow flushed earlier a second time (a duplicate uuid in `program_workflow`) or throws an NPE in `StatefulPersistenceContext.replaceCollection`.

The eviction is removed. `HibernateUtil.saveOrUpdate` merges a detached program, so a loaded copy in the session no longer gets in the way.

Two new tests in `ProgramWorkflowServiceTest` fail on master and pass with this change. `saveProgram_shouldAddAWorkflowToAProgramWhoseNewWorkflowWasAlreadyFlushed` fails with the duplicate-uuid insert. `saveProgram_shouldUpdateProgramCreatedEarlierInTheSameSession`, moved here from #6639, saves a new program a second time before anything is flushed and fails with the NPE. `saveProgram_shouldUpdateDetachedProgram` still passes.

This also fixes the two failing loader tests in the Initializer module's Platform 3.0 upgrade (mekomsolutions/openmrs-module-initializer#338): `ProgramWorkflowsLoaderIntegrationTest` and `ProgramWorkflowStatesLoaderIntegrationTest`. Against a core built from this branch, Initializer's suite passes, with 220 tests and 0 failures.

## Issue I worked on

see https://issues.openmrs.org/browse/TRUNK-6836

## Checklist: I completed these to help reviewers :)

- [x] My IDE is configured to follow the **code style** of this project. (`spotless:apply` run)
- [x] I have **added tests** to cover my changes.
- [ ] I ran `./mvnw clean package` right before creating this pull request and added all formatting changes to my commit. I ran the Program, ProgramWorkflow, PatientProgram and validator test classes (780 tests, 0 failures), not the full build.
- [x] All new and existing **tests passed** in the classes above.
- [x] My pull request is **based on the latest changes** of the master branch.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `afdfd1a5e745`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.