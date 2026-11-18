# Issue

**Title:** fix: use .equals() instead of == for String comparisons

## Description

## Problem

Several files use `==` to compare `String` values instead of `.equals()`. In Java, `==` compares object references, not string content. While this may work by coincidence due to Java's string interning of literals, it is incorrect and fragile.

### Affected locations

| File | Line | Current | Fixed to |
|------|------|---------|----------|
| `BirthStatistics.java` | 95 | `== "M"` | `"M".equals(...)` |
| `CPCDSExporter.java` | 1105 | `== "out"` | `"out".equals(...)` |
| `CPCDSExporter.java` | 1108 | `== "in"` | `"in".equals(...)` |
| `CPCDSExporter.java` | 1115 | `== "emd"` | `"emd".equals(...)` |
| `State.java` | 394 | `== ""` | `.isEmpty()` |

## Why this matters

**BirthStatistics.java:** `mother.attributes.get(Person.GENDER)` returns an `Object` from a `Map<String, Object>`. The value is set via `Variant.getGender()` and `Seed.getGender()` — methods that may return dynamically constructed strings. If the string is not interned (e.g., built via concatenation or returned from a JSON parser), `==` will return `false` even when the content matches `"M"`, causing male patients to be incorrectly processed for pregnancy statistics.

**CPCDSExporter.java:** The `networkStatus` and `sourceAdminCode` fields are set via setter methods with string literals, which happens to work due to interning. However, this pattern is fragile — any refactoring that changes how these strings are constructed would silently break the place-of-service and revenue-center-code logic.

**State.java:** The `altDirectTransition == ""` check may silently fail if the string was deserialized from JSON (Gson returns new String instances, not interned ones), causing the validation to be skipped and a Physiology State to initialize without a fallback transition.

## Solution

- Use `"literal".equals(variable)` pattern (null-safe, avoids NPE)
- Use `.isEmpty()` instead of `== ""` for empty string checks
- No behavioral change when strings are interned (current case)
- Fixes silent failures when strings are not interned

## Verification

- All changes are mechanical `==` → `.equals()`/`.isEmpty()` replacements
- No logic changes, no new dependencies
- The `"literal".equals(variable)` pattern is null-safe by design
- Structural verification: confirmed each `==` comparison has a corresponding setter that uses the same literal value

## Changelog

| Date | Change | Author |
|------|--------|--------|
| 2026-06-18 | Replace == with .equals() for String comparisons in 3 files | rtmalikian |

### Files Changed
- `src/main/java/org/mitre/synthea/engine/State.java` — `== ""` → `.isEmpty()` (line 394)
- `src/main/java/org/mitre/synthea/export/CPCDSExporter.java` — `== "out"`, `== "in"`, `== "emd"` → `.equals()` (lines 1105, 1108, 1115)
- `src/main/java/org/mitre/synthea/world/concepts/BirthStatistics.java` — `== "M"` → `"M".equals()` (line 95)

### Verification
- Structural verification: confirmed each `==` comparison matches a corresponding setter using the same literal
- Pattern verification: `"literal".equals(var)` is the standard Java null-safe idiom
- No logic changes: behavior identical when strings are interned (current case); fixes silent failures when they are not

---

**About the Author:** Raphael Malikian — Clinical AI Solutions Architect. I specialise in building and fixing AI/ML systems for healthcare, including vector databases, RAG pipelines, and clinical NLP. If you need help with your project or think I can add value to your organisation, feel free to reach out — I'd love to connect.

📧 rtmalikian@gmail.com
🔗 GitHub: https://github.com/rtmalikian
🔗 LinkedIn: http://www.linkedin.com/in/raphael-t-malikian-mbbs-bsc-hons-71075436a

---

**Disclosure:** This code was developed with assistance from **MiMo v2.5 Pro** (Xiaomi) via **Hermes Agent** (Nous Research). All changes were reviewed, tested against the actual codebase, and verified for correctness.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d02dcd65b0c8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.