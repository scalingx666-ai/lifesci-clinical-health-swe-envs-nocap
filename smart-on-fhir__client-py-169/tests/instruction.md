# Issue

**Title:** Add pagination functionality to FHIRClient and related unit tests

## Description

### PR Title: Add Pagination to FHIRClient with Unit Tests

**Description:**

This PR introduces pagination to `FHIRClient`, allowing efficient navigation of large FHIR datasets. Key methods include:

- `fetch_next_page`: Retrieves the next page via the `next` link in the FHIR Bundle.
- `get_next_link`: Extracts the `next` link from the Bundle's links.
- `sanitize_next_link`: Validates and sanitizes the `next` link URL.
- `execute_pagination_request`: Handles the HTTP request and manages errors when fetching the next page.

**Testing:**
- Unit tests in `client_pagination_test.py` cover pagination, handling missing `next` links, and errors.

**Notes:**
- Backward-compatible, no breaking changes.

Please review and provide feedback.

Fixes: #108

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `796ffa6eb977`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.