# Issue

**Title:** feat(foomedical): SMART Health Check-in page

## Description

Adds /check-in, where a signed-in patient asks their health app for records and a PHQ-2 form using SMART Health Check-in (@smart-health-checkin/client v0.4.4, installed from its GitHub release tarball; the library is not on npm).

The patient reviews what the app shared, then sends it to the care team. Sending stages the check-in rather than writing to the chart: a DocumentReference holding the response and request, the PHQ-2 QuestionnaireResponse, a "Review check-in" Task listing each item's status, the PHQ-2 score, and any identity mismatch, and a Provenance. Writes are keyed by the check-in request id, so a retry does not duplicate them.

The request matches the KTC connectathon scenarios. /check-in?test also offers a Testing Wallet that declines immunizations.

For SMART Health Check-in connectathon: https://smart-health-checkin.org/connectathon/

Based on https://github.com/jmandel/medplum-smart-health-checkin-demo (thanks @jmandel !)

New "Check in" link:

<img width="1949" height="1520" alt="image" src="https://github.com/user-attachments/assets/5fca98c2-bf5c-4def-88b4-9d80adcf6743" />

New "Check in" page:

<img width="1949" height="1520" alt="image" src="https://github.com/user-attachments/assets/e6844b3d-e486-468b-b0ac-d08fea4cc6f6" />

That list is pulled automatically by the `@smart-health-checkin/client` dependency from https://smart-health-checkin.org/connectathon/wallets.json

You can then use the test wallet:

<img width="1949" height="1520" alt="image" src="https://github.com/user-attachments/assets/6c791975-8bdf-43f5-baf7-f405ddf7071f" />

See what was shared:

<img width="1949" height="1520" alt="image" src="https://github.com/user-attachments/assets/406a0426-079b-4e22-b10d-ab5c0d948e3a" />

Send to care team:

<img width="1949" height="1520" alt="image" src="https://github.com/user-attachments/assets/2984e2b1-339e-41b9-b8c2-715498efeb95" />

Then a success message:

<img width="1949" height="1520" alt="image" src="https://github.com/user-attachments/assets/a305968b-6399-426e-a2bb-27218d2137e7" />

Response is persisted as a `DocumentReference` + `Binary`:

<img width="1949" height="1520" alt="image" src="https://github.com/user-attachments/assets/3f22bbd6-ace2-4985-91bc-0e0e02bc9877" />

Future PR will update the provider app side.  We already have a UI for processing inputs from SMART Health Links.  We need to generalize that into a general purpose "patient intake reconciliation" flow that can be used by both SMART Health Links and also SMART Health Check-in.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd453f256b0d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.