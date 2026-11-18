# Issue

**Title:** maven(deps): bump org.owasp.encoder:encoder from 1.4.1 to 1.5.0

## Description

Bumps [org.owasp.encoder:encoder](https://github.com/OWASP/owasp-java-encoder) from 1.4.1 to 1.5.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/OWASP/owasp-java-encoder/releases">org.owasp.encoder:encoder's releases</a>.</em></p>
<blockquote>
<h1>OWASP Java Encoder 1.5.0</h1>
<p>Version 1.5.0 is available from Maven Central. All nine binary/source/Javadoc JARs, four POMs, and their thirteen signatures were downloaded from Central and verified against the retained signed release files. There is no <code>encoder-esapi:1.5.0</code> release.</p>
<h2>Security and correctness</h2>
<ul>
<li>Fixes encoded fragments completing outer HTML or XML parser delimiters across trusted-text boundaries in JavaScript HTML/block, CDATA, and XML-comment contexts. Versions through 1.4.1 are affected. See <a href="https://github.com/OWASP/owasp-java-encoder/security/advisories/GHSA-g8p6-7r8f-qrpv">GHSA-g8p6-7r8f-qrpv</a>.</li>
<li>Fixes <code>EncodedWriter</code> close/finalization behavior, exception handling, and overflow-safe array-slice validation.</li>
<li>Adds JSON encoding APIs and matching JSP/Jakarta tags and EL functions, plus XML 1.1 bindings.</li>
</ul>
<h2>Compatibility and migration</h2>
<p>Public Java APIs remain binary and source compatible with 1.4.1 for the three supported libraries. Java 8 remains the minimum runtime; packaged consumers passed on Java 8, 11, 17, 21, and 25.</p>
<p>The security fixes deliberately change some encoded output:</p>
<ul>
<li>JavaScript HTML/block modes emit additional hexadecimal escapes while preserving the string value. Review byte snapshots, cache keys, signatures, and output-size budgets.</li>
<li>CDATA preserves parsed text but can expand to 13 output characters per input character and can change parser event boundaries.</li>
<li>XML-comment hyphens become <code>~</code> under the documented lossy policy.</li>
</ul>
<p>The optional ESAPI adapter is retired. Version 1.4.1 is its final published release and is unsupported; migrate to direct Java Encoder APIs. Mixing the 1.4.1 adapter with the 1.5 core is not a supported migration.</p>
<p>See the <a href="https://github.com/OWASP/owasp-java-encoder/blob/v1.5.0/docs/compatibility-decisions.md#15-parser-boundary-output-migration">migration notes</a>, <a href="https://github.com/OWASP/owasp-java-encoder/blob/v1.5.0/docs/encoder-esapi-retirement.md">ESAPI retirement guide</a>, and <a href="https://github.com/OWASP/owasp-java-encoder/blob/v1.5.0/CHANGELOG.md">changelog</a>.</p>
<h2>Maven artifacts</h2>
<p>Use group <code>org.owasp.encoder</code> and version <code>1.5.0</code>:</p>
<ul>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder/1.5.0/">encoder</a></li>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-jsp/1.5.0/">encoder-jsp</a></li>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-jakarta-jsp/1.5.0/">encoder-jakarta-jsp</a></li>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-parent/1.5.0/">encoder-parent</a> (parent POM)</li>
</ul>
<p>The optional test WAR and retired ESAPI adapter are not published.</p>
<h2>Verification</h2>
<p>Exact release source: <code>3fbc5da5bcdc49a6e2b4f39d3df7410b7c13d07d</code>. The signed <code>v1.5.0</code> tag identifies this tested commit. PR <a href="">#229</a>'s squash commit <code>030c137fc14f277afc5fbe303d2ca8a149f8068b</code> has the identical file tree.</p>
<p>Release artifacts were built with Eclipse Temurin 17.0.20.1+1 and the committed Maven 3.9.16 wrapper. All 2,287 local reactor tests passed with zero failures, errors, or skips. All thirteen unsigned payload files matched two fresh source-export builds. Post-merge <a href="https://github.com/OWASP/owasp-java-encoder/actions/runs/36471162477">Java CI</a>, <a href="https://github.com/OWASP/owasp-java-encoder/actions/runs/36471162240">packaged consumers</a>, and <a href="https://github.com/OWASP/owasp-java-encoder/actions/runs/36471162191">CodeQL</a> passed, including the browser and Java 8 gates.</p>
<p>Project signing fingerprint: <code>1C5F632B86809F2F5DB25092BEA0075F94074A9B</code>.</p>
<p>The assets contain the public <code>KEYS</code>, detached signatures, and signed SHA-256/SHA-512 manifests. Follow the <a href="https://github.com/OWASP/owasp-java-encoder/blob/v1.5.0/VERIFYING.md">verification instructions</a>, using this full expected fingerprint and the 1.5.0 filenames. Authenticate each checksum manifest's signature before checking its entries.</p>
<p>Central bundle SHA-256: <code>107b0e4e1f459087d6bbd1e37222c05c7c4630fa55d52bc1e7c99c0077897590</code>.</p>
<p>The source-tag documentation preserves the pre-publication notices from the immutable release commit. This release record confirms the subsequently verified Central publication; publication follow-up documentation belongs in a later commit, not a rebuilt release.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/OWASP/owasp-java-encoder/blob/main/CHANGELOG.md">org.owasp.encoder:encoder's changelog</a>.</em></p>
<blockquote>
<h2>1.5.0 — 2026-09-28 UTC</h2>
<p>This is a security release for
<a href="https://github.com/OWASP/owasp-java-encoder/security/advisories/GHSA-g8p6-7r8f-qrpv">GHSA-g8p6-7r8f-qrpv</a>.
Signed artifact availability and independent verification are tracked in the
<a href="https://github.com/OWASP/owasp-java-encoder/blob/main/releases/1.5.0.md">1.5.0 release record</a>.</p>
<ul>
<li>build: stop Dependabot from recreating already-reviewed incompatible API,
servlet-engine and build-tool version proposals. The ignores are limited to
routine version updates in the rejected SemVer classes; security updates remain
eligible. Mixed historical/current coordinates require manual version review
because Dependabot classifies them from their lowest occurrence.</li>
<li>removed: retire the optional <code>encoder-esapi</code> adapter. Version 1.4.1 is its final published release and is no longer supported; no <code>encoder-esapi:1.5.0</code> artifact will be published. Consumers must remove the adapter and <a href="https://github.com/OWASP/owasp-java-encoder/blob/main/docs/encoder-esapi-retirement.md">migrate Java Encoder-backed calls to the direct context APIs</a>. Historical Maven artifacts remain immutable.</li>
<li>build: remove advisory-affected dependencies from active Maven plugin realms, including the separately invoked compatibility-fixture downloader; invoke the same japicmp engine without its obsolete reporting wrapper; and submit only actually invoked build plugins to GitHub's dependency graph. Shared inherited tooling is recorded once, and no Dependabot alert is dismissed or suppressed.</li>
<li>build/compatibility: update the published JSP provided API to 2.3.3 and the Jakarta test classpath to Servlet 6.1.0 and EL 6.0.1, while retaining independent JSP 2.2.1 and Java 8-compatible Jakarta minimum-consumer fixtures. Japicmp now resolves distinct old/new support classpaths so the 1.4.1 comparison remains complete. Dependabot scans the root Maven reactor once, rather than opening duplicate module proposals, and continues to scan the standalone compatibility-fixture project separately.</li>
<li>feat: all four <code>forJavaScript*</code> methods encode dollar sign (<code>$</code>) as <code>\x24</code>, backtick as <code>\x60</code>, and opening brace (<code>{</code>) as <code>\x7b</code> <a href="">#129</a>. Escaping <code>{</code> prevents input after a trusted <code>$</code> from completing <code>${...}</code>. Encoded output now supports literal text in ordinary (untagged) template literals as well as single- and double-quoted strings. This changes the encoded output while preserving its decoded JavaScript string value. Tagged templates (including <code>String.raw</code>), <code>${...}</code> expression bodies, JSON, and script URLs are unsupported; each method's HTML context restrictions still apply.</li>
<li>fix: all four <code>forJavaScript*</code> methods escape unpaired UTF-16 surrogates as <code>\uXXXX</code>, preserving their JavaScript string values through UTF-8 serialization <a href="">#135</a>, and escape DEL/C1 controls (U+007F to U+009F) as <code>\xNN</code> <a href="">#163</a>. Valid surrogate pairs and other non-ASCII text remain unescaped except U+2028/U+2029. These are output-fidelity changes; NEL was already ordinary JavaScript string data.</li>
<li>fix: the HTML/block JavaScript encoders escape every ASCII character that can contribute to a case-insensitive <code>&lt;/script</code> end tag or the <code>&lt;!--</code> and <code>--&gt;</code> script tokens, including the HTML end-tag delimiters, so any nonempty encoded substring cannot complete a delimiter supplied partly by adjacent trusted literal text. <code>forCDATA</code> represents every <code>]</code> and <code>&gt;</code> with close/reopen sequences, preserving parsed text while breaking every nonempty encoded substring of <code>]]&gt;</code>; its String facade grows with actual output instead of eagerly reserving the 13× maximum. <code>forXmlComment</code> replaces every hyphen with <code>~</code>. These are substantial compatibility-visible output changes; see the <a href="https://github.com/OWASP/owasp-java-encoder/blob/main/docs/compatibility-decisions.md#15-parser-boundary-output-migration">migration record</a>.</li>
<li>fix: <code>EncodedWriter</code> now enforces Writer lifecycle semantics: write, append and flush operations fail after close; repeated close is harmless; the first close finalizes pending input and still attempts the delegate close, preserving simultaneous failures with suppressed exceptions. Array-slice writes now use overflow-safe bounds validation, including <code>Integer.MAX_VALUE</code>-shaped ranges.</li>
<li>build: compare all three 1.5.0 artifacts against the immutable 1.4.1 public-API baseline, and verify that every publishable effective POM inherits repository-root SCM connection, developer connection and URL values without module-name suffixes.</li>
<li>feat: add <code>Encode.forJson</code> String/Writer methods, the <code>json</code> encoder context, and <code>forJson</code> tags and EL functions in both JSP and Jakarta tag libraries <a href="">#145</a>. The caller supplies double quotes. Output uses RFC 8259 string escapes and also escapes HTML script delimiters. Java <code>null</code> becomes the text <code>null</code> (the JSON string <code>&quot;null&quot;</code> when quoted); unpaired surrogates use Unicode escapes and may not interoperate with every JSON consumer. Prefer a serializer for complete JSON documents.</li>
<li>feat: add <code>forXml11</code>, <code>forXml11Content</code> and <code>forXml11Attribute</code> tags and EL functions to the advanced JSP and Jakarta taglibs, and <code>forXml11</code> to the basic taglibs <a href="">#131</a>.</li>
<li>deprecation: <code>Encoders.URI</code> and both <code>ForUriTag</code> classes are now deprecated like <code>Encode.forUri</code>, whose Javadoc now says what to use instead; the <code>forUri</code> TLD descriptions warn about double encoding, the adapter builds show deprecation call sites, and the README has a <a href="https://github.com/OWASP/owasp-java-encoder/blob/main/README.md#migrating-from-foruri">forUri migration section</a> <a href="">#130</a>.</li>
<li>fix: the JSP and Jakarta bundles now declare the core version they need (<code>;</code>, which HTML5 parsers decode as U+2026 <a href="">#136</a>.</li>
<li>fix: the XML 1.1 encoders (<code>forXml11</code>, <code>forXml11Content</code>, <code>forXml11Attribute</code>) now encode U+0085 (NEL) as <code>&amp;#x85;</code> and U+2028 (line separator) as <code>&amp;#x2028;</code>, so they are not normalized to a line feed <a href="">#136</a>.</li>
<li>maintenance: clarify output-context contracts and expand XML 1.1 tests, fix clean reactor compilation, and remove the obsolete benchmark profile.</li>
</ul>
<h3>Build, compatibility and maintenance</h3>
<ul>
<li>Preserve original-JAR consumers on Java 8/11/17/21/25, explicit/automatic JPMS
and Felix R6/R8; add final TLD-surface/Writer contract checks (<a href="">#162</a>, <a href="">#167</a>).</li>
<li>Test packaged javax/Jakarta TLDs through isolated Tomcat/Jasper engines; retain
required real-browser and executable-WAR checks with the modernized optional
Boot 4.1.1 fixture (<a href="">#179</a>, <a href="">#180</a>).</li>
<li>Pin and guard Actions, add CodeQL/dependency submissions/Dependabot, isolate
Maven caches, and preserve required CI/security gates (<a href="">#173</a>, <a href="">#177</a>).</li>
<li>Include Java 9 descriptors in source attachments; normalize source metadata
and retain attribution (<a href="">#184</a>).</li>
<li>Retire the dormant Maven Site/OSS parent, adopt verified Maven 3.9.16 wrapper
and JDK 17 build policy, Checkstyle and measured unit coverage floors; isolate
signing/publishing tools, verify local bundles and measure reproducibility
(<a href="">#185</a>, <a href="">#187</a>). This does not change the Java 8 library runtime baseline.</li>
<li>Add release verification, historical key evidence, and maintainer custody
guidance (<a href="">#164</a>, <a href="">#171</a>, <a href="">#185</a>). Historical signing-key
authorization records (<a href="">#110</a>) now distinguish retrospective maintainer
authentication from historical GitHub/project records; see the
<a href="https://github.com/OWASP/owasp-java-encoder/blob/main/releases/historical-key-authentication.md">key verification record</a>.
Central publication and the reported completion of maintainer access/custody
work (<a href="">#111</a>) are recorded in the <a href="https://github.com/OWASP/owasp-java-encoder/blob/main/releases/1.4.1-central-publication.md">publication follow-up</a>.</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>3fbc5da</code></a> Prepare OWASP Java Encoder 1.5.0 release</li>
<li><a href=""><code>df219a5</code></a> Suppress rejected Dependabot baseline updates (<a href="">#228</a>)</li>
<li><a href=""><code>a006309</code></a> Consolidate Dependabot API updates (<a href="">#217</a>)</li>
<li><a href=""><code>f25c771</code></a> Harden 1.5.0 context boundaries and release checks (<a href="">#210</a>)</li>
<li><a href=""><code>07d8e58</code></a> Complete historical key archive and maintenance closeout (<a href="">#209</a>)</li>
<li><a href=""><code>1111f79</code></a> Record 1.4.1 Central publication and maintainer readiness (<a href="">#208</a>)</li>
<li><a href=""><code>18582d3</code></a> Update bundle plugin and isolate compatibility-sensitive dependency proposals...</li>
<li><a href=""><code>011734a</code></a> Update artifact actions with verified pins and strict digest checks (<a href="">#175</a>)</li>
<li><a href=""><code>21705bd</code></a> Record compatibility commitments and base64url scope decision (<a href="">#190</a>)</li>
<li><a href=""><code>8c32b2c</code></a> Consolidate consumer docs, release history and community metadata (<a href="">#189</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/OWASP/owasp-java-encoder/compare/v1.4.1...v1.5.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.owasp.encoder:encoder&package-manager=maven&previous-version=1.4.1&new-version=1.5.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `015b9c67043f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.