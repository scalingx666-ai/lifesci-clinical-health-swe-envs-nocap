# Issue

**Title:** Two more CCDA fixes

## Description

This PR contains two fixes.

## CCDA Template
The first fix moves a single line in the CCDA template, and addresses the following stack trace when a patient has no documented history of smoking.

```
org.mitre.synthea.export.CCDAExporterTest > testCCDAExport FAILED
    java.lang.AssertionError: Validation of exported CCDA failed: index=41, size=41|Consol Continuity of Care Document (CCD) (V3) SHALL contain  [1..1] component such that it  (CONF:1198-30687, CONF:1198-30688) Conforms to Social History Section (V3) (templateId: 2.16.840.1.113883.10.20.22.2.17:2015-08-01) expected:<0> but was:<2>
        at org.junit.Assert.fail(Assert.java:88)
        at org.junit.Assert.failNotEquals(Assert.java:834)
        at org.junit.Assert.assertEquals(Assert.java:645)
        at org.mitre.synthea.export.CCDAExporterTest.testCCDAExport(CCDAExporterTest.java:71)
```


I tested the fix with the new `CCDAExporterTest.testFailedCCDAExports()` method.

## Last Provider
The second fix addresses a rare case when a patient has no preferred wellness provider, and no history of any wellness provider, encountered in this stack trace:

```
org.mitre.synthea.export.CCDAExporterTest > testExportWithNoPreferredWellnessProvider FAILED
    java.lang.IllegalStateException: Unable to export to CCDA because person Evangelina20 Jacobson885 has no preferred provider.
        at org.mitre.synthea.export.CCDAExporter.export(CCDAExporter.java:120)
        at org.mitre.synthea.export.CCDAExporterTest.testExportWithNoPreferredWellnessProvider(CCDAExporterTest.java:88)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d720465be87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.