# Issue

**Title:** Remove unused apm, jgit and JavaEWAH dependencies and stray StringUtils imports

## Description

Every HAPI consumer ships `co.elastic.apm:apm-agent-api`, `org.eclipse.jgit` (CVE-prone, 3.2 MB) and `JavaEWAH`, but no HAPI class uses them. Two `StringUtils` imports from plantuml and titanium-json-ld were IDE accidents.

**For review**
- The jgit/JavaEWAH exclusions sit on the managed `org.hl7.fhir.r5`, `convertors` and `validation` entries. `hapi-fhir-converter` and `hapi-fhir-validation` repeat them, because their declarations have exclusions of their own and Maven won't merge managed ones in. `README-hapi-fhir-dependency-versioning.md` (rules 5 and 6) now describes this.
- `hapi-fhir-structures-r5` lists jgit as a javadoc `additionalDependency`: its javadoc compiles the `org.hl7.fhir.r5` sources, which import it.
- `ParsedFhirPath` uses `isNotBlank`, because plantuml's `isNotEmpty` treated whitespace as empty.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b63138c4594`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.