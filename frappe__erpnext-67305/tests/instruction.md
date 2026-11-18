# Issue

**Title:** fix(manufacturing): drop upstream loss from a job card's loss instead of refusing submit (backport #66990)

## Description

After #62583, a later Job Card is refused on submit when its completed qty plus process loss is more than the previous operation completed, and the error asks to reduce For Quantity. Once material is transferred against the Job Card, the form locks For Quantity, so the only way out was to cancel the transfer.

When the previous operation is done and the excess is not more than the card's process loss, that part is the loss the previous operation already booked. Submit now takes it off the card's process loss and For Quantity (the change the error asked for) instead of refusing. The error stays when the completed qty alone is more than the previous operation completed.

`test_job_card_input_limited_to_previous_operation_output` changes: the second card (For Quantity 100, previous operation completed 95) used to complete 95 and be refused, then was resubmitted by hand with For Quantity 95 and completed 90 (loss 5). It now completes 90 (loss 10 on save) and submits with For Quantity 95 and loss 5.

Uncertain: For Quantity of the later card is lowered on submit without asking, the same value the old error message asked for.

### Steps to reproduce
1. BOM with Transfer Material Against = Job Card, two sequential operations Op1 and Op2, one raw material per operation. Work Order for 10.
2. On both Job Cards, make and submit the Material Transfer for the full qty.
3. Job Card of Op1: complete 9 and submit (process loss 1).
4. Job Card of Op2: complete 9 and submit.
   - Before: "Completed Qty and Process Loss of operation Op2 add up to 10 ... Reduce Qty To Manufacture to 9", and the field is read-only.
   - After: it submits with Qty To Manufacture 9 and no process loss. Manufacture for 10 gives 9 FG with a process loss of 1.

<hr>This is an automatic backport of pull request #66990 done by [Mergify](https://mergify.com).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `542d37769711`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.