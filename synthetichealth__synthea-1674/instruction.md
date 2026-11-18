# Issue

**Title:** docs: document argument order precedence for -c and --config flags

## Description

## Problem
When using both `-c` (config file) and `--config*=value` (command-line overrides), the precedence depends on argument order — the last one specified wins. This behavior was not documented in the help text, leading to confusion.

## Solution
Added a note to the `usage()` help text explaining:
- That both `-c` and `--config*=value` write to the same `Properties` object
- That the last one in the argument list takes precedence
- Concrete examples showing both orderings and which value wins

## Root Cause
In `App.java`, both `-c` (line 136: `Config.load(configFile)`) and `--config*=value` (line 255: `Config.set(configSetting, value)`) write to the same static `Properties` object in `Config.java`. Since arguments are processed left-to-right from a queue, the later argument overwrites the earlier one's value.

## Verification
The change is documentation-only — no behavioral change. The help text accurately describes the existing behavior confirmed by reading the source code in `Config.java` (lines 34-36 for `load`, lines 175-177 for `set`).

---

**About the Author:** Raphael Malikian — Clinical AI Solutions Architect. I specialise in building and fixing AI/ML systems for healthcare, including vector databases, RAG pipelines, and clinical NLP. If you need help with your project or think I can add value to your organisation, feel free to reach out — I'd love to connect.

📧 rtmalikian@gmail.com
🔗 GitHub: https://github.com/rtmalikian
🔗 LinkedIn: http://www.linkedin.com/in/raphael-t-malikian-mbbs-bsc-hons-71075436a

---

**Disclosure:** This code was developed with assistance from **mimo-2.5-pro** (Xiaomi) via **Hermes Agent** (Nous Research). All changes were reviewed, tested against the actual codebase, and verified for correctness.

## Changelog

| Date | Change | Author |
|------|--------|--------|
| 2026-06-18 | Initial docs: document -c and --config argument precedence | rtmalikian |
| 2026-06-18 | Added DCO sign-off to commit | rtmalikian |
| 2026-06-18 | Updated PR documentation with changelog | rtmalikian |

### Files Changed
- `src/main/java/App.java` — Added note to `usage()` help text explaining argument order precedence for `-c` and `--config` flags

### Verification
- ✅ Help text now explains that last argument wins when both flags are used
- ✅ Includes concrete examples showing both orderings
- ✅ DCO sign-off present on all commits

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d02dcd65b0c8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.