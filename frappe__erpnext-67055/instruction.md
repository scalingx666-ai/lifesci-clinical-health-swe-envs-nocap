# Issue

**Title:** fix(stock): log failed Google Maps requests in Delivery Trip instead of showing the request URL (backport #65792)

## Description

Backport of #65792 to `version-15-hotfix`. The version-16 backport is #67024.

When the Google Maps directions request failed in Delivery Trip, the error text from the HTTP library was shown to the user. For a connection failure that text has the full request URL, including the API key from Google Settings. Now a connection failure is written to the Error Log and the user sees a short message. Errors returned by Google (for example `NOT_FOUND`) still show as before.

**Fix:** Show the Google error text only for `googlemaps.exceptions.ApiError`. For any other exception, log the error and show a fixed message. () The follow-up test commit checks that the failed request is written to the Error Log. ()

**Changes compared with develop:** None. The commit applies without changes. The Delivery Trip contact display backport #67056 (of #65795) also changes `delivery_trip.py` and `test_delivery_trip.py`, in other functions. Each PR merges on its own.

 for the example and the steps to test.

### Tests

- `test_route_transport_error_hides_the_google_maps_key`: passes on this branch, fails on `version-15-hotfix` without the fix (the message has the request URL with the key). It also checks that `frappe.log_error` is called once, and fails when that call is removed.
- `test_route_api_error_shows_the_google_maps_status`: passes on this branch and without the fix (must-still-work check).
- `test_delivery_trip.py` (complete file): 26 of 27 tests pass. `test_delivery_trip_notify_customers` fails on this branch and on `version-15-hotfix` with the same error, because the local test site has no default outgoing Email Account.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fb4711f304ad`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.