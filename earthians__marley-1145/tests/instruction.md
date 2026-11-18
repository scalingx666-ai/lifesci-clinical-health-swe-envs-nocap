# Issue

**Title:** fix(clinical-procedure): sync template consumables and consume stock on manual clinical procedure creation

## Description

Issue Description:-
When a Clinical Procedure is created from an Encounter or Service Request using a Clinical Procedure Template, the template’s consumables and consume_stock setting are populated correctly.

However, when a user creates a Clinical Procedure manually and selects the same template on the form, the consumables table is not populated and consume_stock is not synced from the template even if its exist. This creates inconsistent behavior across creation flows and can lead to missed stock consumption setup for manual procedures.

Fix Applied
Updated the manual Clinical Procedure form flow in clinical_procedure.js so that when procedure_template is selected:
        - consume_stock is fetched from the selected Clinical Procedure Template
        - warehouse defaulting is triggered when needed
        - template consumables are loaded into the items table
        - clearing the template resets consume_stock and clears items

Closes issue

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d737a93d8c87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.