# Issue

**Title:** chore: bump the frontend-minor-patch group in /frontend with 4 updates

## Description

Bumps the frontend-minor-patch group in /frontend with 4 updates: [@types/node](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/HEAD/types/node), [eslint-plugin-svelte](https://github.com/sveltejs/eslint-plugin-svelte/tree/HEAD/packages/eslint-plugin-svelte), [prettier](https://github.com/prettier/prettier) and [vite](https://github.com/vitejs/vite/tree/HEAD/packages/vite).

Updates `@types/node` from 26.6.4 to 26.6.5
<details>
<summary>Commits</summary>
<ul>
<li>See full diff in <a href="https://github.com/DefinitelyTyped/DefinitelyTyped/commits/HEAD/types/node">compare view</a></li>
</ul>
</details>
<br />

Updates `eslint-plugin-svelte` from 3.23.0 to 3.23.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/sveltejs/eslint-plugin-svelte/releases">eslint-plugin-svelte's releases</a>.</em></p>
<blockquote>
<h2>eslint-plugin-svelte@3.23.1</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#1592</a> <a href=""><code>ed67eb7</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Exclude deprecated rules from the <code>all</code> configuration while keeping active rules enabled.</p>
</li>
<li>
<p><a href="">#1594</a> <a href=""><code>af288cd</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Recognize <code>browser</code> from SvelteKit's <code>$app/env</code> alias as a browser guard in <code>no-top-level-browser-globals</code>.</p>
</li>
<li>
<p><a href="">#1588</a> <a href=""><code>9814b51</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Include all active extension rules in the Extension Rules documentation table while preserving their primary-category entries.</p>
</li>
<li>
<p><a href="">#1589</a> <a href=""><code>57863c5</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Keep the documented project service configuration consistent across TypeScript and Svelte files to avoid unnecessary project reloads.</p>
</li>
<li>
<p><a href="">#1593</a> <a href=""><code>4ad2c67</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Limit <code>require-each-key</code> diagnostics to the opening each tag instead of the whole block.</p>
</li>
<li>
<p><a href="">#1599</a> <a href=""><code>90d7b09</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Enable no-navigation-without-resolve on SvelteKit 3 so the recommended config reports internal links and navigation calls that omit resolve().</p>
</li>
<li>
<p><a href="">#1590</a> <a href=""><code>a28563f</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Fix false positives in <code>no-immutable-reactive-statements</code> for TypeScript components when <code>ecmaFeatures.globalReturn</code> is enabled.</p>
</li>
<li>
<p><a href="">#1598</a> <a href=""><code>4607a2c</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Recognize SvelteKit 3 in rule conditions, including prereleases, and document version detection and routes configuration.</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/sveltejs/eslint-plugin-svelte/blob/main/packages/eslint-plugin-svelte/CHANGELOG.md">eslint-plugin-svelte's changelog</a>.</em></p>
<blockquote>
<h2>3.23.1</h2>
<h3>Patch Changes</h3>
<ul>
<li>
<p><a href="">#1592</a> <a href=""><code>ed67eb7</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Exclude deprecated rules from the <code>all</code> configuration while keeping active rules enabled.</p>
</li>
<li>
<p><a href="">#1594</a> <a href=""><code>af288cd</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Recognize <code>browser</code> from SvelteKit's <code>$app/env</code> alias as a browser guard in <code>no-top-level-browser-globals</code>.</p>
</li>
<li>
<p><a href="">#1588</a> <a href=""><code>9814b51</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Include all active extension rules in the Extension Rules documentation table while preserving their primary-category entries.</p>
</li>
<li>
<p><a href="">#1589</a> <a href=""><code>57863c5</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Keep the documented project service configuration consistent across TypeScript and Svelte files to avoid unnecessary project reloads.</p>
</li>
<li>
<p><a href="">#1593</a> <a href=""><code>4ad2c67</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Limit <code>require-each-key</code> diagnostics to the opening each tag instead of the whole block.</p>
</li>
<li>
<p><a href="">#1599</a> <a href=""><code>90d7b09</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Enable no-navigation-without-resolve on SvelteKit 3 so the recommended config reports internal links and navigation calls that omit resolve().</p>
</li>
<li>
<p><a href="">#1590</a> <a href=""><code>a28563f</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Fix false positives in <code>no-immutable-reactive-statements</code> for TypeScript components when <code>ecmaFeatures.globalReturn</code> is enabled.</p>
</li>
<li>
<p><a href="">#1598</a> <a href=""><code>4607a2c</code></a> Thanks <a href="https://github.com/baseballyama"><code>@​baseballyama</code></a>! - Recognize SvelteKit 3 in rule conditions, including prereleases, and document version detection and routes configuration.</p>
</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>24201e0</code></a> chore: release eslint-plugin-svelte (<a href="">#1604</a>)</li>
<li><a href=""><code>90d7b09</code></a> fix(no-navigation-without-resolve): enable on SvelteKit 3 (<a href="">#1599</a>)</li>
<li><a href=""><code>4607a2c</code></a> fix: recognize SvelteKit 3 in rule conditions (<a href="">#1598</a>)</li>
<li><a href=""><code>af288cd</code></a> fix(no-top-level-browser-globals): recognize app env browser guards (<a href="">#1594</a>)</li>
<li><a href=""><code>4ad2c67</code></a> fix(require-each-key): highlight only the opening tag (<a href="">#1593</a>)</li>
<li><a href=""><code>ed67eb7</code></a> fix: omit deprecated rules from the all preset (<a href="">#1592</a>)</li>
<li><a href=""><code>ed49083</code></a> test: show fixture paths in rule test titles (<a href="">#1591</a>)</li>
<li><a href=""><code>a28563f</code></a> fix(no-immutable-reactive-statements): handle globalReturn module scopes (<a href="">#1590</a>)</li>
<li><a href=""><code>57863c5</code></a> docs: share extra file extensions across typed linting (<a href="">#1589</a>)</li>
<li><a href=""><code>9814b51</code></a> docs: list all active extension rules in the extension table (<a href="">#1588</a>)</li>
<li>See full diff in <a href="https://github.com/sveltejs/eslint-plugin-svelte/commits/eslint-plugin-svelte@3.23.1/packages/eslint-plugin-svelte">compare view</a></li>
</ul>
</details>
<br />

Updates `prettier` from 3.9.9 to 3.9.10
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/prettier/prettier/releases">prettier's releases</a>.</em></p>
<blockquote>
<h2>3.9.10</h2>
<ul>
<li>Markdown: Update <code>micromark-extension-gfm-table</code> to fix the table parse issue on performance (<a href="">#20266</a> by <a href="https://github.com/fisker"><code>@​fisker</code></a>)</li>
</ul>
<p>🔗 <a href="https://github.com/prettier/prettier/blob/3.9.10/CHANGELOG.md#3910">Changelog</a></p>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/prettier/prettier/blob/main/CHANGELOG.md">prettier's changelog</a>.</em></p>
<blockquote>
<h1>3.9.10</h1>
<p><a href="https://github.com/prettier/prettier/compare/3.9.9...3.9.10">diff</a></p>
<h4>Markdown: Update <code>micromark-extension-gfm-table</code> to fix the table parse issue on performance (<a href="">#20266</a> by <a href="https://github.com/fisker"><code>@​fisker</code></a>)</h4>
<p>See <a href=""></a> for details.</p>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>1172b82</code></a> Release 3.9.10</li>
<li><a href=""><code>d014227</code></a> Update <code>micromark-extension-gfm-table</code> to fix the table parse issue on perfor...</li>
<li><a href=""><code>953b908</code></a> Bump Prettier dependency to 3.9.9</li>
<li><a href=""><code>ad8a6bf</code></a> Clean changelog_unreleased</li>
<li>See full diff in <a href="https://github.com/prettier/prettier/compare/3.9.9...3.9.10">compare view</a></li>
</ul>
</details>
<br />

Updates `vite` from 8.3.3 to 8.3.4
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/vitejs/vite/releases">vite's releases</a>.</em></p>
<blockquote>
<h2>v8.3.4</h2>
<h3>Features</h3>
<ul>
<li><strong>bundled-dev:</strong> support <code>import.meta.hot.acceptExports</code> (<a href="">#23463</a>) (<a href="">bc0f21c</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>avoid mutating hmr defaults (fix <a href="">#23575</a>) (<a href="">#23576</a>) (<a href="">574d5e3</a>)</li>
<li><strong>build:</strong> correct preloads when chunkImportMap is enabled with non-root base (<a href="">#23698</a>) (<a href="">2a8c0f0</a>)</li>
<li><strong>build:</strong> wait for in-flight stylesheets in preload helper (fix <a href="">#23652</a>) (<a href="">#23662</a>) (<a href="">036b745</a>)</li>
<li><strong>bundled-dev:</strong> serve <code>/@vite/client</code> and stub <code>@vite/env</code> (<a href="">#23664</a>) (<a href="">5afc5a8</a>)</li>
<li><strong>client:</strong> skip rewriting unchanged adopted styles (<a href="">#23697</a>) (<a href="">fa71469</a>)</li>
<li><strong>css:</strong> resolve imported preprocessors from their file path with lightningcss (<a href="">#23688</a>) (<a href="">cf52011</a>)</li>
<li><strong>deps:</strong> update all non-major dependencies (<a href="">#23648</a>) (<a href="">8a4c19c</a>)</li>
<li><strong>deps:</strong> update rolldown-related dependencies (<a href="">#23649</a>) (<a href="">794516d</a>)</li>
<li><strong>dev:</strong> a restart requested during a restart used to be dropped (fix <a href="">#23392</a>) (<a href="">#23484</a>) (<a href="">70d56ea</a>)</li>
<li>don't treat modules ending with js-like query as js (<a href="">#23687</a>) (<a href="">fcb6f12</a>)</li>
<li><strong>html:</strong> avoid adding filesystem root to watcher (<a href="">#23689</a>) (<a href="">3a7f2ae</a>)</li>
<li><strong>html:</strong> skip caching CSS of chunks in a cycle (fix <a href="">#23628</a>) (<a href="">#23636</a>) (<a href="">15d82f7</a>)</li>
<li><strong>optimizer:</strong> scan deep imports with custom extensions (<a href="">#23678</a>) (<a href="">8579189</a>)</li>
<li>remove input option unescaping for now (<a href="">#23694</a>) (<a href="">facc2fb</a>)</li>
<li><strong>server:</strong> match static aliases on path boundaries (<a href="">#23643</a>) (<a href="">b28db28</a>)</li>
<li><strong>watcher:</strong> normalize file before root check in <code>ensureWatchedFile</code> (<a href="">#23673</a>) (<a href="">12bb28c</a>)</li>
</ul>
<h3>Performance Improvements</h3>
<ul>
<li><strong>module-runner:</strong> skip cloning call sites that have no source map (<a href="">#23646</a>) (<a href="">3d67486</a>)</li>
</ul>
<h3>Code Refactoring</h3>
<ul>
<li><strong>bundled-dev:</strong> import CSS HMR helpers from <code>/@vite/client</code> (<a href="">#23674</a>) (<a href="">182f5b2</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/vitejs/vite/blob/main/packages/vite/CHANGELOG.md">vite's changelog</a>.</em></p>
<blockquote>
<h2><!-- raw HTML omitted --><a href="https://github.com/vitejs/vite/compare/v8.3.3...v8.3.4">8.3.4</a> (2026-10-08)<!-- raw HTML omitted --></h2>
<h3>Features</h3>
<ul>
<li><strong>bundled-dev:</strong> support <code>import.meta.hot.acceptExports</code> (<a href="">#23463</a>) (<a href="">bc0f21c</a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li>avoid mutating hmr defaults (fix <a href="">#23575</a>) (<a href="">#23576</a>) (<a href="">574d5e3</a>)</li>
<li><strong>build:</strong> correct preloads when chunkImportMap is enabled with non-root base (<a href="">#23698</a>) (<a href="">2a8c0f0</a>)</li>
<li><strong>build:</strong> wait for in-flight stylesheets in preload helper (fix <a href="">#23652</a>) (<a href="">#23662</a>) (<a href="">036b745</a>)</li>
<li><strong>bundled-dev:</strong> serve <code>/@vite/client</code> and stub <code>@vite/env</code> (<a href="">#23664</a>) (<a href="">5afc5a8</a>)</li>
<li><strong>client:</strong> skip rewriting unchanged adopted styles (<a href="">#23697</a>) (<a href="">fa71469</a>)</li>
<li><strong>css:</strong> resolve imported preprocessors from their file path with lightningcss (<a href="">#23688</a>) (<a href="">cf52011</a>)</li>
<li><strong>deps:</strong> update all non-major dependencies (<a href="">#23648</a>) (<a href="">8a4c19c</a>)</li>
<li><strong>deps:</strong> update rolldown-related dependencies (<a href="">#23649</a>) (<a href="">794516d</a>)</li>
<li><strong>dev:</strong> a restart requested during a restart used to be dropped (fix <a href="">#23392</a>) (<a href="">#23484</a>) (<a href="">70d56ea</a>)</li>
<li>don't treat modules ending with js-like query as js (<a href="">#23687</a>) (<a href="">fcb6f12</a>)</li>
<li><strong>html:</strong> avoid adding filesystem root to watcher (<a href="">#23689</a>) (<a href="">3a7f2ae</a>)</li>
<li><strong>html:</strong> skip caching CSS of chunks in a cycle (fix <a href="">#23628</a>) (<a href="">#23636</a>) (<a href="">15d82f7</a>)</li>
<li><strong>optimizer:</strong> scan deep imports with custom extensions (<a href="">#23678</a>) (<a href="">8579189</a>)</li>
<li>remove input option unescaping for now (<a href="">#23694</a>) (<a href="">facc2fb</a>)</li>
<li><strong>server:</strong> match static aliases on path boundaries (<a href="">#23643</a>) (<a href="">b28db28</a>)</li>
<li><strong>watcher:</strong> normalize file before root check in <code>ensureWatchedFile</code> (<a href="">#23673</a>) (<a href="">12bb28c</a>)</li>
</ul>
<h3>Performance Improvements</h3>
<ul>
<li><strong>module-runner:</strong> skip cloning call sites that have no source map (<a href="">#23646</a>) (<a href="">3d67486</a>)</li>
</ul>
<h3>Code Refactoring</h3>
<ul>
<li><strong>bundled-dev:</strong> import CSS HMR helpers from <code>/@vite/client</code> (<a href="">#23674</a>) (<a href="">182f5b2</a>)</li>
</ul>
</blockquote>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b6c20f6</code></a> release: v8.3.4 (<a href="">#23702</a>)</li>
<li><a href=""><code>b28db28</code></a> fix(server): match static aliases on path boundaries (<a href="">#23643</a>)</li>
<li><a href=""><code>bc0f21c</code></a> feat(bundled-dev): support <code>import.meta.hot.acceptExports</code> (<a href="">#23463</a>)</li>
<li><a href=""><code>fa71469</code></a> fix(client): skip rewriting unchanged adopted styles (<a href="">#23697</a>)</li>
<li><a href=""><code>2a8c0f0</code></a> fix(build): correct preloads when chunkImportMap is enabled with non-root bas...</li>
<li><a href=""><code>3a7f2ae</code></a> fix(html): avoid adding filesystem root to watcher (<a href="">#23689</a>)</li>
<li><a href=""><code>facc2fb</code></a> fix: remove input option unescaping for now (<a href="">#23694</a>)</li>
<li><a href=""><code>70d56ea</code></a> fix(dev): a restart requested during a restart used to be dropped (fix <a href="">#23392</a>...</li>
<li><a href=""><code>cf52011</code></a> fix(css): resolve imported preprocessors from their file path with lightningc...</li>
<li><a href=""><code>fcb6f12</code></a> fix: don't treat modules ending with js-like query as js (<a href="">#23687</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/vitejs/vite/commits/v8.3.4/packages/vite">compare view</a></li>
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
- `@dependabot ignore <dependency name> major version` will close this group update PR and stop Dependabot creating any more for the specific dependency's major version (unless you unignore this specific dependency's major version or upgrade to it yourself)
- `@dependabot ignore <dependency name> minor version` will close this group update PR and stop Dependabot creating any more for the specific dependency's minor version (unless you unignore this specific dependency's minor version or upgrade to it yourself)
- `@dependabot ignore <dependency name>` will close this group update PR and stop Dependabot creating any more for the specific dependency (unless you unignore this specific dependency or upgrade to it yourself)
- `@dependabot unignore <dependency name>` will remove all of the ignore conditions of the specified dependency
- `@dependabot unignore <dependency name> <ignore condition>` will remove the ignore condition of the specified dependency and ignore conditions

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5dafc145153d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.