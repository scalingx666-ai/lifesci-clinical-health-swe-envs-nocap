# Issue

**Title:** resolve ImportErrors for isodate and fhirclient.models

## Description

Hi

When I ran `pip install fhirclient` to evaluate the library, I hit an ImportError for `isodate` when I attempted to import some of the models (like `from fhirclient.models.patient import Patient`).   It looks like `isodate` is in the requirements.txt file but it didn't seem to be listed in the setup.py.   This patch adds `isodate` to the `install_requires` list.   When I tested that change in a fresh virtualenv using `pip install -e .`, I hit ImportErrors trying to import models.   After adding a `__init__.py` file to the models directory, that ImportError was also resolved.   Now, I'm able to interact with a local FHIR server (http://jamesagnew.github.io/hapi-fhir/doc_rest_server.html)

```
(venv) [master] $ python
Python 2.7.9 (295ee98b6928, May 31 2015, 07:28:49)
[PyPy 2.6.0 with GCC 4.2.1 Compatible Apple LLVM 5.1 (clang-503.0.40)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>> from fhirclient import client
>>>> from fhirclient.models.patient import Patient
>>>> defaults = {'app_id': 'local_dev', 'api_base': 'http://localhost:8080/restful-server-example/fhir/'}
>>>> fhir = client.FHIRClient(settings=defaults)
>>>> response = Patient.where({}).perform(fhir.server)
```

We've been using `vcrpy` on projects like https://github.com/pokitdok/pokitdok-python to help replay requests to exercise the code during travisci test runs.  Maybe something similar could be set up for fhirclient?

Thanks for the work on this project,

Brian

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a87600523b2b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.