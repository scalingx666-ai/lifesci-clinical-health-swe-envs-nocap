# Issue

**Title:** Fix issue with setting config via CLI

## Description

This addresses an issue where certain config settings, ie `exporter.years_of_history` don't work when set via the command line args.
I think we've seen a few times and have put fixes on various branches:  , 

This is still a bandage though and we'll probably run into this again, but it should work as a quick fix. The longer andmore permanent fix would be to keep separate variables for the things the cli args can set, and only instantiate the 2 Options objects after all args have been parsed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8008933711db`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.