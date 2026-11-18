# Issue

**Title:** [ENG-941] 🔥 Removes the unused `when` condition feature from keyboard shortcuts

## Description

ENG-941

## The problem

The hook `useKeyboardShortcuts` read the `when` clause of each shortcut. It made a code string from the clause. Then it ran the string with `new Function()`.

Two defects were present:

1. `new Function()` runs code from a string. This is a code-injection risk. It also needs the `unsafe-eval` policy in the browser. A healthcare application must not allow this policy.
2. The old code put each condition value into the string as text. A condition value of the type string could add more code to the expression.

## The evidence

The `when` clause had the value `always` in all 108 entries of `src/config/keyboardShortcuts.json`. No other value was present.

```
$ python3 -c "import json;d=json.load(open('src/config/keyboardShortcuts.json'));print(sorted({s['when'] for v in d.values() for s in v}))"
['always']
```

Only that static file supplies the shortcuts. No plugin and no `care-apps` code supplies a clause. The `conditions` parameter of the hook had one purpose: to feed the `when` clause. No caller read the filtered `shortcuts` result.

So the feature was dead code.

## The fix

This pull request deletes the feature. It is better to delete dead code than to keep an evaluator for it.

The change removes:

- the `when` field from all 108 entries in `src/config/keyboardShortcuts.json`
- the `when` field from the `KeyboardShortcut` interface
- the `ShortcutConditions` interface
- the `conditions` parameter of `useKeyboardShortcuts`
- the `new Function()` call

The hook keeps the same behaviour. All shortcuts were active before, because each clause was `always`. All shortcuts stay active now.

If a shortcut needs a condition later, the team can add a typed boolean field. A string clause is not necessary.

> **Note on the history of this branch**
> The first commit added a safe evaluator to replace `new Function()`. A later check showed that the feature has no user. The second commit deletes the feature and the evaluator. The review comments on the evaluator no longer apply, because that file is gone.

## React Doctor result

Command: `npx react-doctor@latest --verbose`

Before (1 finding):

```
✖ eval() runs untrusted code strings
  react-doctor/no-eval
  src/hooks/useKeyboardShortcuts.ts:65
```

After (0 findings):

```
$ grep -c "no-eval" rd-final.txt
0
```

Errors went from 21 to 20. Warnings went from 1313 to 1312. The score went from 43 to 45.

## Tests

- `npx tsc --noEmit` shows no error.
- `npm run knip` shows no new unused export.
- ESLint and Prettier pass on the changed files.
- `npx playwright test tests/facility/patient/encounter/encounterShortcuts.spec.ts` passed. All 17 tests passed. The 9 shortcut tests show that the shortcuts still work.

## Files changed

- `src/config/keyboardShortcuts.json` — removes the `when` field from 108 entries.
- `src/hooks/useKeyboardShortcuts.ts` — removes the `when` field, the `ShortcutConditions` interface, the `conditions` parameter, and the `new Function()` call.
- `src/context/ShortcutContext.tsx` — removes the `conditions` argument.
- `src/Utils/keyboardShortcutComponents.tsx` — removes the `conditions` argument at 2 call sites.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
## Summary by CodeRabbit

* **Refactor**
  * Simplified keyboard shortcut configuration and handling.
  * Removed obsolete shortcut condition settings while preserving existing shortcut keys, actions, descriptions, and groupings.
  * Updated shortcut components and context integration to use the streamlined configuration.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a578b5a4c32d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.