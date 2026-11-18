# Issue

**Title:** fix: close FileInputStream in Mapping.parseMapping() via try-with-resources

## Description

## Problem

In `Mapping.java`, the `parseMapping()` method creates a `FileInputStream` on line 38 that is never closed:

```java
InputStream selectorInputSteam = new FileInputStream(mappingFile);
Yaml yaml = new Yaml(new Constructor(Mapping.class));
return yaml.loadAs(selectorInputSteam, Mapping.class);
```

The `yaml.loadAs()` call reads from the stream but does not close it. This causes a resource leak — the file descriptor remains open until the garbage collector finalizes the stream, which is non-deterministic. Under heavy load (many flexporter mappings loaded in sequence), this can exhaust OS file descriptors.

## Solution

Wrapped the `FileInputStream` in a `try-with-resources` block so the stream is always closed after `yaml.loadAs()` completes, regardless of whether it succeeds or throws:

```java
try (InputStream selectorInputSteam = new FileInputStream(mappingFile)) {
    Yaml yaml = new Yaml(new Constructor(Mapping.class));
    return yaml.loadAs(selectorInputSteam, Mapping.class);
}
```

Also updated `ActionsTest.setupClass()` throws clause from `FileNotFoundException` to `IOException` to match the widened signature.

### Files Changed
- `src/main/java/org/mitre/synthea/export/flexporter/Mapping.java` — Added try-with-resources, added `IOException` import, updated javadoc
- `src/test/java/org/mitre/synthea/export/flexporter/ActionsTest.java` — Updated `throws FileNotFoundException` to `throws IOException`

### Verification
- All callers already handle `IOException` or broader:
  - `App.java:221` — inside `catch (Exception e)` block
  - `RunFlexporter.java:124` — method declares `throws IOException`
  - `ActionsTest.java:87` — updated to `throws IOException`
- `FileNotFoundException` is a subclass of `IOException`, so the change is backwards compatible
- Java try-with-resources guarantees the stream is closed even if `yaml.loadAs()` throws

## Changelog

| Date | Change | Author |
|------|--------|--------|
| 2026-06-19 | Close FileInputStream via try-with-resources in Mapping.parseMapping() | rtmalikian |

---

**About the Author:** Raphael Malikian — Clinical AI Solutions Architect. I specialise in building and fixing AI/ML systems for healthcare, including vector databases, RAG pipelines, and clinical NLP. If you need help with your project or think I can add value to your organisation, feel free to reach out — I'd love to connect.

📧 rtmalikian@gmail.com
🔗 GitHub: https://github.com/rtmalikian
🔗 LinkedIn: http://www.linkedin.com/in/raphael-t-malikian-mbbs-bsc-hons-71075436a

---

**Disclosure:** This code was developed with assistance from **mimo-v2.5-pro** (Xiaomi) via **Hermes Agent** (Nous Research). All changes were reviewed, tested against the actual codebase, and verified for correctness.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d02dcd65b0c8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.