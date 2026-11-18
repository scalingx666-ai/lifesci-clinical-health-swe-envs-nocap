# Issue

**Title:** fix(server): reject dental, institutional and pharmacy claims in Claim $export

## Description

`$export` rendered every claim as a CMS-1500. For an `oral` claim that drops the tooth and surface (`item.bodySite` / `item.subSite`) and still returns 200, so nothing tells the caller the form is wrong. `institutional` and `pharmacy` claims have the same problem, they go on the UB-04 and NCPDP.

Those three types now get a 400 that names the form the claim needs. Claims with no type, or `professional` / `vision`, export as before.

The check is `getCms1500ClaimTypeError` in `cms1500pdf.ts`. It only looks at codings from the HL7 claim-type system, so a local code that happens to be `oral` isn't rejected.

Tests:
- unit tests for the helper in `cms1500pdf.test.ts` (allowed types, each rejected type, other code systems, coding order)
- endpoint tests in `claimexport.test.ts` for POST with all three types and GET with a stored oral claim. These fail on main.

Also added the new 400 to the `$export` docs page.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `17543f635d70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.