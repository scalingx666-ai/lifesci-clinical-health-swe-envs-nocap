# Issue

**Title:** WIP [ENH,MAINT] More build options

## Description

Add the following options to the build project script:

- [qt=<path>] - lets user specify a path to the desired qt installation to use to build the project.
- [all] - build all project components (libraries, applications, tests, examples)

Change cmake build flags to positive statements rather than double negatives (instead of setting DO_NOT_BUILD_X to OFF we now set BUILD_X to ON)
- Add some group build options for only building realtime or offline apps. (saves a bit of time if you need to rebuild from scratch)
- Turn off examples and tests by default - not too sure about this behavior, but it would save some time when developing. Maybe as an option instead? Thoughts?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0bfd48e609a4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.