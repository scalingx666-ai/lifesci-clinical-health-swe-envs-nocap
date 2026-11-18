# Issue

**Title:** Resolve module enum classes in StringEnumType

## Description

.

`StringEnumType` now loads its enum through `OpenmrsClassLoader.getInstance()` rather than `Class.forName`, so module enums mapped with it resolve. This is the idiom `PersonAttribute`, `ModuleUtil` and `SchedulerFormValidator` already use. Core enums still resolve, because `OpenmrsClassLoader` delegates to core's loader.

The new `StringEnumTypeTest` covers three cases:
- A module enum: it compiles an enum into a temp dir that only a child loader can see, registers an `OpenmrsClassLoader` over that loader, and asserts the enum resolves. This test fails with the reported "Enum class not found" without the fix.
- A core enum (`Obs.Status`) still resolves.
- An unknown class still throws `HibernateException`.

The test puts back the shared `OpenmrsClassLoader` instance by reflection afterwards, so the swapped loader doesn't leak into later tests.

On a real server (core master, `mvn jetty:run`, MySQL 8), I ran the 22 O3 modules upgraded to 3.0 together with this change and #6631. All of them, including reporting and billing, which map their enums with `StringEnumType`, start, and UI login works.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Fp7T1pGYEMrMVp1M7AW9Fg

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34dc604e6eea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.