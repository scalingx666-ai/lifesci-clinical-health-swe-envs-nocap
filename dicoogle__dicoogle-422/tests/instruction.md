# Issue

**Title:** Fix/web api docs

## Description

Updates Swagger Web API definition:
Updated Swagger 2.0 to OpenAPI 3.0.0;
Added missing operationId field;
Added description and useful links.

This allows the update of the Dicoogle Web API webpage (https://bioinformatics-ua.github.io/dicoogle-api/webapi/) to a more readable menu:

![Screenshot 2020-05-19 at 20 17 48](https://user-images.githubusercontent.com/8323694/82368732-d199ee80-9a0d-11ea-8e5c-8666a32bc707.png)
![Screenshot 2020-05-19 at 20 18 51](https://user-images.githubusercontent.com/8323694/82368831-f68e6180-9a0d-11ea-94c1-53e98a2bd2d4.png)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1888b6d81efb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.