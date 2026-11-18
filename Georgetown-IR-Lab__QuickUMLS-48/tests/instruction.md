# Issue

**Title:** Add option to disable lowercase conversion of all uppercase words.

## Description

Hi @soldni thanks for maintaining this tool. I made a small change for my local installation, and thought it would perhaps be useful for others as well.

I ran into an issue when all characters of a medical term were in uppercase. By default, QuickUMLS would convert this term to lowercase. This would then make it difficult to distinguish between the normal word, and the original term in uppercase. For example, the acronym `MAP` for microtubule-associated proteins would be converted to `map`. I added an argument to disable this conversion, resulting in that `MAP` can be more easily identified as microtubule-associated proteins and is not confused with the word `map`.

The added functionality would only work when the database is installed without the `-L` option.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e7011615b96f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.