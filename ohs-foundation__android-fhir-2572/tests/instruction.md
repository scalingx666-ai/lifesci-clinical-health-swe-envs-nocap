# Issue

**Title:** Bump com.squareup:kotlinpoet from 1.15.3 to 1.17.0

## Description

Bumps [com.squareup:kotlinpoet](https://github.com/square/kotlinpoet) from 1.15.3 to 1.17.0.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/square/kotlinpoet/releases">com.squareup:kotlinpoet's releases</a>.</em></p>
<blockquote>
<h2>1.17.0</h2>
<p>Thanks to <a href="https://github.com/jisungbin"><code>@​jisungbin</code></a>, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>, <a href="https://github.com/evant"><code>@​evant</code></a>, <a href="https://github.com/sgjesse"><code>@​sgjesse</code></a>, <a href="https://github.com/sebek64"><code>@​sebek64</code></a> for contributing to this release.</p>
<ul>
<li>Change: kotlinx-metadata 0.9.0. Note that the <code>KotlinClassMetadata.read</code> is deprecated in 0.9.0 and replaced with <code>readStrict</code> (<a href="">#1830</a>).
<ul>
<li>Note: we now also provide <code>lenient</code> parameters to map to the underlying <code>readStrict()</code> and <code>readLenient()</code> calls (<a href="">#1766</a>).</li>
<li>We have also removed various <code>Class</code>/<code>TypeElement</code>/<code>Metadata</code>-to-<code>KmClass</code> APIs from the public API, as these are trivial to write now with kotlinx-metadata's newer APIs and allows us to focus the API surface area of this artifact better (<a href="">#1891</a>).</li>
</ul>
</li>
<li>New: Supertype list wraps to one-per-line if the primary constructor spans multiple lines (<a href="">#1866</a>).</li>
<li>New: Extract <code>MemberSpecHolder</code> interface for constructs that can hold <code>PropertySpec</code>s and <code>FunSpec</code>s and their builders (<a href="">#1877</a>).</li>
<li>New: <code>joinToCode</code> variant which operates on any type, but requires a transform lambda to convert each element into a <code>CodeBlock</code> (<a href="">#1874</a>).</li>
<li>New: Support annotation type arguments in <code>KSAnnotation.toAnnotationSpec()</code> (<a href="">#1889</a>).</li>
<li>Fix: Prevent name clashes between a function in class and a function call in current scope (<a href="">#1850</a>).</li>
<li>Fix: Fix extension function imports (<a href="">#1814</a>).</li>
<li>Fix: Omit implicit modifiers on <code>FileSpec.scriptBuilder</code> (<a href="">#1813</a>).</li>
<li>Fix: Fix trailing newline in <code>PropertySpec</code> (<a href="">#1827</a>).</li>
<li>Fix: <code>KSAnnotation.toAnnotationSpec</code> writes varargs in place instead of making them an array to work around a Kotlin issue with OptIn annotations (<a href="">#1833</a>).</li>
<li>Fix: <code>MemberName</code>s without a package are now correctly imported (<a href="">#1841</a>)</li>
<li>Fix: Throw if primary constructor delegates to other constructors (<a href="">#1859</a>).</li>
<li>Fix: Aliased imports with nested class (<a href="">#1876</a>).</li>
<li>Fix: Check for error types in <code>KSType.toClassName()</code> (<a href="">#1890</a>).</li>
<li>Fix: Support generating a single import for overloaded <code>MemberName</code>s (<a href="">#1909</a>).</li>
</ul>
<h2>1.16.0</h2>
<p>Thanks to <a href="https://github.com/drawers"><code>@​drawers</code></a>, <a href="https://github.com/rickclephas"><code>@​rickclephas</code></a> for contributing to this release.</p>
<ul>
<li>New: Kotlin 1.9.22.</li>
<li>New: KSP 1.9.22-1.0.16.</li>
<li>New: Add <code>NameAllocator</code> API to control keyword pre-allocation (<a href="">#1803</a>).</li>
<li>Fix: Fix issue with missing suspend modifier in <code>KSTypeReference.toTypeName</code> (<a href="">#1793</a>).</li>
<li>Fix: Honour same-package import aliases (<a href="">#1794</a>).</li>
<li>Fix: Always include parameter docs in the type header (<a href="">#1800</a>).</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/square/kotlinpoet/blob/main/docs/changelog.md">com.squareup:kotlinpoet's changelog</a>.</em></p>
<blockquote>
<h2>Version 1.17.0</h2>
<p>Thanks to [<a href="https://github.com/jisungbin"><code>@​jisungbin</code></a>][jisungbin], [<a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>][hfhbd], [<a href="https://github.com/evant"><code>@​evant</code></a>][evant], [<a href="https://github.com/sgjesse"><code>@​sgjesse</code></a>][sgjesse], [<a href="https://github.com/sebek64"><code>@​sebek64</code></a>][sebek64] for
contributing to this release.</p>
<p><em>2024-05-24</em></p>
<ul>
<li>Change: kotlinx-metadata 0.9.0. Note that the <code>KotlinClassMetadata.read</code> is deprecated in 0.9.0 and replaced with
<code>readStrict</code> (<a href="">#1830</a>).
<ul>
<li>Note: we now also provide <code>lenient</code> parameters to map to the underlying <code>readStrict()</code> and <code>readLenient()</code> calls
(<a href="">#1766</a>).</li>
<li>We have also removed various <code>Class</code>/<code>TypeElement</code>/<code>Metadata</code>-to-<code>KmClass</code> APIs from the public API, as these are
trivial to write now with kotlinx-metadata's newer APIs and allows us to focus the API surface area of this artifact
better (<a href="">#1891</a>).</li>
</ul>
</li>
<li>New: Supertype list wraps to one-per-line if the primary constructor spans multiple lines (<a href="">#1866</a>).</li>
<li>New: Extract <code>MemberSpecHolder</code> interface for constructs that can hold <code>PropertySpec</code>s and <code>FunSpec</code>s and their
builders (<a href="">#1877</a>).</li>
<li>New: <code>joinToCode</code> variant which operates on any type, but requires a transform lambda to convert each element into a
<code>CodeBlock</code> (<a href="">#1874</a>).</li>
<li>New: Support annotation type arguments in <code>KSAnnotation.toAnnotationSpec()</code> (<a href="">#1889</a>).</li>
<li>Fix: Prevent name clashes between a function in class and a function call in current scope (<a href="">#1850</a>).</li>
<li>Fix: Fix extension function imports (<a href="">#1814</a>).</li>
<li>Fix: Omit implicit modifiers on <code>FileSpec.scriptBuilder</code> (<a href="">#1813</a>).</li>
<li>Fix: Fix trailing newline in <code>PropertySpec</code> (<a href="">#1827</a>).</li>
<li>Fix: <code>KSAnnotation.toAnnotationSpec</code> writes varargs in place instead of making them an array to work around a Kotlin
issue with <code>OptIn</code> annotations (<a href="">#1833</a>).</li>
<li>Fix: <code>MemberName</code>s without a package are now correctly imported (<a href="">#1841</a>)</li>
<li>Fix: Throw if primary constructor delegates to other constructors (<a href="">#1859</a>).</li>
<li>Fix: Aliased imports with nested class (<a href="">#1876</a>).</li>
<li>Fix: Check for error types in <code>KSType.toClassName()</code> (<a href="">#1890</a>).</li>
<li>Fix: Support generating a single import for overloaded <code>MemberName</code>s (<a href="">#1909</a>).</li>
</ul>
<h2>Version 1.16.0</h2>
<p>Thanks to [<a href="https://github.com/drawers"><code>@​drawers</code></a>][drawers], [<a href="https://github.com/rickclephas"><code>@​rickclephas</code></a>][rickclephas] for contributing to this release.</p>
<p><em>2024-01-18</em></p>
<ul>
<li>New: Kotlin 1.9.22.</li>
<li>New: KSP 1.9.22-1.0.16.</li>
<li>New: Add <code>NameAllocator</code> API to control keyword pre-allocation (<a href="">#1803</a>).</li>
<li>Fix: Fix issue with missing <code>suspend</code> modifier in <code>KSTypeReference.toTypeName</code> (<a href="">#1793</a>).</li>
<li>Fix: Honour same-package import aliases (<a href="">#1794</a>).</li>
<li>Fix: Always include parameter docs in the type header (<a href="">#1800</a>).</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>fb28b0b</code></a> Prepare for release 1.17.0</li>
<li><a href=""><code>4f3154e</code></a> Update dependency mkdocs-material to v9.5.24</li>
<li><a href=""><code>29d409a</code></a> Support generating a single import for overloaded MemberNames (<a href="">#1909</a>)</li>
<li><a href=""><code>790a855</code></a> Update dependency mkdocs-material to v9.5.23</li>
<li><a href=""><code>e26e6ac</code></a> Update dependency mkdocs-material to v9.5.22</li>
<li><a href=""><code>54fe620</code></a> Update Kotlin and KSP (<a href="">#1903</a>)</li>
<li><a href=""><code>7a77eff</code></a> Update dependency Jinja2 to v3.1.4</li>
<li><a href=""><code>9531716</code></a> Update dependency Pygments to v2.18.0</li>
<li><a href=""><code>605b7ea</code></a> Update dependency mkdocs-material to v9.5.21</li>
<li><a href=""><code>3f7650c</code></a> Update dependency com.google.guava:guava to v33.2.0-jre (<a href="">#1899</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/square/kotlinpoet/compare/1.15.3...1.17.0">compare view</a></li>
</ul>
</details>
<br />

[![Dependabot compatibility score](https://dependabot-badges.githubapp.com/badges/compatibility_score?dependency-name=com.squareup:kotlinpoet&package-manager=gradle&previous-version=1.15.3&new-version=1.17.0)](https://docs.github.com/en/github/managing-security-vulnerabilities/about-dependabot-security-updates#about-compatibility-scores)

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
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot show <dependency name> ignore conditions` will show all of the ignore conditions of the specified dependency
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d3841ebd6363`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.