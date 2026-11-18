# Issue

**Title:** chore: bump the python-minor-patch group across 2 directories with 6 updates

## Description

Bumps the python-minor-patch group with 6 updates in the /backend directory:

| Package | From | To |
| --- | --- | --- |
| [flower](https://github.com/mher/flower) | `2.1.0` | `2.2.0` |
| [boto3](https://github.com/boto/boto3) | `1.43.98` | `1.43.103` |
| [resend](https://github.com/resendlabs/resend-python) | `2.46.0` | `2.47.0` |
| [google-auth](https://github.com/googleapis/google-cloud-python) | `2.58.0` | `2.58.1` |
| [ruff](https://github.com/astral-sh/ruff) | `0.16.8` | `0.16.9` |
| [ty](https://github.com/astral-sh/ty) | `0.0.82` | `0.0.84` |
| [ruff](https://github.com/astral-sh/ruff) | `0.16.8` | `0.16.9` |
| [ty](https://github.com/astral-sh/ty) | `0.0.82` | `0.0.84` |

Bumps the python-minor-patch group with 2 updates in the /mcp directory: [ruff](https://github.com/astral-sh/ruff) and [ty](https://github.com/astral-sh/ty).

Updates `flower` from 2.1.0 to 2.2.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/mher/flower/releases">flower's releases</a>.</em></p>
<blockquote>
<h2>v2.2.0</h2>
<h2>Security</h2>
<ul>
<li>Added CSRF protection for cookie-authenticated sessions</li>
<li>Added protection against cross-site state-changing requests</li>
<li>Added an OAuth state check to all login handlers</li>
<li>Restricted the post-login redirect to local paths</li>
<li>Enabled TLS certificate validation for the RabbitMQ management API</li>
<li>Escaped all table cells on the tasks and workers pages</li>
<li>Escaped load average values in the workers grid</li>
<li>Added <code>HttpOnly</code> and <code>SameSite</code> to session cookies</li>
<li>Added the <code>X-Content-Type-Options: nosniff</code> header</li>
<li>Limited CORS headers to the unauthenticated API</li>
<li>Served API error messages as plain text</li>
</ul>
<h2>Features</h2>
<ul>
<li>Added a logout link for OAuth sessions <a href="">#1074</a></li>
<li>Added a <code>timeout</code> option to the task apply API</li>
<li>Added a page size selector to the tasks page <a href="">#1518</a></li>
<li>Linked task names to a list of all tasks with that name</li>
<li>Linked the task counts on the workers page to the matching tasks</li>
<li>Honored the column order of the <code>tasks_columns</code> option <a href="">#1262</a></li>
<li>Added thousands separators to task counts <a href="">#1374</a></li>
<li>Formatted durations and showed a dash for missing values</li>
<li>Added search examples as placeholder text</li>
<li>Made wide tables scroll sideways and shortened UUIDs on mobile</li>
<li>Limited worker page task lists to 50 entries by default <a href="">#1087</a></li>
<li>Removed the Retried column from the workers page</li>
<li>Named browser tabs by page</li>
</ul>
<h2>Performance and reliability</h2>
<ul>
<li>Made persistent state saves atomic <a href="">#1403</a></li>
<li>Fixed startup failing on a corrupt persistent state database <a href="">#1398</a></li>
<li>Added a warning when state saving dominates the save interval</li>
<li>Reapplied <code>--max-tasks</code> to restored persistent state <a href="">#1380</a></li>
<li>Honored the <code>--purge-offline-workers</code> grace period after worker-offline events <a href="">#1190</a></li>
<li>Inspected a worker lazily on its first page visit <a href="">#1388</a></li>
<li>Fetched worker task lists only when inspecting a single worker</li>
<li>Validated the <code>--broker-api</code> URL at startup</li>
<li>Required both <code>--certfile</code> and <code>--keyfile</code> when either is set</li>
<li>Validated task API query parameters and publish payloads</li>
</ul>
<h2>Bug fixes</h2>
<ul>
<li>Fixed worker task table column widths <a href="">#1521</a> by <a href="https://github.com/ShubhAtWork"><code>@​ShubhAtWork</code></a></li>
<li>Fixed the default RabbitMQ management API URL to use the management port <a href="">#1232</a></li>
<li>Fixed the theme dropdown not closing and stuck navbar tooltips</li>
<li>Fixed a server error on the task page for tasks without a name</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4d4a9ac</code></a> Set release version</li>
<li><a href=""><code>b884844</code></a> Exclude compiled and hidden files from the sdist</li>
<li><a href=""><code>fba84ef</code></a> Merge remote-tracking branch 'origin/master' into 2.0</li>
<li><a href=""><code>ea34f92</code></a> Fix broken and moved links in the docs</li>
<li><a href=""><code>1336fbd</code></a> Fix the unpicklable state test on Python 3.10 to 3.13</li>
<li><a href=""><code>0f04846</code></a> Open the state shelves with context managers</li>
<li><a href=""><code>8034099</code></a> Apply the ruff style rewrites to the package</li>
<li><a href=""><code>b14b43d</code></a> Fix the ruff errors in the tests</li>
<li><a href=""><code>b9f7189</code></a> Apply ruff's safe fixes and literal rewrites to the package</li>
<li><a href=""><code>ff33bc8</code></a> Tidy the task API test bodies and name lookups</li>
<li>Additional commits viewable in <a href="https://github.com/mher/flower/compare/v2.1.0...v2.2.0">compare view</a></li>
</ul>
</details>
<br />

Updates `boto3` from 1.43.98 to 1.43.103
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0470368</code></a> Merge branch 'release-1.43.103'</li>
<li><a href=""><code>1b65309</code></a> Bumping version to 1.43.103</li>
<li><a href=""><code>655adc5</code></a> Add changelog entries from botocore</li>
<li><a href=""><code>da00dd2</code></a> Merge branch 'release-1.43.102'</li>
<li><a href=""><code>76d6266</code></a> Merge branch 'release-1.43.102' into develop</li>
<li><a href=""><code>551d660</code></a> Bumping version to 1.43.102</li>
<li><a href=""><code>f63e52e</code></a> Add changelog entries from botocore</li>
<li><a href=""><code>a1acf79</code></a> Merge branch 'release-1.43.101'</li>
<li><a href=""><code>931d5a2</code></a> Merge branch 'release-1.43.101' into develop</li>
<li><a href=""><code>8c719ef</code></a> Bumping version to 1.43.101</li>
<li>Additional commits viewable in <a href="https://github.com/boto/boto3/compare/1.43.98...1.43.103">compare view</a></li>
</ul>
</details>
<br />

Updates `resend` from 2.46.0 to 2.47.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/resendlabs/resend-python/releases">resend's releases</a>.</em></p>
<blockquote>
<h2>v2.47.0</h2>
<h2>What's Changed</h2>
<ul>
<li>feat(webhooks): add support for suppression.added/removed events by <a href="https://github.com/dielduarte"><code>@​dielduarte</code></a> in <a href="">resend/resend-python#287</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/resend/resend-python/compare/v2.46.0...v2.47.0">https://github.com/resend/resend-python/compare/v2.46.0...v2.47.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>390da5f</code></a> feat(webhooks): add support for suppression.added/removed events (<a href="">#287</a>)</li>
<li>See full diff in <a href="https://github.com/resendlabs/resend-python/compare/v2.46.0...v2.47.0">compare view</a></li>
</ul>
</details>
<br />

Updates `google-auth` from 2.58.0 to 2.58.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/googleapis/google-cloud-python/releases">google-auth's releases</a>.</em></p>
<blockquote>
<h2>google-auth: v2.58.1</h2>
<h2><a href="https://github.com/googleapis/google-cloud-python/compare/google-auth-v2.58.0...google-auth-v2.58.1">2.58.1</a> (2026-09-24)</h2>
<h3>Bug Fixes</h3>
<ul>
<li><strong>auth:</strong> allow mTLS retry when credentials raise NotImplementedError on refresh (<a href="">#18349</a>) (<a href="">1665e68</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>e654dc2</code></a> chore(main): release google-auth 2.58.1 (<a href="">#18462</a>)</li>
<li><a href=""><code>1665e68</code></a> fix(auth): allow mTLS retry when credentials raise NotImplementedError on ref...</li>
<li><a href=""><code>89310be</code></a> chore(main): release google-crc32c 1.9.0 (<a href="">#18459</a>)</li>
<li><a href=""><code>9cb21d0</code></a> fix: regenerate gencode with protobuf 6.33.5 (<a href="">#18461</a>)</li>
<li><a href=""><code>54f1019</code></a> feat: update API sources and regenerate (<a href="">#18446</a>)</li>
<li><a href=""><code>a04c831</code></a> feat(firestore): add BSONDecimal128 support (<a href="">#18395</a>)</li>
<li><a href=""><code>1bf979a</code></a> fix(crc32c): remove stale pypy reference from README (<a href="">#18458</a>)</li>
<li><a href=""><code>fdaa618</code></a> chore(crc32c): run manylinux wheel validation and upload in isolated Python 3...</li>
<li><a href=""><code>5fe1ef3</code></a> feat: add 3.15 support to gapic library classifiers (<a href="">#18450</a>)</li>
<li><a href=""><code>322c9bc</code></a> feat(firestore): add BSONRegex support (<a href="">#18394</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/googleapis/google-cloud-python/compare/google-auth-v2.58.0...google-auth-v2.58.1">compare view</a></li>
</ul>
</details>
<br />

Updates `ruff` from 0.16.8 to 0.16.9
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff/releases">ruff's releases</a>.</em></p>
<blockquote>
<h2>0.16.9</h2>
<h2>Release Notes</h2>
<p>Released on 2026-09-24.</p>
<h3>Preview features</h3>
<ul>
<li>[<code>ruff</code>] Avoid false positives for overloaded division (<code>RUF069</code>) (<a href="">#28309</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>[<code>flake8-bugbear</code>] Avoid false positives for calls with keyword arguments (<code>B009</code>, <code>B010</code>, <code>B043</code>) (<a href="">#28776</a>)</li>
<li>[<code>flake8-tidy-imports</code>] Allow lazy imports to be used in deferred annotations (<code>TID255</code>) (<a href="">#28767</a>)</li>
</ul>
<h3>Rule changes</h3>
<ul>
<li>Update LibCST-based fixes for Python 3.15 (<a href="">#28616</a>)</li>
<li>[<code>flake8-pyi</code>] Mention stubs in the diagnostic message (<code>PYI002</code>) (<a href="">#28542</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Fix horizontal overflow on the rules documentation page (<a href="">#28699</a>)</li>
<li>Update rules table with category information (<a href="">#28651</a>)</li>
<li>[<code>flake8-annotations</code>] Clarify that <code>ANN401</code> checks return types in addition to arguments (<a href="">#28334</a>)</li>
<li>[<code>flake8-bugbear</code>] Document type-checker interaction (<code>B010</code>) (<a href="">#28509</a>)</li>
<li>[<code>flake8-comprehensions</code>] Document <code>map</code>/generator exception behavior (<code>C417</code>) (<a href="">#27794</a>)</li>
<li>[<code>ruff</code>] Mention related isort settings (<code>RUF022</code>) (<a href="">#28719</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/qinpei-dev"><code>@​qinpei-dev</code></a></li>
<li><a href="https://github.com/sanjayrohith"><code>@​sanjayrohith</code></a></li>
<li><a href="https://github.com/ntBre"><code>@​ntBre</code></a></li>
<li><a href="https://github.com/webdevsamran"><code>@​webdevsamran</code></a></li>
<li><a href="https://github.com/zaniebot"><code>@​zaniebot</code></a></li>
<li><a href="https://github.com/ewdurbin"><code>@​ewdurbin</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
<li><a href="https://github.com/spaceone"><code>@​spaceone</code></a></li>
<li><a href="https://github.com/IbrahimKhan12"><code>@​IbrahimKhan12</code></a></li>
<li><a href="https://github.com/devtechedge"><code>@​devtechedge</code></a></li>
<li><a href="https://github.com/GruffElixir"><code>@​GruffElixir</code></a></li>
</ul>
<h2>Install ruff 0.16.9</h2>
<h3>Install prebuilt binaries via shell script</h3>
<pre lang="sh"><code>curl --proto '=https' --tlsv1.2 -LsSf https://releases.astral.sh/github/ruff/releases/download/0.16.9/ruff-installer.sh | sh
</code></pre>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff/blob/main/CHANGELOG.md">ruff's changelog</a>.</em></p>
<blockquote>
<h2>0.16.9</h2>
<p>Released on 2026-09-24.</p>
<h3>Preview features</h3>
<ul>
<li>[<code>ruff</code>] Avoid false positives for overloaded division (<code>RUF069</code>) (<a href="">#28309</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>[<code>flake8-bugbear</code>] Avoid false positives for calls with keyword arguments (<code>B009</code>, <code>B010</code>, <code>B043</code>) (<a href="">#28776</a>)</li>
<li>[<code>flake8-tidy-imports</code>] Allow lazy imports to be used in deferred annotations (<code>TID255</code>) (<a href="">#28767</a>)</li>
</ul>
<h3>Rule changes</h3>
<ul>
<li>Update LibCST-based fixes for Python 3.15 (<a href="">#28616</a>)</li>
<li>[<code>flake8-pyi</code>] Mention stubs in the diagnostic message (<code>PYI002</code>) (<a href="">#28542</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Fix horizontal overflow on the rules documentation page (<a href="">#28699</a>)</li>
<li>Update rules table with category information (<a href="">#28651</a>)</li>
<li>[<code>flake8-annotations</code>] Clarify that <code>ANN401</code> checks return types in addition to arguments (<a href="">#28334</a>)</li>
<li>[<code>flake8-bugbear</code>] Document type-checker interaction (<code>B010</code>) (<a href="">#28509</a>)</li>
<li>[<code>flake8-comprehensions</code>] Document <code>map</code>/generator exception behavior (<code>C417</code>) (<a href="">#27794</a>)</li>
<li>[<code>ruff</code>] Mention related isort settings (<code>RUF022</code>) (<a href="">#28719</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/qinpei-dev"><code>@​qinpei-dev</code></a></li>
<li><a href="https://github.com/sanjayrohith"><code>@​sanjayrohith</code></a></li>
<li><a href="https://github.com/ntBre"><code>@​ntBre</code></a></li>
<li><a href="https://github.com/webdevsamran"><code>@​webdevsamran</code></a></li>
<li><a href="https://github.com/zaniebot"><code>@​zaniebot</code></a></li>
<li><a href="https://github.com/ewdurbin"><code>@​ewdurbin</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
<li><a href="https://github.com/spaceone"><code>@​spaceone</code></a></li>
<li><a href="https://github.com/IbrahimKhan12"><code>@​IbrahimKhan12</code></a></li>
<li><a href="https://github.com/devtechedge"><code>@​devtechedge</code></a></li>
<li><a href="https://github.com/GruffElixir"><code>@​GruffElixir</code></a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0be08a2</code></a> Bump version to 0.16.9 (<a href="">#28882</a>)</li>
<li><a href=""><code>b4920b7</code></a> Rename <code>ruff_cli</code> to <code>ruff_command_line</code> (<a href="">#28881</a>)</li>
<li><a href=""><code>47c751b</code></a> Update dependency astral-sh/uv to v0.12.18 (<a href="">#28880</a>)</li>
<li><a href=""><code>8c244e5</code></a> [<code>flake8-comprehensions</code>] Document <code>map</code>/generator exception behavior (<code>C417</code>...</li>
<li><a href=""><code>5edf5a1</code></a> Use <code>target</code> form in <code>rooster.version_files</code> (<a href="">#28876</a>)</li>
<li><a href=""><code>915bb2b</code></a> [ty] Prefer existing @ paths over response files in Ruff and ty (<a href="">#28877</a>)</li>
<li><a href=""><code>4710e1a</code></a> ci(github): update version number in placeholder of issue template (<a href="">#28871</a>)</li>
<li><a href=""><code>eedfc62</code></a> [ty] Propagate outer type context through cast calls (<a href="">#28855</a>)</li>
<li><a href=""><code>ceaa6a0</code></a> [ty] Contain rendered code within Markdown fences (<a href="">#28869</a>)</li>
<li><a href=""><code>dba0f30</code></a> authorize ruff-pre-commit dispatch via OIDC (<a href="">#28867</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/ruff/compare/0.16.8...0.16.9">compare view</a></li>
</ul>
</details>
<br />

Updates `ty` from 0.0.82 to 0.0.84
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ty/releases">ty's releases</a>.</em></p>
<blockquote>
<h2>0.0.84</h2>
<h2>Release Notes</h2>
<p>Released on 2026-09-24.</p>
<p>This release addresses <a href="https://github.com/astral-sh/ty/security/advisories/GHSA-vxvm-j4xq-q7m4">GHSA-vxvm-j4xq-q7m4</a>, a use-after-free vulnerability during incremental type checking that can result in arbitrary code execution when analyzing a specially crafted Python project. Users who run ty on untrusted code should upgrade to 0.0.84 or newer.</p>
<h3>Bug fixes</h3>
<ul>
<li>Fix stale diagnostics from the LSP server after toggling <code>showSyntaxErrors</code> (<a href="">#28759</a>)</li>
</ul>
<h3>LSP server</h3>
<ul>
<li>Complete string keys from dictionary initializers (<a href="">#28820</a>)</li>
<li>Support LSP requests against closed documents (<a href="">#28595</a>)</li>
<li>Select projects for external files using import search paths (<a href="">#28594</a>)</li>
<li>Use workspace editor settings for external files (<a href="">#28639</a>)</li>
</ul>
<h3>Performance</h3>
<ul>
<li>Avoid repeated subtyping checks for materialized recursive protocols (<a href="">#28774</a>)</li>
<li>Skip reading notebooks when discovering scripts (<a href="">#28781</a>)</li>
</ul>
<h3>Core type checking</h3>
<ul>
<li>Avoid incorrect simplification of <code>TypeIs</code> materializations (<a href="">#28817</a>)</li>
<li>Fix disjointness of generic class types (<a href="">#28787</a>)</li>
<li>Fix staticmethod shadowing through generic receivers and unions (<a href="">#28766</a>)</li>
<li>Infer callable signatures from bounded type variables (<a href="">#28599</a>)</li>
<li>Infer constant membership in inline list and set literals (e.g. <code>&quot;foo&quot; in [&quot;foo&quot;]</code> is now inferred as <code>Literal[True]</code>) (<a href="">#28676</a>)</li>
<li>Infer through optional generic containers in the legacy solver (<a href="">#28791</a>)</li>
<li>Preserve call narrowing during cyclic inference (<a href="">#28708</a>)</li>
<li>Preserve intersections of type guard return types (<a href="">#28796</a>)</li>
<li>Use subtyping for constraint-set implication (<a href="">#28657</a>)</li>
</ul>
<h3>Configuration</h3>
<ul>
<li>Disable <code>invalid-legacy-positional-parameter</code> by default (<a href="">#28834</a>)</li>
</ul>
<h3>Other changes</h3>
<ul>
<li>Only consider reachable definitions when determining whether a condition should be exempted from <code>redundant-condition(-strict)</code> due to the condition being defined relative to <code>sys.version_info</code>, <code>sys.platform</code>, <code>os.name</code> or <code>typing.TYPE_CHECKING</code> (<a href="">#28788</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/ibraheemdev"><code>@​ibraheemdev</code></a></li>
<li><a href="https://github.com/zsol"><code>@​zsol</code></a></li>
<li><a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a></li>
<li><a href="https://github.com/lerebear"><code>@​lerebear</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ty/blob/main/CHANGELOG.md">ty's changelog</a>.</em></p>
<blockquote>
<h2>0.0.84</h2>
<p>Released on 2026-09-24.</p>
<p>This release addresses <a href="https://github.com/astral-sh/ty/security/advisories/GHSA-vxvm-j4xq-q7m4">GHSA-vxvm-j4xq-q7m4</a>, a use-after-free vulnerability during incremental type checking that can result in arbitrary code execution when analyzing a specially crafted Python project. Users who run ty on untrusted code should upgrade to 0.0.84 or newer.</p>
<h3>Bug fixes</h3>
<ul>
<li>Fix stale diagnostics from the LSP server after toggling <code>showSyntaxErrors</code> (<a href="">#28759</a>)</li>
</ul>
<h3>LSP server</h3>
<ul>
<li>Complete string keys from dictionary initializers (<a href="">#28820</a>)</li>
<li>Support LSP requests against closed documents (<a href="">#28595</a>)</li>
<li>Select projects for external files using import search paths (<a href="">#28594</a>)</li>
<li>Use workspace editor settings for external files (<a href="">#28639</a>)</li>
</ul>
<h3>Performance</h3>
<ul>
<li>Avoid repeated subtyping checks for materialized recursive protocols (<a href="">#28774</a>)</li>
<li>Skip reading notebooks when discovering scripts (<a href="">#28781</a>)</li>
</ul>
<h3>Core type checking</h3>
<ul>
<li>Avoid incorrect simplification of <code>TypeIs</code> materializations (<a href="">#28817</a>)</li>
<li>Fix disjointness of generic class types (<a href="">#28787</a>)</li>
<li>Fix staticmethod shadowing through generic receivers and unions (<a href="">#28766</a>)</li>
<li>Infer callable signatures from bounded type variables (<a href="">#28599</a>)</li>
<li>Infer constant membership in inline list and set literals (e.g. <code>&quot;foo&quot; in [&quot;foo&quot;]</code> is now inferred as <code>Literal[True]</code>) (<a href="">#28676</a>)</li>
<li>Infer through optional generic containers in the legacy solver (<a href="">#28791</a>)</li>
<li>Preserve call narrowing during cyclic inference (<a href="">#28708</a>)</li>
<li>Preserve intersections of type guard return types (<a href="">#28796</a>)</li>
<li>Use subtyping for constraint-set implication (<a href="">#28657</a>)</li>
</ul>
<h3>Configuration</h3>
<ul>
<li>Disable <code>invalid-legacy-positional-parameter</code> by default (<a href="">#28834</a>)</li>
</ul>
<h3>Other changes</h3>
<ul>
<li>Only consider reachable definitions when determining whether a condition should be exempted from <code>redundant-condition(-strict)</code> due to the condition being defined relative to <code>sys.version_info</code>, <code>sys.platform</code>, <code>os.name</code> or <code>typing.TYPE_CHECKING</code> (<a href="">#28788</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/ibraheemdev"><code>@​ibraheemdev</code></a></li>
<li><a href="https://github.com/zsol"><code>@​zsol</code></a></li>
<li><a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a></li>
<li><a href="https://github.com/lerebear"><code>@​lerebear</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
<li><a href="https://github.com/ewdurbin"><code>@​ewdurbin</code></a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8dd9a7f</code></a> Bump version to 0.0.84 (<a href="">#4585</a>)</li>
<li><a href=""><code>d4e4bf9</code></a> publish to astral-sh/versions via OIDC (<a href="">#4581</a>)</li>
<li><a href=""><code>94ce733</code></a> use oidc issued token for docs publication (<a href="">#4579</a>)</li>
<li><a href=""><code>901eeaa</code></a> Update prek dependencies (<a href="">#4576</a>)</li>
<li><a href=""><code>09bf0b1</code></a> Update docker/setup-buildx-action action to v4.3.0 (<a href="">#4575</a>)</li>
<li><a href=""><code>89d6ffe</code></a> Update astral-sh/setup-uv action to v10.2.0 (<a href="">#4574</a>)</li>
<li><a href=""><code>9c21479</code></a> Bump version to 0.0.83 (<a href="">#4569</a>)</li>
<li><a href=""><code>04c6911</code></a> Sync the ty security mirror (<a href="">#4549</a>)</li>
<li><a href=""><code>3fa57a2</code></a> Grant the versions workflow repository read access (<a href="">#4550</a>)</li>
<li><a href=""><code>a15b353</code></a> use scoped token for release workflow (<a href="">#4506</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/ty/compare/0.0.82...0.0.84">compare view</a></li>
</ul>
</details>
<br />

Updates `ruff` from 0.16.8 to 0.16.9
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff/releases">ruff's releases</a>.</em></p>
<blockquote>
<h2>0.16.9</h2>
<h2>Release Notes</h2>
<p>Released on 2026-09-24.</p>
<h3>Preview features</h3>
<ul>
<li>[<code>ruff</code>] Avoid false positives for overloaded division (<code>RUF069</code>) (<a href="">#28309</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>[<code>flake8-bugbear</code>] Avoid false positives for calls with keyword arguments (<code>B009</code>, <code>B010</code>, <code>B043</code>) (<a href="">#28776</a>)</li>
<li>[<code>flake8-tidy-imports</code>] Allow lazy imports to be used in deferred annotations (<code>TID255</code>) (<a href="">#28767</a>)</li>
</ul>
<h3>Rule changes</h3>
<ul>
<li>Update LibCST-based fixes for Python 3.15 (<a href="">#28616</a>)</li>
<li>[<code>flake8-pyi</code>] Mention stubs in the diagnostic message (<code>PYI002</code>) (<a href="">#28542</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Fix horizontal overflow on the rules documentation page (<a href="">#28699</a>)</li>
<li>Update rules table with category information (<a href="">#28651</a>)</li>
<li>[<code>flake8-annotations</code>] Clarify that <code>ANN401</code> checks return types in addition to arguments (<a href="">#28334</a>)</li>
<li>[<code>flake8-bugbear</code>] Document type-checker interaction (<code>B010</code>) (<a href="">#28509</a>)</li>
<li>[<code>flake8-comprehensions</code>] Document <code>map</code>/generator exception behavior (<code>C417</code>) (<a href="">#27794</a>)</li>
<li>[<code>ruff</code>] Mention related isort settings (<code>RUF022</code>) (<a href="">#28719</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/qinpei-dev"><code>@​qinpei-dev</code></a></li>
<li><a href="https://github.com/sanjayrohith"><code>@​sanjayrohith</code></a></li>
<li><a href="https://github.com/ntBre"><code>@​ntBre</code></a></li>
<li><a href="https://github.com/webdevsamran"><code>@​webdevsamran</code></a></li>
<li><a href="https://github.com/zaniebot"><code>@​zaniebot</code></a></li>
<li><a href="https://github.com/ewdurbin"><code>@​ewdurbin</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
<li><a href="https://github.com/spaceone"><code>@​spaceone</code></a></li>
<li><a href="https://github.com/IbrahimKhan12"><code>@​IbrahimKhan12</code></a></li>
<li><a href="https://github.com/devtechedge"><code>@​devtechedge</code></a></li>
<li><a href="https://github.com/GruffElixir"><code>@​GruffElixir</code></a></li>
</ul>
<h2>Install ruff 0.16.9</h2>
<h3>Install prebuilt binaries via shell script</h3>
<pre lang="sh"><code>curl --proto '=https' --tlsv1.2 -LsSf https://releases.astral.sh/github/ruff/releases/download/0.16.9/ruff-installer.sh | sh
</code></pre>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff/blob/main/CHANGELOG.md">ruff's changelog</a>.</em></p>
<blockquote>
<h2>0.16.9</h2>
<p>Released on 2026-09-24.</p>
<h3>Preview features</h3>
<ul>
<li>[<code>ruff</code>] Avoid false positives for overloaded division (<code>RUF069</code>) (<a href="">#28309</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>[<code>flake8-bugbear</code>] Avoid false positives for calls with keyword arguments (<code>B009</code>, <code>B010</code>, <code>B043</code>) (<a href="">#28776</a>)</li>
<li>[<code>flake8-tidy-imports</code>] Allow lazy imports to be used in deferred annotations (<code>TID255</code>) (<a href="">#28767</a>)</li>
</ul>
<h3>Rule changes</h3>
<ul>
<li>Update LibCST-based fixes for Python 3.15 (<a href="">#28616</a>)</li>
<li>[<code>flake8-pyi</code>] Mention stubs in the diagnostic message (<code>PYI002</code>) (<a href="">#28542</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Fix horizontal overflow on the rules documentation page (<a href="">#28699</a>)</li>
<li>Update rules table with category information (<a href="">#28651</a>)</li>
<li>[<code>flake8-annotations</code>] Clarify that <code>ANN401</code> checks return types in addition to arguments (<a href="">#28334</a>)</li>
<li>[<code>flake8-bugbear</code>] Document type-checker interaction (<code>B010</code>) (<a href="">#28509</a>)</li>
<li>[<code>flake8-comprehensions</code>] Document <code>map</code>/generator exception behavior (<code>C417</code>) (<a href="">#27794</a>)</li>
<li>[<code>ruff</code>] Mention related isort settings (<code>RUF022</code>) (<a href="">#28719</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/qinpei-dev"><code>@​qinpei-dev</code></a></li>
<li><a href="https://github.com/sanjayrohith"><code>@​sanjayrohith</code></a></li>
<li><a href="https://github.com/ntBre"><code>@​ntBre</code></a></li>
<li><a href="https://github.com/webdevsamran"><code>@​webdevsamran</code></a></li>
<li><a href="https://github.com/zaniebot"><code>@​zaniebot</code></a></li>
<li><a href="https://github.com/ewdurbin"><code>@​ewdurbin</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
<li><a href="https://github.com/spaceone"><code>@​spaceone</code></a></li>
<li><a href="https://github.com/IbrahimKhan12"><code>@​IbrahimKhan12</code></a></li>
<li><a href="https://github.com/devtechedge"><code>@​devtechedge</code></a></li>
<li><a href="https://github.com/GruffElixir"><code>@​GruffElixir</code></a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0be08a2</code></a> Bump version to 0.16.9 (<a href="">#28882</a>)</li>
<li><a href=""><code>b4920b7</code></a> Rename <code>ruff_cli</code> to <code>ruff_command_line</code> (<a href="">#28881</a>)</li>
<li><a href=""><code>47c751b</code></a> Update dependency astral-sh/uv to v0.12.18 (<a href="">#28880</a>)</li>
<li><a href=""><code>8c244e5</code></a> [<code>flake8-comprehensions</code>] Document <code>map</code>/generator exception behavior (<code>C417</code>...</li>
<li><a href=""><code>5edf5a1</code></a> Use <code>target</code> form in <code>rooster.version_files</code> (<a href="">#28876</a>)</li>
<li><a href=""><code>915bb2b</code></a> [ty] Prefer existing @ paths over response files in Ruff and ty (<a href="">#28877</a>)</li>
<li><a href=""><code>4710e1a</code></a> ci(github): update version number in placeholder of issue template (<a href="">#28871</a>)</li>
<li><a href=""><code>eedfc62</code></a> [ty] Propagate outer type context through cast calls (<a href="">#28855</a>)</li>
<li><a href=""><code>ceaa6a0</code></a> [ty] Contain rendered code within Markdown fences (<a href="">#28869</a>)</li>
<li><a href=""><code>dba0f30</code></a> authorize ruff-pre-commit dispatch via OIDC (<a href="">#28867</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/ruff/compare/0.16.8...0.16.9">compare view</a></li>
</ul>
</details>
<br />

Updates `ty` from 0.0.82 to 0.0.84
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ty/releases">ty's releases</a>.</em></p>
<blockquote>
<h2>0.0.84</h2>
<h2>Release Notes</h2>
<p>Released on 2026-09-24.</p>
<p>This release addresses <a href="https://github.com/astral-sh/ty/security/advisories/GHSA-vxvm-j4xq-q7m4">GHSA-vxvm-j4xq-q7m4</a>, a use-after-free vulnerability during incremental type checking that can result in arbitrary code execution when analyzing a specially crafted Python project. Users who run ty on untrusted code should upgrade to 0.0.84 or newer.</p>
<h3>Bug fixes</h3>
<ul>
<li>Fix stale diagnostics from the LSP server after toggling <code>showSyntaxErrors</code> (<a href="">#28759</a>)</li>
</ul>
<h3>LSP server</h3>
<ul>
<li>Complete string keys from dictionary initializers (<a href="">#28820</a>)</li>
<li>Support LSP requests against closed documents (<a href="">#28595</a>)</li>
<li>Select projects for external files using import search paths (<a href="">#28594</a>)</li>
<li>Use workspace editor settings for external files (<a href="">#28639</a>)</li>
</ul>
<h3>Performance</h3>
<ul>
<li>Avoid repeated subtyping checks for materialized recursive protocols (<a href="">#28774</a>)</li>
<li>Skip reading notebooks when discovering scripts (<a href="">#28781</a>)</li>
</ul>
<h3>Core type checking</h3>
<ul>
<li>Avoid incorrect simplification of <code>TypeIs</code> materializations (<a href="">#28817</a>)</li>
<li>Fix disjointness of generic class types (<a href="">#28787</a>)</li>
<li>Fix staticmethod shadowing through generic receivers and unions (<a href="">#28766</a>)</li>
<li>Infer callable signatures from bounded type variables (<a href="">#28599</a>)</li>
<li>Infer constant membership in inline list and set literals (e.g. <code>&quot;foo&quot; in [&quot;foo&quot;]</code> is now inferred as <code>Literal[True]</code>) (<a href="">#28676</a>)</li>
<li>Infer through optional generic containers in the legacy solver (<a href="">#28791</a>)</li>
<li>Preserve call narrowing during cyclic inference (<a href="">#28708</a>)</li>
<li>Preserve intersections of type guard return types (<a href="">#28796</a>)</li>
<li>Use subtyping for constraint-set implication (<a href="">#28657</a>)</li>
</ul>
<h3>Configuration</h3>
<ul>
<li>Disable <code>invalid-legacy-positional-parameter</code> by default (<a href="">#28834</a>)</li>
</ul>
<h3>Other changes</h3>
<ul>
<li>Only consider reachable definitions when determining whether a condition should be exempted from <code>redundant-condition(-strict)</code> due to the condition being defined relative to <code>sys.version_info</code>, <code>sys.platform</code>, <code>os.name</code> or <code>typing.TYPE_CHECKING</code> (<a href="">#28788</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/ibraheemdev"><code>@​ibraheemdev</code></a></li>
<li><a href="https://github.com/zsol"><code>@​zsol</code></a></li>
<li><a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a></li>
<li><a href="https://github.com/lerebear"><code>@​lerebear</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ty/blob/main/CHANGELOG.md">ty's changelog</a>.</em></p>
<blockquote>
<h2>0.0.84</h2>
<p>Released on 2026-09-24.</p>
<p>This release addresses <a href="https://github.com/astral-sh/ty/security/advisories/GHSA-vxvm-j4xq-q7m4">GHSA-vxvm-j4xq-q7m4</a>, a use-after-free vulnerability during incremental type checking that can result in arbitrary code execution when analyzing a specially crafted Python project. Users who run ty on untrusted code should upgrade to 0.0.84 or newer.</p>
<h3>Bug fixes</h3>
<ul>
<li>Fix stale diagnostics from the LSP server after toggling <code>showSyntaxErrors</code> (<a href="">#28759</a>)</li>
</ul>
<h3>LSP server</h3>
<ul>
<li>Complete string keys from dictionary initializers (<a href="">#28820</a>)</li>
<li>Support LSP requests against closed documents (<a href="">#28595</a>)</li>
<li>Select projects for external files using import search paths (<a href="">#28594</a>)</li>
<li>Use workspace editor settings for external files (<a href="">#28639</a>)</li>
</ul>
<h3>Performance</h3>
<ul>
<li>Avoid repeated subtyping checks for materialized recursive protocols (<a href="">#28774</a>)</li>
<li>Skip reading notebooks when discovering scripts (<a href="">#28781</a>)</li>
</ul>
<h3>Core type checking</h3>
<ul>
<li>Avoid incorrect simplification of <code>TypeIs</code> materializations (<a href="">#28817</a>)</li>
<li>Fix disjointness of generic class types (<a href="">#28787</a>)</li>
<li>Fix staticmethod shadowing through generic receivers and unions (<a href="">#28766</a>)</li>
<li>Infer callable signatures from bounded type variables (<a href="">#28599</a>)</li>
<li>Infer constant membership in inline list and set literals (e.g. <code>&quot;foo&quot; in [&quot;foo&quot;]</code> is now inferred as <code>Literal[True]</code>) (<a href="">#28676</a>)</li>
<li>Infer through optional generic containers in the legacy solver (<a href="">#28791</a>)</li>
<li>Preserve call narrowing during cyclic inference (<a href="">#28708</a>)</li>
<li>Preserve intersections of type guard return types (<a href="">#28796</a>)</li>
<li>Use subtyping for constraint-set implication (<a href="">#28657</a>)</li>
</ul>
<h3>Configuration</h3>
<ul>
<li>Disable <code>invalid-legacy-positional-parameter</code> by default (<a href="">#28834</a>)</li>
</ul>
<h3>Other changes</h3>
<ul>
<li>Only consider reachable definitions when determining whether a condition should be exempted from <code>redundant-condition(-strict)</code> due to the condition being defined relative to <code>sys.version_info</code>, <code>sys.platform</code>, <code>os.name</code> or <code>typing.TYPE_CHECKING</code> (<a href="">#28788</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/ibraheemdev"><code>@​ibraheemdev</code></a></li>
<li><a href="https://github.com/zsol"><code>@​zsol</code></a></li>
<li><a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a></li>
<li><a href="https://github.com/lerebear"><code>@​lerebear</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
<li><a href="https://github.com/ewdurbin"><code>@​ewdurbin</code></a></li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8dd9a7f</code></a> Bump version to 0.0.84 (<a href="">#4585</a>)</li>
<li><a href=""><code>d4e4bf9</code></a> publish to astral-sh/versions via OIDC (<a href="">#4581</a>)</li>
<li><a href=""><code>94ce733</code></a> use oidc issued token for docs publication (<a href="">#4579</a>)</li>
<li><a href=""><code>901eeaa</code></a> Update prek dependencies (<a href="">#4576</a>)</li>
<li><a href=""><code>09bf0b1</code></a> Update docker/setup-buildx-action action to v4.3.0 (<a href="">#4575</a>)</li>
<li><a href=""><code>89d6ffe</code></a> Update astral-sh/setup-uv action to v10.2.0 (<a href="">#4574</a>)</li>
<li><a href=""><code>9c21479</code></a> Bump version to 0.0.83 (<a href="">#4569</a>)</li>
<li><a href=""><code>04c6911</code></a> Sync the ty security mirror (<a href="">#4549</a>)</li>
<li><a href=""><code>3fa57a2</code></a> Grant the versions workflow repository read access (<a href="">#4550</a>)</li>
<li><a href=""><code>a15b353</code></a> use scoped token for release workflow (<a href="">#4506</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/ty/compare/0.0.82...0.0.84">compare view</a></li>
</ul>
</details>
<br />

Updates `ruff` from 0.16.8 to 0.16.9
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff/releases">ruff's releases</a>.</em></p>
<blockquote>
<h2>0.16.9</h2>
<h2>Release Notes</h2>
<p>Released on 2026-09-24.</p>
<h3>Preview features</h3>
<ul>
<li>[<code>ruff</code>] Avoid false positives for overloaded division (<code>RUF069</code>) (<a href="">#28309</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>[<code>flake8-bugbear</code>] Avoid false positives for calls with keyword arguments (<code>B009</code>, <code>B010</code>, <code>B043</code>) (<a href="">#28776</a>)</li>
<li>[<code>flake8-tidy-imports</code>] Allow lazy imports to be used in deferred annotations (<code>TID255</code>) (<a href="">#28767</a>)</li>
</ul>
<h3>Rule changes</h3>
<ul>
<li>Update LibCST-based fixes for Python 3.15 (<a href="">#28616</a>)</li>
<li>[<code>flake8-pyi</code>] Mention stubs in the diagnostic message (<code>PYI002</code>) (<a href="">#28542</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Fix horizontal overflow on the rules documentation page (<a href="">#28699</a>)</li>
<li>Update rules table with category information (<a href="">#28651</a>)</li>
<li>[<code>flake8-annotations</code>] Clarify that <code>ANN401</code> checks return types in addition to arguments (<a href="">#28334</a>)</li>
<li>[<code>flake8-bugbear</code>] Document type-checker interaction (<code>B010</code>) (<a href="">#28509</a>)</li>
<li>[<code>flake8-comprehensions</code>] Document <code>map</code>/generator exception behavior (<code>C417</code>) (<a href="">#27794</a>)</li>
<li>[<code>ruff</code>] Mention related isort settings (<code>RUF022</code>) (<a href="">#28719</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/qinpei-dev"><code>@​qinpei-dev</code></a></li>
<li><a href="https://github.com/sanjayrohith"><code>@​sanjayrohith</code></a></li>
<li><a href="https://github.com/ntBre"><code>@​ntBre</code></a></li>
<li><a href="https://github.com/webdevsamran"><code>@​webdevsamran</code></a></li>
<li><a href="https://github.com/zaniebot"><code>@​zaniebot</code></a></li>
<li><a href="https://github.com/ewdurbin"><code>@​ewdurbin</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
<li><a href="https://github.com/spaceone"><code>@​spaceone</code></a></li>
<li><a href="https://github.com/IbrahimKhan12"><code>@​IbrahimKhan12</code></a></li>
<li><a href="https://github.com/devtechedge"><code>@​devtechedge</code></a></li>
<li><a href="https://github.com/GruffElixir"><code>@​GruffElixir</code></a></li>
</ul>
<h2>Install ruff 0.16.9</h2>
<h3>Install prebuilt binaries via shell script</h3>
<pre lang="sh"><code>curl --proto '=https' --tlsv1.2 -LsSf https://releases.astral.sh/github/ruff/releases/download/0.16.9/ruff-installer.sh | sh
</code></pre>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff/blob/main/CHANGELOG.md">ruff's changelog</a>.</em></p>
<blockquote>
<h2>0.16.9</h2>
<p>Released on 2026-09-24.</p>
<h3>Preview features</h3>
<ul>
<li>[<code>ruff</code>] Avoid false positives for overloaded division (<code>RUF069</code>) (<a href="">#28309</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>[<code>flake8-bugbear</code>] Avoid false positives for calls with keyword arguments (<code>B009</code>, <code>B010</code>, <code>B043</code>) (<a href="">#28776</a>)</li>
<li>[<code>flake8-tidy-imports</code>] Allow lazy imports to be used in deferred annotations (<code>TID255</code>) (<a href="">#28767</a>)</li>
</ul>
<h3>Rule changes</h3>
<ul>
<li>Update LibCST-based fixes for Python 3.15 (<a href="">#28616</a>)</li>
<li>[<code>flake8-pyi</code>] Mention stubs in the diagnostic message (<code>PYI002</code>) (<a href="">#28542</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>Fix horizontal overflow on the rules documentation page (<a href="">#28699</a>)</li>
<li>Update rules table with category information (<a href="">#28651</a>)</li>
<li>[<code>flake8-annotations</code>] Clarify that <code>ANN401</code> checks return types in addition to arguments (<a href="">#28334</a>)</li>
<li>[<code>flake8-bugbear</code>] Document type-checker interaction (<code>B010</code>) (<a href="">#28509</a>)</li>
<li>[<code>flake8-comprehensions</code>] Document <code>map</code>/generator exception behavior (<code>C417</code>) (<a href="">#27794</a>)</li>
<li>[<code>ruff</code>] Mention related isort settings (<code>RUF022</code>) (<a href="">#28719</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/qinpei-dev"><code>@​qinpei-dev</code></a></li>
<li><a href="https://github.com/sanjayrohith"><code>@​sanjayrohith</code></a></li>
<li><a href="https://github.com/ntBre"><code>@​ntBre</code></a></li>
<li><a href="https://github.com/webdevsamran"><code>@​webdevsamran</code></a></li>
<li><a href="https://github.com/zaniebot"><code>@​zaniebot</code></a></li>
<li><a href="https://github.com/ewdurbin"><code>@​ewdurbin</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
<li><a href="https://github.com/spaceone"><code>@​spaceone</code></a></li>
<li><a href="https://github.com/IbrahimKhan12"><code>@​IbrahimKhan12</code></a></li>
<li><a href="https://github.com/devtechedge"><code>@​devtechedge</code></a></li>
<li><a href="https://github.com/GruffElixir"><code>@​GruffElixir</code></a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>0be08a2</code></a> Bump version to 0.16.9 (<a href="">#28882</a>)</li>
<li><a href=""><code>b4920b7</code></a> Rename <code>ruff_cli</code> to <code>ruff_command_line</code> (<a href="">#28881</a>)</li>
<li><a href=""><code>47c751b</code></a> Update dependency astral-sh/uv to v0.12.18 (<a href="">#28880</a>)</li>
<li><a href=""><code>8c244e5</code></a> [<code>flake8-comprehensions</code>] Document <code>map</code>/generator exception behavior (<code>C417</code>...</li>
<li><a href=""><code>5edf5a1</code></a> Use <code>target</code> form in <code>rooster.version_files</code> (<a href="">#28876</a>)</li>
<li><a href=""><code>915bb2b</code></a> [ty] Prefer existing @ paths over response files in Ruff and ty (<a href="">#28877</a>)</li>
<li><a href=""><code>4710e1a</code></a> ci(github): update version number in placeholder of issue template (<a href="">#28871</a>)</li>
<li><a href=""><code>eedfc62</code></a> [ty] Propagate outer type context through cast calls (<a href="">#28855</a>)</li>
<li><a href=""><code>ceaa6a0</code></a> [ty] Contain rendered code within Markdown fences (<a href="">#28869</a>)</li>
<li><a href=""><code>dba0f30</code></a> authorize ruff-pre-commit dispatch via OIDC (<a href="">#28867</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/ruff/compare/0.16.8...0.16.9">compare view</a></li>
</ul>
</details>
<br />

Updates `ty` from 0.0.82 to 0.0.84
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ty/releases">ty's releases</a>.</em></p>
<blockquote>
<h2>0.0.84</h2>
<h2>Release Notes</h2>
<p>Released on 2026-09-24.</p>
<p>This release addresses <a href="https://github.com/astral-sh/ty/security/advisories/GHSA-vxvm-j4xq-q7m4">GHSA-vxvm-j4xq-q7m4</a>, a use-after-free vulnerability during incremental type checking that can result in arbitrary code execution when analyzing a specially crafted Python project. Users who run ty on untrusted code should upgrade to 0.0.84 or newer.</p>
<h3>Bug fixes</h3>
<ul>
<li>Fix stale diagnostics from the LSP server after toggling <code>showSyntaxErrors</code> (<a href="">#28759</a>)</li>
</ul>
<h3>LSP server</h3>
<ul>
<li>Complete string keys from dictionary initializers (<a href="">#28820</a>)</li>
<li>Support LSP requests against closed documents (<a href="">#28595</a>)</li>
<li>Select projects for external files using import search paths (<a href="">#28594</a>)</li>
<li>Use workspace editor settings for external files (<a href="">#28639</a>)</li>
</ul>
<h3>Performance</h3>
<ul>
<li>Avoid repeated subtyping checks for materialized recursive protocols (<a href="">#28774</a>)</li>
<li>Skip reading notebooks when discovering scripts (<a href="">#28781</a>)</li>
</ul>
<h3>Core type checking</h3>
<ul>
<li>Avoid incorrect simplification of <co...

_Description has been truncated_

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0009f2f8e7a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.