# Issue

**Title:** Return HTTP 500 for uncaught exceptions

## Description

.

`WebConfig`'s `SimpleMappingExceptionResolver` now has a default status code of 500. A JSON request to a handler that throws no longer gets HTTP 200. HTML requests still forward to `uncaughtException.jsp`, which already sets 500.

This doesn't change the response body: the JSON view still serializes the whole exception, stack trace included. Whether clients should get that body at all is a separate question that I've left out of this change.

**Tests:** Two `WebConfigTest` cases run MockMvc over a throwing controller with the real `simpleMappingExceptionResolver()`, `contentNegotiatingViewResolver()` and `jspViewResolver()` beans:
- **JSON:** returns 500. Before the fix it returned 200.
- **HTML:** returns 500 and still forwards to the JSP.

The full web suite passes: 201 tests, 0 failures.

**Runtime:** I ran this together with the other two fixes from this batch (#6640, #6641, #6642) on MySQL 8 (`mvn jetty:run`), with all 31 O3 reference application modules upgraded to Platform 3 and the full O3 reference content loaded. The O3 frontend then worked end to end for: patient registration, starting and ending a visit, vitals, conditions, allergies, lab and drug orders, lab result entry, dispensing, queueing, appointments, a form-engine form, ward admission, billing and stock items.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Fp7T1pGYEMrMVp1M7AW9Fg

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `085d24ca2891`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.