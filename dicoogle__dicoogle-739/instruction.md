# Issue

**Title:** DICOM storage: save sending and receiving AE titles in FMI of stored objects

## Description

This will fill in the standard file meta information group attributes relative to the sending and receiving application entities, so that some level of provenance can be inferred from it.

This can be disabled by setting the server setting `storage.save-ae-titles` to false.

Since dcm4che2 does not recognize these attributes, we also needed to include them in the Dicoogle index `TagsStruct`.

#### Pending questions

- I added _Sending Application Entity Title_ and _Receiving Application Entity Title_. Should I also add _Sending Presentation Address_ and _Receiving Presentation Address_? https://dicom.nema.org/medical/dicom/current/output/chtml/part10/chapter_7.html#sect_7.1.1.1 
   - We have decided not to include it for now.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `83f3b8fd03bc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.