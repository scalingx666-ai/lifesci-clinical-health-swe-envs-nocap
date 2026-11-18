# Issue

**Title:** Bulk unindexing for IndexerInterface

## Description

This proposes an extension to the `IndexerInterface` so that API consumers can request multiple items to be unindexed at once. .

This extension to the API should be carefully reviewed and evaluated to ensure that implementers can use it properly and that it can be well integrated into existing workflows.

Breaking changes are minimal. It is only a problem if an existing plugin already has a method with the exact same signature, which is unlikely. Hence, we are in position to deliver this in 3.4.0, or postpone to version 4 anyway.

---

To ensure some level of quality in this suggestion, we should have:

- [x] at least one proof of concept plugin implementation
   - We could take this as an opportunity to move forward with hosting the open plugins on GitHub. 
- [x] at least one example that the Dicoogle core can consume this method in a usable way without downsides
   - I suggest an extension to the unindexing service so that it accepts multiple URIs

---

Problems resolved in the latest version:

- [x] No way to retrieve the task's unindexing progress from another thread. **Now has a second parameter as a progress callback.**
- [x] Even if the indexer periodically flushes some unindexing operations during the task, other routines cannot work with URIs which have already been unindexed before the task ends completely. This could pose an issue in file removal tasks, because it requires `unindex` to finish before we start cleaning up the files. **The operation is now asynchronous.**

---

Known caveats:
- ~~It is not clear whether we can properly constrain the number of parallel unindexing tasks by pushing this to our indexing task pool. The current indexing task manager depends on task objects returning a different kind of report, which `UnindexReport` does not implement. Maybe it should be subclassed from `Report`?~~ As of the latest version, unindexing tasks can be dispatched by the indexer thread pool.
- Having a second parameter to keep track of progress is quirky. One would naturally expect an `UnindexTask<T>` to extend `Task<T>`, but it is very different from indexing tasks and would make it even harder to attach to the task pool.
- The resulting object is too complex and granular. While there is a lot of power in being able to specify an error for each URI, it is not always the case that files will be unindexed independently, so it may be hard to build such results in batched unindexing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2fa3510b17e2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.