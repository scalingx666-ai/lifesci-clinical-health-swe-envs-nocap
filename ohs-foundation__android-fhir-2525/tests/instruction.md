# Issue

**Title:** #2503 push SNAPSHOT Maven artifacts to github Packages

## Description

**Description**
Publish Maven artifacts in GitHub Packages

**Type**
Feature 

**Checklist**
- Tests done https://github.com/icrc-fdeniger/android-fhir
- Maven packages are deployed here: https://github.com/icrc-fdeniger?tab=packages&repo_name=android-fhir ( will be done on google/android-fhir)
- maven-repository.zip artifact is deployed as usual ( not sure about the usage of this artifact but not changes).
- See https://github.com/icrc-fdeniger/android-fhir/actions/runs/8798380904/job/24145256498 for a full deployment


**Versions**
- When the maven artifacts are deployed in GitHub Packages the SNAPSHOT prefix is used to follow Maven coventions.
- When the maven artifacts are deployed in official maven repositories, the SNAPSHOT prefix is not used ( as it's done actually as far as I can understand)
- In the PR, the artifact versions has been updated to next expected release version: 
  - for instance, `common`module will be automatically deployed with the version `0.1.0-alpha06-SNAPSHOT` in GitHub Packages and with `0.1.0-alpha06` in the next release.

**Suggestion/question**
why not removeing beta/alpha as versions like  0.X.Y are considered as development version ?

<table>
<tr>
 <td>Current Version
 <td>Used in this PR
 <td>Proposition
<tr>
 <td>common:0.1.0-alpha05
 <td>common:0.1.0-alpha06
 <td>common:0.1.1
<tr>
 <td>engine:1.0.0
 <td>engine:1.0.1
 <td>engine:1.0.1
<tr>
 <td>data-capture:1.1.0
 <td>data-capture:1.1.1
 <td>data-capture:1.1.1
<tr>
 <td>workflow:0.1.0-alpha04
 <td>workflow:0.1.0-alpha05
 <td>workflow:0.1.1
<tr>
 <td>ontrib-barcode:0.1.0-beta3
 <td>ontrib-barcode:0.1.0-beta4
 <td>ontrib-barcode:0.1.1
<tr>
 <td>contrib-locationwidget:0.1.0-alpha01
 <td>contrib-locationwidget:0.1.0-alpha02
 <td>contrib-locationwidget:0.1.1
<tr>
 <td>knowledge:0.1.0-alpha03
 <td>knowledge:0.1.0-alpha04
 <td>knowledge:0.1.1
</table>

if a dev Team wants to use an alpha/beta version it can use a dependency to a SNAPSHOT version ( the "unstable version created from the last build").
it's also possible to specify the artifact of a build with by example:  [engine-1.0.1-20240423.083712-3](https://github-registry-files.githubusercontent.com/745459243/cb327a80-014c-11ef-876c-dd8ff3d997f8?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=[REDACTED_AWS_FOR_PUBLIC_RELEASE]%2F20240423%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20240423T094450Z&X-Amz-Expires=300&X-Amz-Signature=81dd5dac799f59f45854974546c050bfb18176063240abedea37cf4d9b27c380&X-Amz-SignedHeaders=host&actor_id=0&key_id=0&repo_id=745459243&response-content-disposition=filename%3Dengine-1.0.1-20240423.083712-3.pom&response-content-type=application%2Foctet-stream)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae8c9bb5d2b2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.