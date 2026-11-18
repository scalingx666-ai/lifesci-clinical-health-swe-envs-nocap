# Issue

**Title:** maven(deps): bump org.owasp.encoder:encoder from 1.5.1 to 1.6.0

## Description

Bumps [org.owasp.encoder:encoder](https://github.com/OWASP/owasp-java-encoder) from 1.5.1 to 1.6.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/OWASP/owasp-java-encoder/releases">org.owasp.encoder:encoder's releases</a>.</em></p>
<blockquote>
<h2>OWASP Java Encoder 1.6.0</h2>
<p>OWASP Java Encoder <strong>1.6.0</strong> reduces unnecessary JavaScript letter escaping while retaining recognized HTML-token protection across trusted fragments. It resolves <a href="">#243</a> through <a href="">#247</a>. This is a minor release because emitted bytes and streaming behavior change.</p>
<h3>Changes and migration</h3>
<ul>
<li><code>forJavaScript</code> and <code>forJavaScriptBlock</code> keep interior script-name letters readable. A final C, I, P, R, S, or T in either case still receives an escape. Punctuation and whitespace escapes remain.</li>
<li><code>http://google.com</code> now produces <code>http:\/\/google.com</code>; <code>script</code> becomes <code>scrip\x74</code>; <code>i</code> remains <code>\x69</code>. The rule is conservative: <code>cat</code> becomes <code>ca\x74</code>.</li>
<li>HTML does not remove whitespace inside tag names. Escaping <code>&lt;</code> in a complete value addresses the HTML tag delimiter concern, but a fragment may have its <code>&lt;</code> supplied by trusted text. The terminal escape preserves that supported protection.</li>
<li>General/block <code>EncodedWriter</code> callers must flush before writing directly to the wrapped writer. Explicit flushes safely emit pending letters/surrogates and can add escapes while preserving the JavaScript UTF-16 value. Low-level callers must retain unread input after UNDERFLOW and supply more input or mark end-of-input.</li>
<li>Review snapshots, signatures and cache keys that depend on encoded bytes. Source and attribute-only methods are unchanged.</li>
</ul>
<p>Public APIs, Java 8 support, runtime dependencies and module/bundle identities are unchanged. No new encoder security fix is introduced. The 1.5.0 protections remain; users of older versions should follow the <a href="https://github.com/OWASP/owasp-java-encoder/security/advisories/GHSA-g8p6-7r8f-qrpv">security advisory</a>. See the <a href="https://github.com/OWASP/owasp-java-encoder/blob/v1.6.0/docs/compatibility-decisions.md#javascript-output-refinement-in-160-243">migration record</a>.</p>
<h3>Maven Central</h3>
<p>Version <strong>1.6.0</strong> is published under <code>org.owasp.encoder</code>:</p>
<ul>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder/1.6.0/">encoder</a></li>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-jsp/1.6.0/">encoder-jsp</a></li>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-jakarta-jsp/1.6.0/">encoder-jakarta-jsp</a></li>
<li><a href="https://repo.maven.apache.org/maven2/org/owasp/encoder/encoder-parent/1.6.0/">encoder-parent</a></li>
</ul>
<p>Keep core and adapter versions aligned. Do not combine javax and Jakarta adapters. The retired ESAPI adapter and optional test WAR are not included. Javadoc JARs are attached; hosted javadoc.io indexing can lag publication.</p>
<h3>Verification</h3>
<p>Exact tested source: <code>d9b0fd62497fb9276429a9ea972f4449ab320f2d</code>; signed tag: <code>v1.6.0</code>.</p>
<p>All 26 downloaded Central payload/signature files matched the retained originals byte for byte. All 13 payload signatures and both checksum-manifest signatures verify with project fingerprint <strong><code>1C5F632B86809F2F5DB25092BEA0075F94074A9B</code></strong>. Attached bundle SHA-256: <strong><code>8d860714634ae3b53f19bb3ea326f639b74df96c0e82bc956d53f237b5804c16</code></strong>.</p>
<p>The clean unsigned and signed builds, Docker/browser/WAR gate, packaged Java 17 consumers and repository checks passed. All thirteen unsigned payloads match two independent clean builds using Temurin 17.0.20.1+1 and Maven 3.10.0. Required CI passed, including Java 8/11/17/21/25 consumers, Java 8 tests and Java/Actions/Python CodeQL. Model-assisted review followed MODELS.md; no Daybreak review was completed before release. The documented maintainer review bypass was authorized; required CI/security checks were not bypassed.</p>
<p><strong>Correction — 2026-10-18:</strong> The original review record described Daybreak access as unavailable, but the explicit picker-route probe had not been attempted. A subsequent probe succeeded, as recorded in [PR <a href="">#251</a>](<a href="">OWASP/owasp-java-encoder#251</a>). This establishes later access, not a pre-release review. The release tag and signed artifacts retain their original bytes.</p>
<p>Verify the attached signatures and signed checksum manifests with <code>KEYS</code>, <code>SHA256SUMS</code>, <code>SHA512SUMS</code> and <a href="https://github.com/OWASP/owasp-java-encoder/blob/v1.6.0/VERIFYING.md">VERIFYING.md</a>. The immutable source retains preparation-stage notices; this release confirms publication without changing those sources or signatures.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/OWASP/owasp-java-encoder/blob/main/CHANGELOG.md">org.owasp.encoder:encoder's changelog</a>.</em></p>
<blockquote>
<h2>1.6.0 — 2026-10-18 UTC</h2>
<p>Publication is verified; see the <a href="https://github.com/OWASP/owasp-java-encoder/blob/main/releases/1.6.0.md">release record</a>.</p>
<ul>
<li>Reduce unnecessary script-letter escaping in <code>forJavaScript</code> and
<code>forJavaScriptBlock</code> (<a href="">#243</a>). Interior letters remain readable; the input's last
character is escaped if it is C, I, P, R, S, or T (either case). Existing punctuation escapes and
protection against recognized HTML tokens across trusted-text boundaries are
preserved. Encoded bytes change, while JavaScript string values do not.
Streaming encoders may retain one trailing letter; <code>EncodedWriter.flush()</code>
safely emits it as a hex escape and any pending high surrogate as a Unicode
escape. Explicit flushes can add safe escapes while preserving UTF-16 values.
Direct <code>Encoder.encode</code> callers must retain unread input after underflow and
supply more input or mark end-of-input, including for a pending ASCII letter.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>d9b0fd6</code></a> release: prepare Java Encoder 1.6.0</li>
<li><a href=""><code>300ef20</code></a> Merge pull request <a href="">#247</a> from OWASP/fix/issue-243-script-letter-escaping</li>
<li><a href=""><code>da8b7a0</code></a> Merge remote-tracking branch 'origin/main' into fix/issue-243-script-letter-e...</li>
<li><a href=""><code>2c5bf4b</code></a> Clarify issue 243 fragment protection and unreleased usage</li>
<li><a href=""><code>caa8aa4</code></a> Merge pull request <a href="">#248</a> from OWASP/docs/model-review-workflow</li>
<li><a href=""><code>9ea2823</code></a> Make model review guidance first-party project instructions</li>
<li><a href=""><code>00d0eb2</code></a> Document model-assisted Java Encoder review workflow</li>
<li><a href=""><code>a596740</code></a> Reduce interior JavaScript letter escaping while preserving boundary safety</li>
<li><a href=""><code>1d0e9f2</code></a> Merge pull request <a href="">#246</a> from OWASP/release/1.5.1-published</li>
<li><a href=""><code>5ce32da</code></a> Record verified 1.5.1 publication and resume 1.5.2 development</li>
<li>Additional commits viewable in <a href="https://github.com/OWASP/owasp-java-encoder/compare/v1.5.1...v1.6.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=org.owasp.encoder:encoder&package-manager=maven&previous-version=1.5.1&new-version=1.6.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `142de1d547c6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.