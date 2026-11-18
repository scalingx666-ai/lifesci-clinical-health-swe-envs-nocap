# Issue

**Title:** Fix connection pool settings and log them on startup

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:** #6201

**Description:**

Part of #6201. Besides running out of memory, the transaction report problem left behind database connections that the database had already closed. The pool kept handing those connections to requests, and the requests failed. This PR changes the connection pool settings so that doesn't happen, and logs the settings the pool actually uses.

#### Connection pool (`application.yml`)

- **`maxAge: 10 * 60000` → `600000`.** Pool settings are bound as they're written, without being evaluated. A value that can't be converted is **silently ignored**, so the pool used its default of `0` (never recycle by age). With a literal, connections are closed and replaced after 10 minutes. **This is a behavior change:** the 10-minute limit was clearly intended, but it has never actually been in effect, so every installation has been keeping connections open indefinitely until now.
- **`testOnBorrow: false` → `true`.** A connection is validated with `SELECT 1` when a request borrows it, at most once per `validationInterval` (15s). A connection the database has dropped is discarded instead of being given to the request. The cost is one quick query per connection at most every 15 seconds.

These are defaults in `application.yml`, so they apply to every implementation unless overridden in an external config.

#### Startup logging (`BootStrap.groovy`)

On startup, the app logs the settings the pool is actually using (with the password masked), for example:

```
Data source pool: initialSize=..., maxActive=..., maxAge=600000, testOnBorrow=true, ...
```

Because bad values are silently ignored, the configuration files alone don't tell you what the pool is doing. This log line does.

#### Local heap options (`build.gradle`)

`bootRun` only, no effect on deployments:

- `-PbootRunMinHeap` / `-PbootRunMaxHeap` set the heap size (defaults unchanged: 1g / 4g).
- `-PheapDumpOnOom` writes a heap dump to `build/heapdumps` on an `OutOfMemoryError`.

These were used to reproduce #6201 with a production-sized heap, e.g. `./gradlew bootRun -PbootRunMaxHeap=1800m -PheapDumpOnOom`.

#### How to test

1. Start the app and check the log for the `Data source pool:` line. It should show `maxAge=600000` and `testOnBorrow=true`.
2. If an implementation overrides these settings in an external config, check that the log shows the override.
3. Optional: kill the app's connections in the database (e.g. `KILL <id>` for the app's connections in `SHOW PROCESSLIST`), then load a page. It should load without a connection error.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01RqDhKQyrN4ZX1iZUg4RvAm

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a19378538056`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.