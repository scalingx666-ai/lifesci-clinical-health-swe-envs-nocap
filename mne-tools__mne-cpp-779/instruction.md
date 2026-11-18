# Issue

**Title:** [ENH] EventManager sintactic sugar

## Description

Hi, 
I wanted the functionality in the singleton EventManager to be accessible through static fcns. Right now it is set to the typical getInstance() method which then allows to retrieve public access to the class. Through this change (sugar) the api is directly accessible and it looks more natural to consume the class's API. 

+ bonus: In Communicator, there is a range for that was detaching from the Qt structure unnecessarily. Apparently, by making it const, c++ will iterate through references. Warnings-- (✊🏻)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d47697ca0a75`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.