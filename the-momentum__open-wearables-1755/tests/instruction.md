# Issue

**Title:** chore: update sentry-sdk[fastapi] requirement from >=2.69.2 to >=2.70.0 in /backend

## Description

Updates the requirements on [sentry-sdk[fastapi]](https://github.com/getsentry/sentry-python) to permit the latest version.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/getsentry/sentry-python/releases">sentry-sdk[fastapi]'s releases</a>.</em></p>
<blockquote>
<h2>2.70.0</h2>
<h3>New Features ✨</h3>
<ul>
<li>
<p><strong>New integration:</strong> Mistral AI (<a href="">#4733</a>) by <a href="https://github.com/alexander-alderman-webb"><code>@​alexander-alderman-webb</code></a></p>
<p>Add the Mistral integration to your <code>sentry_sdk.init</code> call:</p>
</li>
</ul>
<pre lang="python"><code>import sentry_sdk
from sentry_sdk.integrations.mistral import MistralIntegration
<p>sentry_sdk.init(
dsn=&quot;...&quot;,
traces_sample_rate=1.0,
integrations=[
MistralIntegration(),
]
)
</code></pre></p>
<ul>
<li>
<p><strong>New option:</strong> A fine-grained way to configure what data should be sent from the SDK.</p>
<p>Offers much more flexibility than <code>send_default_pii</code>, allowing you to specify what
data should be collected. If <code>data_collection</code> is defined, it takes precedence over
<code>send_default_pii</code>.</p>
<p>See <a href="https://docs.sentry.io/platforms/python/configuration/options/#data_collection">https://docs.sentry.io/platforms/python/configuration/options/#data_collection</a>
for the available configuration options.</p>
</li>
</ul>
<pre lang="python"><code>import sentry_sdk
<p>sentry_sdk.init(
data_collection={
&quot;user_info&quot;: False,
&quot;gen_ai&quot;: {&quot;inputs&quot;: False, &quot;outputs&quot;: False},
&quot;graphql&quot;: {&quot;document&quot;: False, &quot;variables&quot;: False},
&quot;database_query_data&quot;: False,
&quot;queues&quot;: False,
&quot;http_bodies&quot;: [],
&quot;cookies&quot;: {
&quot;mode&quot;: &quot;denylist&quot;,
&quot;terms&quot;: [&quot;forwarded&quot;, &quot;-ip&quot;, &quot;remote-&quot;, &quot;via&quot;, &quot;-user&quot;],
},
&quot;http_headers&quot;: {
&quot;request&quot;: {
&quot;mode&quot;: &quot;denylist&quot;,
&quot;terms&quot;: [&quot;forwarded&quot;, &quot;-ip&quot;, &quot;remote-&quot;, &quot;via&quot;, &quot;-user&quot;],
},
},
&lt;/tr&gt;&lt;/table&gt;
</code></pre></p>
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/getsentry/sentry-python/blob/master/CHANGELOG.md">sentry-sdk[fastapi]'s changelog</a>.</em></p>
<blockquote>
<h2>2.70.0</h2>
<h3>New Features ✨</h3>
<ul>
<li>
<p><strong>New integration:</strong> Mistral AI (<a href="">#4733</a>) by <a href="https://github.com/alexander-alderman-webb"><code>@​alexander-alderman-webb</code></a></p>
<p>Add the Mistral integration to your <code>sentry_sdk.init</code> call:</p>
</li>
</ul>
<pre lang="python"><code>import sentry_sdk
from sentry_sdk.integrations.mistral import MistralIntegration
<p>sentry_sdk.init(
dsn=&quot;...&quot;,
traces_sample_rate=1.0,
integrations=[
MistralIntegration(),
]
)
</code></pre></p>
<ul>
<li>
<p><strong>New option:</strong> A fine-grained way to configure what data should be sent from the SDK.</p>
<p>Offers much more flexibility than <code>send_default_pii</code>, allowing you to specify what
data should be collected. If <code>data_collection</code> is defined, it takes precedence over
<code>send_default_pii</code>.</p>
<p>See <a href="https://docs.sentry.io/platforms/python/configuration/options/#data_collection">https://docs.sentry.io/platforms/python/configuration/options/#data_collection</a>
for the available configuration options.</p>
</li>
</ul>
<pre lang="python"><code>import sentry_sdk
<p>sentry_sdk.init(
data_collection={
&quot;user_info&quot;: False,
&quot;gen_ai&quot;: {&quot;inputs&quot;: False, &quot;outputs&quot;: False},
&quot;graphql&quot;: {&quot;document&quot;: False, &quot;variables&quot;: False},
&quot;database_query_data&quot;: False,
&quot;queues&quot;: False,
&quot;http_bodies&quot;: [],
&quot;cookies&quot;: {
&quot;mode&quot;: &quot;denylist&quot;,
&quot;terms&quot;: [&quot;forwarded&quot;, &quot;-ip&quot;, &quot;remote-&quot;, &quot;via&quot;, &quot;-user&quot;],
},
&quot;http_headers&quot;: {
&quot;request&quot;: {
&quot;mode&quot;: &quot;denylist&quot;,
&quot;terms&quot;: [&quot;forwarded&quot;, &quot;-ip&quot;, &quot;remote-&quot;, &quot;via&quot;, &quot;-user&quot;],
},
&lt;/tr&gt;&lt;/table&gt;
</code></pre></p>
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1eb7df5</code></a> Update CHANGELOG.md</li>
<li><a href=""><code>92fd42b</code></a> release: 2.70.0</li>
<li><a href=""><code>d99edef</code></a> ref(data-collection): Promote <code>data_collection</code> from <code>_experiments</code> o top-lev...</li>
<li><a href=""><code>045d2c1</code></a> test: Close client on teardown (<a href="">#7562</a>)</li>
<li><a href=""><code>b454d7d</code></a> feat(mistral): Record <code>gen_ai.output.messages</code> (<a href="">#7549</a>)</li>
<li><a href=""><code>bdfd68c</code></a> feat(mistral): Record <code>gen_ai.input.messages</code> (<a href="">#7548</a>)</li>
<li><a href=""><code>ea08f64</code></a> feat(mistral): Record <code>gen_ai.system_instructions</code> (<a href="">#7547</a>)</li>
<li><a href=""><code>dbddd0e</code></a> feat(mistral): Record request parameters (<a href="">#7531</a>)</li>
<li><a href=""><code>9342968</code></a> feat(mistral): Record token usage (<a href="">#7529</a>)</li>
<li><a href=""><code>988fd0e</code></a> feat(mistral): Add integration with <code>Chat.complete</code> and <code>Chat.complete_async</code>...</li>
<li>Additional commits viewable in <a href="https://github.com/getsentry/sentry-python/compare/2.69.2...2.70.0">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b03587b3ffb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.