# Issue

**Title:** ENG-1247: use recursive summarization to avoid blowing up context window

## Description

### Dependencies

None

### Description

Do more advanced chunking / recursive chunking to avoid exceeding context window and also cleans up some of the code into commands

This PR resolves the [context window exceeded issue](https://metriport.slack.com/archives/C04T256DQPQ/p1760460533205409?thread_ts=1760009152.297669&cid=C04T256DQPQ) 

### Testing

- Local
  - [x] resource summary generates successfully
- Staging
  - [x] resource summary generates successfully
- Production
  - [ ] resource summary generates successfully

### Metrics

Logs metrics around token usage

### Release Plan

- [ ] Merge this

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `112fee360f2e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.