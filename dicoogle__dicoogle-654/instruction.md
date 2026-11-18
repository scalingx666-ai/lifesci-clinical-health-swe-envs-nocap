# Issue

**Title:** Bump semver, @babel/core and @babel/preset-env in /webcore

## Description

Bumps [semver](https://github.com/npm/node-semver) to 7.5.3 and updates ancestor dependencies [semver](https://github.com/npm/node-semver), [@babel/core](https://github.com/babel/babel/tree/HEAD/packages/babel-core) and [@babel/preset-env](https://github.com/babel/babel/tree/HEAD/packages/babel-preset-env). These dependencies need to be updated together.

Updates `semver` from 7.3.8 to 7.5.3
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/npm/node-semver/releases">semver's releases</a>.</em></p>
<blockquote>
<h2>v7.5.3</h2>
<h2><a href="https://github.com/npm/node-semver/compare/v7.5.2...v7.5.3">7.5.3</a> (2023-06-22)</h2>
<h3>Bug Fixes</h3>
<ul>
<li><a href=""><code>abdd93d</code></a> <a href="">#571</a> set max lengths in regex for numeric and build identifiers (<a href="">#571</a>) (<a href="https://github.com/lukekarrys"><code>@​lukekarrys</code></a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li><a href=""><code>bf53dd8</code></a> <a href="">#569</a> add example for <code>&gt;</code> comparator (<a href="">#569</a>) (<a href="https://github.com/mbtools"><code>@​mbtools</code></a>)</li>
</ul>
<h2>v7.5.2</h2>
<h2><a href="https://github.com/npm/node-semver/compare/v7.5.1...v7.5.2">7.5.2</a> (2023-06-15)</h2>
<h3>Bug Fixes</h3>
<ul>
<li><a href=""><code>58c791f</code></a> <a href="">#566</a> diff when detecting major change from prerelease (<a href="">#566</a>) (<a href="https://github.com/lukekarrys"><code>@​lukekarrys</code></a>)</li>
<li><a href=""><code>5c8efbc</code></a> <a href="">#565</a> preserve build in raw after inc (<a href="">#565</a>) (<a href="https://github.com/lukekarrys"><code>@​lukekarrys</code></a>)</li>
<li><a href=""><code>717534e</code></a> <a href="">#564</a> better handling of whitespace (<a href="">#564</a>) (<a href="https://github.com/lukekarrys"><code>@​lukekarrys</code></a>)</li>
</ul>
<h2>v7.5.1</h2>
<h2><a href="https://github.com/npm/node-semver/compare/v7.5.0...v7.5.1">7.5.1</a> (2023-05-12)</h2>
<h3>Bug Fixes</h3>
<ul>
<li><a href=""><code>d30d25a</code></a> <a href="">#559</a> show type on invalid semver error (<a href="">#559</a>) (<a href="https://github.com/tjenkinson"><code>@​tjenkinson</code></a>)</li>
</ul>
<h2>v7.5.0</h2>
<h2><a href="https://github.com/npm/node-semver/compare/v7.4.0...v7.5.0">7.5.0</a> (2023-04-17)</h2>
<h3>Features</h3>
<ul>
<li><a href=""><code>503a4e5</code></a> <a href="">#548</a> allow identifierBase to be false (<a href="">#548</a>) (<a href="https://github.com/lsvalina"><code>@​lsvalina</code></a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li><a href=""><code>e219bb4</code></a> <a href="">#552</a> throw on bad version with correct error message (<a href="">#552</a>) (<a href="https://github.com/wraithgar"><code>@​wraithgar</code></a>)</li>
<li><a href=""><code>fc2f3df</code></a> <a href="">#546</a> incorrect results from diff sometimes with prerelease versions (<a href="">#546</a>) (<a href="https://github.com/tjenkinson"><code>@​tjenkinson</code></a>)</li>
<li><a href=""><code>2781767</code></a> <a href="">#547</a> avoid re-instantiating SemVer during diff compare (<a href="">#547</a>) (<a href="https://github.com/macno"><code>@​macno</code></a>)</li>
</ul>
<h2>v7.4.0</h2>
<h2><a href="https://github.com/npm/node-semver/compare/v7.3.8...v7.4.0">7.4.0</a> (2023-04-10)</h2>
<h3>Features</h3>
<ul>
<li><a href=""><code>113f513</code></a> <a href="">#532</a> identifierBase parameter for .inc (<a href="">#532</a>) (<a href="https://github.com/wraithgar"><code>@​wraithgar</code></a>, <a href="https://github.com/b-bly"><code>@​b-bly</code></a>)</li>
<li><a href=""><code>48d8f8f</code></a> <a href="">#530</a> export new RELEASE_TYPES constant (<a href="https://github.com/hcharley"><code>@​hcharley</code></a>)</li>
</ul>
<h3>Bug Fixes</h3>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/npm/node-semver/blob/main/CHANGELOG.md">semver's changelog</a>.</em></p>
<blockquote>
<h2><a href="https://github.com/npm/node-semver/compare/v7.5.2...v7.5.3">7.5.3</a> (2023-06-22)</h2>
<h3>Bug Fixes</h3>
<ul>
<li><a href=""><code>abdd93d</code></a> <a href="">#571</a> set max lengths in regex for numeric and build identifiers (<a href="">#571</a>) (<a href="https://github.com/lukekarrys"><code>@​lukekarrys</code></a>)</li>
</ul>
<h3>Documentation</h3>
<ul>
<li><a href=""><code>bf53dd8</code></a> <a href="">#569</a> add example for <code>&gt;</code> comparator (<a href="">#569</a>) (<a href="https://github.com/mbtools"><code>@​mbtools</code></a>)</li>
</ul>
<h2><a href="https://github.com/npm/node-semver/compare/v7.5.1...v7.5.2">7.5.2</a> (2023-06-15)</h2>
<h3>Bug Fixes</h3>
<ul>
<li><a href=""><code>58c791f</code></a> <a href="">#566</a> diff when detecting major change from prerelease (<a href="">#566</a>) (<a href="https://github.com/lukekarrys"><code>@​lukekarrys</code></a>)</li>
<li><a href=""><code>5c8efbc</code></a> <a href="">#565</a> preserve build in raw after inc (<a href="">#565</a>) (<a href="https://github.com/lukekarrys"><code>@​lukekarrys</code></a>)</li>
<li><a href=""><code>717534e</code></a> <a href="">#564</a> better handling of whitespace (<a href="">#564</a>) (<a href="https://github.com/lukekarrys"><code>@​lukekarrys</code></a>)</li>
</ul>
<h2><a href="https://github.com/npm/node-semver/compare/v7.5.0...v7.5.1">7.5.1</a> (2023-05-12)</h2>
<h3>Bug Fixes</h3>
<ul>
<li><a href=""><code>d30d25a</code></a> <a href="">#559</a> show type on invalid semver error (<a href="">#559</a>) (<a href="https://github.com/tjenkinson"><code>@​tjenkinson</code></a>)</li>
</ul>
<h2><a href="https://github.com/npm/node-semver/compare/v7.4.0...v7.5.0">7.5.0</a> (2023-04-17)</h2>
<h3>Features</h3>
<ul>
<li><a href=""><code>503a4e5</code></a> <a href="">#548</a> allow identifierBase to be false (<a href="">#548</a>) (<a href="https://github.com/lsvalina"><code>@​lsvalina</code></a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li><a href=""><code>e219bb4</code></a> <a href="">#552</a> throw on bad version with correct error message (<a href="">#552</a>) (<a href="https://github.com/wraithgar"><code>@​wraithgar</code></a>)</li>
<li><a href=""><code>fc2f3df</code></a> <a href="">#546</a> incorrect results from diff sometimes with prerelease versions (<a href="">#546</a>) (<a href="https://github.com/tjenkinson"><code>@​tjenkinson</code></a>)</li>
<li><a href=""><code>2781767</code></a> <a href="">#547</a> avoid re-instantiating SemVer during diff compare (<a href="">#547</a>) (<a href="https://github.com/macno"><code>@​macno</code></a>)</li>
</ul>
<h2><a href="https://github.com/npm/node-semver/compare/v7.3.8...v7.4.0">7.4.0</a> (2023-04-10)</h2>
<h3>Features</h3>
<ul>
<li><a href=""><code>113f513</code></a> <a href="">#532</a> identifierBase parameter for .inc (<a href="">#532</a>) (<a href="https://github.com/wraithgar"><code>@​wraithgar</code></a>, <a href="https://github.com/b-bly"><code>@​b-bly</code></a>)</li>
<li><a href=""><code>48d8f8f</code></a> <a href="">#530</a> export new RELEASE_TYPES constant (<a href="https://github.com/hcharley"><code>@​hcharley</code></a>)</li>
</ul>
<h3>Bug Fixes</h3>
<ul>
<li><a href=""><code>940723d</code></a> <a href="">#538</a> intersects with v0.0.0 and v0.0.0-0 (<a href="">#538</a>) (<a href="https://github.com/wraithgar"><code>@​wraithgar</code></a>)</li>
<li><a href=""><code>aa516b5</code></a> <a href="">#535</a> faster parse options (<a href="">#535</a>) (<a href="https://github.com/H4ad"><code>@​H4ad</code></a>)</li>
<li><a href=""><code>61e6ea1</code></a> <a href="">#536</a> faster cache key factory for range (<a href="">#536</a>) (<a href="https://github.com/H4ad"><code>@​H4ad</code></a>)</li>
<li><a href=""><code>f8b8b61</code></a> <a href="">#541</a> optimistic parse (<a href="">#541</a>) (<a href="https://github.com/H4ad"><code>@​H4ad</code></a>)</li>
<li><a href=""><code>796cbe2</code></a> <a href="">#533</a> semver.diff prerelease to release recognition (<a href="">#533</a>) (<a href="https://github.com/wraithgar"><code>@​wraithgar</code></a>, <a href="https://github.com/dominique-blockchain"><code>@​dominique-blockchain</code></a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>7fdf1ef</code></a> chore: release 7.5.3</li>
<li><a href=""><code>bf53dd8</code></a> docs: add example for <code>&gt;</code> comparator (<a href="">#569</a>)</li>
<li><a href=""><code>abdd93d</code></a> fix: set max lengths in regex for numeric and build identifiers (<a href="">#571</a>)</li>
<li><a href=""><code>e7b78de</code></a> chore: release 7.5.2</li>
<li><a href=""><code>58c791f</code></a> fix: diff when detecting major change from prerelease (<a href="">#566</a>)</li>
<li><a href=""><code>5c8efbc</code></a> fix: preserve build in raw after inc (<a href="">#565</a>)</li>
<li><a href=""><code>717534e</code></a> fix: better handling of whitespace (<a href="">#564</a>)</li>
<li><a href=""><code>2f738e9</code></a> chore: bump <code>@​npmcli/template-oss</code> from 4.14.1 to 4.15.1 (<a href="">#558</a>)</li>
<li><a href=""><code>aa016a6</code></a> chore: release 7.5.1</li>
<li><a href=""><code>d30d25a</code></a> fix: show type on invalid semver error (<a href="">#559</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/npm/node-semver/compare/v7.3.8...v7.5.3">compare view</a></li>
</ul>
</details>
<details>
<summary>Maintainer changes</summary>
<p>This version was pushed to npm by <a href="https://www.npmjs.com/~npm-cli-ops">npm-cli-ops</a>, a new releaser for semver since your current version.</p>
</details>
<br />

Updates `@babel/core` from 7.19.3 to 7.22.8
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/babel/babel/releases"><code>@​babel/core</code>'s releases</a>.</em></p>
<blockquote>
<h2>v7.22.8 (2023-07-06)</h2>
<p>This release reverts a commit that caused all new angular installations to fail: <a href="">angular/angular-cli#25496</a></p>
<h4>:leftwards_arrow_with_hook: Revert</h4>
<ul>
<li><code>babel-core</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15754</a> Revert &quot;Use <code>NodePath#hub</code> as part of the paths cache key&quot; (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
</ul>
<h4>Committers: 1</h4>
<ul>
<li>Nicolò Ribaudo (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
<h2>v7.22.7 (2023-07-06)</h2>
<h4>:bug: Bug Fix</h4>
<ul>
<li><code>babel-generator</code>
<ul>
<li><a href="">#15719</a> fix: Avoid internally generating negative source maps columns (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-core</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15725</a> Use <code>NodePath#hub</code> as part of the paths cache key (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li>Other
<ul>
<li><a href="">#15747</a> fix: export <code>meta</code> from <code>eslint-parser/experimental-worker</code> (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
</ul>
<h4>:house: Internal</h4>
<ul>
<li><code>babel-core</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15702</a> Refactor visitors merging (<a href="https://github.com/nullableVoidPtr"><code>@​nullableVoidPtr</code></a>)</li>
</ul>
</li>
</ul>
<h4>Committers: 4</h4>
<ul>
<li>Avery (<a href="https://github.com/nullableVoidPtr"><code>@​nullableVoidPtr</code></a>)</li>
<li>Huáng Jùnliàng (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
<li>Nicolò Ribaudo (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
<li><a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a></li>
</ul>
<h2>v7.22.6 (2023-07-04)</h2>
<h4>:bug: Bug Fix</h4>
<ul>
<li><code>babel-compat-data</code>, <code>babel-helper-compilation-targets</code>, <code>babel-preset-env</code>
<ul>
<li><a href="">#15727</a> Add opera mobile compat data (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
<li><code>babel-plugin-transform-optional-chaining</code>
<ul>
<li><a href="">#15739</a> Fix transform of <code>delete a?.b</code> in function params (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li><code>babel-helper-split-export-declaration</code>, <code>babel-plugin-transform-modules-commonjs</code>
<ul>
<li><a href="">#15736</a> fix: Default export for duplicate names (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-compat-data</code>, <code>babel-preset-env</code>
<ul>
<li><a href="">#15726</a> update compat-data sources (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
<li><code>babel-helpers</code>, <code>babel-plugin-proposal-explicit-resource-management</code>, <code>babel-runtime-corejs3</code>, <code>babel-runtime</code>
<ul>
<li><a href="">#15705</a> Fix handling of sync error in <code>@@asyncDispose</code> (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li><code>babel-standalone</code>
<ul>
<li><a href="">#15707</a> fix: Support transforming Explicit Resource Management in <code>stage-2</code> (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-core</code>
<ul>
<li><a href="">#15626</a> fix: Works correctly with <code>--frozen-intrinsics</code> (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
</ul>
<h4>:house: Internal</h4>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/babel/babel/blob/main/CHANGELOG.md"><code>@​babel/core</code>'s changelog</a>.</em></p>
<blockquote>
<h2>v7.22.8 (2023-07-06)</h2>
<h4>:leftwards_arrow_with_hook: Revert</h4>
<ul>
<li><code>babel-core</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15754</a> Revert &quot;Use <code>NodePath#hub</code> as part of the paths cache key&quot; (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
</ul>
<h2>v7.22.7 (2023-07-06)</h2>
<h4>:bug: Bug Fix</h4>
<ul>
<li><code>babel-generator</code>
<ul>
<li><a href="">#15719</a> fix: Avoid internally generating negative source maps columns (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-core</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15725</a> Use <code>NodePath#hub</code> as part of the paths cache key (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li>Other
<ul>
<li><a href="">#15747</a> fix: export <code>meta</code> from <code>eslint-parser/experimental-worker</code> (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
</ul>
<h4>:house: Internal</h4>
<ul>
<li><code>babel-core</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15702</a> Refactor visitors merging (<a href="https://github.com/nullableVoidPtr"><code>@​nullableVoidPtr</code></a>)</li>
</ul>
</li>
</ul>
<h2>v7.22.6 (2023-07-04)</h2>
<h4>:bug: Bug Fix</h4>
<ul>
<li><code>babel-compat-data</code>, <code>babel-helper-compilation-targets</code>, <code>babel-preset-env</code>
<ul>
<li><a href="">#15727</a> Add opera mobile compat data (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
<li><code>babel-plugin-transform-optional-chaining</code>
<ul>
<li><a href="">#15739</a> Fix transform of <code>delete a?.b</code> in function params (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li><code>babel-helper-split-export-declaration</code>, <code>babel-plugin-transform-modules-commonjs</code>
<ul>
<li><a href="">#15736</a> fix: Default export for duplicate names (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-compat-data</code>, <code>babel-preset-env</code>
<ul>
<li><a href="">#15726</a> update compat-data sources (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
<li><code>babel-helpers</code>, <code>babel-plugin-proposal-explicit-resource-management</code>, <code>babel-runtime-corejs3</code>, <code>babel-runtime</code>
<ul>
<li><a href="">#15705</a> Fix handling of sync error in <code>@@asyncDispose</code> (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li><code>babel-standalone</code>
<ul>
<li><a href="">#15707</a> fix: Support transforming Explicit Resource Management in <code>stage-2</code> (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-core</code>
<ul>
<li><a href="">#15626</a> fix: Works correctly with <code>--frozen-intrinsics</code> (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
</ul>
<h4>:house: Internal</h4>
<ul>
<li><code>babel-helper-create-class-features-plugin</code>, <code>babel-plugin-transform-classes</code>
<ul>
<li><a href="">#15700</a> Minor class transform cleanups (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
</ul>
<h4>:microscope: Output optimization</h4>
<ul>
<li><code>babel-plugin-bugfix-v8-spread-parameters-in-optional-chaining</code>, <code>babel-plugin-transform-class-properties</code>, <code>babel-plugin-transform-optional-chaining</code>, <code>babel-plugin-transform-typescript</code>
<ul>
<li><a href="">#15740</a> Compress output for optional chain with multiple <code>?.</code> (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li><code>babel-plugin-proposal-destructuring-private</code>, <code>babel-plugin-proposal-do-expressions</code>, <code>babel-plugin-proposal-pipeline-operator</code>, <code>babel-plugin-transform-class-properties</code>, <code>babel-plugin-transform-nullish-coalescing-operator</code>, <code>babel-plugin-transform-optional-chaining</code>, <code>babel-plugin-transform-private-property-in-object</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15741</a> Inject tmp vars in the params list of IIFEs when possible (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
</ul>
<h2>v7.22.5 (2023-06-08)</h2>
<h4>:bug: Bug Fix</h4>
<ul>
<li><code>babel-preset-env</code>, <code>babel-standalone</code>
<ul>
<li><a href="">#15675</a> Fix using <code>syntax-unicode-sets-regex</code> in standalone (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>34a611c</code></a> v7.22.8</li>
<li><a href=""><code>c1fe357</code></a> Revert &quot;Use <code>NodePath#hub</code> as part of the paths cache key&quot; (<a href="">#15754</a>)</li>
<li><a href=""><code>b16081e</code></a> v7.22.7</li>
<li><a href=""><code>b1de75f</code></a> Refactor visitors merging (<a href="">#15702</a>)</li>
<li><a href=""><code>abb5a7c</code></a> Use <code>NodePath#hub</code> as part of the paths cache key (<a href="">#15725</a>)</li>
<li><a href=""><code>b5c2669</code></a> chore: Update TS 5.1 (<a href="">#15681</a>)</li>
<li><a href=""><code>4e431d1</code></a> v7.22.6</li>
<li><a href=""><code>230ea2c</code></a> Use forked <code>semver@6</code> with backported security fixes (<a href="">#15742</a>)</li>
<li><a href=""><code>980b63c</code></a> Use more optional chaining (<a href="">#15703</a>)</li>
<li><a href=""><code>5fed5af</code></a> fix: Works correctly with <code>--frozen-intrinsics</code> (<a href="">#15626</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/babel/babel/commits/v7.22.8/packages/babel-core">compare view</a></li>
</ul>
</details>
<br />

Updates `@babel/preset-env` from 7.19.3 to 7.22.7
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/babel/babel/releases"><code>@​babel/preset-env</code>'s releases</a>.</em></p>
<blockquote>
<h2>v7.22.7 (2023-07-06)</h2>
<h4>:bug: Bug Fix</h4>
<ul>
<li><code>babel-generator</code>
<ul>
<li><a href="">#15719</a> fix: Avoid internally generating negative source maps columns (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-core</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15725</a> Use <code>NodePath#hub</code> as part of the paths cache key (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li>Other
<ul>
<li><a href="">#15747</a> fix: export <code>meta</code> from <code>eslint-parser/experimental-worker</code> (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
</ul>
<h4>:house: Internal</h4>
<ul>
<li><code>babel-core</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15702</a> Refactor visitors merging (<a href="https://github.com/nullableVoidPtr"><code>@​nullableVoidPtr</code></a>)</li>
</ul>
</li>
</ul>
<h4>Committers: 4</h4>
<ul>
<li>Avery (<a href="https://github.com/nullableVoidPtr"><code>@​nullableVoidPtr</code></a>)</li>
<li>Huáng Jùnliàng (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
<li>Nicolò Ribaudo (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
<li><a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a></li>
</ul>
<h2>v7.22.6 (2023-07-04)</h2>
<h4>:bug: Bug Fix</h4>
<ul>
<li><code>babel-compat-data</code>, <code>babel-helper-compilation-targets</code>, <code>babel-preset-env</code>
<ul>
<li><a href="">#15727</a> Add opera mobile compat data (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
<li><code>babel-plugin-transform-optional-chaining</code>
<ul>
<li><a href="">#15739</a> Fix transform of <code>delete a?.b</code> in function params (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li><code>babel-helper-split-export-declaration</code>, <code>babel-plugin-transform-modules-commonjs</code>
<ul>
<li><a href="">#15736</a> fix: Default export for duplicate names (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-compat-data</code>, <code>babel-preset-env</code>
<ul>
<li><a href="">#15726</a> update compat-data sources (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
<li><code>babel-helpers</code>, <code>babel-plugin-proposal-explicit-resource-management</code>, <code>babel-runtime-corejs3</code>, <code>babel-runtime</code>
<ul>
<li><a href="">#15705</a> Fix handling of sync error in <code>@@asyncDispose</code> (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li><code>babel-standalone</code>
<ul>
<li><a href="">#15707</a> fix: Support transforming Explicit Resource Management in <code>stage-2</code> (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-core</code>
<ul>
<li><a href="">#15626</a> fix: Works correctly with <code>--frozen-intrinsics</code> (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
</ul>
<h4>:house: Internal</h4>
<ul>
<li><code>babel-helper-create-class-features-plugin</code>, <code>babel-plugin-transform-classes</code>
<ul>
<li><a href="">#15700</a> Minor class transform cleanups (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
</ul>
<h4>:microscope: Output optimization</h4>
<ul>
<li><code>babel-plugin-bugfix-v8-spread-parameters-in-optional-chaining</code>, <code>babel-plugin-transform-class-properties</code>, <code>babel-plugin-transform-optional-chaining</code>, <code>babel-plugin-transform-typescript</code>
<ul>
<li><a href="">#15740</a> Compress output for optional chain with multiple <code>?.</code> (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li><code>babel-plugin-proposal-destructuring-private</code>, <code>babel-plugin-proposal-do-expressions</code>, <code>babel-plugin-proposal-pipeline-operator</code>, <code>babel-plugin-transform-class-properties</code>, <code>babel-plugin-transform-nullish-coalescing-operator</code>, <code>babel-plugin-transform-optional-chaining</code>, <code>babel-plugin-transform-private-property-in-object</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15741</a> Inject tmp vars in the params list of IIFEs when possible (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
</ul>
<h4>Committers: 5</h4>
<ul>
<li>Babel Bot (<a href="https://github.com/babel-bot"><code>@​babel-bot</code></a>)</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/babel/babel/blob/main/CHANGELOG.md"><code>@​babel/preset-env</code>'s changelog</a>.</em></p>
<blockquote>
<h2>v7.22.7 (2023-07-06)</h2>
<h4>:bug: Bug Fix</h4>
<ul>
<li><code>babel-generator</code>
<ul>
<li><a href="">#15719</a> fix: Avoid internally generating negative source maps columns (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-core</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15725</a> Use <code>NodePath#hub</code> as part of the paths cache key (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li>Other
<ul>
<li><a href="">#15747</a> fix: export <code>meta</code> from <code>eslint-parser/experimental-worker</code> (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
</ul>
<h4>:house: Internal</h4>
<ul>
<li><code>babel-core</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15702</a> Refactor visitors merging (<a href="https://github.com/nullableVoidPtr"><code>@​nullableVoidPtr</code></a>)</li>
</ul>
</li>
</ul>
<h2>v7.22.6 (2023-07-04)</h2>
<h4>:bug: Bug Fix</h4>
<ul>
<li><code>babel-compat-data</code>, <code>babel-helper-compilation-targets</code>, <code>babel-preset-env</code>
<ul>
<li><a href="">#15727</a> Add opera mobile compat data (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
<li><code>babel-plugin-transform-optional-chaining</code>
<ul>
<li><a href="">#15739</a> Fix transform of <code>delete a?.b</code> in function params (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li><code>babel-helper-split-export-declaration</code>, <code>babel-plugin-transform-modules-commonjs</code>
<ul>
<li><a href="">#15736</a> fix: Default export for duplicate names (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-compat-data</code>, <code>babel-preset-env</code>
<ul>
<li><a href="">#15726</a> update compat-data sources (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
<li><code>babel-helpers</code>, <code>babel-plugin-proposal-explicit-resource-management</code>, <code>babel-runtime-corejs3</code>, <code>babel-runtime</code>
<ul>
<li><a href="">#15705</a> Fix handling of sync error in <code>@@asyncDispose</code> (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li><code>babel-standalone</code>
<ul>
<li><a href="">#15707</a> fix: Support transforming Explicit Resource Management in <code>stage-2</code> (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
<li><code>babel-core</code>
<ul>
<li><a href="">#15626</a> fix: Works correctly with <code>--frozen-intrinsics</code> (<a href="https://github.com/liuxingbaoyu"><code>@​liuxingbaoyu</code></a>)</li>
</ul>
</li>
</ul>
<h4>:house: Internal</h4>
<ul>
<li><code>babel-helper-create-class-features-plugin</code>, <code>babel-plugin-transform-classes</code>
<ul>
<li><a href="">#15700</a> Minor class transform cleanups (<a href="https://github.com/JLHwung"><code>@​JLHwung</code></a>)</li>
</ul>
</li>
</ul>
<h4>:microscope: Output optimization</h4>
<ul>
<li><code>babel-plugin-bugfix-v8-spread-parameters-in-optional-chaining</code>, <code>babel-plugin-transform-class-properties</code>, <code>babel-plugin-transform-optional-chaining</code>, <code>babel-plugin-transform-typescript</code>
<ul>
<li><a href="">#15740</a> Compress output for optional chain with multiple <code>?.</code> (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
<li><code>babel-plugin-proposal-destructuring-private</code>, <code>babel-plugin-proposal-do-expressions</code>, <code>babel-plugin-proposal-pipeline-operator</code>, <code>babel-plugin-transform-class-properties</code>, <code>babel-plugin-transform-nullish-coalescing-operator</code>, <code>babel-plugin-transform-optional-chaining</code>, <code>babel-plugin-transform-private-property-in-object</code>, <code>babel-traverse</code>
<ul>
<li><a href="">#15741</a> Inject tmp vars in the params list of IIFEs when possible (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
</ul>
<h2>v7.22.5 (2023-06-08)</h2>
<h4>:bug: Bug Fix</h4>
<ul>
<li><code>babel-preset-env</code>, <code>babel-standalone</code>
<ul>
<li><a href="">#15675</a> Fix using <code>syntax-unicode-sets-regex</code> in standalone (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
</ul>
<h4>:nail_care: Polish</h4>
<ul>
<li><code>babel-core</code>
<ul>
<li><a href="">#15683</a> Suggest <code>-transform-</code> when resolving missing plugins (<a href="https://github.com/nicolo-ribaudo"><code>@​nicolo-ribaudo</code></a>)</li>
</ul>
</li>
</ul>
<h2>v7.22.4 (2023-05-29)</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>b16081e</code></a> v7.22.7</li>
<li><a href=""><code>b60e0c2</code></a> Update polyfills packages (<a href="">#15749</a>)</li>
<li><a href=""><code>b5c2669</code></a> chore: Update TS 5.1 (<a href="">#15681</a>)</li>
<li><a href=""><code>4e431d1</code></a> v7.22.6</li>
<li><a href=""><code>e8c596c</code></a> Add opera mobile compat data (<a href="">#15727</a>)</li>
<li><a href=""><code>230ea2c</code></a> Use forked <code>semver@6</code> with backported security fixes (<a href="">#15742</a>)</li>
<li><a href=""><code>134aa17</code></a> Update compat data (<a href="">#15732</a>)</li>
<li><a href=""><code>e827372</code></a> update compat-data sources (<a href="">#15726</a>)</li>
<li><a href=""><code>be8fccd</code></a> chore: Run <code>readmes.js</code> in CI (<a href="">#15690</a>)</li>
<li><a href=""><code>2fcd653</code></a> Update compat data (<a href="">#15692</a>)</li>
<li>Additional commits viewable in <a href="https://github.com/babel/babel/commits/v7.22.7/packages/babel-preset-env">compare view</a></li>
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
- `@dependabot merge` will merge this PR after your CI passes on it
- `@dependabot squash and merge` will squash and merge this PR after your CI passes on it
- `@dependabot cancel merge` will cancel a previously requested merge and block automerging
- `@dependabot reopen` will reopen this PR if it is closed
- `@dependabot close` will close this PR and stop Dependabot recreating it. You can achieve the same result by closing it manually
- `@dependabot ignore this major version` will close this PR and stop Dependabot creating any more for this major version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this minor version` will close this PR and stop Dependabot creating any more for this minor version (unless you reopen the PR or upgrade to it yourself)
- `@dependabot ignore this dependency` will close this PR and stop Dependabot creating any more for this dependency (unless you reopen the PR or upgrade to it yourself)
You can disable automated security fix PRs for this repo from the [Security Alerts page](https://github.com/bioinformatics-ua/dicoogle/network/alerts).

</details>

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `28affe6cb0c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.