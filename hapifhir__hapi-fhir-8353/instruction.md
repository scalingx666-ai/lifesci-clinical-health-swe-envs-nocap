# Issue

**Title:** 8270 partition conditional url placeholder

## Description

#### Problem Description                                                                                                                                                                              
In Patient ID partition mode, a transaction entry whose conditional URL (an                                                                                                 
If-None-Exist value or a conditional update URL) referenced another entry's                                                                                                 
placeholder fullUrl was rejected with HAPI-0539. The same bundle succeeds                                                                                                   
outside partition mode. 

#### What was done
- The partition interceptor's after-prefetch hook now stamps minted Patient ids                                                                                             
  as server-assigned ids (`RESOURCE_ID_SERVER_ASSIGNED_VALUE`) instead of                                                                                                   
  rewriting POST entries to PUTs, so the transaction write loop's native entry                                                                                              
  ordering, conditional-URL id substitution, duplicate consolidation, and                                                                                                   
  operation outcomes all apply unchanged.                                                                                                                                   
- The hook also resolves placeholders inside conditional URLs up front, covering                                                                                            
  referenced Patients that process in the PUT phase (conditional update /                                                                                                   
  update-as-create), which no write ordering can fix.                                                                                                                       
- Transaction pre-fetch now canonicalizes type-less If-None-Exist values (the                                                                                               
  bare form shown by the FHIR spec, and the leading-`?` form) via a shared                                                                                                  
  `massageForStorage`, giving them the same behaviour and query cost as the                                                                                                 
  type-qualified form (previously ~10x the SELECTs and, in partition mode,                                                                                                  
  HAPI-2279/HAPI-2006 failures).                                                                                                                                            
- Pre-fetch records match-URL-cache hits into the TransactionDetails, so                                                                                                    
  repeated conditional creates no longer fail in partition mode when                                                                                                        
  `matchUrlCacheEnabled` is on.                                                                                                                                             
- Added corresponding tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d098b2e9a58`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.