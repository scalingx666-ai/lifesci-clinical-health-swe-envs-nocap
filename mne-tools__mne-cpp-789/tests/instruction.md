# Issue

**Title:** [ENH] MNE_Scan splashscreen

## Description

I make MNE Scan's splash screen hide 1 second after the main application's gui has finished its setup. During that second the splash screen can be hidden just by clicking on it, and since the splashscreen's management is offloaded to a new thread, even with the splash screen on top, the main GUI is still responsive. 

I think it gives a much sense of well tuned application. Since it is pretty much the first interaction with the user, i think it has some importance. 

More info... Some prs back, MNE Scan splash screen used to not be taken off by the application after it started. It would simply remain underneath the main gui window. I fixed that by making mne_scan's splash screen to hide the moment the initialization of the main screen had finished. Right before the main application loop started. This was not good enouth, and since then, I planned on finding time to implement the behavior shown in this pr.

thanks.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ea70801cb025`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.