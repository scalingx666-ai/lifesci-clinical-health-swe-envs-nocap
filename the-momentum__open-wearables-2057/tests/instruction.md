# Issue

**Title:** chore: bump the python-minor-patch group across 2 directories with 16 updates

## Description

Bumps the python-minor-patch group with 15 updates in the /backend directory:

| Package | From | To |
| --- | --- | --- |
| [pydantic-settings](https://github.com/pydantic/pydantic-settings) | `2.16.0` | `2.16.2` |
| [sqlalchemy](https://github.com/sqlalchemy/sqlalchemy) | `2.1.4` | `2.1.6` |
| [python-multipart](https://github.com/Kludex/python-multipart) | `0.0.32` | `0.0.33` |
| [alembic](https://github.com/sqlalchemy/alembic) | `1.20.0` | `1.20.1` |
| [boto3](https://github.com/boto/boto3) | `1.43.115` | `1.43.123` |
| [resend](https://github.com/resendlabs/resend-python) | `2.49.1` | `2.50.0` |
| [svix](https://github.com/svix/svix-webhooks) | `2.8.0` | `2.9.1` |
| [faker](https://github.com/joke2k/faker) | `40.43.0` | `40.44.0` |
| [opentelemetry-sdk](https://github.com/open-telemetry/opentelemetry-python) | `1.45.1` | `1.45.2` |
| [opentelemetry-exporter-otlp-proto-http](https://github.com/open-telemetry/opentelemetry-python) | `1.45.1` | `1.45.2` |
| [opentelemetry-instrumentation-logging](https://github.com/open-telemetry/opentelemetry-python-contrib) | `0.66b1` | `0.66b2` |
| [ruff](https://github.com/astral-sh/ruff) | `0.17.1` | `0.17.3` |
| [ty](https://github.com/astral-sh/ty) | `0.0.89` | `0.0.95` |
| [pytest](https://github.com/pytest-dev/pytest) | `9.1.1` | `9.2.0` |
| [pytest-asyncio](https://github.com/pytest-dev/pytest-asyncio) | `1.4.0` | `1.4.1.post1` |
| [pydantic-settings](https://github.com/pydantic/pydantic-settings) | `2.16.0` | `2.16.2` |
| [ruff](https://github.com/astral-sh/ruff) | `0.17.1` | `0.17.3` |
| [ty](https://github.com/astral-sh/ty) | `0.0.89` | `0.0.95` |
| [pytest](https://github.com/pytest-dev/pytest) | `9.1.1` | `9.2.0` |
| [pytest-asyncio](https://github.com/pytest-dev/pytest-asyncio) | `1.4.0` | `1.4.1.post1` |

Bumps the python-minor-patch group with 6 updates in the /mcp directory:

| Package | From | To |
| --- | --- | --- |
| [pydantic-settings](https://github.com/pydantic/pydantic-settings) | `2.16.0` | `2.16.2` |
| [ruff](https://github.com/astral-sh/ruff) | `0.17.1` | `0.17.3` |
| [ty](https://github.com/astral-sh/ty) | `0.0.89` | `0.0.95` |
| [pytest](https://github.com/pytest-dev/pytest) | `9.1.1` | `9.2.0` |
| [pytest-asyncio](https://github.com/pytest-dev/pytest-asyncio) | `1.4.0` | `1.4.1.post1` |
| [pydantic](https://github.com/pydantic/pydantic) | `2.14.1` | `2.14.2` |
| [pydantic-settings](https://github.com/pydantic/pydantic-settings) | `2.16.0` | `2.16.2` |
| [ruff](https://github.com/astral-sh/ruff) | `0.17.1` | `0.17.3` |
| [ty](https://github.com/astral-sh/ty) | `0.0.89` | `0.0.95` |
| [pytest](https://github.com/pytest-dev/pytest) | `9.1.1` | `9.2.0` |
| [pytest-asyncio](https://github.com/pytest-dev/pytest-asyncio) | `1.4.0` | `1.4.1.post1` |

Updates `pydantic-settings` from 2.16.0 to 2.16.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/pydantic/pydantic-settings/releases">pydantic-settings's releases</a>.</em></p>
<blockquote>
<h2>v2.16.1</h2>
<h2>Highlights</h2>
<p>This patch release fixes two CLI regressions introduced in 2.16.0.</p>
<h3>Bug fixes</h3>
<p><strong>CLI</strong></p>
<ul>
<li>Fixed-length tuple positionals such as <code>CliPositionalArg[tuple[int, int]]</code> and <code>NamedTuple</code>s are single-valued again (<a href="">#1069</a>). Since 2.16.0 they were treated as variadic, so a CLI either refused to start with a <code>SettingsError</code> or put the wrong argument into the tuple. Variable-length tuples (<code>tuple[int, ...]</code> and bare <code>Tuple</code>) are still variadic.</li>
<li>A field typed as an alias of a list of dicts, e.g. <code>type ListOfDict = list[dict[str, int]]</code>, accepts a JSON list again (<a href="">#1049</a>). Since 2.16.0, <code>--xx '[{&quot;a&quot;:1},{&quot;b&quot;:2}]'</code> was merged into the single dict <code>{&quot;a&quot;: 1, &quot;b&quot;: 2}</code> and failed validation.</li>
</ul>
<!-- raw HTML omitted -->
<h2>What's Changed</h2>
<ul>
<li>Harden CI by <a href="https://github.com/Viicos"><code>@​Viicos</code></a> in <a href="">pydantic/pydantic-settings#1044</a></li>
<li>Keep list of dicts CLI values as lists by <a href="https://github.com/hramezani"><code>@​hramezani</code></a> in <a href="">pydantic/pydantic-settings#1049</a></li>
<li>Keep fixed-length tuple CLI positionals single-valued by <a href="https://github.com/hramezani"><code>@​hramezani</code></a> in <a href="">pydantic/pydantic-settings#1069</a></li>
<li>Prepare release 2.16.1 by <a href="https://github.com/hramezani"><code>@​hramezani</code></a> in <a href="">pydantic/pydantic-settings#1087</a></li>
<li>build(deps): bump the python-packages group with 3 updates by <a href="https://github.com/dependabot"><code>@​dependabot</code></a>[bot] in <a href="">pydantic/pydantic-settings#1056</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/pydantic/pydantic-settings/compare/v2.16.0...v2.16.1">https://github.com/pydantic/pydantic-settings/compare/v2.16.0...v2.16.1</a></p>
<!-- raw HTML omitted -->
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>94150a0</code></a> Prepare release 2.16.2 (<a href="">#1111</a>)</li>
<li><a href=""><code>9e02de0</code></a> Fix JSON decoding of nested dictionary environment values (<a href="">#1109</a>)</li>
<li><a href=""><code>7e2dacb</code></a> Fix CliApp reconstruction of AliasPath inputs (<a href="">#1096</a>)</li>
<li><a href=""><code>2d1f924</code></a> Fix explicit nested secrets directory precedence (<a href="">#1093</a>)</li>
<li><a href=""><code>e9588ae</code></a> Fix regressions from nested dict union value decoding (<a href="">#1089</a>) (<a href="">#1097</a>)</li>
<li><a href=""><code>e71a53e</code></a> Decode nested dictionary values with complex union types (<a href="">#1089</a>)</li>
<li><a href=""><code>8dc9e05</code></a> Resolve only the discriminator annotation of stdlib dataclass defaults (<a href="">#1077</a>)</li>
<li><a href=""><code>c50c853</code></a> Detect nested Field discriminators in default partial updates (<a href="">#1076</a>)</li>
<li><a href=""><code>9aabb8a</code></a> build(deps): bump the python-packages group with 3 updates (<a href="">#1056</a>)</li>
<li><a href=""><code>4e286e2</code></a> Prepare release 2.16.1 (<a href="">#1087</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/pydantic/pydantic-settings/compare/v2.16.0...v2.16.2">compare view</a></li>
</ul>
</details>
<br />

Updates `sqlalchemy` from 2.1.4 to 2.1.6
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/sqlalchemy/sqlalchemy/releases">sqlalchemy's releases</a>.</em></p>
<blockquote>
<h1>2.1.6</h1>
<p>Released: October 21, 2026</p>
<h2>orm</h2>
<ul>
<li>
<p><strong>[orm] [bug]</strong> Fixed issue where a <code>Session</code> flush that replaced an expired
object in the identity map with a newly flushed object of the same
primary key would emit a SELECT to refresh the expired object, solely in
order to determine whether to emit an &quot;Identity map already had an
identity&quot; warning.  This could occur when a row loaded within a
transaction is rolled back and its primary key value is subsequently
reused, and could lead to an <code>AttributeError</code> if the expired object
were garbage collected during that load.  The check now emits no SQL, and
an expired object that is replaced in this way no longer causes the
warning to be emitted.</p>
<p>This change is also <strong>backported</strong> to: 2.0.56</p>
<p>References: <a href="https://www.sqlalchemy.org/trac/ticket/13711">#13711</a></p>
</li>
<li>
<p><strong>[orm] [bug] [regression]</strong> Fixed regression caused by <a href="https://www.sqlalchemy.org/trac/ticket/13070">#13070</a> where using more than one
<code>orm.with_loader_criteria()</code> option for the same entity, where the
criteria made use of correlated subqueries referring to that entity, would
fail with a <code>RecursionError</code> when compiling.</p>
<p>References: <a href="https://www.sqlalchemy.org/trac/ticket/13701">#13701</a></p>
</li>
<li>
<p><strong>[orm] [bug] [regression]</strong> Fixed regression caused by the new implementation of <code>.params()</code> for
statements introduced in <a href="https://www.sqlalchemy.org/trac/ticket/7066">#7066</a>, where parameter values passed to
the <code>.params()</code> method of an ORM statement created using
<code>Select.from_statement()</code> would not be applied when the statement
was compiled without the compiled statement cache, such as when the cache
was disabled or when the statement was stringified directly, leading to
an error that a value is required for the bound parameter.</p>
<p>References: <a href="https://www.sqlalchemy.org/trac/ticket/13709">#13709</a></p>
</li>
</ul>
<h2>orm extensions</h2>
<ul>
<li>
<p><strong>[bug] [orm extensions]</strong> Fixed an issue in the <code>instrumentation_toplevel</code> extension where
unrelated classes inheriting from <code>typing.Generic</code> could incorrectly
raise a <code>TypeError</code> when using different instrumentation implementations.
Pull request courtesy TomasCaruso10.</p>
<p>This change is also <strong>backported</strong> to: 2.0.56</p>
<p>References: <a href="https://www.sqlalchemy.org/trac/ticket/13680">#13680</a></p>
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

Updates `python-multipart` from 0.0.32 to 0.0.33
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/Kludex/python-multipart/releases">python-multipart's releases</a>.</em></p>
<blockquote>
<h2>Version 0.0.33</h2>
<h2>🛡️ Safer form parsing</h2>
<p>This release lets you cap URL-encoded form fields as they stream in, and fixes several upload and decoding edge cases. It also drops Python 3.10 and adds Python 3.15.</p>
<pre lang="console"><code>pip install python-multipart==0.0.33
</code></pre>
<ul>
<li><strong>Limit URL-encoded fields while streaming</strong> (<a href="">#333</a>). The new opt-in <code>MAX_FIELDS</code> and <code>MAX_FIELD_SIZE</code> options for <code>FormParser</code> raise <code>FormParserError</code> before oversized data is buffered. Both default to no limit, and multipart forms are unaffected.</li>
<li><strong>Nameless uploads no longer crash when spilled to disk</strong> (<a href="">#343</a>). Uploads without a filename used to raise <code>AttributeError</code> when <code>UPLOAD_KEEP_EXTENSIONS</code> or <code>UPLOAD_KEEP_FILENAME</code> was set.</li>
<li><strong><code>UPLOAD_DIR</code> accepts <code>str</code> with <code>UPLOAD_KEEP_FILENAME</code></strong> (<a href="">#335</a>). A <code>str</code> upload directory used to fail on the first write to disk.</li>
<li><strong>Decoded data is complete before callbacks run</strong> (<a href="">#336</a>, <a href="">#355</a>). <code>Content-Transfer-Encoding</code> decoders are finalized at the end of each part, and quoted-printable escapes split across writes decode correctly.</li>
<li><strong><code>parse_options_header</code> lowercases content types with parameters</strong> (<a href="">#287</a>). <code>Multipart/Form-Data; boundary=abc</code> now returns <code>multipart/form-data</code>, the same as headers without parameters.</li>
</ul>
<h2>⚡ Faster parsing</h2>
<ul>
<li><strong>Faster opening boundary matching</strong> (<a href="">#328</a>). Complete boundaries are matched in one step.</li>
<li><strong>Faster parser state lookups</strong> (<a href="">#330</a>). Parser states are module-level enum members, so their <code>repr</code> is now <code>multipart.END</code> instead of <code>&lt;MultipartState.END: 12&gt;</code>.</li>
<li><strong>Faster querystring callback dispatch</strong> (<a href="">#316</a>).</li>
</ul>
<h2>🐍 Python support</h2>
<ul>
<li><strong>Python 3.10 is no longer supported</strong> (<a href="">#329</a>). Python 3.11 is now the minimum.</li>
<li><strong>Python 3.15 is supported</strong> (<a href="">#350</a>).</li>
</ul>
<h2>💜 Thank you</h2>
<p>Thanks to <a href="https://github.com/Edneam"><code>@​Edneam</code></a>, <a href="https://github.com/sungbin1015"><code>@​sungbin1015</code></a>, <a href="https://github.com/carlok"><code>@​carlok</code></a>, and <a href="https://github.com/fjvbn2003"><code>@​fjvbn2003</code></a> for contributing to this release.</p>
<p>Thanks to the individual sponsors who contributed $134.00 to support this work. If python-multipart is useful to you, consider <a href="https://github.com/sponsors/Kludex">sponsoring me on GitHub</a>.</p>
<p><strong>Full changelog:</strong> <a href="https://github.com/Kludex/python-multipart/compare/0.0.32...0.0.33">0.0.32...0.0.33</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/Kludex/python-multipart/blob/main/CHANGELOG.md">python-multipart's changelog</a>.</em></p>
<blockquote>
<h2>0.0.33 (2026-10-31)</h2>
<ul>
<li>Drop Python 3.10 support <a href="">#329</a>.</li>
<li>Add Python 3.15 support <a href="">#350</a>.</li>
<li>Add opt-in field-count and field-size limits for URL-encoded forms in <code>FormParser</code> <a href="">#333</a>.</li>
<li>Normalize the content type returned by <code>parse_options_header</code> when the header has parameters <a href="">#287</a>.</li>
<li>Finalize <code>Content-Transfer-Encoding</code> decoding before invoking field and file callbacks <a href="">#336</a>.</li>
<li>Keep only the incomplete escape when quoted-printable data is split across writes <a href="">#355</a>.</li>
<li>Handle nameless uploads when <code>UPLOAD_KEEP_FILENAME</code> or <code>UPLOAD_KEEP_EXTENSIONS</code> is set <a href="">#343</a>.</li>
<li>Accept a <code>str</code> <code>UPLOAD_DIR</code> when <code>UPLOAD_KEEP_FILENAME</code> is set <a href="">#335</a>.</li>
<li>Speed up parser state lookups <a href="">#330</a>.</li>
<li>Speed up opening boundary matching <a href="">#328</a>.</li>
<li>Speed up querystring callback dispatch <a href="">#316</a>.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>9217f26</code></a> Bump version to 0.0.33 (<a href="">#357</a>)</li>
<li><a href=""><code>d0344c1</code></a> Keep only the incomplete escape when quoted-printable data is split (<a href="">#355</a>)</li>
<li><a href=""><code>44871df</code></a> Handle nameless uploads when keeping the filename or extension (<a href="">#343</a>)</li>
<li><a href=""><code>b21ea59</code></a> Add streaming field limits to <code>FormParser</code> (<a href="">#333</a>)</li>
<li><a href=""><code>48f9e21</code></a> Fix the In-Depth Example in the docs to return bytes (<a href="">#338</a>)</li>
<li><a href=""><code>12a2f8f</code></a> Accept a <code>str</code> <code>UPLOAD_DIR</code> when <code>UPLOAD_KEEP_FILENAME</code> is set (<a href="">#335</a>)</li>
<li><a href=""><code>95f6376</code></a> Use the shared security policy (<a href="">#353</a>)</li>
<li><a href=""><code>8ec84ef</code></a> Migrate documentation from MkDocs to Zensical (<a href="">#352</a>)</li>
<li><a href=""><code>d7af81c</code></a> Rewrite README for newcomers (<a href="">#351</a>)</li>
<li><a href=""><code>b035d14</code></a> Add Python 3.15 classifier (<a href="">#350</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/Kludex/python-multipart/compare/0.0.32...0.0.33">compare view</a></li>
</ul>
</details>
<br />

Updates `alembic` from 1.20.0 to 1.20.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/sqlalchemy/alembic/releases">alembic's releases</a>.</em></p>
<blockquote>
<h1>1.20.1</h1>
<p>Released: October 21, 2026</p>
<h2>bug</h2>
<ul>
<li>
<p><strong>[bug] [autogenerate]</strong> Fixed issue where a table or column comment set to an empty string would
cause autogenerate to detect a comment change on every run.  As most
backends, including PostgreSQL, MySQL, MariaDB and Oracle, don't store an
empty string comment distinctly from no comment, autogenerate now treats
an empty string comment the same as <code>None</code> when comparing comments.
Additionally, an empty string comment is now rendered in
<code>op.create_table()</code> and <code>op.add_column()</code> directives, where it was
previously omitted.  Pull request courtesy vineoy.</p>
<p>References: <a href="">#1085</a></p>
</li>
<li>
<p><strong>[bug] [autogenerate] [postgresql]</strong> Fixed rendering of the PostgreSQL
<code>~sqlalchemy.dialects.postgresql.DOMAIN</code> type in autogenerated
migration scripts.  Previously the type was rendered using <code>repr()</code>,
which omitted the <code>check</code>, <code>not_null</code>, <code>default</code>, <code>collation</code>,
<code>constraint_name</code>, <code>schema</code> and <code>create_type</code> arguments and did not
apply a dialect prefix to the underlying data type.  The full set of
arguments is now rendered and the underlying data type is rendered using
the standard type-rendering logic.  Pull request courtesy Sebastian Cao.</p>
<p>References: <a href="">#1360</a></p>
</li>
<li>
<p><strong>[bug] [autogenerate] [postgresql]</strong> Fixed false-positive &quot;Computed default cannot be modified&quot; warning emitted
during autogenerate when comparing PostgreSQL <code>Computed</code> columns
whose reflected SQL expression includes type cast specifiers such as
<code>::regconfig</code> or <code>::text</code>, which PostgreSQL adds to the expression as
stored.  These cast specifiers are now stripped before comparison so that
otherwise equivalent expressions no longer trigger the warning.  Pull
request courtesy Sebastian Cao.</p>
<p>References: <a href="">#1462</a></p>
</li>
<li>
<p><strong>[bug] [autogenerate] [postgresql]</strong> Fixed issue where autogenerate would detect an unchanged PostgreSQL
expression-based index as modified when the expression included type
casts, such as a cast to a type with a length or precision, a nested
cast, or a cast followed by a <code>DESC</code> modifier.</p>
</li>
<li>
<p><strong>[bug] [postgresql]</strong> Fixed bug where <code>Operations.alter_column()</code> against a PostgreSQL
identity column would render an incomplete, invalid <code>ALTER TABLE ... ALTER COLUMN</code> statement with no clause at all when <code>existing_server_default</code>
was omitted, even if there were no existing server default.  Pull request
courtesy Riti Grover.</p>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/sqlalchemy/alembic/commits">compare view</a></li>
</ul>
</details>
<br />

Updates `boto3` from 1.43.115 to 1.43.123
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>6334d9f</code></a> Merge branch 'release-1.43.123'</li>
<li><a href=""><code>51224ed</code></a> Bumping version to 1.43.123</li>
<li><a href=""><code>3dfd2b6</code></a> Add changelog entries from botocore</li>
<li><a href=""><code>f89caef</code></a> Merge branch 'release-1.43.122'</li>
<li><a href=""><code>f0464ef</code></a> Merge branch 'release-1.43.122' into develop</li>
<li><a href=""><code>5af8c5f</code></a> Bumping version to 1.43.122</li>
<li><a href=""><code>1af5d47</code></a> Add changelog entries from botocore</li>
<li><a href=""><code>cc2e975</code></a> Merge branch 'release-1.43.121'</li>
<li><a href=""><code>807ecf8</code></a> Merge branch 'release-1.43.121' into develop</li>
<li><a href=""><code>21a159b</code></a> Bumping version to 1.43.121</li>
<li>Additional commits viewable in <a href="https://github.com/boto/boto3/compare/1.43.115...1.43.123">compare view</a></li>
</ul>
</details>
<br />

Updates `resend` from 2.49.1 to 2.50.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/resendlabs/resend-python/releases">resend's releases</a>.</em></p>
<blockquote>
<h2>v2.50.0</h2>
<h2>What's Changed</h2>
<ul>
<li>chore(deps): update dependency python to v3.15.0 by <a href="https://github.com/renovate"><code>@​renovate</code></a>[bot] in <a href="">resend/resend-python#292</a></li>
<li>fix: honor legacy custom async HTTP clients by <a href="https://github.com/mayankbohradev"><code>@​mayankbohradev</code></a> in <a href="">resend/resend-python#294</a></li>
<li>fix(broadcasts): accept preview_text and topic_id in create and update params by <a href="https://github.com/RaphaelFakhri"><code>@​RaphaelFakhri</code></a> in <a href="">resend/resend-python#297</a></li>
<li>fix(broadcasts): add topic_id to the Broadcast response type by <a href="https://github.com/felipefreitag"><code>@​felipefreitag</code></a> in <a href="">resend/resend-python#299</a></li>
<li>feat(inboxes): add support for the Inboxes API by <a href="https://github.com/felipefreitag"><code>@​felipefreitag</code></a> in <a href="">resend/resend-python#298</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/resend/resend-python/compare/v2.49.1...v2.50.0">https://github.com/resend/resend-python/compare/v2.49.1...v2.50.0</a></p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b64da65</code></a> feat(inboxes): add support for the Inboxes API (<a href="">#298</a>)</li>
<li><a href=""><code>063f797</code></a> fix(broadcasts): add topic_id to the Broadcast response type (<a href="">#299</a>)</li>
<li><a href=""><code>ac6aae5</code></a> fix(broadcasts): accept preview_text and topic_id in create and update params...</li>
<li><a href=""><code>486a69d</code></a> fix: honor legacy custom async HTTP clients (<a href="">#294</a>)</li>
<li><a href=""><code>6b7d105</code></a> chore(deps): update dependency python to v3.15.0 (<a href="">#292</a>)</li>
<li>See full diff in <a href="https://github.com/resendlabs/resend-python/compare/v2.49.1...v2.50.0">compare view</a></li>
</ul>
</details>
<br />

Updates `svix` from 2.8.0 to 2.9.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/svix/svix-webhooks/releases">svix's releases</a>.</em></p>
<blockquote>
<h2>SDKs + CLI v2.9.1</h2>
<h2>Changes</h2>
<ul>
<li>Libs/JavaScript: Throw <code>ApiException</code> (with the raw response text as <code>body</code>) instead of a <code>SyntaxError</code> when a 4xx error response body is not JSON (thanks <a href="https://github.com/RishavTiwari25"><code>@​RishavTiwari25</code></a>)</li>
<li>CLI: Rebuild Docker image for CVE-2026-111497</li>
</ul>
<h2>New Contributors</h2>
<ul>
<li><a href="https://github.com/RishavTiwari25"><code>@​RishavTiwari25</code></a> made their first contribution in <a href="">svix/svix-webhooks#2743</a></li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/svix/svix-webhooks/compare/v2.9.0...v2.9.1">https://github.com/svix/svix-webhooks/compare/v2.9.0...v2.9.1</a></p>
<h2>SDKs + CLI v2.9.0</h2>
<h2>Changes</h2>
<ul>
<li>Libs/(Java and Kotlin): Strip trailing slashes from server URLs</li>
<li>Libs/Python: Retry on HTTP 423 and on I/O errors; add test coverage for SvixAsync</li>
<li>Libs/All: Update to latest Svix Cloud API, including adding ElasticSearch support for Advanced Destinations</li>
<li>Libs/(C#, Go, Java, JavaScript, Kotlin, PHP, Ruby and Rust): Retry requests that fail due to timeouts or other network errors (connection failures, DNS errors, etc.), not just 5xx responses</li>
<li>Libs/Go: Fix the default retry schedule being 50µs, 100µs and 200µs instead of 50ms, 100ms and 200ms</li>
<li>Libs/PHP: Send the <code>svix-retry-count</code> header on retries, and reuse the same <code>svix-req-id</code> across retries of a request</li>
<li>Libs/JavaScript: Requests now time out after 15 seconds by default (previously there was no timeout unless <code>requestTimeout</code> was set)</li>
<li>Libs/(Go, Java, Kotlin, PHP and Ruby): Change the default request timeout to 15 seconds, matching the other SDKs (previously 60s for Go, 30s for PHP, 60s per connect/read/write for Ruby, and no overall  timeout for Java and Kotlin)</li>
</ul>
<p><strong>Full Changelog</strong>: <a href="https://github.com/svix/svix-webhooks/compare/v2.8.0...v2.9.0">https://github.com/svix/svix-webhooks/compare/v2.8.0...v2.9.0</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/svix/svix-webhooks/blob/main/ChangeLog.md">svix's changelog</a>.</em></p>
<blockquote>
<h2>Version 2.9.1</h2>
<ul>
<li>Libs/JavaScript: Throw <code>ApiException</code> (with the raw response text as <code>body</code>) instead of a
<code>SyntaxError</code> when a 4xx error response body is not JSON</li>
<li>CLI: Rebuild Docker image for CVE-2026-111497</li>
</ul>
<h2>Version 2.9.0</h2>
<ul>
<li>Libs/(Java and Kotlin): Strip trailing slashes from server URLs</li>
<li>Libs/Python: Retry on HTTP 423 and on I/O errors; add test coverage for SvixAsync</li>
<li>Libs/All: Update to latest Svix Cloud API, including adding ElasticSearch support for Advanced Destinations</li>
<li>Libs/(C#, Go, Java, JavaScript, Kotlin, PHP, Ruby and Rust): Retry requests that fail due to
timeouts or other network errors (connection failures, DNS errors, etc.), not just 5xx responses</li>
<li>Libs/Go: Fix the default retry schedule being 50µs, 100µs and 200µs instead of 50ms, 100ms and 200ms</li>
<li>Libs/PHP: Send the <code>svix-retry-count</code> header on retries, and reuse the same <code>svix-req-id</code> across
retries of a request</li>
<li>Libs/JavaScript: Requests now time out after 15 seconds by default (previously there was no
timeout unless <code>requestTimeout</code> was set)</li>
<li>Libs/(Go, Java, Kotlin, PHP and Ruby): Change the default request timeout to 15 seconds, matching the
other SDKs (previously 60s for Go, 30s for PHP, 60s per connect/read/write for Ruby, and no overall
timeout for Java and Kotlin)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7660691</code></a> prepare release 2.9.1 (<a href="">#2745</a>)</li>
<li><a href=""><code>1245421</code></a> deps: upgrade jwt-simple and chacha20poly1305 for RUSTSEC-2026-0387 (<a href="">#2747</a>)</li>
<li><a href=""><code>db251fb</code></a> bridge: update ChangeLog (<a href="">#2750</a>)</li>
<li><a href=""><code>b9d1169</code></a> prepare bridge release 1.101.1 (<a href="">#2746</a>)</li>
<li><a href=""><code>17d3a8b</code></a> bridge: Add dlq_config to redis queue plugin (<a href="">#2705</a>)</li>
<li><a href=""><code>b7a89e0</code></a> cli: bump wolfi-base for CVE-2026-111497 (<a href="">#2744</a>)</li>
<li><a href=""><code>e220253</code></a> js: Throw ApiException when a 4xx error response is not JSON (<a href="">#2743</a>)</li>
<li><a href=""><code>bcc36ef</code></a> deps: upgrade to sqlx 0.9 / seaorm 2 (<a href="">#2733</a>)</li>
<li><a href=""><code>c07c464</code></a> gha: pin cargo-sort to v2.1.3 (<a href="">#2740</a>)</li>
<li><a href=""><code>42bc3fa</code></a> libs: bump to v2.9.0 (<a href="">#2738</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/svix/svix-webhooks/compare/v2.8.0...v2.9.1">compare view</a></li>
</ul>
</details>
<br />

Updates `faker` from 40.43.0 to 40.44.0
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/joke2k/faker/releases">faker's releases</a>.</em></p>
<blockquote>
<h2>Release v40.44.0</h2>
<p>See <a href="https://github.com/joke2k/faker/blob/refs/tags/v40.44.0/CHANGELOG.md">CHANGELOG.md</a>.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/joke2k/faker/blob/master/CHANGELOG.md">faker's changelog</a>.</em></p>
<blockquote>
<h3><a href="https://github.com/joke2k/faker/compare/v40.43.0...v40.44.0">v40.44.0 - 2026-10-28</a></h3>
<ul>
<li>Fix: allow repeated digits in <code>pt_BR</code> CPF and RG generators (<a href="">#2457</a>). Thanks <a href="https://github.com/Sreekant13"><code>@​Sreekant13</code></a>.</li>
<li>Fix: keep <code>en_CA</code> SINs out of the 0 and 8 series (<a href="">#2467</a>). Thanks <a href="https://github.com/feiiiiii5"><code>@​feiiiiii5</code></a>.</li>
<li>Fix: use Luhn check digit for <code>no_NO</code> Postgiro (0000) BBANs (<a href="">#2468</a>). Thanks <a href="https://github.com/DYNOSuprovo"><code>@​DYNOSuprovo</code></a>.</li>
<li>Fix: <code>en_GB</code> VAT ID generation (<a href="">#2469</a>). Thanks <a href="https://github.com/orilucky"><code>@​orilucky</code></a>.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>685ea97</code></a> Bump version: 40.43.0 → 40.44.0</li>
<li><a href=""><code>c871efe</code></a> 📝 Update CHANGELOG.md</li>
<li><a href=""><code>bfacd97</code></a> Fixed en_GB VAT ID generation and added regression tests (<a href="">#2469</a>)</li>
<li><a href=""><code>19024ee</code></a> fix(no_NO): use Luhn check digit for Postgiro (0000) BBANs (<a href="">#2468</a>)</li>
<li><a href=""><code>496ed7a</code></a> fix(ssn): keep en_CA SINs out of the 0 and 8 series (<a href="">#2467</a>)</li>
<li><a href=""><code>73755da</code></a> fix(pt_BR): allow repeated digits in CPF and RG generators (<a href="">#2457</a>)</li>
<li>See full diff in <a href="https://github.com/joke2k/faker/compare/v40.43.0...v40.44.0">compare view</a></li>
</ul>
</details>
<br />

Updates `opentelemetry-sdk` from 1.45.1 to 1.45.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/open-telemetry/opentelemetry-python/releases">opentelemetry-sdk's releases</a>.</em></p>
<blockquote>
<h2>Version 1.45.2/0.66b2</h2>
<p>This is a patch release on the previous 1.45.1/0.66b1 release, fixing the issue(s) below.</p>
<h3>Added</h3>
<ul>
<li><code>opentelemetry-sdk</code>, <code>opentelemetry-configuration</code>, <code>opentelemetry-exporter-prometheus</code>: enforce metric cardinality limits (default 2000) with the <code>otel.metric.overflow</code> attribute, configurable through <code>View(aggregation_cardinality_limit=...)</code>, reader <code>cardinality_limits</code> and declarative configuration (<a href="">#5809</a>)</li>
</ul>
<h3>Fixed</h3>
<ul>
<li><code>opentelemetry-api</code>: limit <code>traceparent</code> header length to 512 characters in <code>TraceContextTextMapPropagator</code> during extraction (<a href="">#5818</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/open-telemetry/opentelemetry-python/blob/main/CHANGELOG.md">opentelemetry-sdk's changelog</a>.</em></p>
<blockquote>
<h2>Version 1.45.2/0.66b2 (2026-10-29)</h2>
<h3>Added</h3>
<ul>
<li><code>opentelemetry-sdk</code>, <code>opentelemetry-configuration</code>,
<code>opentelemetry-exporter-prometheus</code>: enforce metric cardinality limits
(default 2000) with the <code>otel.metric.overflow</code> attribute, configurable
through <code>View(aggregation_cardinality_limit=...)</code>, reader
<code>cardinality_limits</code> and declarative configuration
(<a href="">#5809</a>)</li>
</ul>
<h3>Fixed</h3>
<ul>
<li><code>opentelemetry-api</code>: limit <code>traceparent</code> header length to 512 characters in
<code>TraceContextTextMapPropagator</code> during extraction
(<a href="">#5818</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ad75594</code></a> [release/v1.45.x-0.66bx] Prepare release 1.45.2/0.66b2 (<a href="">#5862</a>)</li>
<li><a href=""><code>78123a2</code></a> [release/v1.45.x-0.66bx] Backport metric cardinality limits and traceparent p...</li>
<li>See full diff in <a href="https://github.com/open-telemetry/opentelemetry-python/compare/v1.45.1...v1.45.2">compare view</a></li>
</ul>
</details>
<br />

Updates `opentelemetry-exporter-otlp-proto-http` from 1.45.1 to 1.45.2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/open-telemetry/opentelemetry-python/releases">opentelemetry-exporter-otlp-proto-http's releases</a>.</em></p>
<blockquote>
<h2>Version 1.45.2/0.66b2</h2>
<p>This is a patch release on the previous 1.45.1/0.66b1 release, fixing the issue(s) below.</p>
<h3>Added</h3>
<ul>
<li><code>opentelemetry-sdk</code>, <code>opentelemetry-configuration</code>, <code>opentelemetry-exporter-prometheus</code>: enforce metric cardinality limits (default 2000) with the <code>otel.metric.overflow</code> attribute, configurable through <code>View(aggregation_cardinality_limit=...)</code>, reader <code>cardinality_limits</code> and declarative configuration (<a href="">#5809</a>)</li>
</ul>
<h3>Fixed</h3>
<ul>
<li><code>opentelemetry-api</code>: limit <code>traceparent</code> header length to 512 characters in <code>TraceContextTextMapPropagator</code> during extraction (<a href="">#5818</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/open-telemetry/opentelemetry-python/blob/main/CHANGELOG.md">opentelemetry-exporter-otlp-proto-http's changelog</a>.</em></p>
<blockquote>
<h2>Version 1.45.2/0.66b2 (2026-10-29)</h2>
<h3>Added</h3>
<ul>
<li><code>opentelemetry-sdk</code>, <code>opentelemetry-configuration</code>,
<code>opentelemetry-exporter-prometheus</code>: enforce metric cardinality limits
(default 2000) with the <code>otel.metric.overflow</code> attribute, configurable
through <code>View(aggregation_cardinality_limit=...)</code>, reader
<code>cardinality_limits</code> and declarative configuration
(<a href="">#5809</a>)</li>
</ul>
<h3>Fixed</h3>
<ul>
<li><code>opentelemetry-api</code>: limit <code>traceparent</code> header length to 512 characters in
<code>TraceContextTextMapPropagator</code> during extraction
(<a href="">#5818</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ad75594</code></a> [release/v1.45.x-0.66bx] Prepare release 1.45.2/0.66b2 (<a href="">#5862</a>)</li>
<li><a href=""><code>78123a2</code></a> [release/v1.45.x-0.66bx] Backport metric cardinality limits and traceparent p...</li>
<li>See full diff in <a href="https://github.com/open-telemetry/opentelemetry-python/compare/v1.45.1...v1.45.2">compare view</a></li>
</ul>
</details>
<br />

Updates `opentelemetry-instrumentation-logging` from 0.66b1 to 0.66b2
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/open-telemetry/opentelemetry-python-contrib/releases">opentelemetry-instrumentation-logging's releases</a>.</em></p>
<blockquote>
<h2>Version 1.45.2/0.66b2</h2>
<p>This is a patch release on the previous 1.45.1/0.66b1 release, fixing the issue(s) below.</p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/open-telemetry/opentelemetry-python-contrib/blob/main/CHANGELOG.md">opentelemetry-instrumentation-logging's changelog</a>.</em></p>
<blockquote>
<h1>Changelog</h1>
<p>All notable changes to this project will be documented in this file.</p>
<!-- raw HTML omitted -->
<p>The format is based on <a href="https://keepachangelog.com/en/1.0.0/">Keep a Changelog</a>,
and this project adheres to <a href="https://semver.org/spec/v2.0.0.html">Semantic Versioning</a>.</p>
<blockquote>
<p>[!NOTE]
The following components are released independently and maintain individual CHANGELOG files.
Use <a href="https://github.com/search?q=repo%3Aopen-telemetry%2Fopentelemetry-python-contrib+path%3A**%2FCHANGELOG.md&amp;type=code">this search for a list of all CHANGELOG.md files in this repo</a>.</p>
</blockquote>
<!-- raw HTML omitted -->
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/open-telemetry/opentelemetry-python-contrib/commits">compare view</a></li>
</ul>
</details>
<br />

Updates `ruff` from 0.17.1 to 0.17.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff/releases">ruff's releases</a>.</em></p>
<blockquote>
<h2>0.17.3</h2>
<h2>Release Notes</h2>
<p>Released on 2026-10-26.</p>
<h3>Preview features</h3>
<ul>
<li>[<code>suspicious</code>] Add <code>shared-clock-mock</code> (<a href="">#29074</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>[<code>pyupgrade</code>] Avoid incorrect conversions to f-strings (<code>UP032</code>) (<a href="">#25485</a>)</li>
</ul>
<h3>Performance</h3>
<ul>
<li>Buffer stdout in <code>ruff format</code> (<a href="">#29631</a>)</li>
<li>Specialize ASCII identifier lexing (<a href="">#29503</a>)</li>
<li>Speed up identifier and keyword lexing (<a href="">#29463</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>[<code>flake8-bandit</code>] Describe what the rule actually checks for <code>httpx</code> (<code>S113</code>) (<a href="">#27936</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/itsvedantkumar"><code>@​itsvedantkumar</code></a></li>
<li><a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a></li>
<li><a href="https://github.com/anishgirianish"><code>@​anishgirianish</code></a></li>
</ul>
<h2>Install ruff 0.17.3</h2>
<h3>Install prebuilt binaries via shell script</h3>
<pre lang="sh"><code>curl --proto '=https' --tlsv1.2 -LsSf https://releases.astral.sh/github/ruff/releases/download/0.17.3/ruff-installer.sh | sh
</code></pre>
<h3>Install prebuilt binaries via powershell script</h3>
<pre lang="sh"><code>powershell -ExecutionPolicy Bypass -c &quot;irm https://releases.astral.sh/github/ruff/releases/download/0.17.3/ruff-installer.ps1 | iex&quot;
</code></pre>
<h2>Download ruff 0.17.3</h2>
<table>
<thead>
<tr>
<th>File</th>
<th>Platform</th>
<th>Checksum</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://releases.astral.sh/github/ruff/releases/download/0.17.3/ruff-aarch64-apple-darwin.tar.gz">ruff-aarch64-apple-darwin.tar.gz</a></td>
<td>Apple Silicon macOS</td>
<td><a href="https://releases.astral.sh/github/ruff/releases/download/0.17.3/ruff-aarch64-apple-darwin.tar.gz.sha256">checksum</a></td>
</tr>
<tr>
<td><a href="https://releases.astral.sh/github/ruff/releases/download/0.17.3/ruff-x86_64-apple-darwin.tar.gz">ruff-x86_64-apple-darwin.tar.gz</a></td>
<td>Intel macOS</td>
<td><a href="https://releases.astral.sh/github/ruff/releases/download/0.17.3/ruff-x86_64-apple-darwin.tar.gz.sha256">checksum</a></td>
</tr>
<tr>
<td><a href="https://releases.astral.sh/github/ruff/releases/download/0.17.3/ruff-aarch64-pc-windows-msvc.zip">ruff-aarch64-pc-windows-msvc.zip</a></td>
<td>ARM64 Windows</td>
<td><a href="https://releases.astral.sh/github/ruff/releases/download/0.17.3/ruff-aarch64-pc-windows-msvc.zip.sha256">checksum</a></td>
</tr>
</tbody>
</table>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ruff/blob/main/CHANGELOG.md">ruff's changelog</a>.</em></p>
<blockquote>
<h2>0.17.3</h2>
<p>Released on 2026-10-26.</p>
<h3>Preview features</h3>
<ul>
<li>[<code>suspicious</code>] Add <code>shared-clock-mock</code> (<a href="">#29074</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>[<code>pyupgrade</code>] Avoid incorrect conversions to f-strings (<code>UP032</code>) (<a href="">#25485</a>)</li>
</ul>
<h3>Performance</h3>
<ul>
<li>Buffer stdout in <code>ruff format</code> (<a href="">#29631</a>)</li>
<li>Specialize ASCII identifier lexing (<a href="">#29503</a>)</li>
<li>Speed up identifier and keyword lexing (<a href="">#29463</a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li>[<code>flake8-bandit</code>] Describe what the rule actually checks for <code>httpx</code> (<code>S113</code>) (<a href="">#27936</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/itsvedantkumar"><code>@​itsvedantkumar</code></a></li>
<li><a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a></li>
<li><a href="https://github.com/anishgirianish"><code>@​anishgirianish</code></a></li>
</ul>
<h2>0.17.2</h2>
<p>Released on 2026-10-22.</p>
<h3>Preview features</h3>
<ul>
<li>[<code>complexity</code>] Add <code>unnecessary-regular-expression-compile</code> (<a href="">#25533</a>)</li>
</ul>
<h3>Bug fixes</h3>
<ul>
<li>Avoid syntax errors for type variables with starred constraints (<code>UP040</code>, <code>UP046</code>, <code>UP047</code>, <code>RUF053</code>) (<a href="">#28362</a>)</li>
<li>[<code>pydocstyle</code>] Treat backslash-escaped <code>*args</code> and <code>**kwargs</code> as documented (<code>D417</code>) (<a href="">#29536</a>)</li>
<li>[<code>pylint</code>] Avoid false positive on starred elements (<code>PLE0643</code>) (<a href="">#29483</a>)</li>
<li>[<code>pylint</code>] Mark fixes unsafe when deleting comments (<code>PLR5501</code>, <code>PLW0120</code>) (<a href="">#29414</a>)</li>
<li>[<code>pyupgrade</code>] Mark fix unsafe when deleting comments (<code>UP035</code>) (<a href="">#29413</a>)</li>
</ul>
<h3>Performance</h3>
<ul>
<li>Avoid intermediate names in lint name resolution (<a href="">#29506</a>)</li>
<li>Prefilter bidirectional Unicode checks by UTF-8 leading bytes (<a href="">#29561</a>)</li>
<li>Share postfix parsing and reduce expression copies (<a href="">#29480</a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>ba65abf</code></a> Bump version to 0.17.3 (<a href="">#29745</a>)</li>
<li><a href=""><code>fb2f921</code></a> [ty] Fix narrowing of strings and integers compared with enum members (<a href="">#29743</a>)</li>
<li><a href=""><code>d181287</code></a> [ty] Index nominal union alternatives (<a href="">#29196</a>)</li>
<li><a href=""><code>07872ad</code></a> [ty] Preserve string literals in comparisons with <code>LiteralString</code> (<a href="">#29741</a>)</li>
<li><a href=""><code>95888b2</code></a> [ty] Preserve narrowing after guarded match subject captures (<a href="">#29558</a>)</li>
<li><a href=""><code>3c8166b</code></a> [ty] Fix hang when negating recursive unions of instance types (<a href="">#29652</a>)</li>
<li><a href=""><code>3fd20e0</code></a> [ty] Preserve generic callback specializations during return refinement (<a href="">#29667</a>)</li>
<li><a href=""><code>2f0a29e</code></a> [ty] Record predicate truthiness alongside expression inference (<a href="">#29706</a>)</li>
<li><a href=""><code>60f104a</code></a> [ty] Honor <a href="https://github.com/override"><code>@​override</code></a> on overload implementations in stubs (<a href="">#29470</a>)</li>
<li><a href=""><code>207ec3a</code></a> [ty] Add diagnostic baseline support (<a href="">#27636</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/astral-sh/ruff/compare/0.17.1...0.17.3">compare view</a></li>
</ul>
</details>
<br />

Updates `ty` from 0.0.89 to 0.0.95
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ty/releases">ty's releases</a>.</em></p>
<blockquote>
<h2>0.0.95</h2>
<h2>Release Notes</h2>
<p>Released on 2026-10-29.</p>
<h3>Bug fixes</h3>
<ul>
<li>Accept another unpacked TypeVarTuple as a default (<a href="">#29752</a>)</li>
<li>Accept keyword arguments for <code>TypeAliasType</code> name and value (<a href="">#29802</a>)</li>
<li>Detect traversal budget exhaustion in products of lower bounds (<a href="">#29679</a>)</li>
<li>Fix recursive protocol materialization self-comparison (<a href="">#29809</a>)</li>
<li>Reject out-of-scope type variables in PEP 695 pack defaults (<a href="">#29805</a>)</li>
<li>Use a trailing ParamSpec default after a TypeVarTuple (<a href="">#29755</a>)</li>
</ul>
<h3>LSP server</h3>
<ul>
<li>Parenthesize assignment and generator expressions in argument hint edits (<a href="">#29797</a>)</li>
<li>Place argument name inlay hints before grouping parentheses (<a href="">#29794</a>)</li>
<li>Place variable type inlay hints after grouping parentheses (<a href="">#29795</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/carljm"><code>@​carljm</code></a></li>
<li><a href="https://github.com/AlexWaygood"><code>@​AlexWaygood</code></a></li>
<li><a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a></li>
</ul>
<h2>Install ty 0.0.95</h2>
<h3>Install prebuilt binaries via shell script</h3>
<pre lang="sh"><code>curl --proto '=https' --tlsv1.2 -LsSf https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-installer.sh | sh
</code></pre>
<h3>Install prebuilt binaries via powershell script</h3>
<pre lang="sh"><code>powershell -ExecutionPolicy Bypass -c &quot;irm https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-installer.ps1 | iex&quot;
</code></pre>
<h2>Download ty 0.0.95</h2>
<table>
<thead>
<tr>
<th>File</th>
<th>Platform</th>
<th>Checksum</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-aarch64-apple-darwin.tar.gz">ty-aarch64-apple-darwin.tar.gz</a></td>
<td>Apple Silicon macOS</td>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-aarch64-apple-darwin.tar.gz.sha256">checksum</a></td>
</tr>
<tr>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-x86_64-apple-darwin.tar.gz">ty-x86_64-apple-darwin.tar.gz</a></td>
<td>Intel macOS</td>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-x86_64-apple-darwin.tar.gz.sha256">checksum</a></td>
</tr>
<tr>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-aarch64-pc-windows-msvc.zip">ty-aarch64-pc-windows-msvc.zip</a></td>
<td>ARM64 Windows</td>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-aarch64-pc-windows-msvc.zip.sha256">checksum</a></td>
</tr>
<tr>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-i686-pc-windows-msvc.zip">ty-i686-pc-windows-msvc.zip</a></td>
<td>x86 Windows</td>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-i686-pc-windows-msvc.zip.sha256">checksum</a></td>
</tr>
<tr>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-x86_64-pc-windows-msvc.zip">ty-x86_64-pc-windows-msvc.zip</a></td>
<td>x64 Windows</td>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-x86_64-pc-windows-msvc.zip.sha256">checksum</a></td>
</tr>
<tr>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-aarch64-unknown-linux-gnu.tar.gz">ty-aarch64-unknown-linux-gnu.tar.gz</a></td>
<td>ARM64 Linux</td>
<td><a href="https://releases.astral.sh/github/ty/releases/download/0.0.95/ty-aarch64-unknown-linux-gnu.tar.gz.sha256">checksum</a></td>
</tr>
</tbody>
</table>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/astral-sh/ty/blob/main/CHANGELOG.md">ty's changelog</a>.</em></p>
<blockquote>
<h2>0.0.95</h2>
<p>Released on 2026-10-29.</p>
<h3>Bug fixes</h3>
<ul>
<li>Accept another unpacked TypeVarTuple as a default (<a href="">#29752</a>)</li>
<li>Accept keyword arguments for <code>TypeAliasType</code> name and value (<a href="">#29802</a>)</li>
<li>Detect traversal budget exhaustion in products of lower bounds (<a href="">#29679</a>)</li>
<li>Fix recursive protocol materialization self-comparison (<a href="">#29809</a>)</li>
<li>Reject out-of-scope type variables in PEP 695 pack defaults (<a href="">#29805</a>)</li>
<li>Use a trailing ParamSpec default after a TypeVarTuple (<a href="">#29755</a>)</li>
</ul>
<h3>LSP server</h3>
<ul>
<li>Parenthesize assignment and generator expressions in argument hint edits (<a href="">#29797</a>)</li>
<li>Place argument name inlay hints before grouping parentheses (<a href="">#29794</a>)</li>
<li>Place variable type inlay hints after grouping parentheses (<a href="">#29795</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/carljm"><code>@​carljm</code></a></li>
<li><a href="https://github.com/AlexWaygood"><code>@​AlexWaygood</code></a></li>
<li><a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a></li>
</ul>
<h2>0.0.94</h2>
<p>Released on 2026-10-28.</p>
<h3>Bug fixes</h3>
<ul>
<li>Correctly handle line continuation when fixing unused ignore comments (<a href="">#29781</a>)</li>
<li>Fix Linux x86-64 startup on older kernels (<a href="">#4853</a>)</li>
<li>Fix a panic when a comprehension filter depends on a later binding (<a href="">#29786</a>)</li>
<li>Fix a panic when sorting diagnostics without a source location (<a href="">#29780</a>)</li>
<li>Fix panic on a chained assignment with a missing value (<a href="">#29787</a>)</li>
<li>Reject defaulted TypeVars after a TypeVarTuple in legacy generic classes (<a href="">#29753</a>)</li>
</ul>
<h3>Other changes</h3>
<ul>
<li>Django: suppress invalid-override errors for <code>Meta</code> configurations (<a href="">#29769</a>)</li>
</ul>
<h3>Contributors</h3>
<ul>
<li><a href="https://github.com/sharkdp"><code>@​sharkdp</code></a></li>
<li><a href="https://github.com/charliermarsh"><code>@​charliermarsh</code></a></li>
<li><a href="https://github.com/MichaReiser"><code>@​MichaReiser</code></a></li>
</ul>
<h2>0.0.93</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>48c5ea1</code></a> Bump version to 0.0.95 (<a href="">#4870</a>)</li>
<li><a href=""><code>13ef399</code></a> Speed up releases by using larger runners for all Windows builds (<a href="">#4805</a>)</li>
<li><a href=""><code>f8ea270</code></a> Bump version to 0.0.94 (<a href="">#4857</a>)</li>
<li><a href=""><code>7a36fc9</code></a> Fix Linux x86-64 startup on older kernels (<a href="">#4853</a>)</li>
<li><a href=""><code>3db5e4d</code></a> Bump version to 0.0.93 (<a href="">#4842</a>)</li>
<li><a href=""><code>f8fd0e8</code></a> Update astral-sh/setup-uv action to v10.3.2 (<a href="">#4843</a>)</li>
<li><a href=""><code>c1ca420</code></a> Update uv to v0.13.6 (<a href="">#4845</a>)</li>
<li><a href=""><code>4c5c907</code></a> Update prek dependencies (<a href="">#4844</a>)</li>
<li><a href="

_Description has been truncated_

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1204faa2a7dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.