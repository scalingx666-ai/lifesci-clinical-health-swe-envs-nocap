# Issue

**Title:** Added ViewModelBase that implements INotifyPropertyChanged

## Description

Added methods to avoid backing fields in the get/set

---
Name: Refactoring
---
I created a base class for all the view models in order to centralize the OnPropertyChange calls
Plus I have added some methods that lets you write accessor without backing fields (it hits performance but for this application I guess you may accept it)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `005d393a725d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.