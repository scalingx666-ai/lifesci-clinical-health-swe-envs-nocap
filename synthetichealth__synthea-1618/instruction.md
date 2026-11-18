# Issue

**Title:** Limit resources per CSV file

## Description

This branch allows users to limit the number of resources per CSV file.

```
> ./run_synthea -p 250 --exporter.csv.export=true --exporter.csv.max_lines_per_file=100 --exporter.csv.file_number_digits=4
...
> ls output/csv
...
claims_transactions-1269.csv claims_transactions-2552.csv encounters-0049.csv          observations-0904.csv        observations-2187.csv        supplies-0100.csv
claims_transactions-1270.csv claims_transactions-2553.csv encounters-0050.csv          observations-0905.csv        observations-2188.csv
```

`exporter.csv.max_lines_per_file` is the limit for the number of resources per file (there will be one additional line for the header). The filenames will be `basename-###.csv`, with the number padded to the number of digits specified in `exporter.csv.file_number_digits`. In append mode, resources will be added to the last file before creating a new file.

Addresses #1367.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9363a4520d89`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.