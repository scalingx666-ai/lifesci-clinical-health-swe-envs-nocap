# Issue

**Title:** [Scheduling] Share a service facility input that lists sites by name

## Description

Service facility pickers in the scheduling workspace and its config pages each configured a ResourceInput, whose default row shows a ResourceAvatar and the resource id. Neither helps tell sites apart.

Add a shared ServiceFacilityInput whose rows show only the site's name, and use it in CalendarFilters, AppointmentProposalForm and the actor page's service facility field. The service facilities multi-select reuses its row, which checks the facilities already chosen.

<img width="1459" height="1023" alt="Scheduling Workspace with the Service Facility filter open" src="https://github.com/user-attachments/assets/26cc18b3-9d90-41f6-a4f3-2a3799f53997" />

<img width="1459" height="1023" alt="Scheduling Config Workspace with service facility multi-select open" src="https://github.com/user-attachments/assets/44fd7bfb-b3d1-40c2-8a2e-7b5b36a280cd" />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc5a6bc90b07`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.