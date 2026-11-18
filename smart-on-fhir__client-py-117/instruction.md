# Issue

**Title:** Add authorize for system app

## Description

According to http://fhir.cerner.com/authorization/#requesting-authorization-on-behalf-of-a-system

In order to refresh `access_token` after `expires_in` runs out, you can follow this pattern together with this PR:

```
from fhirclient.client import FHIRClient

class FHIRService:

    def __init__(self, settings=settings):
        assert len(settings), 'Missing `fhir` settings'
        self.client = FHIRClient(settings=settings)

    @property
    def server(self):
        if not self.client.ready:
            self.client.prepare()
            self.client.authorize()
        return self.client.server
```

And use this `FHIRService.server` property to perform FHIR requests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6047277daa31`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.