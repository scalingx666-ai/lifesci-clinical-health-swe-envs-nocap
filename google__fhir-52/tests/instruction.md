# Issue

**Title:** Changes to ResourceCollection Internals

## Description

Changes to ResourceCollection Internals

- Change name of method from GetResource to Get
- Replace AddUriAtPath method with Put method
- Remove method CacheParsedResource
- On Put, store the JSON representation of the resource in memory. On
  Get, parse the previously stored representation into a proto. This
  replaces the previous behavior of GetResource which would perform
  I/O to retrieve the JSON representation of resource from the FHIR
  Package on disk.
- These changes match the behavior of the Java version of the
  package manager.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `03d780f05241`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.