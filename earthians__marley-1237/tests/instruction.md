# Issue

**Title:** fix(practitioner schedule): treat blank maximum appointments as uncapped

## Description

Fix TypeError when a schedule time slot leaves Maximum Appointments blank

## Problem

Saving a `Practitioner Schedule` raises an unhandled Python `TypeError`
whenever any time slot leaves `maximum_appointments` blank:

```
TypeError: '>' not supported between instances of 'NoneType' and 'int'
```

`maximum_appointments` is a plain nullable `Int` in
`healthcare_schedule_time_slot.json` — no `reqd`, no `default`. A blank child
value is NULL, `dict.get()` returns `None`, and line 22 compares it against an
`int`.

The surrounding guard checks `from_time`, `to_time` and `duration`, but not
`maximum_appointments`, so the comparison is reached on every save where that
one field is empty — which is the default state for any newly added slot. The
`TypeError` surfaces as a server error rather than a form validation message,
and there is no way for a practitioner to create a schedule without
discovering an undocumented required field.

## Reproduction

On a site with `healthcare` v16.6.1, inserting a `Practitioner Schedule` with
one 09:00–12:00 slot at 30-minute duration (`maximum_apps` computes to `6`),
varying only `maximum_appointments`:

| `maximum_appointments` | Result |
| --- | --- |
| field omitted | `TypeError: '>' not supported between instances of 'NoneType' and 'int'` |
| explicit `None` | same `TypeError` |
| `6` | saved |
| `99` | `ValidationError: Maximum appointments cannot be more than 6 in row #1` |

The last two rows are the control: the validation logic and its error message
are correct, and this line is the only defect.

## Fix

Treat a missing cap as "no cap" rather than comparing `None` to an integer:

```python
if (slots.get("maximum_appointments") or 0) > maximum_apps:
```

This matches the style of the guards already in the function. A blank field now
means an uncapped slot, which is what leaving the field empty means to a user,
and the existing "cannot be more than N" validation is unchanged for any value
that is actually set.

The alternative — adding `"default": 0` to the doctype JSON — would also stop
the crash, but it would make `0` mean both "explicitly unlimited" and "never
set", and it would not help sites whose existing rows are already NULL. The
one-line guard fixes existing data as well.

## Impact

Practitioners can add schedule slots without being forced to fill in a field
the UI does not mark as required. No schema change, no migration, no behaviour
change for any schedule that already has a cap.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d0a4d7bcce4c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.