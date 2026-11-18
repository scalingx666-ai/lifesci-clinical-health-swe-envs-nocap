# Issue

**Title:** chore: bump the python-minor-patch group across 2 directories with 15 updates

## Description

Bumps the python-minor-patch group with 14 updates in the /backend directory:

| Package | From | To |
| --- | --- | --- |
| [cryptography](https://github.com/pyca/cryptography) | `50.0.1` | `50.0.2` |
| [pydantic-settings](https://github.com/pydantic/pydantic-settings) | `2.15.0` | `2.16.0` |
| [sqlalchemy](https://github.com/sqlalchemy/sqlalchemy) | `2.0.54` | `2.1.4` |
| [fastapi](https://github.com/fastapi/fastapi) | `0.143.1` | `0.143.5` |
| [boto3](https://github.com/boto/boto3) | `1.43.103` | `1.43.115` |
| [resend](https://github.com/resendlabs/resend-python) | `2.47.0` | `2.49.1` |
| [svix](https://github.com/svix/svix-webhooks) | `2.5.0` | `2.8.0` |
| [numpy](https://github.com/numpy/numpy) | `2.5.3` | `2.5.4` |
| [faker](https://github.com/joke2k/faker) | `40.39.0` | `40.43.0` |
| [google-auth](https://github.com/googleapis/google-cloud-python) | `2.58.1` | `2.62.0` |
| [opentelemetry-exporter-otlp-proto-http](https://github.com/open-telemetry/opentelemetry-python) | `1.45.0` | `1.45.1` |
| [pre-commit](https://github.com/pre-commit/pre-commit) | `4.6.2` | `4.7.0` |
| [ruff](https://github.com/astral-sh/ruff) | `0.16.9` | `0.17.1` |
| [ty](https://github.com/astral-sh/ty) | `0.0.84` | `0.0.89` |
| [pydantic-settings](https://github.com/pydantic/pydantic-settings) | `2.15.0` | `2.16.0` |
| [pre-commit](https://github.com/pre-commit/pre-commit) | `4.6.2` | `4.7.0` |
| [ruff](https://github.com/astral-sh/ruff) | `0.16.9` | `0.17.1` |
| [ty](https://github.com/astral-sh/ty) | `0.0.84` | `0.0.89` |

Bumps the python-minor-patch group with 5 updates in the /mcp directory:

| Package | From | To |
| --- | --- | --- |
| [pydantic-settings](https://github.com/pydantic/pydantic-settings) | `2.15.0` | `2.16.0` |
| [pre-commit](https://github.com/pre-commit/pre-commit) | `4.6.2` | `4.7.0` |
| [ruff](https://github.com/astral-sh/ruff) | `0.16.9` | `0.17.1` |
| [ty](https://github.com/astral-sh/ty) | `0.0.84` | `0.0.89` |
| [pydantic](https://github.com/pydantic/pydantic) | `2.13.5` | `2.14.1` |
| [pydantic-settings](https://github.com/pydantic/pydantic-settings) | `2.15.0` | `2.16.0` |
| [pre-commit](https://github.com/pre-commit/pre-commit) | `4.6.2` | `4.7.0` |
| [ruff](https://github.com/astral-sh/ruff) | `0.16.9` | `0.17.1` |
| [ty](https://github.com/astral-sh/ty) | `0.0.84` | `0.0.89` |

Updates `cryptography` from 50.0.1 to 50.0.2
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pyca/cryptography/blob/main/CHANGELOG.rst">cryptography's changelog</a>.</em></p>
<blockquote>
<p>50.0.2 - 2026-09-30</p>
<pre><code>
* Updated Windows, macOS, and Linux wheels to be compiled with OpenSSL 4.0.3.
* Added ``abi3.abi3t`` wheels for free-threaded CPython 3.15 and later.
* Updated to PyO3 0.29.2, which fixes building ``cryptography`` on Cygwin and
  MSYS2.
<p>.. _v50-0-1:
</code></pre></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4dda5c7</code></a> [50.0.x] Bump for 50.0.2 release + changelog (<a href="">#15733</a>)</li>
<li><a href=""><code>70c881c</code></a> [50.0.x] Bump pyo3 to 0.29.2 (<a href="">#15731</a>)</li>
<li><a href=""><code>a8c45c4</code></a> [50.0.x] Build abi3.abi3t wheels for CPython 3.15+ (<a href="">#15496</a>) (<a href="">#15732</a>)</li>
<li>See full diff in <a href="https://github.com/pyca/cryptography/compare/50.0.1...50.0.2">compare view</a></li>
</ul>
</details>
<br />

Updates `pydantic-settings` from 2.15.0 to 2.16.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pydantic/pydantic-settings/releases">pydantic-settings's releases</a>.</em></p>
<blockquote>
<h2>v2.16.0</h2>
<h2>Highlights</h2>
<h3>Breaking changes and behavior changes</h3>
<ul>
<li><strong>Python 3.10 is no longer supported</strong> (<a href="">#1003</a>). pydantic-settings now requires Python 3.11+, since 3.10 reaches end of life this month. The <code>tomli</code> fallback is gone in favor of stdlib <code>tomllib</code>; the <code>toml</code> extra is kept as an empty extra so <code>pip install pydantic-settings[toml]</code> keeps working.</li>
<li><strong><code>python-dotenv&gt;=1.2.2</code> is now required</strong> (<a href="">#971</a>) to pick up the fix for CVE-2026-28684.</li>
<li><strong>Aliases are ignored in every source when <code>validate_by_alias=False</code></strong> (<a href="">#1033</a>). Env vars, secrets, CLI flags and defaults now use only field names, matching pydantic. An env var named after the alias is now ignored instead of raising <code>extra_forbidden</code>, and the CLI exposes <code>--apple</code> rather than <code>--pomo</code>.</li>
<li><strong><code>validation_alias</code> takes precedence over <code>alias</code></strong> (<a href="">#1038</a>). When the two differ, values from JSON/YAML/TOML files and the CLI were silently ignored; they now load. CLI help lists the <code>validation_alias</code> flag first, and <code>CliApp.serialize</code> emits it.</li>
<li><strong>CLI case-insensitivity only lowercases registered options</strong> (<a href="">#1036</a>). With <code>case_sensitive=False</code>, args after <code>--</code> and those captured by <code>CliUnknownArgs</code> keep their case (<code>-Xmx4G</code> no longer becomes <code>-xmx4g</code>). Unrecognized options are now reported as typed (<code>--NOPE</code> instead of <code>--nope</code>).</li>
<li><strong>JSON and YAML config files are read as UTF-8 by default</strong> (<a href="">#955</a>) instead of the locale encoding, completing the secrets-file fix from 2.15.0. <code>json_file_encoding</code>/<code>yaml_file_encoding</code> still override it.</li>
<li><strong>Discriminated union defaults are partially updated again</strong> (<a href="">#997</a>). This reverts the 2.15.0 regression with <code>nested_model_default_partial_update=True</code>: the default is only dropped when the incoming value selects a <em>different</em> union member.</li>
</ul>
<h3>New features</h3>
<ul>
<li><strong>Python 3.15 and pydantic 2.14 support</strong> (<a href="">#1026</a>, <a href="">#1029</a>, <a href="">#1022</a>). pydantic 2.14 broke <code>CliApp.run</code> and <code>validate_by_alias=False</code> handling; both are fixed.</li>
<li><strong>Cached settings instances</strong> via <code>Settings.settings_cached()</code> and <code>Settings.settings_clear_cache()</code> (<a href="">#952</a>). These give you a process-local singleton per settings class without hand-rolling <code>lru_cache</code> wrappers. Calling the class directly still builds a fresh instance.</li>
<li><strong>AWS Systems Manager Parameter Store source</strong> — <code>AWSSystemsManagerSettingsSource</code> (<a href="">#941</a>). It recursively reads every parameter under an <code>ssm_path</code>, with <code>/</code> mapping onto nested models. Install it with the new <code>aws-systems-manager</code> extra.</li>
<li><strong><code>env_file_depth</code></strong> (<a href="">#940</a>) lets a relative <code>env_file</code> be found in parent directories, mirroring <code>pyproject_toml_depth</code>. This is useful when scripts run from a subdirectory of a monorepo. It defaults to <code>0</code>, which keeps the current behavior.</li>
<li><strong><code>CliVariadicArg</code> for named variadic options</strong> (<a href="">#949</a>, <a href="">#958</a>). It accepts <code>--param a b c</code> in addition to repeated <code>--param a --param b</code>. Required fields need at least one value.</li>
</ul>
<h3>Bug fixes</h3>
<p><strong>CLI</strong></p>
<ul>
<li><code>CliApp.serialize</code> output now round-trips through <code>CliApp.run</code> for enums, tuples, dates and <code>Decimal</code>s (<a href="">#988</a>), explicit <code>None</code> values (<a href="">#981</a>), empty containers (<a href="">#1008</a>), <code>CliVariadicArg</code> values (<a href="">#976</a>) and populated <code>CliUnknownArgs</code> fields, which previously raised <code>IndexError</code> (<a href="">#992</a>).</li>
<li>Empty JSON arrays (<code>--items []</code>) now give an empty list instead of <code>['']</code> (<a href="">#994</a>).</li>
<li>Tuples, <code>frozenset</code>, <code>MutableSequence</code> and other collection subtypes are now treated as repeatable/variadic options (<a href="">#972</a>), and so are named collection type aliases such as <code>TypeAliasType('Addrs', list[IPvAnyAddress])</code> (<a href="">#1032</a>).</li>
<li><code>cli_exit_on_error=False</code> is now honored in <code>CliSubCommand</code> parsers, which raise <code>SettingsError</code> instead of exiting (<a href="">#977</a>).</li>
<li><code>CliSubCommand</code> aliases keep their case with <code>case_sensitive=False</code> (<a href="">#989</a>).</li>
<li>Each <code>CliUnknownArgs</code> field now receives only its own subcommand's leftover args (<a href="">#1004</a>).</li>
<li><code>CliApp.format_help</code> no longer crashes when <code>cli_prefix</code> is set in <code>model_config</code> (<a href="">#945</a>).</li>
</ul>
<p><strong>Type aliases and parsing</strong></p>
<ul>
<li>Named union type aliases (<code>TypeAliasType('V', list[int] | str)</code>) now decode like their inline equivalents in env and dotenv sources, including under <code>Optional</code>, <code>Annotated</code> and custom validation aliases (<a href="">#1006</a>, <a href="">#1030</a>, <a href="">#1041</a>).</li>
<li>Resolving a named <code>Annotated</code> type alias no longer mutates shared <code>FieldInfo</code> metadata, which made validators run twice on subclasses or after <code>model_rebuild()</code> (<a href="">#979</a>).</li>
<li>A bare single-segment <code>AliasPath('SOME_KEY')</code> no longer tries to JSON-decode plain string values (<a href="">#980</a>).</li>
<li><code>collections.abc.Set</code>/<code>MutableSet</code>/<code>typing.AbstractSet</code> fields now JSON-decode env values (<a href="">#973</a>).</li>
<li>A bare <code>typing.Dict</code> field with <code>env_nested_delimiter</code> no longer raises <code>IndexError</code>, which was a regression in 2.13.0 (<a href="">#1009</a>).</li>
<li>Case-insensitive matching now works for nested pydantic dataclasses (<a href="">#1010</a>).</li>
</ul>
<p><strong>Dotenv, secrets and config files</strong></p>
<ul>
<li>With <code>extra='allow'</code>, a non-lowercase <code>env_prefix</code> is now stripped from dotenv extras (<a href="">#959</a>, <a href="">#968</a>).</li>
<li><code>secrets_case_sensitive=True</code> is now honored on Windows (<a href="">#1001</a>).</li>
<li>An empty JSON config file is treated as an empty mapping instead of crashing (<a href="">#947</a>), matching YAML and TOML.</li>
<li>TOML table headers: <code>~</code> paths are now expanded when checking that the file exists (<a href="">#1034</a>), and an explicit <code>toml_table_header=()</code> now overrides the model config to read the file root (<a href="">#1027</a>).</li>
</ul>
<p><strong>Cloud sources</strong></p>
<ul>
<li>Azure Key Vault and GCP Secret Manager now honor <code>env_parse_none_str</code> (<a href="">#1019</a>, <a href="">#1040</a>).</li>
<li>Azure Key Vault: <code>dash_to_underscore=True</code> now works for nested model fields (<a href="">#1025</a>).</li>
<li><code>NestedSecretsSettingsSource</code> now validates its specific constructor arguments (<a href="">#975</a>).</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8c259f4</code></a> Prepare release 2.16.0 (<a href="">#1043</a>)</li>
<li><a href=""><code>4bc667a</code></a> Keep case of non-option CLI args when case_sensitive=False (<a href="">#1036</a>)</li>
<li><a href=""><code>f75a805</code></a> Simplify alias resolution branch and test alias with AliasChoices/AliasPath (...</li>
<li><a href=""><code>cfdc558</code></a> Honor env_parse_none_str for GCP Secret Manager (<a href="">#1040</a>)</li>
<li><a href=""><code>081d39f</code></a> Fix config file and CLI values being ignored when alias differs from validati...</li>
<li><a href=""><code>c46ebc4</code></a> Expand home paths when checking TOML table headers (<a href="">#1034</a>)</li>
<li><a href=""><code>6ea85e6</code></a> Decode optional Annotated named union aliases (<a href="">#1041</a>)</li>
<li><a href=""><code>ca9d7c4</code></a> Fix JSON decoding for optional named union aliases (<a href="">#1030</a>)</li>
<li><a href=""><code>b6ddda2</code></a> Fix CLI parsing for named collection type aliases (<a href="">#1032</a>)</li>
<li><a href=""><code>bedb60e</code></a> Honor explicit empty TOML table header overrides (<a href="">#1027</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/pydantic/pydantic-settings/compare/v2.15.0...v2.16.0">compare view</a></li>
</ul>
</details>
<br />

Updates `sqlalchemy` from 2.0.54 to 2.1.4
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/sqlalchemy/sqlalchemy/releases">sqlalchemy's releases</a>.</em></p>
<blockquote>
<h1>2.1.4</h1>
<p>Released: October 7, 2026</p>
<h2>orm</h2>
<ul>
<li>
<p><strong>[orm] [bug] [regression]</strong> Fixed regression caused by <a href="https://www.sqlalchemy.org/trac/ticket/13333">#13333</a> where assigning a
<code>MetaData</code> object to the <code>metadata</code> attribute of a mapped
Declarative class, in order to place that class's <code>Table</code> in a
<code>MetaData</code> collection other than that of the
<code>_orm.registry</code>, would emit a warning that the attribute name
<code>metadata</code> should be left reserved.  The warning is now emitted only
when the <code>metadata</code> attribute is assigned to an object other than a
<code>MetaData</code>.</p>
<p>References: <a href="https://www.sqlalchemy.org/trac/ticket/13659">#13659</a></p>
</li>
</ul>
<h2>engine</h2>
<ul>
<li>
<p><strong>[engine] [bug] [regression]</strong> Fixed regression from the 1.4 series where the DBAPI cursor used for a
compiled statement that returns no rows, which includes DDL constructs
such as <code>CreateTable</code> and <code>DropTable</code> as well as the
SAVEPOINT, ROLLBACK TO SAVEPOINT and RELEASE SAVEPOINT statements emitted
by <code>_engine.Connection.begin_nested()</code>, was not closed after
execution, and was instead left to be released when garbage collected.
The cursor is now closed immediately, as was the case in 1.3 and as is
already the case for INSERT, UPDATE, DELETE and <code>_sql.text()</code>
statements.</p>
<p>This change is also <strong>backported</strong> to: 2.0.55</p>
<p>References: <a href="https://www.sqlalchemy.org/trac/ticket/13640">#13640</a></p>
</li>
<li>
<p><strong>[engine] [bug]</strong> Fixed issue in the
<code>_engine.Connection.execution_options.logging_token</code> option
where setting the value to <code>None</code> or another false value would raise
<code>AttributeError</code> if a logging token had not already been established on
that <code>_engine.Connection</code>, such as on a newly checked out
connection, when the option was set at the <code>_engine.Engine</code> level,
or when the token was reset to <code>None</code> more than once.  Regression
introduced in 2.0.30 as part of <a href="https://www.sqlalchemy.org/trac/ticket/11210">#11210</a>.</p>
<p>This change is also <strong>backported</strong> to: 2.0.55</p>
<p>References: <a href="https://www.sqlalchemy.org/trac/ticket/13641">#13641</a></p>
</li>
<li>
<p><strong>[engine] [bug] [regression]</strong> Fixed regression where iterating a <code>Result</code> directly would create
reference cycles that prevented the <code>Result</code> along with the DBAPI</p>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/sqlalchemy/sqlalchemy/commits">compare view</a></li>
</ul>
</details>
<br />

Updates `fastapi` from 0.143.1 to 0.143.5
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/fastapi/fastapi/releases">fastapi's releases</a>.</em></p>
<blockquote>
<h2>0.143.5</h2>
<h3>Fixes</h3>
<ul>
<li>🐛 Fix handling of empty value for <code>byte</code> file list parameter. PR <a href="">#9383</a> by <a href="https://github.com/Viicos"><code>@​Viicos</code></a>.</li>
</ul>
<h2>0.143.4</h2>
<h3>Upgrades</h3>
<ul>
<li>⬆️ Add httpx2 to optional dependencies. PR <a href="">#16512</a> by <a href="https://github.com/tiangolo"><code>@​tiangolo</code></a>.</li>
</ul>
<h2>0.143.3</h2>
<h3>Fixes</h3>
<ul>
<li>🐛 Fix non-finite float serialization in JSONL and SSE streams. PR <a href="">#16509</a> by <a href="https://github.com/tiangolo"><code>@​tiangolo</code></a>.</li>
</ul>
<h3>Docs</h3>
<ul>
<li>🎨 Update Python format in Markdown with Ruff. PR <a href="">#16505</a> by <a href="https://github.com/tiangolo"><code>@​tiangolo</code></a>.</li>
</ul>
<h2>0.143.2</h2>
<h3>Fixes</h3>
<ul>
<li>🐛 Fix blocking frontend fallback file checks. PR <a href="">#16503</a> by <a href="https://github.com/tiangolo"><code>@​tiangolo</code></a>.</li>
</ul>
<h3>Translations</h3>
<ul>
<li>🌐 Update translations for zh-hant (update-outdated). PR <a href="">#16500</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
<li>🌐 Update translations for ja (update-outdated). PR <a href="">#16499</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
<li>🌐 Update translations for zh (update-outdated). PR <a href="">#16501</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
<li>🌐 Update translations for hi (update-outdated). PR <a href="">#16498</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
<li>🌐 Update translations for es (update-outdated). PR <a href="">#16497</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
<li>🌐 Update translations for fr (update-outdated). PR <a href="">#16495</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
<li>🌐 Update translations for ko (update-outdated). PR <a href="">#16496</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
<li>🌐 Update translations for de (update-outdated). PR <a href="">#16493</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
<li>🌐 Update translations for uk (update-outdated). PR <a href="">#16494</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
<li>🌐 Update translations for tr (update-outdated). PR <a href="">#16490</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
<li>🌐 Update translations for pt (update-outdated). PR <a href="">#16491</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
<li>🌐 Update translations for ru (update-outdated). PR <a href="">#16492</a> by <a href="https://github.com/apps/pr-submit"><code>@​pr-submit[bot]</code></a>.</li>
</ul>
<h3>Internal</h3>
<ul>
<li>⬆ Bump pydantic-ai-slim from 2.49.0 to 2.53.0. PR <a href="">#16487</a> by <a href="https://github.com/apps/dependabot"><code>@​dependabot[bot]</code></a>.</li>
<li>⬆ Bump werkzeug from 3.1.6 to 3.1.9. PR <a href="">#16464</a> by <a href="https://github.com/apps/dependabot"><code>@​dependabot[bot]</code></a>.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4bf5ee9</code></a> 🔖 Release version 0.143.5 (<a href="">#16515</a>)</li>
<li><a href=""><code>6e9caf8</code></a> 📝 Update release notes</li>
<li><a href=""><code>fab6eea</code></a> 🐛 Fix handling of empty value for <code>byte</code> file list parameter (<a href="">#9383</a>)</li>
<li><a href=""><code>b23d78f</code></a> 🔖 Release version 0.143.4 (<a href="">#16513</a>)</li>
<li><a href=""><code>4c5dca9</code></a> 📝 Update release notes</li>
<li><a href=""><code>5bebde9</code></a> ⬆️ Add httpx2 to optional dependencies (<a href="">#16512</a>)</li>
<li><a href=""><code>bb7f314</code></a> 🔖 Release version 0.143.3 (<a href="">#16510</a>)</li>
<li><a href=""><code>c34a14c</code></a> 📝 Update release notes</li>
<li><a href=""><code>d1fd422</code></a> 🐛 Fix non-finite float serialization in JSONL and SSE streams (<a href="">#16509</a>)</li>
<li><a href=""><code>0b91981</code></a> 📝 Update release notes</li>
<li>Additional commits viewable in <a href="https://github.com/fastapi/fastapi/compare/0.143.1...0.143.5">compare view</a></li>
</ul>
</details>
<br />

Updates `boto3` from 1.43.103 to 1.43.115
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>2f9e300</code></a> Merge branch 'release-1.43.115'</li>
<li><a href=""><code>4587ee6</code></a> Bumping version to 1.43.115</li>
<li><a href=""><code>ec8fad0</code></a> Add changelog entries from botocore</li>
<li><a href=""><code>3701f39</code></a> Bump <a href="https://github.com/astral-sh/ruff-pre-commit">https://github.com/astral-sh/ruff-pre-commit</a> (<a href="">#4859</a>)</li>
<li><a href=""><code>432fa17</code></a> Merge branch 'release-1.43.114'</li>
<li><a href=""><code>899bd85</code></a> Merge branch 'release-1.43.114' into develop</li>
<li><a href=""><code>bf4aed7</code></a> Bumping version to 1.43.114</li>
<li><a href=""><code>fa3e3f2</code></a> Add changelog entries from botocore</li>
<li><a href=""><code>69ed308</code></a> Merge branch 'release-1.43.113'</li>
<li><a href=""><code>3abaa49</code></a> Merge branch 'release-1.43.113' into develop</li>
<li>Additional commits viewable in <a href="https://github.com/boto/boto3/compare/1.43.103...1.43.115">compare view</a></li>
</ul>
</details>
<br />

Updates `resend` from 2.47.0 to 2.49.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/resendlabs/resend-python/releases">resend's releases</a>.</em></p>
<blockquote>
<h2>v2.49.1</h2>
<h2>What's Changed</h2>
<ul>
<li>fix(webhooks): raise ValueError for non-ASCII signature in Webhooks.verify by <a href="https://github.com/RaphaelFakhri"><code>@​RaphaelFakhri</code></a> in <a href="">resend/resend-python#290</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/RaphaelFakhri"><code>@​RaphaelFakhri</code></a> made their first contribution in <a href="">resend/resend-python#290</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/resend/resend-python/compare/v2.49.0...v2.49.1">https://github.com/resend/resend-python/compare/v2.49.0...v2.49.1</a></p>
<h2>v2.49.0</h2>
<h2>What's Changed</h2>
<ul>
<li>feat(webhooks): add support for topic and contact.topics.updated events by <a href="https://github.com/joaopcm"><code>@​joaopcm</code></a> in <a href="">resend/resend-python#291</a></li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/joaopcm"><code>@​joaopcm</code></a> made their first contribution in <a href="">resend/resend-python#291</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/resend/resend-python/compare/v2.48.0...v2.49.0">https://github.com/resend/resend-python/compare/v2.48.0...v2.49.0</a></p>
<h2>v2.48.0</h2>
<h2>What's Changed</h2>
<ul>
<li>feat(usage): add support for the GET /usage endpoint by <a href="https://github.com/dielduarte"><code>@​dielduarte</code></a> in <a href="">resend/resend-python#289</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/resend/resend-python/compare/v2.47.0...v2.48.0">https://github.com/resend/resend-python/compare/v2.47.0...v2.48.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4ce466e</code></a> fix(webhooks): raise ValueError for non-ASCII signature in Webhooks.verify (#...</li>
<li><a href=""><code>eac30ca</code></a> feat(webhooks): add support for topic and contact.topics.updated events (<a href="">#291</a>)</li>
<li><a href=""><code>f6ad2be</code></a> feat(usage): add support for the GET /usage endpoint (<a href="">#289</a>)</li>
<li>See full diff in <a href="https://github.com/resendlabs/resend-python/compare/v2.47.0...v2.49.1">compare view</a></li>
</ul>
</details>
<br />

Updates `svix` from 2.5.0 to 2.8.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/svix/svix-webhooks/releases">svix's releases</a>.</em></p>
<blockquote>
<h2>SDKs + CLI v2.8.0</h2>
<h2>What's Changed</h2>
<ul>
<li>CLI: You can now populate a request body from a file by using cURL-style <code>@filename</code> syntax; e.g.,
<code>svix streaming events create strm_abcdef123456789 @filename.json</code></li>
<li>Libs/C#: Honor cancellation duration wait for retry (use <code>Task.Delay</code> instead of <code>Thread.Sleep</code>)
in <code>Async</code> methods</li>
<li>Libs/Ruby: Fix <code>Svix::Webhook.new_using_raw_bytes</code> to actually accept raw key bytes instead of
base64 encoded bytes</li>
<li>Libs/Go: Make <code>svix.Message().GetOrCreate()</code> work by changing an accidental pointer receiver
(inconsistent with all other methods) to a value receiver, and allow passing <code>nil</code> for options</li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/guilhermeappel"><code>@​guilhermeappel</code></a> made their first contribution in <a href="">svix/svix-webhooks#2689</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/svix/svix-webhooks/compare/v2.7.0...v2.8.0">https://github.com/svix/svix-webhooks/compare/v2.7.0...v2.8.0</a></p>
<h2>SDKs + CLI v2.7.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Libs/All: Return the new secret from <code>v1.endpoint.rotate-secret</code>, <code>v1.destination.rotate-secret</code>
and <code>v1.streaming.sink.rotate-secret</code></li>
<li>Libs/C#: Fix <code>TimeoutMilliseconds</code> option not being respected</li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/kdcokenny"><code>@​kdcokenny</code></a> made their first contribution in <a href="">svix/svix-webhooks#2679</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/svix/svix-webhooks/compare/v2.6.2...v2.7.0">https://github.com/svix/svix-webhooks/compare/v2.6.2...v2.7.0</a></p>
<h2>SDKs + CLI v2.6.2</h2>
<h2>What's Changed</h2>
<ul>
<li>Libs/(Java and Kotlin): Fix a bug that broke SDK methods where the underlying HTTP call
uses a POST or PUT method and doesn't have any HTTP body parameters</li>
<li>Libs/Go: Fix module path such that v2 are properly released</li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/AdzerKI"><code>@​AdzerKI</code></a> made their first contribution in <a href="">svix/svix-webhooks#2678</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/svix/svix-webhooks/compare/v2.6.1...v2.6.2">https://github.com/svix/svix-webhooks/compare/v2.6.1...v2.6.2</a></p>
<h2>SDKs + CLI v2.6.1</h2>
<h2>Changes</h2>
<ul>
<li>Libs/All: Update to latest Svix Cloud spec</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/svix/svix-webhooks/compare/v2.6.0...v2.6.1">https://github.com/svix/svix-webhooks/compare/v2.6.0...v2.6.1</a></p>
<h2>SDKs + CLI v2.6.0</h2>
<h2>What's Changed</h2>
<ul>
<li>Libs/PHP: Add support for <code>destination</code> and <code>stream</code> APIs</li>
<li>Libs/PHP: Add <code>AutoConfigConsumer</code></li>
<li>Libs/Python <strong>(Breaking)</strong>: Drop support for Python 3.9 (EOL). Minimum supported version is now 3.10</li>
<li>Libs/Rust: Revert an accidental breaking change to <code>AutoConfigConsumer</code> that made a couple methods</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/svix/svix-webhooks/blob/main/ChangeLog.md">svix's changelog</a>.</em></p>
<blockquote>
<h2>Version 2.8.0</h2>
<ul>
<li>CLI: You can now populate a request body from a file by using cURL-style <code>@filename</code> syntax; e.g.,
<code>svix streaming events create strm_abcdef123456789 @filename.json</code></li>
<li>Libs/C#: Honor cancellation duration wait for retry (use <code>Task.Delay</code> instead of <code>Thread.Sleep</code>)
in <code>Async</code> methods</li>
<li>Libs/Ruby: Fix <code>Svix::Webhook.new_using_raw_bytes</code> to actually accept raw key bytes instead of
base64 encoded bytes</li>
<li>Libs/Go: Make <code>svix.Message().GetOrCreate()</code> work by changing an accidental pointer receiver
(inconsistent with all other methods) to a value receiver, and allow passing <code>nil</code> for options</li>
</ul>
<h2>Version 2.7.0</h2>
<ul>
<li>Libs/All: Return the new secret from <code>v1.endpoint.rotate-secret</code>, <code>v1.destination.rotate-secret</code>
and <code>v1.streaming.sink.rotate-secret</code> (if you are using the open-source Svix Server,
please upgrade it to server v1.102.0 before upgrading the SDK)</li>
<li>Libs/C#: Fix <code>TimeoutMilliseconds</code> option not being respected</li>
</ul>
<h2>Version 2.6.2</h2>
<ul>
<li>Libs/(Java and Kotlin): Fix a bug that broke SDK methods where the underlying HTTP call
uses a POST or PUT method and doesn't have any HTTP body parameters</li>
<li>Libs/Go: Fix module path such that v2 are properly released</li>
</ul>
<h2>Version 2.6.1</h2>
<ul>
<li>Libs/All: Update to latest Svix Cloud spec</li>
</ul>
<h2>Version 2.6.0</h2>
<ul>
<li>Libs/PHP: Add support for <code>destination</code> and <code>stream</code> APIs</li>
<li>Libs/PHP: Add <code>AutoConfigConsumer</code></li>
<li>Libs/Python <strong>(Breaking)</strong>: Drop support for Python 3.9 (EOL). Minimum supported version is now 3.10</li>
<li>Libs/Rust: Revert an accidental breaking change to <code>AutoConfigConsumer</code> that made a couple methods
require unique access to the object (<code>&amp;mut self</code>) instead of shared access (<code>&amp;self</code>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>8712f58</code></a> Publish SDKs + CLI v2.8.0 (<a href="">#2692</a>)</li>
<li><a href=""><code>f450286</code></a> go: Fix Application.GetOrCreate (<a href="">#2691</a>)</li>
<li><a href=""><code>6f23037</code></a> ruby: Use the bytes passed to Webhook.new_using_raw_bytes as the key (<a href="">#2661</a>)</li>
<li><a href=""><code>df5099a</code></a> build(deps-dev): bump the development group in /python with 3 updates (<a href="">#2690</a>)</li>
<li><a href=""><code>e38b6e0</code></a> csharp: Use Task.Delay between retries so cancellation is honored (<a href="">#2689</a>)</li>
<li><a href=""><code>48b5805</code></a> cli: allow loading a request from a named file (<a href="">#2685</a>)</li>
<li><a href=""><code>adb3b5c</code></a> build(deps-dev): bump proxy-addr from 2.0.7 to 2.0.8 in /javascript (<a href="">#2688</a>)</li>
<li><a href=""><code>4710557</code></a> build(deps): bump werkzeug from 3.1.8 to 3.1.9 in /python (<a href="">#2687</a>)</li>
<li><a href=""><code>d9f3058</code></a> Publish SDKs + CLI v2.7.0 (<a href="">#2686</a>)</li>
<li><a href=""><code>5114f17</code></a> Update cloud spec and regenerate SDKs (<a href="">#2684</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/svix/svix-webhooks/compare/v2.5.0...v2.8.0">compare view</a></li>
</ul>
</details>
<br />

Updates `numpy` from 2.5.3 to 2.5.4
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/numpy/numpy/releases">numpy's releases</a>.</em></p>
<blockquote>
<h2>v2.5.4 (Oct 10,  2026)</h2>
<h1>NumPy 2.5.4 Release Notes</h1>
<p><em>Released on 2026-10-10.</em></p>
<p>NumPy 2.5.4 is a patch release that fixes bugs discovered after the 2.5.3
release. Highlights are:</p>
<ul>
<li>Many typing fixes and improvements,</li>
<li>A workaround for the MSVC 19.51 bug, see below.</li>
</ul>
<p>This release supports Python versions 3.12-3.15.</p>
<h2>Improvements</h2>
<ul>
<li>
<p><code>numpy.linalg.svd</code> and <code>numpy.linalg.lstsq</code> now raise for inputs containing
infinities instead of returning garbage results.</p>
</li>
<li>
<p>Fixed hangs in <code>numpy.linalg.svd</code> and <code>numpy.linalg.lstsq</code> for certain inputs
containing infinities for recent versions of some LAPACK implementations.</p>
</li>
<li>
<p><code>numpy.linalg.cond</code> now handles non-finite inputs more consistently.</p>
</li>
</ul>
<p>(<a href="">gh-32593</a>)</p>
<h3>StringDType hashing with NaN sentinels</h3>
<p><code>StringDType</code> instances with equivalent floating-point NaN sentinels now
have equal hashes. Previously, distinct NaN objects could produce equal
dtype instances with different hashes, causing dictionary lookups and set
deduplication to fail.</p>
<p>(<a href="">gh-32563</a>)</p>
<h2>Changes</h2>
<h3><code>MaskedArray</code> resets a fill_value that cannot be represented in a new dtype</h3>
<p>A fill_value copied from a source array is now reset to the default fill_value
for the new dtype when it cannot be represented in that dtype. Previously the
copied value could be stale: ufuncs that change dtype left the result holding a
fill_value typed for the old dtype, which raised a <code>TypeError</code> only when
something later validated it (such as <code>.view()</code>), and a floating point
fill_value that overflows an integer dtype was kept as an out-of-range value
together with a <code>RuntimeWarning</code>. Both now fall back to the default,
including when a masked array is passed to <code>MaskedArray</code> with a different
<code>dtype</code>. A fill_value given explicitly by the user is still validated and
raises as before. This can now raise a <code>ComplexWarning</code> if the fill_value is
complex and the new dtype is real.</p>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>a3d0ef1</code></a> Merge pull request <a href="">#32969</a> from charris/prepare-2.5.4</li>
<li><a href=""><code>087b536</code></a> MAINT: Make OpenBLAS version check use 2.5.x branch.</li>
<li><a href=""><code>91acd87</code></a> REL: Prepare for the NumPy 2.5.4 release.</li>
<li><a href=""><code>9cc555b</code></a> Merge pull request <a href="">#32956</a> from charris/backport-typing-1</li>
<li><a href=""><code>e04b972</code></a> TYP: <code>dtype[void].names</code>: allow setting with list (<a href="">#32943</a>)</li>
<li><a href=""><code>d929969</code></a> TYP: <code>timedelta64</code>: <code>datetime.timedelta</code> construction isn't deprecated (#...</li>
<li><a href=""><code>839467f</code></a> TYP: <code>ma.getmaskarray</code>: accept array-likes (<a href="">#32934</a>)</li>
<li><a href=""><code>64b721b</code></a> TYP: <code>polynomial</code>: accept scalar <code>coef</code> in the poly constructors (<a href="">#32931</a>)</li>
<li><a href=""><code>06b7ad2</code></a> TYP: <code>void</code>: accept any <code>dtype: str</code> in constructor calls (<a href="">#32928</a>)</li>
<li><a href=""><code>c7bcd2c</code></a> TYP: <code>place</code>: widen <code>mask</code> (<a href="">#32926</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/numpy/numpy/compare/v2.5.3...v2.5.4">compare view</a></li>
</ul>
</details>
<br />

Updates `faker` from 40.39.0 to 40.43.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/joke2k/faker/releases">faker's releases</a>.</em></p>
<blockquote>
<h2>Release v40.43.0</h2>
<p>See <a href="https://github.com/joke2k/faker/blob/refs/tags/v40.43.0/CHANGELOG.md">CHANGELOG.md</a>.</p>
<h2>Release v40.42.0</h2>
<p>See <a href="https://github.com/joke2k/faker/blob/refs/tags/v40.42.0/CHANGELOG.md">CHANGELOG.md</a>.</p>
<h2>Release v40.41.0</h2>
<p>See <a href="https://github.com/joke2k/faker/blob/refs/tags/v40.41.0/CHANGELOG.md">CHANGELOG.md</a>.</p>
<h2>Release v40.40.0</h2>
<p>See <a href="https://github.com/joke2k/faker/blob/refs/tags/v40.40.0/CHANGELOG.md">CHANGELOG.md</a>.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/joke2k/faker/blob/master/CHANGELOG.md">faker's changelog</a>.</em></p>
<blockquote>
<h3><a href="https://github.com/joke2k/faker/compare/v40.42.0...v40.43.0">v40.43.0 - 2026-10-09</a></h3>
<ul>
<li>Add <code>es_CO</code> bank provider (<a href="">#2453</a>). Thanks <a href="https://github.com/saratobonr"><code>@​saratobonr</code></a>.</li>
<li>Add <code>es_CO</code> internet provider (<a href="">#2455</a>). Thanks <a href="https://github.com/saratobonr"><code>@​saratobonr</code></a>.</li>
</ul>
<h3><a href="https://github.com/joke2k/faker/compare/v40.41.0...v40.42.0">v40.42.0 - 2026-10-09</a></h3>
<ul>
<li>Fix: generate <code>fa_IR</code> and <code>mk_MK</code> IBANs with the correct BBAN length (<a href="">#2451</a>). Thanks <a href="https://github.com/anandghegde"><code>@​anandghegde</code></a>.</li>
<li>Catch <code>NotImplementedError</code> when documenting unimplemented formatters (<a href="">#2461</a>). Thanks <a href="https://github.com/ekanshul"><code>@​ekanshul</code></a>.</li>
<li>Catch <code>NotImplementedError</code> in <code>Documentor.get_provider_formatters</code> (<a href="">#2462</a>). Thanks <a href="https://github.com/kdmadeit"><code>@​kdmadeit</code></a>.</li>
</ul>
<h3><a href="https://github.com/joke2k/faker/compare/v40.40.0...v40.41.0">v40.41.0 - 2026-10-05</a></h3>
<ul>
<li>Fix: update <code>vi_VN</code> address formats, administrative units, and postcodes (<a href="">#2433</a>). Thanks <a href="https://github.com/hmtrii"><code>@​hmtrii</code></a>.</li>
</ul>
<h3><a href="https://github.com/joke2k/faker/compare/v40.39.0...v40.40.0">v40.40.0 - 2026-09-28</a></h3>
<ul>
<li>Fix: generate valid CNP birth dates in <code>ro_RO</code> <code>ssn()</code> (<a href="">#2431</a>). Thanks <a href="https://github.com/chuenchen309"><code>@​chuenchen309</code></a>.</li>
<li>Add boundary tests for <code>text(max_nb_chars)</code> (<a href="">#2439</a>). Thanks <a href="https://github.com/saimoon504"><code>@​saimoon504</code></a>.</li>
<li>Clarify in the docs that <code>text()</code> <code>max_nb_chars</code> is an upper bound (<a href="">#2438</a>). Thanks <a href="https://github.com/saimoon504"><code>@​saimoon504</code></a>.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>df289bf</code></a> Bump version: 40.42.0 → 40.43.0</li>
<li><a href=""><code>7593afa</code></a> 📝 Update CHANGELOG.md</li>
<li><a href=""><code>4d178fe</code></a> Add es_CO internet provider (<a href="">#2455</a>)</li>
<li><a href=""><code>d4861a9</code></a> Add es_CO bank provider (<a href="">#2453</a>)</li>
<li><a href=""><code>a4563c8</code></a> Bump version: 40.41.0 → 40.42.0</li>
<li><a href=""><code>db94c7b</code></a> 📝 Update CHANGELOG.md</li>
<li><a href=""><code>a832d8b</code></a> Catch NotImplementedError in Documentor.get_provider_formatters (<a href="">#2462</a>)</li>
<li><a href=""><code>06db7eb</code></a> Catch NotImplementedError when documenting unimplemented formatters (<a href="">#2461</a>)</li>
<li><a href=""><code>e9b9ae8</code></a> fix(fa_IR, mk_MK): generate IBANs with the correct BBAN length (<a href="">#2451</a>)</li>
<li><a href=""><code>72e2fa4</code></a> Bump version: 40.40.0 → 40.41.0</li>
<li>Additional commits viewable in <a href="https://github.com/joke2k/faker/compare/v40.39.0...v40.43.0">compare view</a></li>
</ul>
</details>
<br />

Updates `google-auth` from 2.58.1 to 2.62.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/googleapis/google-cloud-python/releases">google-auth's releases</a>.</em></p>
<blockquote>
<h2>google-auth: v2.62.0</h2>
<h2><a href="https://github.com/googleapis/google-cloud-python/compare/google-auth-v2.61.0...google-auth-v2.62.0">2.62.0</a> (2026-10-12)</h2>
<h3>Features</h3>
<ul>
<li><strong>auth:</strong> enable bound ID tokens by default on Cloud Run (<a href="">#18635</a>) (<a href="">8b625c4</a>)</li>
</ul>
<h2>google-auth: v2.61.0</h2>
<h2><a href="https://github.com/googleapis/google-cloud-python/compare/google-auth-v2.60.0...google-auth-v2.61.0">2.61.0</a> (2026-10-07)</h2>
<h3>Features</h3>
<ul>
<li><strong>auth:</strong> support bound access and ID tokens for GKE (<a href="">#18594</a>) (<a href="">9f5fd7b</a>)</li>
</ul>
<h2>google-auth: v2.60.0</h2>
<h2><a href="https://github.com/googleapis/google-cloud-python/compare/google-auth-v2.59.1...google-auth-v2.60.0">2.60.0</a> (2026-10-02)</h2>
<h3>Features</h3>
<ul>
<li><strong>auth:</strong> Support sync credentials in AsyncAuthorizedSession (<a href="">#18542</a>) (<a href="">3799568</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>5deaacb</code></a> chore(main): release google-auth 2.62.0 (<a href="">#18637</a>)</li>
<li><a href=""><code>8b625c4</code></a> feat(auth): enable bound ID tokens by default on Cloud Run (<a href="">#18635</a>)</li>
<li><a href=""><code>98fc304</code></a> feat(dbapi): wire timeout parameter through Connection to execute_sql (<a href="">#18484</a>)</li>
<li><a href=""><code>0cabf7c</code></a> test(spanner): increase stale database cleanup cutoff to 3 hours (<a href="">#18633</a>)</li>
<li><a href=""><code>ab56473</code></a> perf(spanner): prune lock and begin event allocations on single-use snapshots...</li>
<li><a href=""><code>78b9da2</code></a> fix(google-cloud-spanner): do not replay DDL statements on transaction retry ...</li>
<li><a href=""><code>f18a11e</code></a> feat(db-dtypes): support pandas 3.1 (<a href="">#18590</a>)</li>
<li><a href=""><code>590e43d</code></a> fix(bigquery): accept empty sourceFormat fields (<a href="">#18472</a>)</li>
<li><a href=""><code>05b3775</code></a> perf(spanner): optimize single-chunk results and single-row lookups (<a href="">#18602</a>)</li>
<li><a href=""><code>a7678fd</code></a> fix(spanner): eliminate duplicate metrics capture and measure full streaming ...</li>
<li>Additional commits viewable in <a href="https://github.com/googleapis/google-cloud-python/compare/google-auth-v2.58.1...google-auth-v2.62.0">compare view</a></li>
</ul>
</details>
<br />

Updates `opentelemetry-exporter-otlp-proto-http` from 1.45.0 to 1.45.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/open-telemetry/opentelemetry-python/releases">opentelemetry-exporter-otlp-proto-http's releases</a>.</em></p>
<blockquote>
<h2>Version 1.45.1/0.66b1</h2>
<p>This is a patch release on the previous 1.45.0/0.66b0 release, fixing the issue(s) below.</p>
<h3>Fixed</h3>
<ul>
<li><code>opentelemetry-api</code>: make <code>AnyValue</code> and <code>AttributeValue</code> explicit type aliases (<a href="">#5703</a>)</li>
<li><code>opentelemetry-sdk</code>: fix thread leak bug in resource initialization logic for long running resource detectors (<a href="">#5706</a>)</li>
<li><code>opentelemetry-exporter-otlp-proto-http</code>: restore <code>requests</code> as the default HTTP transport so proxy environment variables such as <code>HTTPS_PROXY</code> are honored again (<a href="">#5714</a>)</li>
<li><code>opentelemetry-api</code>: fix quadratic time parsing of the <code>tracestate</code> header and discard <code>tracestate</code> headers longer than 8192 characters (<a href="">#5746</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/open-telemetry/opentelemetry-python/blob/main/CHANGELOG.md">opentelemetry-exporter-otlp-proto-http's changelog</a>.</em></p>
<blockquote>
<h2>Version 1.45.1/0.66b1 (2026-10-06)</h2>
<h3>Fixed</h3>
<ul>
<li><code>opentelemetry-api</code>: make <code>AnyValue</code> and <code>AttributeValue</code> explicit type
aliases
(<a href="">#5703</a>)</li>
<li><code>opentelemetry-sdk</code>: fix thread leak bug in resource initialization logic for
long running resource detectors
(<a href="">#5706</a>)</li>
<li><code>opentelemetry-exporter-otlp-proto-http</code>: restore <code>requests</code> as the default
HTTP transport so proxy environment variables such as <code>HTTPS_PROXY</code> are
honored again
(<a href="">#5714</a>)</li>
<li><code>opentelemetry-api</code>: fix quadratic time parsing of the <code>tracestate</code> header
and discard <code>tracestate</code> headers longer than 8192 characters
(<a href="">#5746</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>14971ce</code></a> Prepare release 1.45.1/0.66b1 (<a href="">#5752</a>)</li>
<li><a href=""><code>44ac26e</code></a> opentelemetry-sdk: fix thread leak bug in resource initialization logic (<a href="">#570</a>...</li>
<li><a href=""><code>a2ec3f9</code></a> [release/v1.45.x-0.66bx] opentelemetry-exporter-otlp-proto-http: restore requ...</li>
<li><a href=""><code>d5224bf</code></a> opentelemetry-api: improve performance of tracestate parsing (<a href="">#5746</a>) (<a href="">#5749</a>)</li>
<li><a href=""><code>db61173</code></a> Declare AnyValue and AttributeValue as explicit type aliases (<a href="">#5703</a>) (<a href="">#5750</a>)</li>
<li>See full diff in <a href="https://github.com/open-telemetry/opentelemetry-python/compare/v1.45.0...v1.45.1">compare view</a></li>
</ul>
</details>
<br />

Updates `pre-commit` from 4.6.2 to 4.7.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pre-commit/pre-commit/releases">pre-commit's releases</a>.</em></p>
<blockquote>
<h2>pre-commit v4.7.0</h2>
<h3>Fixes</h3>
<ul>
<li>Fix <code>language: node</code> hooks during commit with <code>-a</code> or inside a submodule.
<ul>
<li>Regressed in 4.6.1.</li>
<li><a href="">#3773</a> issue by <a href="https://github.com/cbirkhold"><code>@​cbirkhold</code></a>.</li>
<li><a href="">#3774</a> PR by <a href="https://github.com/cbirkhold"><code>@​cbirkhold</code></a>.</li>
</ul>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/pre-commit/pre-commit/blob/main/CHANGELOG.md">pre-commit's changelog</a>.</em></p>
<blockquote>
<h1>4.7.0 - 2026-10-12</h1>
<h3>Fixes</h3>
<ul>
<li>Fix <code>language: node</code> hooks during commit with <code>-a</code> or inside a submodule.
<ul>
<li>Regressed in 4.6.1.</li>
<li><a href="">#3773</a> issue by <a href="https://github.com/cbirkhold"><code>@​cbirkhold</code></a>.</li>
<li><a href="">#3774</a> PR by <a href="https://github.com/cbirkhold"><code>@​cbirkhold</code></a>.</li>
</ul>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>65bb884</code></a> v4.7.0</li>
<li><a href=""><code>73926c1</code></a> Merge pull request <a href="">#3774</a> from cbirkhold/node-no-git-env-npm-install</li>
<li><a href=""><code>860d07d</code></a> don't leak GIT_* env into <code>npm install</code> for <code>language: node</code></li>
<li><a href=""><code>9ad8a0a</code></a> Merge pull request <a href="">#3775</a> from pre-commit/contextlib-chdir</li>
<li><a href=""><code>9905e88</code></a> use contextlib.chdir</li>
<li><a href=""><code>59cb792</code></a> Merge pull request <a href="">#3771</a> from pre-commit/all-repos_autofix_py311-plus</li>
<li><a href=""><code>2be1701</code></a> remove triple-nested withs for 3.14 coverage</li>
<li><a href=""><code>4c8d22a</code></a> py311+</li>
<li><a href=""><code>c429238</code></a> Merge pull request <a href="">#3770</a> from pre-commit/pre-commit-ci-update-config</li>
<li><a href=""><code>f49e251</code></a> [pre-commit.ci] pre-commit autoupdate</li>
<li>Additional commits viewable in <a href="https://github.com/pre-commit/pre-commit/compare/v4.6.2...v4.7.0">compare view</a></li>
</ul>
</details>
<br />

Updates `ruff` from 0.16.9 to 0.17.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff/releases">ruff's rel...

_Description has been truncated_

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bec35eec3314`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.