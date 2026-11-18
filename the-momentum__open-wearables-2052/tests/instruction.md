# Issue

**Title:** chore: update sentry-sdk[fastapi] requirement from >=2.72.0 to >=2.73.0 in /backend

## Description

Updates the requirements on [sentry-sdk[fastapi]](https://github.com/getsentry/sentry-python) to permit the latest version.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/getsentry/sentry-python/releases">sentry-sdk[fastapi]'s releases</a>.</em></p>
<blockquote>
<h2>2.73.0</h2>
<h3>New Features ✨</h3>
<ul>
<li>(arq) Add an option to monitor arq cron jobs by <a href="https://github.com/wedamija"><code>@​wedamija</code></a> in <a href="">#8051</a></li>
<li>(huey) Add an option to monitor Huey periodic tasks by <a href="https://github.com/wedamija"><code>@​wedamija</code></a> in <a href="">#8052</a></li>
<li>(rq) Add an option to monitor rq-scheduler jobs by <a href="https://github.com/wedamija"><code>@​wedamija</code></a> in <a href="">#8053</a></li>
<li>(types) Export Attributes from the public types module by <a href="https://github.com/sansynx"><code>@​sansynx</code></a> in <a href="">#8019</a></li>
</ul>
<h3>Bug Fixes 🐛</h3>
<ul>
<li>(arq) Don't monitor cron jobs with unsupported schedules by <a href="https://github.com/wedamija"><code>@​wedamija</code></a> in <a href="">#8098</a></li>
<li>(attributes) Handle special float values correctly by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#8067</a></li>
<li>(celery) Don't round down beat schedule intervals by <a href="https://github.com/wedamija"><code>@​wedamija</code></a> in <a href="">#7842</a></li>
<li>(cohere) Stop swallowing exceptions during stream iteration by <a href="https://github.com/intertermux-code"><code>@​intertermux-code</code></a> in <a href="">#8017</a></li>
<li>(huggingface_hub) Stop swallowing exceptions during stream iteration by <a href="https://github.com/intertermux-code"><code>@​intertermux-code</code></a> in <a href="">#8018</a></li>
<li>Exclude litellm==1.107.0 from extras by <a href="https://github.com/jonny-norwine"><code>@​jonny-norwine</code></a> in <a href="">#8104</a></li>
</ul>
<h3>Internal Changes 🔧</h3>
<h4>Deps</h4>
<ul>
<li>Update github workflows by <a href="https://github.com/renovate"><code>@​renovate</code></a> in <a href="">#8045</a></li>
<li>Update github workflows by <a href="https://github.com/renovate"><code>@​renovate</code></a> in <a href="">#8036</a></li>
<li>Update github workflows by <a href="https://github.com/renovate"><code>@​renovate</code></a> in <a href="">#7276</a></li>
</ul>
<h4>Other</h4>
<ul>
<li>(litellm) Require filelock&gt;=4.0.3 on Python 3.10/3.11 by <a href="https://github.com/sentry-junior"><code>@​sentry-junior</code></a> in <a href="">#8026</a></li>
<li>(monitor) Stop background health checks in tests that drive the monitor by <a href="https://github.com/sentry-junior"><code>@​sentry-junior</code></a> in <a href="">#8032</a></li>
<li>Update <code>AGENTS.md</code> by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#8077</a></li>
<li>🤖 Update test matrix with new releases (10/12) by <a href="https://github.com/github-actions"><code>@​github-actions</code></a> in <a href="">#7944</a></li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/getsentry/sentry-python/blob/master/CHANGELOG.md">sentry-sdk[fastapi]'s changelog</a>.</em></p>
<blockquote>
<h2>2.73.0</h2>
<h3>New Features ✨</h3>
<ul>
<li>(arq) Add an option to monitor arq cron jobs by <a href="https://github.com/wedamija"><code>@​wedamija</code></a> in <a href="">#8051</a></li>
<li>(huey) Add an option to monitor Huey periodic tasks by <a href="https://github.com/wedamija"><code>@​wedamija</code></a> in <a href="">#8052</a></li>
<li>(rq) Add an option to monitor rq-scheduler jobs by <a href="https://github.com/wedamija"><code>@​wedamija</code></a> in <a href="">#8053</a></li>
<li>(types) Export Attributes from the public types module by <a href="https://github.com/sansynx"><code>@​sansynx</code></a> in <a href="">#8019</a></li>
</ul>
<h3>Bug Fixes 🐛</h3>
<ul>
<li>(arq) Don't monitor cron jobs with unsupported schedules by <a href="https://github.com/wedamija"><code>@​wedamija</code></a> in <a href="">#8098</a></li>
<li>(attributes) Handle special float values correctly by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#8067</a></li>
<li>(celery) Don't round down beat schedule intervals by <a href="https://github.com/wedamija"><code>@​wedamija</code></a> in <a href="">#7842</a></li>
<li>(cohere) Stop swallowing exceptions during stream iteration by <a href="https://github.com/intertermux-code"><code>@​intertermux-code</code></a> in <a href="">#8017</a></li>
<li>(huggingface_hub) Stop swallowing exceptions during stream iteration by <a href="https://github.com/intertermux-code"><code>@​intertermux-code</code></a> in <a href="">#8018</a></li>
<li>Exclude litellm==1.107.0 from extras by <a href="https://github.com/jonny-norwine"><code>@​jonny-norwine</code></a> in <a href="">#8104</a></li>
</ul>
<h3>Internal Changes 🔧</h3>
<h4>Deps</h4>
<ul>
<li>Update github workflows by <a href="https://github.com/renovate"><code>@​renovate</code></a> in <a href="">#8045</a></li>
<li>Update github workflows by <a href="https://github.com/renovate"><code>@​renovate</code></a> in <a href="">#8036</a></li>
<li>Update github workflows by <a href="https://github.com/renovate"><code>@​renovate</code></a> in <a href="">#7276</a></li>
</ul>
<h4>Other</h4>
<ul>
<li>(litellm) Require filelock&gt;=4.0.3 on Python 3.10/3.11 by <a href="https://github.com/sentry-junior"><code>@​sentry-junior</code></a> in <a href="">#8026</a></li>
<li>(monitor) Stop background health checks in tests that drive the monitor by <a href="https://github.com/sentry-junior"><code>@​sentry-junior</code></a> in <a href="">#8032</a></li>
<li>Update <code>AGENTS.md</code> by <a href="https://github.com/sentrivana"><code>@​sentrivana</code></a> in <a href="">#8077</a></li>
<li>🤖 Update test matrix with new releases (10/12) by <a href="https://github.com/github-actions"><code>@​github-actions</code></a> in <a href="">#7944</a></li>
</ul>
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
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>54160ae</code></a> release: 2.73.0</li>
<li><a href=""><code>25d265b</code></a> fix: Exclude litellm==1.107.0 from extras (<a href="">#8104</a>)</li>
<li><a href=""><code>60116ac</code></a> fix(celery): Don't round down beat schedule intervals (<a href="">#7842</a>)</li>
<li><a href=""><code>68bc4dd</code></a> fix(arq): Don't monitor cron jobs with unsupported schedules (<a href="">#8098</a>)</li>
<li><a href=""><code>1c249d8</code></a> feat(huey): Add an option to monitor Huey periodic tasks (<a href="">#8052</a>)</li>
<li><a href=""><code>4e19592</code></a> feat(rq): Add an option to monitor rq-scheduler jobs (<a href="">#8053</a>)</li>
<li><a href=""><code>f8b08b3</code></a> meta: Update <code>AGENTS.md</code> (<a href="">#8077</a>)</li>
<li><a href=""><code>cfce72f</code></a> chore(deps): bump uv from 0.13.0 to 0.13.4 (<a href="">#8095</a>)</li>
<li><a href=""><code>a9553c4</code></a> feat(arq): Add an option to monitor arq cron jobs (<a href="">#8051</a>)</li>
<li><a href=""><code>641517a</code></a> fix(attributes): Handle special float values correctly (<a href="">#8067</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/getsentry/sentry-python/compare/2.72.0...2.73.0">compare view</a></li>
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

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e7f842717d9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.