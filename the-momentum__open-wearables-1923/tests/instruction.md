# Issue

**Title:** chore: update sentry-sdk[fastapi] requirement from >=2.70.0 to >=2.72.0 in /backend

## Description

Updates the requirements on [sentry-sdk[fastapi]](https://github.com/getsentry/sentry-python) to permit the latest version.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/getsentry/sentry-python/releases">sentry-sdk[fastapi]'s releases</a>.</em></p>
<blockquote>
<h2>2.72.0</h2>
<h3>New Features ✨</h3>
<h4>Asgi</h4>
<ul>
<li>Set <code>user_agent.original</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7794</a></li>
<li>Add <code>sentry.is_localhost</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7781</a></li>
</ul>
<h4>Boto3</h4>
<ul>
<li>Add <code>ServiceExtension</code> class by <a href="https://github.com/pabloDeputter"><code>@​pabloDeputter</code></a> in <a href="">#7536</a></li>
<li>Add response, retry, and error span attributes by <a href="https://github.com/pabloDeputter"><code>@​pabloDeputter</code></a> in <a href="">#7499</a></li>
<li>Add common OTel AWS client attributes by <a href="https://github.com/pabloDeputter"><code>@​pabloDeputter</code></a> in <a href="">#7481</a></li>
</ul>
<h4>Wsgi</h4>
<ul>
<li>Add <code>user_agent.original</code> attr for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7793</a></li>
<li>Add <code>sentry.is_localhost</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7780</a></li>
</ul>
<h4>Other</h4>
<ul>
<li>(aiohttp) Add <code>sentry.is_localhost</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7785</a></li>
<li>(aiohttp,sanic,tornado) Add <code>user_agent.original</code> attr for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7795</a></li>
<li>(sanic) Add <code>sentry.is_localhost</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7783</a></li>
<li>(tornado) Add <code>sentry.is_localhost</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7787</a></li>
<li>(types) Export DataCollectionUserOptions from sentry_sdk.types by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7957</a></li>
<li>Better IPv6 localhost detection by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7786</a></li>
</ul>
<h3>Bug Fixes 🐛</h3>
<h4>Boto3</h4>
<ul>
<li>Trace the complete botocore client-call lifecycle by <a href="https://github.com/pabloDeputter"><code>@​pabloDeputter</code></a> in <a href="">#7538</a></li>
<li>Finish <code>StreamingBody</code> span correctly by <a href="https://github.com/pabloDeputter"><code>@​pabloDeputter</code></a> in <a href="">#7540</a></li>
</ul>
<h4>Other</h4>
<ul>
<li>(crons) Return <code>None</code> from <code>capture_checkin</code> when nothing is sent by <a href="https://github.com/HardMax71"><code>@​HardMax71</code></a> in <a href="">#7868</a></li>
<li>(scrubber) Scrub request bodies that are JSON arrays by <a href="https://github.com/Om-singhaI"><code>@​Om-singhaI</code></a> in <a href="">#7561</a></li>
<li>Fix span, metrics, log client reports by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7933</a></li>
</ul>
<h3>Internal Changes 🔧</h3>
<h4>Deps</h4>
<ul>
<li>Lock file maintenance by <a href="https://github.com/renovate"><code>@​renovate</code></a> in <a href="">#7848</a></li>
<li>Lock file maintenance by <a href="https://github.com/renovate"><code>@​renovate</code></a> in <a href="">#7484</a></li>
</ul>
<h4>Openai Agents</h4>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/getsentry/sentry-python/blob/master/CHANGELOG.md">sentry-sdk[fastapi]'s changelog</a>.</em></p>
<blockquote>
<h2>2.72.0</h2>
<h3>New Features ✨</h3>
<h4>Asgi</h4>
<ul>
<li>Set <code>user_agent.original</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7794</a></li>
<li>Add <code>sentry.is_localhost</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7781</a></li>
</ul>
<h4>Boto3</h4>
<ul>
<li>Add <code>ServiceExtension</code> class by <a href="https://github.com/pabloDeputter"><code>@​pabloDeputter</code></a> in <a href="">#7536</a></li>
<li>Add response, retry, and error span attributes by <a href="https://github.com/pabloDeputter"><code>@​pabloDeputter</code></a> in <a href="">#7499</a></li>
<li>Add common OTel AWS client attributes by <a href="https://github.com/pabloDeputter"><code>@​pabloDeputter</code></a> in <a href="">#7481</a></li>
</ul>
<h4>Wsgi</h4>
<ul>
<li>Add <code>user_agent.original</code> attr for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7793</a></li>
<li>Add <code>sentry.is_localhost</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7780</a></li>
</ul>
<h4>Other</h4>
<ul>
<li>(aiohttp) Add <code>sentry.is_localhost</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7785</a></li>
<li>(aiohttp,sanic,tornado) Add <code>user_agent.original</code> attr for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7795</a></li>
<li>(sanic) Add <code>sentry.is_localhost</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7783</a></li>
<li>(tornado) Add <code>sentry.is_localhost</code> for inbound filters by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7787</a></li>
<li>(types) Export DataCollectionUserOptions from sentry_sdk.types by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7957</a></li>
<li>Better IPv6 localhost detection by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7786</a></li>
</ul>
<h3>Bug Fixes 🐛</h3>
<h4>Boto3</h4>
<ul>
<li>Trace the complete botocore client-call lifecycle by <a href="https://github.com/pabloDeputter"><code>@​pabloDeputter</code></a> in <a href="">#7538</a></li>
<li>Finish <code>StreamingBody</code> span correctly by <a href="https://github.com/pabloDeputter"><code>@​pabloDeputter</code></a> in <a href="">#7540</a></li>
</ul>
<h4>Other</h4>
<ul>
<li>(crons) Return <code>None</code> from <code>capture_checkin</code> when nothing is sent by <a href="https://github.com/HardMax71"><code>@​HardMax71</code></a> in <a href="">#7868</a></li>
<li>(scrubber) Scrub request bodies that are JSON arrays by <a href="https://github.com/Om-singhaI"><code>@​Om-singhaI</code></a> in <a href="">#7561</a></li>
<li>Fix span, metrics, log client reports by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#7933</a></li>
</ul>
<h3>Internal Changes 🔧</h3>
<h4>Deps</h4>
<ul>
<li>Lock file maintenance by <a href="https://github.com/renovate"><code>@​renovate</code></a> in <a href="">#7848</a></li>
<li>Lock file maintenance by <a href="https://github.com/renovate"><code>@​renovate</code></a> in <a href="">#7484</a></li>
</ul>
<h4>Openai Agents</h4>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>9d24514</code></a> release: 2.72.0</li>
<li><a href=""><code>4dc1d72</code></a> fix: Fix span, metrics, log client reports (<a href="">#7933</a>)</li>
<li><a href=""><code>5780399</code></a> feat(types): Export DataCollectionUserOptions from sentry_sdk.types (<a href="">#7957</a>)</li>
<li><a href=""><code>1ca0326</code></a> chore(deps): lock file maintenance (<a href="">#7848</a>)</li>
<li><a href=""><code>f5bf69b</code></a> ci(mypy): Bump version to 2.4.0 (<a href="">#7937</a>)</li>
<li><a href=""><code>02210fa</code></a> ci(openai-agents): Bump version for type checking to 0.23.1 (<a href="">#7935</a>)</li>
<li><a href=""><code>fcccb7b</code></a> ci(strawberry-graphql): Bump version for type checking to 0.332.0 (<a href="">#7936</a>)</li>
<li><a href=""><code>7cb8094</code></a> chore: Deprecate <code>ai.monitoring.record_token_usage()</code> (<a href="">#7918</a>)</li>
<li><a href=""><code>1f4ba26</code></a> chore: Deprecate <code>send_default_pii</code> (<a href="">#7694</a>)</li>
<li><a href=""><code>4b9d329</code></a> refactor: move FastAPI active thread tracking into Starlette (<a href="">#7825</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/getsentry/sentry-python/compare/2.70.0...2.72.0">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65855e82922b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.