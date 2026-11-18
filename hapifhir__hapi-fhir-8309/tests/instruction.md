# Issue

**Title:** Adding additional SQL statement to tag query that loads tags up front

## Description

Context:
1. Resolve the matching TAG_ID(s) from HFJ_TAG_DEF (by type/system/code) before building the resource search.
2. In the resource search, filter HFJ_RES_TAG.TAG_ID IN (...) directly and drop the HFJ_TAG_DEF join.

NOTE: Applies uniformly to _tag, _security, and _profile (they share the code path, differing only by TAG_TYPE).

-- Step 1: resolve tag_id(s)
SELECT tag_id
FROM hfj_tag_def
WHERE tag_system = 'http://hapifhir.io/fhir/NamingSystem/mdm-record-status'
  AND tag_code   = 'GOLDEN_RECORD'
  AND tag_type   = 0;

-- Step 2: inject as literal
SELECT t1.PARTITION_ID, t1.RES_ID
FROM hfj_resource t1
  INNER JOIN hfj_spidx_token t0 ON t1.RES_ID = t0.RES_ID
  INNER JOIN hfj_res_tag     t2 ON t1.RES_ID = t2.RES_ID
WHERE t0.PARTITION_ID = 1
  AND t0.HASH_SYS_AND_VALUE = -8958345584868966345
  AND t2.PARTITION_ID = 1
  AND t2.TAG_ID IN (...from Step 1...)
FETCH FIRST 10000 ROWS ONLY;{code}

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e4aa0103171`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.