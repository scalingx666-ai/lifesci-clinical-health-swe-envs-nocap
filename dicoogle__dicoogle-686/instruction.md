# Issue

**Title:** [core] Add kill switch for dead plugin sets

## Description

This implements a safety measure against misconfigured or malfunctioning plugins. If the JVM property `dicoogle.deadPluginKillSwitch` is set to `true` (case insensitive), any dead plugin will kill the Dicoogle process, thus requiring devops to investigate and fix the issues reported in the logs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2fa3510b17e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.