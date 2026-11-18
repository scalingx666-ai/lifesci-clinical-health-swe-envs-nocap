# Issue

**Title:** Reduce chances of duplicate uuids in large populations

## Description

Addresses the duplicate UUID issue from #1545 

Our UUID generation uses the seeded random number generator to ensure reproduceability, and picks 2 randLong()s to pass into the UUID constructor. For small populations this works ok but in larger populations we wind up with UUID collisions within the same resource type.

I believe what's happening when we get duplicate UUIDs is we're seeing two separate patients (two separate RNGs with separate seeds) where their RNGs have lined up in terms of state and where they are in that sequence, and so they produce the same 2 long values in a row, resulting in the same UUID. In small populations the range of numbers is so large that collisions are unlikely, but when we get up to say 1,000,000 patients, we start to see a small handful of collisions. By replacing the first randLong with the seed, we eliminate the possibility of duplicate UUIDs happening between different patients. It does mean there is maybe a higher possibility of duplicate UUIDs for the same patient seed, but that should be a lot more rare. I.e., the number of random calls for a single patient tends to be many orders of magnitude lower than the number of possible random values from a Random.

To test this I ran 2 populations of 1,000,000 records, 1 before and 1 after, and checked the IDs in the encounters file with this command to show duplicates:
`cut -d',' -f1 output/csv/encounters.csv | sort | uniq -d`
There should be some IDs printed in the before, but none in the after. (My test instance had 6 duplicates.) Note this doesn't even consider dups across different resource types.
I'm still trying to think of a way to formally prove this is better with a test case, so I'm open to suggestions on that front.

Note the change to the random class produces a different sequence of random values so one hardcoded value in a test case had to change as well.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bbdc5c689c2a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.