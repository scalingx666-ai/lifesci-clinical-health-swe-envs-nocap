# Issue

**Title:** fix: apply treatment plan filters

## Description

Issue: 
<img width="1852" height="903" alt="treamentplanfixedimage" src="https://github.com/user-attachments/assets/e0fb91ed-ac8c-4e40-af94-2e8143681670" />

In patient encounter the treament plan on click button , it show a list of all templates without filtering based on the patient age , diagnosis , gender 

the bug: Inside the js function the call back function missing a paramereter due to that its not catching the server filtered data 

callback: function (r) now captures the server response instead of discarding it, and pulls applicable_plans (the names of templates the backend already filtered by age/gender/diagnosis) out of r.message.
Added a get_query() on the MultiSelectDialog restricting it to name in [...applicable_plans], on top of the existing medical_department setter.
If nothing qualifies, shows a message instead of opening an unrestricted picker.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `021119a35a67`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.