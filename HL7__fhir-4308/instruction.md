# Issue

**Title:** FHIR-54542, FHIR-57520, FHIR-58053: Update DiagnosticReport guidance

## Description

This PR addresses 3 ticket(s).

## Tickets
- [FHIR-54542](https://jira.hl7.org/browse/FHIR-54542): DiagnosticReport does support structured docs
- [FHIR-57520](https://jira.hl7.org/browse/FHIR-57520): Consider changing DiagnosticReport Invariant dgr-1 from error to warning
- [FHIR-58053](https://jira.hl7.org/browse/FHIR-58053): Diagnostic report scope includes only completed investigations.

## FHIR-54542: DiagnosticReport does support structured docs

Removed outdated DiagnosticReport scope limitations for cumulative result presentation and detailed structured sequencing reports, and recorded the clarification under Changes since 6.0.0-ballot5.

**Files:** `source/diagnosticreport/diagnosticreport-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-54542)

---

## FHIR-57520: Consider changing DiagnosticReport Invariant dgr-1 from error to warning

Changed DiagnosticReport invariant dgr-1 from error severity to warning while preserving its expression, and recorded the clarification under Changes since 6.0.0-ballot5.

**Files:** `source/diagnosticreport/diagnosticreport-introduction.xml`, `source/diagnosticreport/structuredefinition-DiagnosticReport.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-57520)

---

## FHIR-58053: Diagnostic report scope includes only completed investigations.

Clarified that DiagnosticReport may describe an investigation that is preliminary, partial, or final, and recorded the clarification under Changes since 6.0.0-ballot5.

**Files:** `source/diagnosticreport/diagnosticreport-introduction.xml`

[Ticket](https://jira.hl7.org/browse/FHIR-58053)

---

## Publisher QA

| metric | baseline | current | delta |
|---|---:|---:|---:|
| errors | 0 | 0 | 0 |
| warnings | 80 | 80 | 0 |
| info | 347 | 347 | 0 |
| broken_links | 0 | 0 | 0 |

The unmodified `origin/master` baseline and every ticket run reached the clean validation summary shown above, then failed during archive packaging because `temp/profiles-types-r3.xml` was absent. This is a reproducible baseline build failure rather than a ticket-specific validation regression; the local full build is therefore not green.

Rendered-page QA confirmed that all three linked ticket entries appear exactly once under **Changes since 6.0.0-ballot5**, the revised scope text is present, the removed scope limitations are absent, and `dgr-1` is displayed as a warning.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ef782bfa3e71`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.