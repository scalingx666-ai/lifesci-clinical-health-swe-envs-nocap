# Issue

**Title:** Add new mappings to fix data issues

## Description

Part of ENG-000

### Dependencies

- Upstream: 

### Description
Fix data issues for Bamboo by adding new mappings.

### Testing
- Local
  - [x] Test new mappings - [link](https://www.typescriptlang.org/play/?#code/GYVwdgxgLglg9mABAZwA4BsZQIIBNcBOApssgBSZhECMA-AFwpQExgDmANIpUQEwNMW7AJSIA3gChEiCAmRREqAIYEoyRAF5urGrQB0aTFDIAiADpQTo2rUQBtALoBuKTLkLlq6psUq1dgAYHRBtEExMXaVkweV9VXh9Pf2pg0J4E0PDIxGIoEAIkMTioai4khIBfFwqJCVBIWARBGFQABRUiMCgACxISMmAYAnkAOSUAWyJGeSE2UUlpXPykQeGoMcm9YgwlCCIyAHozZAAqMzI7AD1hBzPhA84wq2ra+uh4JAheiABrMlgoOgps12FwAO7dJRQAAq3RgyFaBDgADcSNNmKxHrs8kp0IxwD8wHAwWAuEQAB6oIjQIi4fFgQnEsDzVzRWLKUi0nzYkC4zQaLQUqk03DZNkKeRQkDqLQc5Bc2wmdqc3CIQCg5CZEIwTAAxJQwIGqwAy5BFWXI4EC9Og4GwyAADaEkWDsRAAEjEAKBFUY7ohUNh8MRKJIFUQgCTCN1iSV5ZAVO3CbIwYCIMgAQjltJZ0ii5st1ttdukQupUFpPrEACkAMoAeRGBgx7CTAE8yMWRcI4wnXDmYhaiFabfbpDzcYxpO7q3WG7MW2RR+hO-HsjUahIDgd+QLtzvdwLEI75DK9yedxIFm4YgoiklSsVKj5DFg8IQSOQTNReABmRAAWX1SBVlAFjYKgCgACwAEImFwJgAKpgFgiAABrPKy3x-D2iAAORPgoABGzaIFASj4Smt7CNhHBYdh0SrOM6hgkQKAYEhTTmBYmpKGAqokT8zE9MxQLABKMC4MxrBQHAxTUFRWG3tR2ZhJ+P7-qwiBASYrjdlEGFkDReGIIRxGkeRfi8JRinZrRCD0eogk5DAbDdKJ4mIHAyYORxliIGwcAkIgknSeUKZOUSsyIEo+DEKQAAyOgWXJSnlFZ0gmKBEHQdpLzrpuFmIHq6DoPhuw-MR0lRa+cUJSmRIHtgkGKDFnRQMI55mle4gyWU5mIKGWh4S+MXvgArAEASIO0BBldgqIwWEVYgFgzGfmhunUphSkmMAuLFaV5WRdFb7xVQCRkBRMFYSYdFDAxiAQp0xG9MQgXqHV2FmBYVEya9T3MS1QzMZVw0nTQl3JX4pRXWNE1TTNc3ZehG36VtO1FSVvwHcDx01ed5nCOD2bXbZt2Mb0SCCS98KIO9n1QN9IWyJM6jAEi4yHVVyCg7whPSClV2LctiCrYja4bogX6iCM0nQg1kU8TTFVHdVp3hogRDjGBREzJi7W9rEN6Qz18R9Y+rE4Mr77eJBSJRWCSjNvN4DiYMVC4DpMh6VddUkWRABkiscyDuMXalYQ3QQd23kwBroOrACOvLoOo2Mq2DYcKVd1u27g9uO4j62-CjRM+6ZAd1anXMh-jvPhyTkfqCF+HUnAzPy+rmtQNrjZsPd5OBx9X3y6qFeW9ztf81tWnSN2YubuBogAEoa8GTAgMAyasMgYnMZ4LW9PKLNs4gqyjBMRB65esQQEC3FcgNGJtB0XQH-0JgVnA3RIGQH9f2AzYEw9l8ZGV1iDjFXnvF+fR1DRFLF0WuNkwB2RPkMM+kxECQhTv-HomJtD8TCCmQAZAQExyCvVEuAkrZhvkQO+uAw7v0-mAaeiBZ61AvOKGQt83aPkflNfe0DTDYHGI7IBXsto6lQQoMA597pYG6IHSBglt7qDAQBdQ4AvjcTYLSWu4Qw7UNofQoR+cZ45TZP2QctoTCABQCRAAARBAzFrFoSAA)
- Staging
  - [x] Upload a roster and make sure it has the new fields
- Production
  - [ ] Upload a roster and see what Bamboo says


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Roster export now includes three new fields to improve address-line parsing (split address components) and first-name normalization (removes nicknames), enhancing roster generation and downstream display/processing.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0500574f8154`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.