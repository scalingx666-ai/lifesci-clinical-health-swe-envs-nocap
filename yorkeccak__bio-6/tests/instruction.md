# Issue

**Title:** Add pharma and healthcare data sources

## Description

## Summary

- Add 5 new specialized search tools for pharma/healthcare data sources:
  - **ChEMBL** - Bioactive compounds, drug-like molecules, bioactivity data
  - **DrugBank** - Drug mechanisms, targets, pharmacology, interactions
  - **Open Targets** - Drug target validation, disease associations, genetic evidence
  - **NPI Registry** - US healthcare provider directory with specialties
  - **WHO ICD** - ICD-10/ICD-11 disease classification codes

- Add code snippets and documentation for each new source in the data source showcase

## Test plan

- [ ] Verify each new search tool returns results when queried
- [ ] Test compound search with ChEMBL for kinase inhibitors
- [ ] Test drug database search with DrugBank for drug interactions
- [ ] Test target search with Open Targets for disease associations
- [ ] Test provider search with NPI registry
- [ ] Test ICD code search for diagnosis codes

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8a03a5179736`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.