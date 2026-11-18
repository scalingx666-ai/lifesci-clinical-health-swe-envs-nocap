# Issue

**Title:** Add ability to use JWT tokens for auth

## Description

Used to obtain an access token for a backend service accessing an Epic endpoint: 
https://fhir.epic.com/Documentation?docId=oauth2&section=BackendOAuth2Guide

Tested locally by authorizing against Epic's Sandbox to fetch data: 
```
settings = {
    'app_id': APP_ID,
    'api_base': 'https://fhir.epic.com/interconnect-fhir-oauth/api/FHIR/R4/',
    'scope': 'system/Observation.read system/Patient.read',
    'jwt_token': jwt_token
}

smart = client.FHIRClient(settings=settings)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cf7bab29f330`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.