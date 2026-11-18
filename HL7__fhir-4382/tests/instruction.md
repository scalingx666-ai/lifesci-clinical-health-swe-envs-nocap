# Issue

**Title:** J#58533, J#58551, J#58345 ResearchStudy element changes and ResearchSubject.status isModifierReason change

## Description

J#58533 ResearchStudy element changes

1. Removed ResearchStudy.name

2. Removed ResearchStudy.label

3. Modified ResearchStudy.title 0..1 string  Primary title for the study, used in listing for search results

4. Added ResearchStudy.officialTitle 0..1 string   Official or scientific title for the study, used when the scientific title does not match the primary title or when the primary title is declared to be an official or scientific title

5. Added ResearchStudy.layTitle 0..1 string    Title for the study expressed in plain language

6. Added ResearchStudy.acronym 0..1 string    Study acronym or abbreviation

7. Added ResearchStudy.shortTitle 0..1 string   Shorter title for the study

I also updated the example by changing the label to now be the new officialTitle element and removed name.
I also removed the ResearchStudy.name search parameter and added one for officialTitle instead.

J#58551 ResearchStudy.description and ResearchStudy.descriptionSummary definition changes

1. ResearchStudy.description definition removed "e.g., study abstract"
2. ResearchStudy.descriptionSummary definition added "e.g., study abstract"
3. ResearchStudy.descriptionSummary added comment: "Some systems use the brief description to be a plain language description for a general audience."

J#58345 changed isModifierReason for ResearchStudy.status and ResearchSubject.status

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `87d4a25c106c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.