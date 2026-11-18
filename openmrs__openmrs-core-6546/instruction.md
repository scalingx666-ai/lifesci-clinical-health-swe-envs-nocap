# Issue

**Title:** TRUNK-6768: Remove unused BOM entries and ban SNAPSHOT dependencies in release builds

## Description

## Description of what I changed

Audits the BOM against actual module usage, removes unused managed entries, and adds a release-build check that fails on SNAPSHOT dependencies.

### 1. BOM audit (`bom/pom.xml`, root `pom.xml`, `NOTICE.md`)

Checked every managed dependency in `bom/pom.xml` against what the modules declare or resolve, using `mvn dependency:tree`.

**Removed (no module uses them):**
- `org.openmrs.liquibase.ext:type-converter`, its version property and its `NOTICE.md` entry
- `sonar-jacoco-listeners` and `sonarJacocoListenersVersion`, together with the `sonar` profile in the root `pom.xml`. Its only consumer was that profile, which nothing activates and which no longer works, because the listener needs JUnit 4 and JUnit 4 is not on the test classpath. Thanks @dkayiwa for tracing this.
- `org.openmrs.tools:openmrs-tools`. Nothing in core has used it since #5911, and the modules that reference it use it only as a formatter plugin dependency, which a BOM cannot version. The `tools` module itself is unchanged. Thanks @dkayiwa.

**Kept, with explanatory comments:**
- `jaxen`: declared by the `liquibase` module, where dom4j needs it for the XPath queries in `CoreDataTuner` and `SchemaOnlyTuner`
- `netty-bom`: pins the Netty version pulled in transitively by the AWS SDK S3 client

### 2. Release-build check for SNAPSHOT dependencies (root `pom.xml`, `web/pom.xml`, `api/pom.xml`)

Added the Maven Enforcer `requireReleaseDeps` rule with `onlyWhenRelease` set to `true` to the existing enforcer rules in `pluginManagement`.
- While the project version ends in `-SNAPSHOT` (as on `master`), the rule is skipped, so normal builds are unaffected.
- Once the project version is a release version (for example after `mvn versions:set` in the release workflow), the build fails if any dependency still resolves to a SNAPSHOT.
- It needs no profile and no flag, so `release.yaml` stays unchanged.
- It ignores optional dependencies.
- Moved the two scope overrides in the root `pom.xml` (`jakarta.servlet-api`, `reflections`) into `web` and `api`. The overrides replaced the BOM entries, so `requireReleaseDeps` never saw `jakartaServletVersion` or `reflectionsVersion`. The BOM stays scope-free. Resolved scopes, versions and the war's `WEB-INF/lib` are unchanged (compared with `dependency:tree` and a before/after listing).

It's documented in the README's Build section.

### 3. What was tried and dropped

- **A `release` profile with `banDynamicVersions`, switched on by adding `-Prelease` to `release.yaml`.** Dropped, because `release` is already the id of profiles in `api`, `web` and `webapp` that attach `-sources` and `-javadoc` jars. Passing `-Prelease` turns those on too, and the javadoc step currently fails with about 100 errors. `requireReleaseDeps` with `onlyWhenRelease` needs no flag.
- **Banning milestone, alpha, beta and RC versions with `bannedDependencies`.** Moved to TRUNK-6855. In my tests a `regex:`-prefixed pattern matched nothing, and `*:*:*-M*` matched every dependency in the project. As @dkayiwa explained, when a version pattern does not match as a glob, `ArtifactMatcher` falls back to "this version or newer". A pattern such as `*:*:99999999999|*-M\d*|*-alpha*|*-beta*|*-RC*|*-rc*|*.Alpha*|*.Beta*|*.CR*` avoids the fallback and works, but only through undocumented behaviour, and it needs an exception for `commons-fileupload2-*`.

### 4. Not part of this PR

- **`commons-fileupload2-jakarta-servlet6`** stays in `web/pom.xml` and the BOM. `legacyui` declares it with `provided` scope and relies on the war to supply it, so its removal is handled in #6451.
- **`release.yaml`** is unchanged. An earlier commit added `-Prelease` and a later one reverted it.

## Issue

https://openmrs.atlassian.net/browse/TRUNK-6768
Follow-up for the other pre-release qualifiers: TRUNK-6855

## Testing

```bash
mvn validate -pl api
# → BUILD SUCCESS

mvn clean install -pl bom,api,web,webapp,liquibase,test -am -DskipTests
# → BUILD SUCCESS
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6a2048e644f3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.