# Issue

**Title:** [ENH] Use explicit copy elision in plugin::clone()

## Description

Hi, 

Some weeks ago I proposed this changed in another unrelated pr. Here is now a specific one for discussing this change. 

Going through mne_analyze plugin docs, I saw the code snippet for [the clone method](https://mne-cpp.github.io/pages/development/analyze_plugin.html). I think that this is OK, however it is improvable, due to the fact that: 

 - Since it is a part of the code that is actually described in the documentation we should have special care. 
 - The code is not wrong, but I don't think it is correct either. I haven't seen the asm but I'm quite certain that the compiler will get that code referred to the clone method and disregard it's implementation. 
 - The change I propose makes explicit what the reader should know and understand as part of the c++ standard because it is there and it is great. What we see in the code is an x-value, which will probably not be implemented at all in the compiled code.
 - Even if we want to go with other options, like using create static method from the QSharedPointer class, I still don't think that is 100% correct. What the code describes is to create a local variable, then copy it as a smart shared pointer and let it get deleted by running out of scope. Supposedly the counter in the smart pointer will be decreased, but that is not what the standard says and that is not what will happen.
 
So these are the reasons for the change. What do you guys think?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b00fbba5696e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.