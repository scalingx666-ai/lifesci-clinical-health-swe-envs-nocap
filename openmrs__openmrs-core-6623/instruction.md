# Issue

**Title:** maven(deps): bump org.owasp.encoder:encoder from 1.4.0 to 1.4.1

## Description

Bumps [org.owasp.encoder:encoder](https://github.com/owasp/owasp-java-encoder) from 1.4.0 to 1.4.1.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/owasp/owasp-java-encoder/releases">org.owasp.encoder:encoder's releases</a>.</em></p>
<blockquote>
<h2>v1.4.1 — Security release</h2>
<h1>OWASP Java Encoder 1.4.1</h1>
<p><strong>Version 1.4.1 is available from Maven Central.</strong> Published on 2026-09-27 UTC (2026-09-26 in America/Los_Angeles) from the original retained signed bundle. All 12 binary/source/Javadoc JARs, five POMs, and their 17 signatures were downloaded from Central and matched the original release byte for byte. Versions through 1.4.0 remain affected.</p>
<p>Central artifacts: <a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder/1.4.1/">encoder</a>, <a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-jsp/1.4.1/">encoder-jsp</a>, <a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-jakarta-jsp/1.4.1/">encoder-jakarta-jsp</a>, <a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-esapi/1.4.1/">encoder-esapi</a>, <a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-parent/1.4.1/">encoder-parent</a>.</p>
<h2>Security fixes</h2>
<p>Upgrade all OWASP Java Encoder dependencies to <strong>1.4.1</strong>. Versions through 1.4.0
are affected by the following issues:</p>
<ul>
<li><strong>GHSA-57jg-769q-93vh:</strong> <code>EncodedWriter</code> could lose encoding context when pending
lookahead overflowed its output buffer, allowing CDATA or XML comment delimiters
to escape and dropping or duplicating characters. The fix preserves unconsumed
input across buffer flushes.</li>
<li><strong>GHSA-q6jj-5396-8mq2:</strong> <code>EncodedWriter</code> could loop indefinitely when a write did
not supply enough input to resolve pending lookahead. The fix retains pending
input for the next write or close instead of spinning.</li>
<li><strong>GHSA-p9ff-j89j-9xhx:</strong> long runs of U+2028 or U+2029 could cause the String
overloads of <code>Encode.forCssString</code> and <code>Encode.forCssUrl</code> to throw <code>AssertionError</code>.
The fix corrects the maximum encoded output size. The JSP/Jakarta CSS EL
functions and the ESAPI CSS adapter also benefit from this fix.</li>
</ul>
<p>The first two issues require direct use of <code>EncodedWriter</code>; the <code>Encode</code> facade,
JSP/Jakarta tags, and ESAPI adapter do not call it internally. The CSS size issue
affects String-returning APIs; Writer overloads and CSS tags are unaffected.</p>
<h2>Compatibility and other changes</h2>
<ul>
<li>Java 8 remains the minimum runtime. Build and test with JDK 17.</li>
<li>Public method signatures, Maven coordinates, explicit JPMS module names, and
historical <code>Automatic-Module-Name</code> values are retained.</li>
<li>The JSP, Jakarta, and ESAPI module descriptors now expose their public API
dependencies transitively (<a href="">#98</a>).</li>
<li>The ESAPI adapter now uses a fixed ESAPI 2.7.0.0 dependency; tested compatibility
is documented in <code>esapi/README.md</code> (<a href="">#99</a>).</li>
<li>Build tooling, packaged OSGi compatibility tests, project metadata, and Jakarta
test dependency alignment have been updated (<a href="">#90</a>, <a href="">#106</a>).</li>
</ul>
<h2>Maven artifacts</h2>
<p>Use version <code>1.4.1</code> for every artifact you consume:</p>
<table>
<thead>
<tr>
<th>Group ID</th>
<th>Artifact ID</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>org.owasp.encoder</code></td>
<td><code>encoder</code></td>
</tr>
<tr>
<td><code>org.owasp.encoder</code></td>
<td><code>encoder-jsp</code></td>
</tr>
<tr>
<td><code>org.owasp.encoder</code></td>
<td><code>encoder-jakarta-jsp</code></td>
</tr>
<tr>
<td><code>org.owasp.encoder</code></td>
<td><code>encoder-esapi</code></td>
</tr>
</tbody>
</table>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/OWASP/owasp-java-encoder/blob/main/CHANGELOG.md">org.owasp.encoder:encoder's changelog</a>.</em></p>
<blockquote>
<h2>1.4.1 — 2026-09-26 UTC</h2>
<p><a href="https://github.com/OWASP/owasp-java-encoder/releases/tag/v1.4.1">Signed GitHub release</a>
(<a href="https://github.com/OWASP/owasp-java-encoder/tree/v1.4.1">tag created 2026-09-25 in America/Los_Angeles</a>).
<strong>Available from Maven Central. Upgrade all four Java Encoder artifacts;
versions through 1.4.0 are affected.</strong>
Central publication was verified on 2026-09-27 UTC (2026-09-26 in
America/Los_Angeles); <a href="https://github.com/OWASP/owasp-java-encoder/blob/main/releases/1.4.1-central-publication.md">all artifacts and signatures match the retained release</a>.</p>
<ul>
<li>Fix <code>EncodedWriter</code> context corruption during buffer overflow
(<a href="https://github.com/OWASP/owasp-java-encoder/security/advisories/GHSA-57jg-769q-93vh">GHSA-57jg-769q-93vh</a>).</li>
<li>Fix insufficient-lookahead infinite loops in <code>EncodedWriter</code>
(<a href="https://github.com/OWASP/owasp-java-encoder/security/advisories/GHSA-q6jj-5396-8mq2">GHSA-q6jj-5396-8mq2</a>).</li>
<li>Fix CSS String API maximum-output sizing for long U+2028/U+2029 runs
(<a href="https://github.com/OWASP/owasp-java-encoder/security/advisories/GHSA-p9ff-j89j-9xhx">GHSA-p9ff-j89j-9xhx</a>).</li>
<li>Preserve Java 8 runtime, public method signatures, Maven and JPMS identities;
make adapter API dependencies transitively readable in module descriptors.</li>
<li>Pin the ESAPI adapter's default to 2.7.0.0 rather than a Maven version range.</li>
</ul>
<p>See the <a href="https://github.com/OWASP/owasp-java-encoder/blob/main/releases/1.4.1.md">full release record</a> for affected entry points,
coordinates, verification and publication status. Later 1.5 changes do not alter
these retained artifacts.</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ab76d58</code></a> Use primary OWASP release email and document pending Central access</li>
<li><a href=""><code>b51c575</code></a> Prepare 1.4.1 security release with a dedicated project signing key</li>
<li><a href=""><code>0583c22</code></a> Fix EncodedWriter handling of pending lookahead characters</li>
<li><a href=""><code>d15c6fe</code></a> Fix CSSEncoder.maxEncodedLength for U+2028 and U+2029</li>
<li><a href=""><code>b52a954</code></a> Merge pull request <a href="">#150</a> from OWASP/docs/security-policy</li>
<li><a href=""><code>80851e3</code></a> Qualify the SECURITY.md upgrade note with the Java 8 baseline</li>
<li><a href=""><code>16312e6</code></a> Expand the security policy now that private reporting is enabled</li>
<li><a href=""><code>14fd1c5</code></a> Merge pull request <a href="">#106</a> from OWASP/fix/jakarta-test-encoder-version</li>
<li><a href=""><code>2a55ccc</code></a> Merge pull request <a href="">#98</a> from OWASP/fix/jpms-adapter-dependencies</li>
<li><a href=""><code>316290a</code></a> Merge main into fix/jpms-adapter-dependencies</li>
<li>Additional commits viewable in <a href="https://github.com/owasp/owasp-java-encoder/compare/v1.4.0...v1.4.1">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.owasp.encoder:encoder&package-manager=maven&previous-version=1.4.0&new-version=1.4.1)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d801de9eb121`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.