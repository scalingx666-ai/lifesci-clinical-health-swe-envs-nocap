# Issue

**Title:** fix claim/provider/org serialization

## Description

Fixes two issues with serialization that are the root cause of #1594.  Claim costs were not serialized which was causing the cost value to be 0 when read from file, which causes more than half of the claim transactions to not be output into the csv since they only get generated when cost (remainder) is greater than 0.

Providers/Organizations were also not appearing in the csv files due to having their utilization numbers set to 0 when exporting.  The read/write serialization functions on the Provider class specifically handle the utilization table to ensure the values carry over, but the object thats created after reading from the snapshot file is not put into the provider map.  An identical copy, created fresh on the init of the generator, would get put in instead with utilization values at 0.  This PR merges the object loaded from file into the provider map, so that the utilization numbers carry over correctly.

It would be possible to create a setting to make this behavior optional if the provider csv is intended to only include providers that have had an encounter during the current simulation/time period.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bfbf02bca2eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.