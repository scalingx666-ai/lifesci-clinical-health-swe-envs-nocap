# Issue

**Title:** maven(deps): bump org.owasp.encoder:encoder from 1.5.0 to 1.5.1

## Description

Bumps [org.owasp.encoder:encoder](https://github.com/OWASP/owasp-java-encoder) from 1.5.0 to 1.5.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/OWASP/owasp-java-encoder/releases">org.owasp.encoder:encoder's releases</a>.</em></p>
<blockquote>
<p>OWASP Java Encoder 1.5.1 is a documentation and build-maintenance patch. <strong>Encoding behavior, public APIs, runtime dependencies, and Java 8 support are unchanged from 1.5.0.</strong></p>
<h3>What changed</h3>
<ul>
<li>Clarify JavaScript encoding modes, output growth, and where encoded values can safely be inserted.</li>
<li>Explain why script-letter escapes remain necessary in the general and block modes; Source mode already leaves the URL in <a href="">#243</a> unchanged.</li>
<li>Distinguish JSON whole-string HTML embedding from JavaScript fragment protection, with clearer surrounding-template requirements.</li>
<li>Strengthen parser regression tests and include the build/test maintenance recorded in <a href="https://github.com/OWASP/owasp-java-encoder/blob/v1.5.1/CHANGELOG.md">CHANGELOG.md</a>.</li>
</ul>
<p>The documentation changes are in <a href="">#244</a>. The release preparation is in <a href="">#245</a>. This patch preserves the security fixes from 1.5.0 and introduces no new encoder security fix. Users upgrading from versions older than 1.5.0 should read the <a href="https://github.com/OWASP/owasp-java-encoder/releases/tag/v1.5.0">1.5.0 migration notes</a> and <a href="https://github.com/OWASP/owasp-java-encoder/security/advisories/GHSA-g8p6-7r8f-qrpv">security advisory</a>.</p>
<h3>Maven Central</h3>
<p>Version <strong>1.5.1</strong> is published under <code>org.owasp.encoder</code>:</p>
<ul>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder/1.5.1/"><code>encoder</code></a></li>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-jsp/1.5.1/"><code>encoder-jsp</code></a></li>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-jakarta-jsp/1.5.1/"><code>encoder-jakarta-jsp</code></a></li>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-parent/1.5.1/"><code>encoder-parent</code></a></li>
</ul>
<p>Keep core and adapter versions aligned. The retired ESAPI adapter and optional Jakarta test WAR are not included. The Javadoc JARs are attached. Hosted <a href="https://javadoc.io/doc/org.owasp.encoder/encoder/1.5.1/">core</a>, <a href="https://javadoc.io/doc/org.owasp.encoder/encoder-jsp/1.5.1/">JSP</a>, and <a href="https://javadoc.io/doc/org.owasp.encoder/encoder-jakarta-jsp/1.5.1/">Jakarta</a> documentation is live and was checked against the released Javadoc content.</p>
<h3>Verification</h3>
<p>Exact tested source: <code>1ab0cfbececf9969452fe03cbf5b5504b03a8b1b</code>; signed tag: <code>v1.5.1</code>.</p>
<p>All 26 downloaded Central payload/signature files match the retained originals byte for byte. All 13 payload signatures verify with the project key, full fingerprint <strong><code>1C5F632B86809F2F5DB25092BEA0075F94074A9B</code></strong>. The attached bundle SHA-256 is <strong><code>fcb226abfee84db155f27d40fe78173a96524d74dfc14a577eb1106ef57337f8</code></strong>.</p>
<p>The signed build passed 2,290 tests; the separate browser/WAR build passed 2,297, with zero failures/errors/skips. All 13 unsigned payloads match two independent clean builds using Temurin 17.0.20.1+1 and Maven 3.10.0. Required CI passed, including packaged consumers on Java 8/11/17/21/25, Java 8 tests, and CodeQL.</p>
<p>Verify signatures and signed checksum manifests using the attached <code>KEYS</code>, <code>SHA256SUMS</code>, and <code>SHA512SUMS</code> and <a href="https://github.com/OWASP/owasp-java-encoder/blob/v1.5.1/VERIFYING.md">these instructions</a>. Pending notices in the immutable source tag describe its preparation stage; this release confirms publication without changing those sources or signatures.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/OWASP/owasp-java-encoder/blob/main/CHANGELOG.md">org.owasp.encoder:encoder's changelog</a>.</em></p>
<blockquote>
<h2>1.5.1 — 2026-10-15 UTC</h2>
<p>Documentation and build-maintenance patch; publication is verified in the
<a href="https://github.com/OWASP/owasp-java-encoder/blob/main/releases/1.5.1-central-publication.md">publication record</a>. Encoding behavior and public APIs are unchanged.</p>
<ul>
<li>
<p>Clarify JavaScript encoding modes, output growth, and insertion-boundary
requirements for <a href="">#243</a>; distinguish JSON whole-string HTML embedding from
JavaScript fragment protection. Correct internal HTML/XML comments and
strengthen parser tests to verify script text, not only absence of a marker.
Encoding behavior is unchanged.</p>
</li>
<li>
<p>Verify public API compatibility against immutable 1.5.0 artifacts and their
matching support APIs. Minimum-consumer fixtures are unchanged.</p>
</li>
<li>
<p>Discover release tags independently of commit ancestry so squash merges cannot
leave the compatibility baseline stale; add isolated Git regressions.</p>
</li>
<li>
<p>Record verified 1.5.0 publication and replace pending-availability notices.</p>
</li>
<li>
<p>Update Jackson core/databind to 3.1.7 in the unpublished Jakarta fixture's
Spring Boot Maven plugin realm for GHSA-q4xh-88c3-wmh7, GHSA-wjgm-6hv5-3cvf,
GHSA-wv8q-qhhj-9h54 and GHSA-cxp5-3px4-pw24. Published library dependencies
and release artifacts are unchanged.</p>
</li>
<li>
<p>Route Jackson plugin-realm pins and Maven wrapper upgrades out of the grouped
Dependabot PR for individual review, and keep Jackson on its 3.1 line until the
Boot parent moves. Security updates remain eligible.</p>
</li>
<li>
<p>Build with Maven 3.10.0 through the committed wrapper and require it for signed
releases. Ordinary builds still accept Maven 3.9.16 or later. Library JARs and
module POMs are byte-identical to 3.9.16 builds
(<a href="https://github.com/OWASP/owasp-java-encoder/blob/main/releases/maven-3.10.0-validation.md">validation</a>).</p>
</li>
<li>
<p>Update isolated Tomcat/Jasper test engines to 9.0.123 and 10.1.61 and give
each its own Dependabot scan (<a href="">#241</a>, <a href="">#242</a>). These are test tooling, not
dependencies shipped inside the encoder libraries.</p>
</li>
<li>
<p>Update reviewed build tooling and pinned Actions, including japicmp 0.26.3,
Commons Lang 3.21.0, and the publisher's HttpClient 5.6.5 (<a href="">#234</a>, <a href="">#237</a>, <a href="">#240</a>).</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1ab0cfb</code></a> release: prepare Java Encoder 1.5.1 documentation patch</li>
<li><a href=""><code>ba3aade</code></a> Clarify JavaScript encoding contracts and strengthen boundary tests (<a href="">#244</a>)</li>
<li><a href=""><code>cb18f7e</code></a> Give each Tomcat JSP engine its own Dependabot scan (<a href="">#242</a>)</li>
<li><a href=""><code>0753931</code></a> Update Tomcat JSP fixtures to 9.0.123 and 10.1.61 (<a href="">#241</a>)</li>
<li><a href=""><code>1c08c6a</code></a> Bump the maven-dependencies group across 1 directory with 2 updates (<a href="">#237</a>)</li>
<li><a href=""><code>0d4cb88</code></a> Bump the actions group with 4 updates (<a href="">#240</a>)</li>
<li><a href=""><code>f200fae</code></a> Move the Maven wrapper to 3.10.0 (<a href="">#236</a>)</li>
<li><a href=""><code>914bd27</code></a> Bump org.apache.commons:commons-lang3 (<a href="">#234</a>)</li>
<li><a href=""><code>ee1e2a8</code></a> Update fixture Jackson to 3.1.7 and route pinned Dependabot updates (<a href="">#233</a>)</li>
<li><a href=""><code>454a07c</code></a> Complete 1.5.0 post-release cleanup (<a href="">#230</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/OWASP/owasp-java-encoder/compare/v1.5.0...v1.5.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.owasp.encoder:encoder&package-manager=maven&previous-version=1.5.0&new-version=1.5.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

Dependabot will resolve any conflicts with this PR as long as you don't alter it yourself. You can also trigger a rebase manually by commenting `@dependabot rebase`.

[//]: # (dependabot-automerge-start)
[//]: # (dependabot-automerge-end)

---

<details>
<summary>Dependabot commands and options</summary>
<br />

You can trigger Dependabot actions by commenting on this PR:
- `@dependabot rebase` will rebase this PR
- `@dependabot recreate` will recreate this PR, overwriting any edits that have been made to it
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `29a868a6403e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.