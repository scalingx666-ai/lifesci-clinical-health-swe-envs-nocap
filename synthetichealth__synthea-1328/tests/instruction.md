# Issue

**Title:** Update BFD HHA Exporter

## Description

Update BFD HHA exporter to:

1. Add support for PPS codes
2. Improve HCPCS to revenue center mapping

Note that two new code files (`hha_pps_case_mix_codes.csv`, `hha_pps_pdgm_codes.csv`) and updated `hha_rev_centr_code_map.json` and `hcpcs_code_map.json` files are available in the usual places.

A comparison of real vs Synthea revenue center frequency is shown below.

Rev Center | Real % of Total | Synthea % of Total | Diff
-- | -- | -- | --
0551 | 39.3% | 25.7% | -13.59%
0421 | 24.2% | 23.0% | -1.23%
0023 | 9.4% | 14.0% | +4.55%
0001 | 7.3% | 8.5% | +1.26%
0431 | 6.8% | 7.6% | +0.78%
0571 | 5.8% | 5.8% | -0.04%
0550 | 2.3% | 2.2% | -0.11%
0420 | 1.5% | 1.4% | -0.11%
0441 | 1.4% | 3.0% | +1.60%
0561 | 0.5% | 5.9% | +5.33%
0570 | 0.5% | 0.2% | -0.28%
0430 | 0.3% | 0.1% | -0.21%
0572 | 0.2% | 1.1% | +0.91%
0424 | 0.1% | 0.1% | -0.03%
0440 | 0.1% | 0.2% | +0.12%
0559 | 0.0% | 0.0% | -0.00%
0560 | 0.0% | 0.6% | +0.54%
0623 | 0.0% | 0.0% | -0.03%
0270 | 0.0% | 0.0% | -0.03%
0552 | 0.0% | 0.0% | -0.00%
0434 | 0.0% | 0.0% | -0.01%
0444 | 0.0% | 0.0% | +0.01%
0429 | 0.0% | 0.0% | +0.00%
0989 | 0.0% | 0.0% | +0.00%
0422 | 0.0% | 0.0% | -0.00%
0583 | 0.0% | 0.0% | -0.00%
0579 | 0.0% | 0.6% | +0.56%
0432 | 0.0% | 0.0% | +0.01%
0410 | 0.0% | 0.0% | -0.00%
0590 | 0.0% | 0.0% | -0.00%
0581 | 0.0% | 0.0% | -0.00%
0580 | 0.0% | 0.0% | -0.00%
0582 | 0.0% | 0.0% | -0.00%
0272 | 0.0% | 0.0% | -0.00%
0449 | 0.0% | 0.0% | -0.00%
0439 | 0.0% | 0.0% | -0.00%
0271 | 0.0% | 0.0% | -0.00%
(blank) | 0.0% | 0.0% | -

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `15c84344eb44`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.