# Issue

**Title:** [BUG] Orbit camera instead of rotating objects in 3D view

## Description

Sorry this took so long to have a decent enough start to commit @LorenzE! I think I have the lay of the land and can work on a solution. I'm trying to implement it like here https://doc.qt.io/qt-5/qt3d-simple-cpp-example.html (I tried first with `QCamera::panAboutViewCenter` but I guess you can't animate functions only properties?). It's still crashing but I was going to work on it for another hour or so and then maybe ask for help if it's still breaking.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c87ddd88f092`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.