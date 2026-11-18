# Issue

**Title:** maven(deps): bump commons-validator:commons-validator from 1.10.1 to 1.11.0

## Description

Bumps [commons-validator:commons-validator](https://github.com/apache/commons-validator) from 1.10.1 to 1.11.0.
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/apache/commons-validator/blob/master/RELEASE-NOTES.txt">commons-validator:commons-validator's changelog</a>.</em></p>
<blockquote>
<h2>Apache Commons Validator 1.11.0 RELEASE NOTES</h2>
<p>The Apache Commons Validator team is pleased to announce the release of Apache Commons Validator 1.11.0.</p>
<p>Apache Commons Validator provides the building blocks for both client-side and server-side data validation.
It may be used standalone or with a framework like Struts.</p>
<p>This is a feature and maintenance release. Java 8 or later is required.</p>
<p>For complete information on Apache Commons Validator, including instructions on how to submit bug reports,
patches, or suggestions for improvement, see the Apache Commons Validator website:</p>
<p><a href="https://commons.apache.org/proper/commons-validator/">https://commons.apache.org/proper/commons-validator/</a></p>
<p>Download page: <a href="https://commons.apache.org/proper/commons-validator/download_validator.cgi">https://commons.apache.org/proper/commons-validator/download_validator.cgi</a></p>
<h2>Changes in this version</h2>
<h2>New features</h2>
<ul>
<li>
<pre><code>            Add and use CheckDigitException.CheckDigitException(String, Object...) (). Thanks to Gary Gregory.
</code></pre>
</li>
<li>
<pre><code>            Add and use ValidatorException.ValidatorException(Throwable). Call sites that previously called new ValidatorException(Throwable#getMessage()) now preserve that exception (). Thanks to Gary Gregory.
</code></pre>
</li>
<li>
<pre><code>            Add and use ValidatorException.ValidatorException(String, Object...) (). Thanks to Gary Gregory.
</code></pre>
</li>
<li>
<pre><code>            Add and use ValidatorException(String, Throwable) (). Thanks to Gary Gregory.
</code></pre>
</li>
</ul>
<h2>Fixed Bugs</h2>
<ul>
<li>
<pre><code>            Fix Apache RAT plugin console warnings. Thanks to Gary Gregory.
</code></pre>
</li>
<li>
<pre><code>            Fixes to non-final static fields.
</code></pre>
</li>
<li>VALIDATOR-503:  DomainValidator Revocation for .dunlop: <a href="https://www.iana.org/reports/tld-transfer/20251021-dunlop">https://www.iana.org/reports/tld-transfer/20251021-dunlop</a>. Thanks to Gary Gregory.</li>
<li>VALIDATOR-504:  DomainValidator ICAAN .kerrylogistics Registry Agreement - Terminated: <a href="https://www.icann.org/en/registry-agreements/terminated/kerrylogistics">https://www.icann.org/en/registry-agreements/terminated/kerrylogistics</a>. Thanks to Gary Gregory.</li>
<li>VALIDATOR-505:  DomainValidator ICAAN .lancaster Registry Agreement - Terminated: <a href="https://www.icann.org/en/registry-agreements/terminated/lancaster">https://www.icann.org/en/registry-agreements/terminated/lancaster</a>. Thanks to Gary Gregory.</li>
<li>VALIDATOR-506:  DomainValidator ICAAN Revocation for .lipsy: <a href="https://www.iana.org/reports/tld-transfer/20250227-lipsy">https://www.iana.org/reports/tld-transfer/20250227-lipsy</a>. Thanks to Gary Gregory.</li>
<li>VALIDATOR-507:  DomainValidator ICAAN Revocation for .pramerica&quot; <a href="https://www.iana.org/reports/tld-transfer/20250516-pramerica">https://www.iana.org/reports/tld-transfer/20250516-pramerica</a>. Thanks to Gary Gregory.</li>
<li>VALIDATOR-508:  DomainValidator ICAAN Revocation for .redstone: <a href="https://www.iana.org/reports/tld-transfer/20250826-redstone">https://www.iana.org/reports/tld-transfer/20250826-redstone</a>. Thanks to Gary Gregory.</li>
<li>VALIDATOR-508:  Reject signed hex group in InetAddressValidator.isValidInet6Address(String) <a href="">#379</a>. Thanks to Sahana Surendra Bogar, Gary Gregory.</li>
<li>
<pre><code>            CheckDigit implementations check for input in the alphanumeric range (). Thanks to Gary Gregory, sahvx655-wq.
</code></pre>
</li>
<li>
<pre><code>            Removing a country code from an IBANValidator now removes associated &quot;other&quot; codes (). Thanks to Gary Gregory, sahvx655-wq.
</code></pre>
</li>
<li>
<pre><code>            DoubleValidator and FloatValidator now treat special symbols consistently (). Thanks to Gary Gregory, sahvx655-wq.
</code></pre>
</li>
<li>
<pre><code>            Fix long range check in GenericTypeValidator.formatLong (). Thanks to Gary Gregory, sahvx655-wq.
</code></pre>
</li>
<li>
<pre><code>            Fix BigIntegerValidator minValue(), maxValue(), and processParsedValue() for out of Long range values (). Thanks to Gary Gregory, sahvx655-wq.
</code></pre>
</li>
<li>
<pre><code>            Add missing tests for ValidatorUtils.replace and ValidatorUtils.copyMap (). Thanks to Mauricio Bento, Gary Gregory.
</code></pre>
</li>
<li>
<pre><code>            Fix RegexValidator.validate() returning null for a valid match (). Thanks to sahvx655-wq, Gary Gregory.
</code></pre>
</li>
<li>
<pre><code>            Compare CAS and EC check digit against validated code, not raw input (). Thanks to sahvx655-wq, Gary Gregory.
</code></pre>
</li>
<li>
<pre><code>            Prevent URL path traversal bypass via percent encoding in UrlValidator (). Thanks to sahvx655-wq.
</code></pre>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>eaee281</code></a> Prepare for the release candidate 1.11.0 RC1</li>
<li><a href=""><code>1a0292a</code></a> Prepare for the next release candidate</li>
<li><a href=""><code>519c3ba</code></a> Precompile Pattern in ISSNValidator.convertToEAN13(String, String).</li>
<li><a href=""><code>e07dfa6</code></a> Bump actions/checkout from 7.0.0 to 7.0.1</li>
<li><a href=""><code>5a28bc4</code></a> Reject nameprep-stripped code points in unicodeToASCII (<a href="">#429</a>).</li>
<li><a href=""><code>b41a464</code></a> Merge pull request <a href="">#429</a> from sahvx655-wq/domain-reject-nameprep-stripped</li>
<li><a href=""><code>b608cb5</code></a> cover zero-width non-joiner in testIDNFormatCodePoints</li>
<li><a href=""><code>21722b1</code></a> reject nameprep-stripped code points in unicodeToASCII</li>
<li><a href=""><code>8cd7a4f</code></a> Require the IPv6: tag for bracketed IPv6 email literals (<a href="">#428</a>).</li>
<li><a href=""><code>aeacecf</code></a> Merge pull request <a href="">#428</a> from sahvx655-wq/email-ipv6-literal-tag</li>
<li>Additional commits viewable in <a href="https://github.com/apache/commons-validator/compare/rel/commons-validator-1.10.1...rel/commons-validator-1.11.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=commons-validator:commons-validator&package-manager=maven&previous-version=1.10.1&new-version=1.11.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c472c1e925c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.