# Issue

**Title:** maven(deps): bump graalJsVersion from 25.2.4 to 25.3.4.1

## Description

Bumps `graalJsVersion` from 25.2.4 to 25.3.4.1.
Updates `org.graalvm.js:js` from 25.2.4 to 25.3.4.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/oracle/graaljs/releases">org.graalvm.js:js's releases</a>.</em></p>
<blockquote>
<h2>GraalJS 25 Innovation 3 (25.3.4.1)</h2>
<p><a href="https://www.graalvm.org/javascript/">GraalJS</a> is an ECMAScript-compliant runtime to execute JavaScript and Node.js applications.
It is fully standard-compliant, executes applications with high performance, and provides all benefits from the GraalVM stack, including language interoperability and common tooling.</p>
<p>You can download GraalJS as a Native Standalone distribution for Oracle GraalVM or GraalVM Community Edition.
Native Standalone contains a Native Image compiled launcher.</p>
<p>Starting with 25.0.3, JVM Standalone artifacts are no longer supported and are not included in this release.</p>
<p>To distinguish between Oracle GraalVM and GraalVM Community Edition, the Community Edition distribution has the suffix <code>-community</code> in its name.</p>
<p>Learn more about GraalJS and how to get started on the website at <a href="https://www.graalvm.org/javascript/">https://www.graalvm.org/javascript/</a>.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/oracle/graaljs/blob/master/CHANGELOG.md">org.graalvm.js:js's changelog</a>.</em></p>
<blockquote>
<h2>Version 25.3.4.1</h2>
<ul>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-includes"><code>Iterator Includes</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-join"><code>Iterator Join</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-chunking"><code>Iterator Chunking</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Updated Node.js to version 24.18.1.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>aede65d</code></a> [GR-78747] Fix iterator closing for <code>Array.from</code> and collection constructors.</li>
<li><a href=""><code>4d5b9b6</code></a> [GR-78730] Avoid duplicate builtin key and name strings.</li>
<li><a href=""><code>5cfa11d</code></a> Update test262 status.</li>
<li><a href=""><code>0daf607</code></a> Fix iterator closing for <code>Array.from</code> and collection constructors.</li>
<li><a href=""><code>735f95c</code></a> [GR-78733] Preserve pending return value across finally blocks.</li>
<li><a href=""><code>5294bb8</code></a> Update test262 status.</li>
<li><a href=""><code>0f79287</code></a> Preserve pending return value across finally blocks.</li>
<li><a href=""><code>05e11b8</code></a> [GR-78732] Avoid prototype mutation during context initialization.</li>
<li><a href=""><code>cd3aaac</code></a> Fix and assert functionData.hasStrictFunctionProperties() for async functions.</li>
<li><a href=""><code>e09a6d8</code></a> Allocate built-in derived constructor functions with their expected prototype.</li>
<li>Additional commits viewable in <a href="https://github.com/oracle/graaljs/compare/vm-25.2.4...vm-25.3.4.1">compare view</a></li>
</ul>
</details>
<br />

Updates `org.graalvm.js:js-scriptengine` from 25.2.4 to 25.3.4.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/oracle/graaljs/releases">org.graalvm.js:js-scriptengine's releases</a>.</em></p>
<blockquote>
<h2>GraalJS 25 Innovation 3 (25.3.4.1)</h2>
<p><a href="https://www.graalvm.org/javascript/">GraalJS</a> is an ECMAScript-compliant runtime to execute JavaScript and Node.js applications.
It is fully standard-compliant, executes applications with high performance, and provides all benefits from the GraalVM stack, including language interoperability and common tooling.</p>
<p>You can download GraalJS as a Native Standalone distribution for Oracle GraalVM or GraalVM Community Edition.
Native Standalone contains a Native Image compiled launcher.</p>
<p>Starting with 25.0.3, JVM Standalone artifacts are no longer supported and are not included in this release.</p>
<p>To distinguish between Oracle GraalVM and GraalVM Community Edition, the Community Edition distribution has the suffix <code>-community</code> in its name.</p>
<p>Learn more about GraalJS and how to get started on the website at <a href="https://www.graalvm.org/javascript/">https://www.graalvm.org/javascript/</a>.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/oracle/graaljs/blob/master/CHANGELOG.md">org.graalvm.js:js-scriptengine's changelog</a>.</em></p>
<blockquote>
<h2>Version 25.3.4.1</h2>
<ul>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-includes"><code>Iterator Includes</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-join"><code>Iterator Join</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-chunking"><code>Iterator Chunking</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Updated Node.js to version 24.18.1.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>aede65d</code></a> [GR-78747] Fix iterator closing for <code>Array.from</code> and collection constructors.</li>
<li><a href=""><code>4d5b9b6</code></a> [GR-78730] Avoid duplicate builtin key and name strings.</li>
<li><a href=""><code>5cfa11d</code></a> Update test262 status.</li>
<li><a href=""><code>0daf607</code></a> Fix iterator closing for <code>Array.from</code> and collection constructors.</li>
<li><a href=""><code>735f95c</code></a> [GR-78733] Preserve pending return value across finally blocks.</li>
<li><a href=""><code>5294bb8</code></a> Update test262 status.</li>
<li><a href=""><code>0f79287</code></a> Preserve pending return value across finally blocks.</li>
<li><a href=""><code>05e11b8</code></a> [GR-78732] Avoid prototype mutation during context initialization.</li>
<li><a href=""><code>cd3aaac</code></a> Fix and assert functionData.hasStrictFunctionProperties() for async functions.</li>
<li><a href=""><code>e09a6d8</code></a> Allocate built-in derived constructor functions with their expected prototype.</li>
<li>Additional commits viewable in <a href="https://github.com/oracle/graaljs/compare/vm-25.2.4...vm-25.3.4.1">compare view</a></li>
</ul>
</details>
<br />

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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4793794c23e4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.