# Issue

**Title:** chore: bump virtualenv from 21.7.10 to 21.7.12 in /backend

## Description

Bumps [virtualenv](https://github.com/pypa/virtualenv) from 21.7.10 to 21.7.12.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pypa/virtualenv/releases">virtualenv's releases</a>.</em></p>
<blockquote>
<h2>21.7.12</h2>
<!-- raw HTML omitted -->
<h2>What's Changed</h2>
<ul>
<li>🔧 chore(changelog): drop dead CVE-2026-24049 fragment by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3249</a></li>
<li>🐛 fix(activation): escape batch quote() against injection by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3250</a></li>
<li>🐛 fix(seed): verify downloaded wheel digests by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3251</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/pypa/virtualenv/compare/21.7.11...21.7.12">https://github.com/pypa/virtualenv/compare/21.7.11...21.7.12</a></p>
<h2>21.7.11</h2>
<!-- raw HTML omitted -->
<h2>What's Changed</h2>
<ul>
<li>Add OpenSSF Scorecard workflow by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3238</a></li>
<li>Document AI-assisted contributions and licensing policy by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3239</a></li>
<li>👷 ci(release): attest and sign release provenance by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3242</a></li>
<li>👷 ci: harden Scorecard-scored checks in CI by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3241</a></li>
<li>🐛 fix(ci): parallelize graalpy tests, recover crashed workers by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3240</a></li>
<li>🐛 fix(ci): mark real-shell activation tests as slow by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3243</a></li>
<li>👷 ci: run macOS jobs on macos-26 by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3244</a></li>
<li>🐛 fix(activation): undo a live activation before activate.bat saves values by <a href="https://github.com/darrenhuai"><code>@​darrenhuai</code></a> in <a href="">pypa/virtualenv#3245</a></li>
<li>🐛 fix(create): keep pyvenv.cfg values on a single line by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3247</a></li>
<li>🔧 chore(test): add opt-in Atheris fuzz harness by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3246</a></li>
<li>📝 docs(readme): add OpenSSF Best Practices badge by <a href="https://github.com/gaborbernat"><code>@​gaborbernat</code></a> in <a href="">pypa/virtualenv#3248</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/pypa/virtualenv/compare/21.7.10...21.7.11">https://github.com/pypa/virtualenv/compare/21.7.10...21.7.11</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pypa/virtualenv/blob/main/docs/changelog.rst">virtualenv's changelog</a>.</em></p>
<blockquote>
<h1>Bugfixes - 21.7.12</h1>
<ul>
<li>Fix <code>activate.bat</code> running arbitrary commands from a crafted <code>--prompt</code>, <code>VIRTUALENV_PROMPT</code>, or config file
value. (:issue:<code>3250</code>)</li>
<li>Verify a downloaded seed wheel's sha256 against PyPI before seeding it into a virtual environment, skipped when a
custom pip index is configured. (:issue:<code>3251</code>)</li>
</ul>
<hr />
<p>v21.7.11 (2026-09-17)</p>
<hr />
<h1>Bugfixes - 21.7.11</h1>
<ul>
<li>Running <code>activate.bat</code> again before <code>deactivate</code> no longer makes <code>deactivate</code> leave the environment's
<code>PKG_CONFIG_PATH</code>, <code>TCL_LIBRARY</code> and <code>TK_LIBRARY</code> behind, or lose values the user had set before the first
activation - by :user:<code>darrenhuai</code>. (:issue:<code>3245</code>)</li>
<li>Write <code>pyvenv.cfg</code> values on a single line, so a prompt carrying a line boundary can no longer inject configuration.
<code>--prompt</code>, the <code>VIRTUALENV_PROMPT</code> environment variable and the config file all set the prompt, and
<code>pyvenv.cfg</code> has no escape syntax, so a newline, a carriage return, or any other boundary <code>str.splitlines</code>
recognizes, such as <code>U+2028</code>, started a new configuration line. Reading the file back picked up those lines as keys,
and since the last value for a key wins, they replaced anything written earlier, including <code>home</code>. (:issue:<code>3247</code>)</li>
</ul>
<h1>Improved Documentation - 21.7.11</h1>
<ul>
<li>Document the policy for AI-assisted contributions and the licensing rules for dependencies. (:issue:<code>3239</code>)</li>
</ul>
<h1>Misc - 21.7.11</h1>
<ul>
<li>:issue:<code>3238</code>, :issue:<code>3240</code>, :issue:<code>3241</code>, :issue:<code>3242</code>, :issue:<code>3243</code>, :issue:<code>3244</code>, :issue:<code>3246</code></li>
</ul>
<hr />
<p>v21.7.10 (2026-09-15)</p>
<hr />
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>9666b42</code></a> release 21.7.12</li>
<li><a href=""><code>a01ed3e</code></a> 🐛 fix(seed): verify downloaded wheel digests (<a href="">#3251</a>)</li>
<li><a href=""><code>d721ff1</code></a> 🐛 fix(activation): escape batch quote() against injection (<a href="">#3250</a>)</li>
<li><a href=""><code>087a2ef</code></a> 🔧 chore(changelog): drop dead CVE-2026-24049 fragment (<a href="">#3249</a>)</li>
<li><a href=""><code>73e352a</code></a> release 21.7.11</li>
<li><a href=""><code>68ee5a3</code></a> 📝 docs(readme): add OpenSSF Best Practices badge (<a href="">#3248</a>)</li>
<li><a href=""><code>787d1c9</code></a> 🔧 chore(test): add opt-in Atheris fuzz harness (<a href="">#3246</a>)</li>
<li><a href=""><code>a30f995</code></a> 🐛 fix(create): keep pyvenv.cfg values on a single line (<a href="">#3247</a>)</li>
<li><a href=""><code>469dd28</code></a> 🐛 fix(activation): undo a live activation before activate.bat saves values (#...</li>
<li><a href=""><code>a045a14</code></a> 👷 ci: run macOS jobs on macos-26 (<a href="">#3244</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/pypa/virtualenv/compare/21.7.10...21.7.12">compare view</a></li>
</ul>
</details>
<br />

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e3496624e64`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.