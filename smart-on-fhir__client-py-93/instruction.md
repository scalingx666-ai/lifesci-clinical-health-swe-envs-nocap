# Issue

**Title:** Use a full UUID4 for the state param

## Description

According to the [hl7 SMART App Launch Implementation Guide](http://www.hl7.org/fhir/smart-app-launch/#step-1-app-asks-for-authorization):

>The app SHALL use an unpredictable value for the state parameter with at least 122 bits of entropy

The current state param used by this client is only 8 characters and, according to [this](https://en.wikipedia.org/wiki/Password_strength#Entropy_as_a_measure_of_password_strength) entropy calculation, has only 41 bits of entropy.

The SMART App Launch Implementation Guide suggests using a "properly configured random uuid", which the [uuid wiki](https://en.wikipedia.org/wiki/Universally_unique_identifier#Version_4_(random)) indicates gives us the requisite 122 bits.

I'd like to have this in the 3.0 (STU3) version of the client, and also to merge it forward to master (R4).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `89b4afc2d9a8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.