# Issue

**Title:** Pipeline v3：dynamic facial detection

## Description

Pipeline v3：①**Add dynamic facial detection part**. When preprocessing original data, it will use intermediate frames for every “detecetion_length” frames to do facial detection. You can change the setting in yamls:  DYNAMIC_DETECTION(True or False)  DYNAMIC_LENGTH（setting interval length） 		

②fix a bug about FACE_DETECT paramater . I find out that in last version, in _Baseloader.py_ function _resize_ : if face_detection=False, then  face_region = frames[0]. It's not reasonable, because face_region should be a vector with the size of [1,4]. The correcet one should be [0, 0, frames[0].shape[0], frames[0].shape[1]].

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21f290316e8e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.