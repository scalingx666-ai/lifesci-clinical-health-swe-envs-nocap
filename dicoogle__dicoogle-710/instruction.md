# Issue

**Title:** Extend Move SCP response and abort DcmSend associations on C-STORE I/O errors mid transfer

## Description

This PR addresses two major concerns in the C-MOVE operation with Dicoogle:

### Indefinite hanging

an edge case where a remote transfer association can hang indefinitely due to errors in the storage provider, such as corrupted storage data. Getting an `IOException` while invoking `cstore` would result in the local store SCU proceeding to wait for a response from the SCP, even though it had not sent the final PData, resulting in both peers waiting for each other.

The approach adopted here was to abort the association as soon as an `IOException` happens.

### Opaque C-MOVE response

Moreover, this PR includes an extension to the C-MOVE SCP so that it also returns more accurate information about how the C-MOVE operation went, so that the C-MOVE SCU can more reliably understand what happened.

- Command Status reflects the success (or lack thereof) of the underlying C-STORE operations
- Command data set may also provide Number of Completed Suboperations, Number of Remaining Suboperations, and Number of Failed Suboperations).
- On error, Status will have an error code in `Cxxx`, as mandated by the standard. Error ID and Error Comment may also be provided.
- If at least one of the suboperations fails, the status code will be `B000`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a64b3770965`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.