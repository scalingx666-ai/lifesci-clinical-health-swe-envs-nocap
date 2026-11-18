# Issue

**Title:** Replace SimpleDateFormat with FastDateFormat in ExportHelper

## Description

ExportHelper originally used SimpleDateFormat, which is not thread-safe. Hence access to the static DATE_FORMAT and ISO_DATE_FORMAT had to be protected using `synchronized`, as noted in the original code.

This synchronized access is especially visible on higher end machines. For example on a VM with 48 vCPUs, a `jstack -l` output analysis showed almost 50% of the pool threads were waiting on the static `ISO_DATE_FORMAT` instance within ExportHelper. On such machines, CPU usage would be low and Synthea's throughput was not scaling well with higher number of vCPUs.

This change safely replaces those usage of SimpleDateFormat with FastDateFormat, which is thread-safe, thereby removing the need to synchronize access to those static instances across threads. The result of this is better scalability and improved usage of CPU, especially on higher-end compute.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6192ed703d85`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.