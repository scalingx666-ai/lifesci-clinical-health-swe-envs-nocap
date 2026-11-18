# Issue

**Title:** maven(deps): bump graalJsVersion from 25.3.4.1 to 25.4.4.1.1

## Description

Bumps `graalJsVersion` from 25.3.4.1 to 25.4.4.1.1.
Updates `org.graalvm.js:js` from 25.3.4.1 to 25.4.4.1.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/oracle/graaljs/releases">org.graalvm.js:js's releases</a>.</em></p>
<blockquote>
<h2>GraalJS 25 Innovation 4 (25.4.4.1.1)</h2>
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
<h1>GraalJS Changelog</h1>
<p>This changelog summarizes major changes between GraalVM versions of the GraalVM JavaScript (ECMAScript) language runtime.
The main focus is on user-observable behavior of the engine.
Changelog may include unreleased versions.
See <a href="https://www.graalvm.org/release-calendar/">release calendar</a> for release dates.</p>
<h2>Version 25.4.4</h2>
<ul>
<li>Implemented the <a href="https://github.com/tc39/proposal-await-dictionary"><code>Await Dictionary</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
</ul>
<h2>Version 25.3.4</h2>
<ul>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-includes"><code>Iterator Includes</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-join"><code>Iterator Join</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-chunking"><code>Iterator Chunking</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Updated Node.js to version 24.18.1.</li>
</ul>
<h2>Version 25.2.4</h2>
<ul>
<li>Updated Node.js to version 24.17.0.</li>
</ul>
<h2>Version 25.1.3</h2>
<ul>
<li>ECMAScript 2026 mode/features enabled by default.</li>
<li>Removed support and builds for macOS x86-64 (darwin-amd64).</li>
<li>Added an experimental option <code>js.crypto</code> that provides <code>getRandomValues()</code> and <code>randomUUID()</code> from the <a href="https://w3c.github.io/webcrypto/#crypto-interface">Web Crypto API</a>.</li>
<li>Added stable option <code>js.performance</code> that provides <code>performance.now()</code>, <code>timeOrigin</code>, and <code>toJSON()</code> from the <a href="https://w3c.github.io/hr-time/">Web High Resolution Time API</a>.</li>
<li>Finished support for <a href="https://github.com/tc39/proposal-temporal">Temporal</a>. It is available in ECMAScript 2027 mode (<code>--js.ecmascript-version=2027</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-immutable-arraybuffer"><code>Immutable ArrayBuffers</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-explicit-resource-management"><code>Explicit Resource Management</code></a> proposal. It is available behind the experimental option (<code>--js.explicit-resource-management</code>).</li>
<li>Updated Node.js to version 24.14.1.</li>
<li>Limited Chrome inspector remote debugging to localhost.</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-joint-iteration"><code>Joint Iteration</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-import-text"><code>Import Text</code></a> proposal. It is available behind the experimental option (<code>--js.import-text</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-import-bytes"><code>Import Bytes</code></a> proposal. It is available behind the experimental option (<code>--js.import-bytes</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-error-stack-accessor"><code>Error Stack Accessor</code></a> proposal. It is available behind the experimental option (<code>--js.error-stack-accessor</code>).</li>
<li>Removed support for legacy import assertions (<code>import ... assert {type: &quot;...&quot;}</code>) and the <code>--js.import-assertions</code> option; use import attributes (<code>import ... with {type: &quot;...&quot;}</code>, option <code>--js.import-attributes</code>) instead.</li>
</ul>
<h2>Version 25.0.0</h2>
<ul>
<li>ECMAScript 2025 mode/features enabled by default.</li>
<li>Updated Node.js to version 22.17.1.</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-intl-duration-format"><code>Intl.DurationFormat</code></a> proposal.</li>
<li>Made option <code>js.text-encoding</code> stable and allowed in <code>SandboxPolicy.CONSTRAINED</code>.</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-defer-import-eval"><code>import defer</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-upsert"><code>Upsert</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Enabled source phase imports from WebAssembly modules (<code>import source mod from &quot;./mod.wasm&quot;</code>) by default if the <code>js.webassembly</code> option is enabled and the <code>js.source-phase-imports</code> option is not explicitly set to <code>false</code>.</li>
</ul>
<h2>Version 24.2.0</h2>
<ul>
<li>Updated Node.js to version 22.13.1.</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-is-error"><code>Error.isError</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-math-sum"><code>Math.sumPrecise</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-promise-try"><code>Promise.try</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-atomics-microwait"><code>Atomics.pause</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>58f1795</code></a> [GR-23997] Periodic update of the graal import (2026-09-04).</li>
<li><a href=""><code>d5b0fde</code></a> Update graal import.</li>
<li><a href=""><code>fb21e3b</code></a> [GR-64345] Update GraalJS site for Maven artifacts 25.3.4.1.</li>
<li><a href=""><code>565c952</code></a> Update Jekyll theme revision in Gemfile.lock</li>
<li><a href=""><code>2ef7b14</code></a> Update GraalJS site for Maven artifacts 25.3.4.1</li>
<li><a href=""><code>55734fa</code></a> [GR-79202] Correction of Reflect.set for frozen arrays.</li>
<li><a href=""><code>fca7cf3</code></a> Regression test of Reflect.set for frozen arrays.</li>
<li><a href=""><code>7193578</code></a> Correction of Reflect.set for frozen arrays.</li>
<li><a href=""><code>6f96bf3</code></a> [GR-79127] Proxy constructor should not read prototype of NewTarget.</li>
<li><a href=""><code>e0a508e</code></a> [GR-79125] Correction of StringToBigInt() conversion.</li>
<li>Additional commits viewable in <a href="https://github.com/oracle/graaljs/compare/vm-25.3.4.1...vm-25.4.4.1.1">compare view</a></li>
</ul>
</details>
<br />

Updates `org.graalvm.js:js-scriptengine` from 25.3.4.1 to 25.4.4.1.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/oracle/graaljs/releases">org.graalvm.js:js-scriptengine's releases</a>.</em></p>
<blockquote>
<h2>GraalJS 25 Innovation 4 (25.4.4.1.1)</h2>
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
<h1>GraalJS Changelog</h1>
<p>This changelog summarizes major changes between GraalVM versions of the GraalVM JavaScript (ECMAScript) language runtime.
The main focus is on user-observable behavior of the engine.
Changelog may include unreleased versions.
See <a href="https://www.graalvm.org/release-calendar/">release calendar</a> for release dates.</p>
<h2>Version 25.4.4</h2>
<ul>
<li>Implemented the <a href="https://github.com/tc39/proposal-await-dictionary"><code>Await Dictionary</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
</ul>
<h2>Version 25.3.4</h2>
<ul>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-includes"><code>Iterator Includes</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-join"><code>Iterator Join</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-iterator-chunking"><code>Iterator Chunking</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Updated Node.js to version 24.18.1.</li>
</ul>
<h2>Version 25.2.4</h2>
<ul>
<li>Updated Node.js to version 24.17.0.</li>
</ul>
<h2>Version 25.1.3</h2>
<ul>
<li>ECMAScript 2026 mode/features enabled by default.</li>
<li>Removed support and builds for macOS x86-64 (darwin-amd64).</li>
<li>Added an experimental option <code>js.crypto</code> that provides <code>getRandomValues()</code> and <code>randomUUID()</code> from the <a href="https://w3c.github.io/webcrypto/#crypto-interface">Web Crypto API</a>.</li>
<li>Added stable option <code>js.performance</code> that provides <code>performance.now()</code>, <code>timeOrigin</code>, and <code>toJSON()</code> from the <a href="https://w3c.github.io/hr-time/">Web High Resolution Time API</a>.</li>
<li>Finished support for <a href="https://github.com/tc39/proposal-temporal">Temporal</a>. It is available in ECMAScript 2027 mode (<code>--js.ecmascript-version=2027</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-immutable-arraybuffer"><code>Immutable ArrayBuffers</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-explicit-resource-management"><code>Explicit Resource Management</code></a> proposal. It is available behind the experimental option (<code>--js.explicit-resource-management</code>).</li>
<li>Updated Node.js to version 24.14.1.</li>
<li>Limited Chrome inspector remote debugging to localhost.</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-joint-iteration"><code>Joint Iteration</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-import-text"><code>Import Text</code></a> proposal. It is available behind the experimental option (<code>--js.import-text</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-import-bytes"><code>Import Bytes</code></a> proposal. It is available behind the experimental option (<code>--js.import-bytes</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-error-stack-accessor"><code>Error Stack Accessor</code></a> proposal. It is available behind the experimental option (<code>--js.error-stack-accessor</code>).</li>
<li>Removed support for legacy import assertions (<code>import ... assert {type: &quot;...&quot;}</code>) and the <code>--js.import-assertions</code> option; use import attributes (<code>import ... with {type: &quot;...&quot;}</code>, option <code>--js.import-attributes</code>) instead.</li>
</ul>
<h2>Version 25.0.0</h2>
<ul>
<li>ECMAScript 2025 mode/features enabled by default.</li>
<li>Updated Node.js to version 22.17.1.</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-intl-duration-format"><code>Intl.DurationFormat</code></a> proposal.</li>
<li>Made option <code>js.text-encoding</code> stable and allowed in <code>SandboxPolicy.CONSTRAINED</code>.</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-defer-import-eval"><code>import defer</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-upsert"><code>Upsert</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Enabled source phase imports from WebAssembly modules (<code>import source mod from &quot;./mod.wasm&quot;</code>) by default if the <code>js.webassembly</code> option is enabled and the <code>js.source-phase-imports</code> option is not explicitly set to <code>false</code>.</li>
</ul>
<h2>Version 24.2.0</h2>
<ul>
<li>Updated Node.js to version 22.13.1.</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-is-error"><code>Error.isError</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-math-sum"><code>Math.sumPrecise</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-promise-try"><code>Promise.try</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
<li>Implemented the <a href="https://github.com/tc39/proposal-atomics-microwait"><code>Atomics.pause</code></a> proposal. It is available in ECMAScript staging mode (<code>--js.ecmascript-version=staging</code>).</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>58f1795</code></a> [GR-23997] Periodic update of the graal import (2026-09-04).</li>
<li><a href=""><code>d5b0fde</code></a> Update graal import.</li>
<li><a href=""><code>fb21e3b</code></a> [GR-64345] Update GraalJS site for Maven artifacts 25.3.4.1.</li>
<li><a href=""><code>565c952</code></a> Update Jekyll theme revision in Gemfile.lock</li>
<li><a href=""><code>2ef7b14</code></a> Update GraalJS site for Maven artifacts 25.3.4.1</li>
<li><a href=""><code>55734fa</code></a> [GR-79202] Correction of Reflect.set for frozen arrays.</li>
<li><a href=""><code>fca7cf3</code></a> Regression test of Reflect.set for frozen arrays.</li>
<li><a href=""><code>7193578</code></a> Correction of Reflect.set for frozen arrays.</li>
<li><a href=""><code>6f96bf3</code></a> [GR-79127] Proxy constructor should not read prototype of NewTarget.</li>
<li><a href=""><code>e0a508e</code></a> [GR-79125] Correction of StringToBigInt() conversion.</li>
<li>Additional commits viewable in <a href="https://github.com/oracle/graaljs/compare/vm-25.3.4.1...vm-25.4.4.1.1">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f39e8f277c9e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.