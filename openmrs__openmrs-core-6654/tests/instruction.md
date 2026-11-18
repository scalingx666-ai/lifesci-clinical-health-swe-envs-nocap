# Issue

**Title:** TRUNK-6819: Start the JobRunr job server only once OpenMRS has started

## Description

## Description of what I changed

Running the webapp with `mvn jetty:run` and modules installed logged job failures during startup, because the JobRunr background job server started while its application context was still being created:

- `IllegalStateException: EntityManagerFactory is closed`: a job ran during the context refresh that follows module startup, against the closed session factory of the context being replaced.
- `TaskException: Task class org.openmrs.module.stockmanagement.api.jobs.AsyncTasksBatchJob not found`: a module's job ran right after the first, core-only refresh, before modules were loaded.

The server is now created with `startBackgroundJobServer = false` and driven by a new `JobRunrServerLifecycle` (a `SmartLifecycle`). It starts once its context has finished refreshing and stops before the context closes. The webapp `Listener` defers that start until `SchedulerService.onStartup()`, which both startup paths call once modules have started. Contexts refreshed after startup, for example when a module is installed, start their server straight away, and contexts that never go through the webapp (tests) start it on refresh as before.

The webapp never closes its application context, so that lifecycle stop does not run when OpenMRS shuts down. `Context.shutdown()` therefore calls `SchedulerService.onShutdown()` first, as it did before the move to JobRunr, and `JobRunrSchedulerService` stops the server there, before the modules and the session factory are shut down.

## Verification

- `jetty:run` with 31 modules: the server's first heartbeat comes after the module refresh, and an overdue recurring job runs once and succeeds. Without this change the same startup logs the failures above.
- `jetty:run` with 31 modules, redeploying the webapp to run `contextDestroyed()`: the server stops before the modules and the session factory are shut down. Without the shutdown change it keeps running, and its next heartbeat fails with `No suitable driver found` once the webapp has deregistered the JDBC drivers.
- `mvn test -pl api,web`: api 5523 tests, web 199 tests, 0 failures. `SchedulerServiceIT` passes 22/22.
- New `JobRunrServerLifecycleTest` covers the deferral, `JobRunrSchedulerServiceTest` covers `onStartup()` starting a deferred server and `onShutdown()` stopping it, and `ContextTest` covers the scheduler shutting down before the database.

## Issue I worked on

see https://openmrs.atlassian.net/browse/TRUNK-6819

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01NK4kFG8qyevx9Bk9jWoEgS
https://claude.ai/code/session_01PdDdZrB8Q5eMgej5FmRx4R

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b9993c839cf8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.