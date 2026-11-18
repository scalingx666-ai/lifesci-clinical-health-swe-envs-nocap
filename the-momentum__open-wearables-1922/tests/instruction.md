# Issue

**Title:** chore: update fastapi[opentelemetry] requirement from >=0.142.2 to >=0.143.1 in /backend

## Description

Updates the requirements on [fastapi[opentelemetry]](https://github.com/fastapi/fastapi) to permit the latest version.
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/fastapi/fastapi/releases">fastapi[opentelemetry]'s releases</a>.</em></p>
<blockquote>
<h2>0.143.1</h2>
<h3>Fixes</h3>
<ul>
<li>🐛 Fix included route metadata in <code>iter_route_contexts()</code>. PR <a href="">#16484</a> by <a href="https://github.com/tiangolo"><code>@​tiangolo</code></a>.</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>4dda462</code></a> 🔖 Release version 0.143.1 (<a href="">#16485</a>)</li>
<li><a href=""><code>bf18b23</code></a> 📝 Update release notes</li>
<li><a href=""><code>5e6a1ee</code></a> 🐛 Fix included route metadata in <code>iter_route_contexts()</code> (<a href="">#16484</a>)</li>
<li><a href=""><code>f5c6e9b</code></a> 🔖 Release version 0.143.0 (<a href="">#16477</a>)</li>
<li><a href=""><code>182c8b8</code></a> 📝 Update release notes</li>
<li><a href=""><code>af889e4</code></a> 💥 Require opt-in for automatic OpenTelemetry exporter setup (<a href="">#16476</a>)</li>
<li><a href=""><code>9269f17</code></a> 🔖 Release version 0.142.4 (<a href="">#16471</a>)</li>
<li><a href=""><code>78ede01</code></a> 📝 Update release notes</li>
<li><a href=""><code>4e31a07</code></a> 🐛 Isolate FastAPI telemetry for excluded requests (<a href="">#16470</a>)</li>
<li><a href=""><code>cb8dabc</code></a> 🔖 Release version 0.142.3 (<a href="">#16469</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/fastapi/fastapi/compare/0.142.2...0.143.1">compare view</a></li>
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