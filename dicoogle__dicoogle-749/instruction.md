# Issue

**Title:** Integrate dicoogle-next UI

## Description

## Description
This PR integrates the new **dicoogle-next web application** accessible via a dedicated Servlet under the `/experimental` path. 

## Summary
* Added a new `DicoogleNextWebAppServlet.java` servlet mapped to `/experimental/*` to serve the new UI.
* Included the [dicoogle-next](https://github.com/dicoogle/dicoogle-next) repository as a submodule.
* Modified `pom.xml` and `DicoogleWeb.java` to accomodate the build and routing of the new UI alongside the current one.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fbcc08e1a6b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.