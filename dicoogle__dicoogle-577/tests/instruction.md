# Issue

**Title:** Change DICOM logging and deprecate XML log

## Description

.

- Change implementation to send log line to slf4j logger
   - format is `"[{peer-aetitle}] {type} {additional-info} {params}"`, suggestions on a different structure are welcome
- Disable XML logging by default ("DICOM_Services_Log.xml")
   - can be enabled again with `-Ddicoogle.dicom.xmlLog=true`
- mark related constructs as deprecated, so we can remove them in Dicoogle 4
- tweak `LogLine` class
   - deprecate current constructor, advise users to discard `date`
   - currently still stores `date`, but will be gone in the future

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e3e0753fdd69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.