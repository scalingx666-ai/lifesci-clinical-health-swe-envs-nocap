# Issue

**Title:** feat(cdk): add loadBalancerSslPolicy config for ALB HTTPS listeners

## Description

Lets deployments choose the ELB security policy for the API and mTLS HTTPS listeners, e.g. a post-quantum or FIPS policy. Defaults to RECOMMENDED_TLS (ELBSecurityPolicy-TLS13-1-2-2021-06), so existing stacks are unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4e75ed351f7b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.