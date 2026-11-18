# Issue

**Title:** OBLS-1018 Apply label template default values when a value is missing

## Description

### :sparkles: Description of Change

**Link to GitHub issue or Jira ticket:**
https://openboxes.atlassian.net/browse/OBLS-1018 (follow-up to OBLS-1016)

**Description:**

Makes the default in `${name.property:-text}` apply when the value is missing: an empty value (no value, or empty text), an empty link in the path (a product without a category), or a label object the page provided without a value (a product label printed from a page that passes no bin). A label object the page does not provide at all, and a name that is not a label object, stay errors. `0` and `false` are values and never replaced by the default. Documents the syntax in the templates README.

Since OBLS-1016 the template service accepted the default syntax, but the default never applied: the service turned an empty value into empty text, which `StringSubstitutor` does not treat as missing, and an empty link or empty label object failed before the default was looked at. `${a.b:-}` is the way to print an empty field where older templates used `?.`, so templates being updated by hand need it to work.

| Template | Data | Before | After |
|---|---|---|---|
| `${product.name:-none}` | product without a name, or an empty name | (empty) | `none` |
| `${product.category.name:-none}` | product without a category | error | `none` |
| `${product.category.name:-}` | product without a category | error | (empty) |
| `${location.name:-no bin}` | page passes no bin | error | `no bin` |
| `${product.quantity:-none}` | `0` (or `false`, or text made of spaces) | `0` | `0` |
| `${location.name:-x}` | page does not provide `location` at all | error | error |
| `${product.bogus:-x}` | property does not exist | error | error |
| `${product.category.nmae:-x}` | product without a category, misspelled property | error | error |
| any template without `:-` | any | unchanged | unchanged |

How: `StringSubstitutor` now hands the whole expression, default included, to the service (`setValueDelimiterMatcher(null)`), and `BeanPropertyTemplateService.resolveExpression` splits it at the first `:-` and applies the default itself. Only a null link in the path (`NullValueInNestedPathException`) is turned into the default, and only when the rest of the path exists on the declared property types (with their generic arguments; an index only on an array, a `List` or a `Set`); otherwise the null link is reported as it is without a default, so a misspelled property is not hidden behind a product without a category. When the label object itself is empty its properties cannot be checked, and the default is printed. Every other error stays an error. The default is inserted as written. The startup template check now uses the service's own property path pattern, so the two stay in step. The change is self-contained in `BeanPropertyTemplateService`; develop's copy of the service (#5943) has the same behavior and gets this with the planned merge of this branch.

## Tests

- `BeanPropertyTemplateServiceSpec` (54 new cases): the default for no value, empty text, an empty link (also indexed: a list, an array; an interface-typed link; generic types) and an empty label object; `0`, `0.0`, `false` (as `Integer`, `BigDecimal`, `Boolean`), blank text and present values printed as they are; still refused with a default: a label object not provided, a missing property (also after an empty link), an index past the end of a list, an index on a property that is not a list, a non-numeric or too large index, blocked properties and types (also after an empty link), an untyped link, an expression and `?.`; whitespace around the path, `:-`, `$` and `${` inside a default, the `$${...}` escape, and the three bundled templates rendering exactly as before. The existing features for templates without a default are unchanged and pass.
- `LabelTemplateCheckServiceSpec` (5 new cases): the startup check and the renderer agree on templates with defaults; a template reading a value the page does not pass is accepted by the check and refused at print time (the known difference, as for values today).
- `ZebraServiceSpec`: a template with `${product.category.name:-}` renders through `renderZpl` for a product without a category.
- Regression suite, `ZebraLabelIntegrationSpec`: a stored template with `${location.name:-}` built through `DocumentController.buildZebraTemplate` from a product with no bin prints a blank field.

Run against the unchanged service first, the new cases of the first commit failed as expected (13 of them: the defaults for empty values, empty links and empty label objects); all pass with the change. The refusal cases were checked by disabling each check in turn and confirming they fail.

## Verification

Run locally the way this branch's workflows run it (backend and regression workflows):

- Backend (`./gradlew jacocoTestReport`) on `TEST_DATABASE=mysql:8.0.36` and on `mariadb:10.3.39`: unit 1,349 tests, integration 70 tests, 0 failed on both.
- Regression suite (`./gradlew regressionTest regressionIntegrationTest`) on both databases: 2,433 unit and 1,248 integration tests, 0 failed on both. 67 and 272 skipped are the suite's pending features.
- This change touches no frontend file.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7184a7ea5b5f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.