# Issue

**Title:** [SchedulingWorkspace] Keep a picked time when the search moves to other days

## Description

Picking another day or stretch in the time search, a calendar click that moves the search, or "Search more options" no longer drops a time already picked.

For example, in the booking form:
- Choose a time, say Monday at 2pm.
- Reopen "Find a time" and pick other days in its calendar, as if checking what else you could offer the patient.

Before this change, the Monday 2pm pick was cleared as soon as you looked at another day, and you had to go back to Monday and pick it again.

Looking at other times shouldn't undo the one you've picked; picking a different time replaces it. Keeping it is safe: which days are on show doesn't change whether that time is free (and the scheduling operations will revalidate your selection on submission in any case).

Changing the visit type, the actors, the site or the repeat count still drops the pick, since it was found for those.

In the workspace, the picked visit stays drawn while other days are searched, including when a click on the calendar moves the highlight, and the search, to another day.

`useDaySearch` loses its `onResultsReplaced` option, which only served this.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0dde0a173577`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.