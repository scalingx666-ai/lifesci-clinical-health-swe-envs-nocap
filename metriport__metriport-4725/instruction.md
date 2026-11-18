# Issue

**Title:** ENG-1133 + ENG-1123: Unrevert (requestId in wh + DiagnosticReport missing status / code) and fix breakage.

## Description

### Dependencies

None

### Description

This release needed to be rolled back due to conversion failures. See fix in the second sha - there were templates other than Assessments.hbs using the assessment.hbs partial, they needed to be updated as well. I realized that there was a pattern that other DiagnosticReport partials were using that the assessment.hbs partial had simply not been following, so also updated to match the pattern properly.

Here's the diff betw develop + my feature branch against the original problem file:
<img width="572" height="272" alt="image" src="https://github.com/user-attachments/assets/f8e4ca3f-0c43-4e5e-882d-44accc80d50f" />

Proof no resource counts were different:
<img width="943" height="101" alt="image" src="https://github.com/user-attachments/assets/97055be3-6713-4434-aefe-87b974fe4216" />

Proof of stdout differences between changes on develop + changes on my feature branch:
<img width="1728" height="469" alt="image" src="https://github.com/user-attachments/assets/e4c14490-858a-4a2a-a9bb-03b04ebc79d9" />

### Testing

- Local
  - [x] Run original offending file - verify that all DiagnosticReport resources have a status and a code.
  - [x] Reproduce base64 production failure using 2 different large XML files from different CXs 
  - [x] After making change verify that conversions do not fail.
  - [x] Run integration test over 10K xmls 
- Staging
  - [x] Run original offending file - verify that all DiagnosticReport resources have a status and a code.
  - [x] Reproduce base64 failure seen in production using 2 different large XML files from different CXs 
  - [x] After making change verify that conversions do not fail.
- Production
  - [ ] Run original offending file - verify that all DiagnosticReport resources have a status and a code.

### Release Plan
- [ ] Merge this
- [ ] Reconvert xmls for problem CX


<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **New Features**
  * Webhook payload metadata can include an optional requestId for async request tracing.
  * FHIR DiagnosticReport now surfaces code and status.
  * Analytics tool reports which patient IDs lack consolidated data during checks.

* **Documentation**
  * Webhook docs, realtime notifications, and request-id snippet updated to show optional requestId.

* **Chores**
  * Sample app paginates patient listing to 10; example env adds IS_PROD (false).
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aab4396ecfb7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.