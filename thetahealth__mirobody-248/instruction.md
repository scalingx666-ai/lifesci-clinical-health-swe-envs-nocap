# Issue

**Title:** units: L/L is a volume fraction, 100 % of one

## Description

. Part of #234 (the hematocrit item).

### What was wrong

`L/L`, the SI spelling of a volume fraction, was not a unit the engine knew. A hematocrit printed as `0.45 L/L` was stored with `unit_ucum = ''` and no canonical value. A series holding that reading and a `45 %` reading therefore had no common canonical unit, so it had no min, max or average.

### Why not the change the issue suggests

The issue suggests giving `%` a dimensionless scale of 0.01. That puts `%` in the class `scale()` builds for every unit whose dimensions cancel. On `main` that class has 28 members: `1, 10*6, 10*9, 10*12, g/g, g/kg, h/d, min/d, mg/g, mg/kg, mL/dL, mL/L, mmol/mol, umol/mol, …`. `%` would then convert to all of them:

- **HbA1c:** 6.5 % (NGSP) would become 65 mmol/mol, but the IFCC value is 48. The two scales measure the same analyte, but the relation between them is not a factor.
- **Other units:** a count printed as bare `10*9`, a dose in `mg/kg`, time per day in `h/d` and an index in `1` would all become convertible to `%`.

It would also change the stored canonical pair of every percent reading, from `(45, '%')` to `(0.45, '1')`. `recode` would never rewrite the rows already stored, because `observations._same_coding` compares the coding, not the pair. Rows stored before and after would then disagree for good, and `election._candidates` reads `value_canonical` before `value_num`.

### What changed

- **`L/L` is a known unit.** `L/L`, `l/l`, `L/l` and `升/升` normalize to `L/L`, family `VFr`. The unit table goes from 330 to 331 units.
- **`%` and `L/L` convert only to each other.** `units.convert._PERCENT = {"%": 1, "L/L": 100}` converts the two by a factor of 100 and to nothing else. `scale()` returns None for both, so neither joins the dimensionless class.
- **Both fold to `%`.** That is the canonical unit every stored percent already carries: `canonicalize(0.45, "L/L") == canonicalize(45, "%") == (45.0, "%")`. A series holding both units now has statistics, and percent rows stored before this change count too.
- **Two Chinese names for hematocrit now code to 4544-3.** `红细胞比容` and `红细胞比积` resolved to 24360-0, the hemoglobin and hematocrit *panel*. With `%`, the unit gate refused that code and the reading asked for input. With `L/L`, which the engine did not recognize, the reading was filed under the panel. Two rows in `resolver_overrides.tsv` now send both names to 4544-3. Without them, recognizing `L/L` would have moved those readings from the panel to needs-input. The coverage score goes from 345 to 347.

I checked 14 hematocrit and plateletcrit names, each as `0.45 L/L`, `45 %` and `0.45 l/l`, against `main`:

- Every reading that was coded before is coded to the same LOINC code now; only its canonical pair is new.
- `红细胞比容` and `红细胞比积` move from 24360-0 or needs-input to 4544-3.
- `PCT` (plateletcrit or procalcitonin) still needs input, now as `unit:conflict` in `L/L` instead of `unit:unrecognized`.

### Not changed

- **`mL/dL` and `mL/L`** stay in the dimensionless class with canonical unit `1`, because that is the pair their stored rows carry. `L/L` therefore does not convert to them.
- **`%` and `1` still do not convert.** In the device catalogue, `1` is an index (`sleepAutonomicBalanceIndex`, `femaleMoistureIndex`), and on a lab report it is INR. Neither is known to be a fraction.
- **Readings already stored in `L/L` keep `unit_ucum = ''`.** `recode` replays the coding with the stored unit. Until they are re-extracted, a series that holds one still has no statistics. `recode` does move `红细胞比容` and `红细胞比积` readings to 4544-3.

### Test

The tests in `mirobody/tests/test_unit_conversions.py` check:

- the golden vectors from the issue: `conversion_factor("L/L", "%") == 100`, `conversion_factor("%", "L/L") == 0.01`, `convert_value(0.45, "L/L", "%") == 45.0`, and `partition_units(["%", "L/L", "/uL"])` giving two classes;
- the shared canonical pair;
- that `%` and `L/L` convert to none of `mmol/mol`, `10*9`, `10*9/L`, `mg/kg`, `h/d`, `1` or `mg/g`;
- that HbA1c 6.5 % → mmol/mol with code 4548-4 is refused.

`mirobody/tests/test_engine_coverage.py` adds the two Chinese names to the name cases and two `L/L` reading cases. Against `main`, the volume-fraction test fails.

```
pytest mirobody/tests/test_unit_conversions.py mirobody/tests/test_engine_coverage.py -q  → 102 passed (score 347/347)
pytest -q                                           → 1266 passed, 121 skipped, 12 xfailed *
ruff check mirobody examples                        → All checks passed
lint-imports                                        → 6 kept, 0 broken
```

\* Run locally without `tests/agent/test_code_tool_probe.py` and `tests/test_code_tool_capability.py`, which need `quickjs_rs`; CI installs it.

I ran the maintainers' gitignored suite on `main` and on this branch and compared the failure sets. They differ in two tests:

- `tests/translate/test_report_spellings.py::…[红细胞比容-42-%-4544-3]` failed on `main` and passes here.
- `tests/units/test_units.py::test_canonicalize_returns_atomic_units_untouched[%]` now fails. It asserts `canonical_unit("%") is None`. `canonicalize(120.0, "%")` still returns `(120.0, "%")`, but `%` is no longer atomic now that `L/L` folds into it, so `canonical_unit("%")` is `"%"`. Drop `%` from that parametrize.

`test_the_ucum_unit_count` passes with 331.

### Merge order

The figures this changes (345 → 347 and 330 → 331, in the three READMEs, `docs/standardization*.md`, `docs/testing.md` and the skill) sit on README lines next to lines #228 edits. Whichever of the two merges second needs a small rebase.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3c3b042e8eb0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.