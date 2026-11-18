# Issue

**Title:** Fix crashes in `CompiledExpression::Compile` when compiling malformed FHIRPath expressions:

## Description

Fix crashes in `CompiledExpression::Compile` when compiling malformed FHIRPath expressions:
1. Catch `std::exception` when invoking ANTLR so invalid UTF-8 input strings return `absl::InvalidArgumentError` instead of throwing an uncaught `antlr4::IllegalArgumentException`.
2. Add child vector bounds checks and null checks in `FhirPathCompilerVisitor` methods so incomplete ANTLR parse trees (such as `"%"` or `"-%"`) return an error instead of aborting.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `190539f9049a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.