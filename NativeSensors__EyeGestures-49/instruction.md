# Issue

**Title:** ensure multi_face_landmarks exists

## Description

Should fix #48? In addition for formatting, it adds the check `if face_mesh.multi_face_landmarks:` on line 118, which ensures that the face is a valid face to process before processing. Please ensure that it maintains all original functionality.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3347ec0bc774`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.