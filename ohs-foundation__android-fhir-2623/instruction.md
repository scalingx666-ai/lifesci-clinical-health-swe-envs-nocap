# Issue

**Title:** Bump kotlinx-coroutines from 1.7.2 to 1.8.1

## Description

Bumps `kotlinx-coroutines` from 1.7.2 to 1.8.1.
Updates `org.jetbrains.kotlinx:kotlinx-coroutines-android` from 1.7.2 to 1.8.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/Kotlin/kotlinx.coroutines/releases">org.jetbrains.kotlinx:kotlinx-coroutines-android's releases</a>.</em></p>
<blockquote>
<h2>1.8.1</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Introduce a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li><code>Flow.timeout</code> throws the exception with which the channel was closed (<a href="">#4071</a>).</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.8.1-Beta</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Attempt a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li>Small tweaks.</li>
</ul>
<h2>1.8.0</h2>
<ul>
<li>Implement the library for the Web Assembly (Wasm) for JavaScript (<a href="">#3713</a>). Thanks <a href="https://github.com/igoriakovlev"><code>@​igoriakovlev</code></a>!</li>
<li>Major Kotlin version update: was 1.8.20, became 1.9.21.</li>
<li>On Android, ensure that <code>Dispatchers.Main != Dispatchers.Main.immediate</code> (<a href="">#3545</a>, <a href="">#3963</a>).</li>
<li>Fixed a bug that caused <code>Flow</code> operators that limit cancel the upstream flow to forget that they were already finished if there is another such operator upstream (<a href="">#4035</a>, <a href="">#4038</a>).</li>
<li><code>kotlinx-coroutines-debug</code> is published with the correct Java 9 module info (<a href="">#3944</a>).</li>
<li><code>kotlinx-coroutines-debug</code> no longer requires manually setting <code>DebugProbes.enableCoroutineCreationStackTraces</code> to <code>false</code>, it's the default (<a href="">#3783</a>).</li>
<li><code>kotlinx-coroutines-test</code>: set the default timeout of <code>runTest</code> to 60 seconds, added the ability to configure it on the JVM with the <code>kotlinx.coroutines.test.default_timeout=10s</code> (<a href="">#3800</a>).</li>
<li><code>kotlinx-coroutines-test</code>: fixed a bug that could lead to not all uncaught exceptions being reported after some tests failed (<a href="">#3800</a>).</li>
<li><code>delay(Duration)</code> rounds nanoseconds up to whole milliseconds and not down (<a href="">#3920</a>). Thanks <a href="https://github.com/kevincianfarini"><code>@​kevincianfarini</code></a>!</li>
<li><code>Dispatchers.Default</code> and the default thread for background work are guaranteed to use the same context classloader as the object containing it them (<a href="">#3832</a>).</li>
<li>It is guaranteed that by the time <code>SharedFlow.collect</code> suspends for the first time, it's registered as a subscriber for that <code>SharedFlow</code> (<a href="">#3885</a>). Before, it was also true, but not documented.</li>
<li>Atomicfu version is updated to 0.23.1, and Kotlin/Native atomic transformations are enabled, reducing the footprint of coroutine-heavy code (<a href="">#3954</a>).</li>
<li>Added a workaround for miscompilation of <code>withLock</code> on JS (<a href="">#3881</a>). Thanks <a href="https://github.com/CLOVIS-AI"><code>@​CLOVIS-AI</code></a>!</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.8.0-RC2</h2>
<ul>
<li>Fixed a bug introduced in 1.8.0-RC where <code>Mutex.onLock</code> would not unlock if a non-local return was performed (<a href="">#3985</a>).</li>
<li>Fixed a bug introduced in 1.8.0-RC where depending on kotlinx-coroutines in Native code failed with a compilation error <code>Could not find &quot;org.jetbrains.kotlinx:atomicfu-cinterop-interop&quot;</code> (<a href="">#3968</a>).</li>
<li>Small documentation fixes.</li>
</ul>
<h2>1.8.0-RC</h2>
<ul>
<li>Implement the library for the Web Assembly (Wasm) for JavaScript (<a href="">#3713</a>). Thanks <a href="https://github.com/igoriakovlev"><code>@​igoriakovlev</code></a>!</li>
<li>On Android, ensure that <code>Dispatchers.Main != Dispatchers.Main.immediate</code> (<a href="">#3545</a>, <a href="">#3963</a>).</li>
<li><code>kotlinx-coroutines-debug</code> is published with the incorrect Java 9 module info (<a href="">#3944</a>).</li>
<li>Major Kotlin version update: was 1.8.20, became 1.9.21.</li>
<li><code>kotlinx-coroutines-test</code>: set the default timeout of <code>runTest</code> to 60 seconds, added the ability to configure it on the JVM with the <code>kotlinx.coroutines.test.default_timeout=10s</code> (<a href="">#3800</a>).</li>
<li><code>kotlinx-coroutines-test</code>: fixed a bug that could lead to not all uncaught exceptions being reported after some tests failed (<a href="">#3800</a>).</li>
<li><code>delay(Duration)</code> rounds nanoseconds up to whole milliseconds and not down (<a href="">#3920</a>). Thanks <a href="https://github.com/kevincianfarini"><code>@​kevincianfarini</code></a>!</li>
<li><code>Dispatchers.Default</code> and the default thread for background work are guaranteed to use the same context classloader as the object containing it them (<a href="">#3832</a>).</li>
<li>It is guaranteed that by the time <code>SharedFlow.collect</code> suspends for the first time, it's registered as a subscriber for that <code>SharedFlow</code> (<a href="">#3885</a>). Before, it was also true, but not documented.</li>
<li>Atomicfu version is updated to 0.23.1, and Kotlin/Native atomic transformations are enabled, reducing the footprint of coroutine-heavy code (<a href="">#3954</a>).</li>
<li>Added a workaround for miscompilation of <code>withLock</code> on JS (<a href="">#3881</a>). Thanks <a href="https://github.com/CLOVIS-AI"><code>@​CLOVIS-AI</code></a>!</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.7.3</h2>
<ul>
<li>Disabled the publication of the multiplatform library metadata for the old (1.6 and earlier) KMP Gradle plugin (<a href="">#3809</a>).</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/Kotlin/kotlinx.coroutines/blob/master/CHANGES.md">org.jetbrains.kotlinx:kotlinx-coroutines-android's changelog</a>.</em></p>
<blockquote>
<h2>Version 1.8.1</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Introduce a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li><code>Flow.timeout</code> throws the exception with which the channel was closed (<a href="">#4071</a>).</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h3>Changelog relative to version 1.8.1-Beta</h3>
<ul>
<li><code>Flow.timeout</code> throws the exception with which the channel was closed (<a href="">#4071</a>).</li>
<li>Small documentation fixes.</li>
</ul>
<h2>Version 1.8.1-Beta</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Attempt a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li>Small tweaks.</li>
</ul>
<h2>Version 1.8.0</h2>
<ul>
<li>Implement the library for the Web Assembly (Wasm) for JavaScript (<a href="">#3713</a>). Thanks <a href="https://github.com/igoriakovlev"><code>@​igoriakovlev</code></a>!</li>
<li>Major Kotlin version update: was 1.8.20, became 1.9.21.</li>
<li>On Android, ensure that <code>Dispatchers.Main != Dispatchers.Main.immediate</code> (<a href="">#3545</a>, <a href="">#3963</a>).</li>
<li>Fixed a bug that caused <code>Flow</code> operators that limit cancel the upstream flow to forget that they were already finished if there is another such operator upstream (<a href="">#4035</a>, <a href="">#4038</a>)</li>
<li><code>kotlinx-coroutines-debug</code> is published with the correct Java 9 module info (<a href="">#3944</a>).</li>
<li><code>kotlinx-coroutines-debug</code> no longer requires manually setting <code>DebugProbes.enableCoroutineCreationStackTraces</code> to <code>false</code>, it's the default (<a href="">#3783</a>).</li>
<li><code>kotlinx-coroutines-test</code>: set the default timeout of <code>runTest</code> to 60 seconds, added the ability to configure it on the JVM with the <code>kotlinx.coroutines.test.default_timeout=10s</code> (<a href="">#3800</a>).</li>
<li><code>kotlinx-coroutines-test</code>: fixed a bug that could lead to not all uncaught exceptions being reported after some tests failed (<a href="">#3800</a>).</li>
<li><code>delay(Duration)</code> rounds nanoseconds up to whole milliseconds and not down (<a href="">#3920</a>). Thanks <a href="https://github.com/kevincianfarini"><code>@​kevincianfarini</code></a>!</li>
<li><code>Dispatchers.Default</code> and the default thread for background work are guaranteed to use the same context classloader as the object containing it them (<a href="">#3832</a>).</li>
<li>It is guaranteed that by the time <code>SharedFlow.collect</code> suspends for the first time, it's registered as a subscriber for that <code>SharedFlow</code> (<a href="">#3885</a>). Before, it was also true, but not documented.</li>
<li>Atomicfu version is updated to 0.23.1, and Kotlin/Native atomic transformations are enabled, reducing the footprint of coroutine-heavy code (<a href="">#3954</a>).</li>
<li>Added a workaround for miscompilation of <code>withLock</code> on JS (<a href="">#3881</a>). Thanks <a href="https://github.com/CLOVIS-AI"><code>@​CLOVIS-AI</code></a>!</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h3>Changelog relative to version 1.8.0-RC2</h3>
<ul>
<li><code>kotlinx-coroutines-debug</code> no longer requires manually setting <code>DebugProbes.enableCoroutineCreationStackTraces</code> to <code>false</code>, it's the default (<a href="">#3783</a>).</li>
<li>Fixed a bug that caused <code>Flow</code> operators that limit cancel the upstream flow to forget that they were already finished if there is another such operator upstream (<a href="">#4035</a>, <a href="">#4038</a>)</li>
<li>Small documentation fixes.</li>
</ul>
<h2>Version 1.8.0-RC2</h2>
<ul>
<li>Fixed a bug introduced in 1.8.0-RC where <code>Mutex.onLock</code> would not unlock if a non-local return was performed (<a href="">#3985</a>).</li>
<li>Fixed a bug introduced in 1.8.0-RC where depending on kotlinx-coroutines in Native code failed with a compilation error <code>Could not find &quot;org.jetbrains.kotlinx:atomicfu-cinterop-interop&quot;</code> (<a href="">#3968</a>).</li>
<li>Small documentation fixes.</li>
</ul>
<h2>Version 1.8.0-RC</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>cd696d3</code></a> Version 1.8.1</li>
<li><a href=""><code>c1ba5af</code></a> Fix the ticker channel example giving wrong results on the website (<a href="">#4109</a>)</li>
<li><a href=""><code>2430d9a</code></a> Fix broken API reference links to the Project Reactor Javadoc (<a href="">#4111</a>)</li>
<li><a href=""><code>f22b229</code></a> fix the link to <code>Thread.uncaughtExceptionHandler</code></li>
<li><a href=""><code>515308d</code></a> fix: get rid of horizontal scrolling by splitting the comment and show more c...</li>
<li><a href=""><code>f8d1821</code></a> Fix typo in coroutine-context-and-dispatchers.md (<a href="">#3941</a>)</li>
<li><a href=""><code>20707d3</code></a> fix: remove <code>sampleStart</code> and <code>sampleEnd</code> comments from example in coroutine-...</li>
<li><a href=""><code>0148534</code></a> chore: fix identation in example loadContributorsBlocking() (<a href="">#4085</a>)</li>
<li><a href=""><code>74774df</code></a> Docs: reference to The Hitchhiker's Guide to the Galaxy (<a href="">#4082</a>)</li>
<li><a href=""><code>d106ac7</code></a> Docs: avoid scrolling sample code; fix test description; add () to functions ...</li>
<li>Additional commits viewable in <a href="https://github.com/Kotlin/kotlinx.coroutines/compare/1.7.2...1.8.1">compare view</a></li>
</ul>
</details>
<br />

Updates `org.jetbrains.kotlinx:kotlinx-coroutines-core` from 1.7.2 to 1.8.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/Kotlin/kotlinx.coroutines/releases">org.jetbrains.kotlinx:kotlinx-coroutines-core's releases</a>.</em></p>
<blockquote>
<h2>1.8.1</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Introduce a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li><code>Flow.timeout</code> throws the exception with which the channel was closed (<a href="">#4071</a>).</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.8.1-Beta</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Attempt a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li>Small tweaks.</li>
</ul>
<h2>1.8.0</h2>
<ul>
<li>Implement the library for the Web Assembly (Wasm) for JavaScript (<a href="">#3713</a>). Thanks <a href="https://github.com/igoriakovlev"><code>@​igoriakovlev</code></a>!</li>
<li>Major Kotlin version update: was 1.8.20, became 1.9.21.</li>
<li>On Android, ensure that <code>Dispatchers.Main != Dispatchers.Main.immediate</code> (<a href="">#3545</a>, <a href="">#3963</a>).</li>
<li>Fixed a bug that caused <code>Flow</code> operators that limit cancel the upstream flow to forget that they were already finished if there is another such operator upstream (<a href="">#4035</a>, <a href="">#4038</a>).</li>
<li><code>kotlinx-coroutines-debug</code> is published with the correct Java 9 module info (<a href="">#3944</a>).</li>
<li><code>kotlinx-coroutines-debug</code> no longer requires manually setting <code>DebugProbes.enableCoroutineCreationStackTraces</code> to <code>false</code>, it's the default (<a href="">#3783</a>).</li>
<li><code>kotlinx-coroutines-test</code>: set the default timeout of <code>runTest</code> to 60 seconds, added the ability to configure it on the JVM with the <code>kotlinx.coroutines.test.default_timeout=10s</code> (<a href="">#3800</a>).</li>
<li><code>kotlinx-coroutines-test</code>: fixed a bug that could lead to not all uncaught exceptions being reported after some tests failed (<a href="">#3800</a>).</li>
<li><code>delay(Duration)</code> rounds nanoseconds up to whole milliseconds and not down (<a href="">#3920</a>). Thanks <a href="https://github.com/kevincianfarini"><code>@​kevincianfarini</code></a>!</li>
<li><code>Dispatchers.Default</code> and the default thread for background work are guaranteed to use the same context classloader as the object containing it them (<a href="">#3832</a>).</li>
<li>It is guaranteed that by the time <code>SharedFlow.collect</code> suspends for the first time, it's registered as a subscriber for that <code>SharedFlow</code> (<a href="">#3885</a>). Before, it was also true, but not documented.</li>
<li>Atomicfu version is updated to 0.23.1, and Kotlin/Native atomic transformations are enabled, reducing the footprint of coroutine-heavy code (<a href="">#3954</a>).</li>
<li>Added a workaround for miscompilation of <code>withLock</code> on JS (<a href="">#3881</a>). Thanks <a href="https://github.com/CLOVIS-AI"><code>@​CLOVIS-AI</code></a>!</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.8.0-RC2</h2>
<ul>
<li>Fixed a bug introduced in 1.8.0-RC where <code>Mutex.onLock</code> would not unlock if a non-local return was performed (<a href="">#3985</a>).</li>
<li>Fixed a bug introduced in 1.8.0-RC where depending on kotlinx-coroutines in Native code failed with a compilation error <code>Could not find &quot;org.jetbrains.kotlinx:atomicfu-cinterop-interop&quot;</code> (<a href="">#3968</a>).</li>
<li>Small documentation fixes.</li>
</ul>
<h2>1.8.0-RC</h2>
<ul>
<li>Implement the library for the Web Assembly (Wasm) for JavaScript (<a href="">#3713</a>). Thanks <a href="https://github.com/igoriakovlev"><code>@​igoriakovlev</code></a>!</li>
<li>On Android, ensure that <code>Dispatchers.Main != Dispatchers.Main.immediate</code> (<a href="">#3545</a>, <a href="">#3963</a>).</li>
<li><code>kotlinx-coroutines-debug</code> is published with the incorrect Java 9 module info (<a href="">#3944</a>).</li>
<li>Major Kotlin version update: was 1.8.20, became 1.9.21.</li>
<li><code>kotlinx-coroutines-test</code>: set the default timeout of <code>runTest</code> to 60 seconds, added the ability to configure it on the JVM with the <code>kotlinx.coroutines.test.default_timeout=10s</code> (<a href="">#3800</a>).</li>
<li><code>kotlinx-coroutines-test</code>: fixed a bug that could lead to not all uncaught exceptions being reported after some tests failed (<a href="">#3800</a>).</li>
<li><code>delay(Duration)</code> rounds nanoseconds up to whole milliseconds and not down (<a href="">#3920</a>). Thanks <a href="https://github.com/kevincianfarini"><code>@​kevincianfarini</code></a>!</li>
<li><code>Dispatchers.Default</code> and the default thread for background work are guaranteed to use the same context classloader as the object containing it them (<a href="">#3832</a>).</li>
<li>It is guaranteed that by the time <code>SharedFlow.collect</code> suspends for the first time, it's registered as a subscriber for that <code>SharedFlow</code> (<a href="">#3885</a>). Before, it was also true, but not documented.</li>
<li>Atomicfu version is updated to 0.23.1, and Kotlin/Native atomic transformations are enabled, reducing the footprint of coroutine-heavy code (<a href="">#3954</a>).</li>
<li>Added a workaround for miscompilation of <code>withLock</code> on JS (<a href="">#3881</a>). Thanks <a href="https://github.com/CLOVIS-AI"><code>@​CLOVIS-AI</code></a>!</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.7.3</h2>
<ul>
<li>Disabled the publication of the multiplatform library metadata for the old (1.6 and earlier) KMP Gradle plugin (<a href="">#3809</a>).</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/Kotlin/kotlinx.coroutines/blob/master/CHANGES.md">org.jetbrains.kotlinx:kotlinx-coroutines-core's changelog</a>.</em></p>
<blockquote>
<h2>Version 1.8.1</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Introduce a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li><code>Flow.timeout</code> throws the exception with which the channel was closed (<a href="">#4071</a>).</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h3>Changelog relative to version 1.8.1-Beta</h3>
<ul>
<li><code>Flow.timeout</code> throws the exception with which the channel was closed (<a href="">#4071</a>).</li>
<li>Small documentation fixes.</li>
</ul>
<h2>Version 1.8.1-Beta</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Attempt a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li>Small tweaks.</li>
</ul>
<h2>Version 1.8.0</h2>
<ul>
<li>Implement the library for the Web Assembly (Wasm) for JavaScript (<a href="">#3713</a>). Thanks <a href="https://github.com/igoriakovlev"><code>@​igoriakovlev</code></a>!</li>
<li>Major Kotlin version update: was 1.8.20, became 1.9.21.</li>
<li>On Android, ensure that <code>Dispatchers.Main != Dispatchers.Main.immediate</code> (<a href="">#3545</a>, <a href="">#3963</a>).</li>
<li>Fixed a bug that caused <code>Flow</code> operators that limit cancel the upstream flow to forget that they were already finished if there is another such operator upstream (<a href="">#4035</a>, <a href="">#4038</a>)</li>
<li><code>kotlinx-coroutines-debug</code> is published with the correct Java 9 module info (<a href="">#3944</a>).</li>
<li><code>kotlinx-coroutines-debug</code> no longer requires manually setting <code>DebugProbes.enableCoroutineCreationStackTraces</code> to <code>false</code>, it's the default (<a href="">#3783</a>).</li>
<li><code>kotlinx-coroutines-test</code>: set the default timeout of <code>runTest</code> to 60 seconds, added the ability to configure it on the JVM with the <code>kotlinx.coroutines.test.default_timeout=10s</code> (<a href="">#3800</a>).</li>
<li><code>kotlinx-coroutines-test</code>: fixed a bug that could lead to not all uncaught exceptions being reported after some tests failed (<a href="">#3800</a>).</li>
<li><code>delay(Duration)</code> rounds nanoseconds up to whole milliseconds and not down (<a href="">#3920</a>). Thanks <a href="https://github.com/kevincianfarini"><code>@​kevincianfarini</code></a>!</li>
<li><code>Dispatchers.Default</code> and the default thread for background work are guaranteed to use the same context classloader as the object containing it them (<a href="">#3832</a>).</li>
<li>It is guaranteed that by the time <code>SharedFlow.collect</code> suspends for the first time, it's registered as a subscriber for that <code>SharedFlow</code> (<a href="">#3885</a>). Before, it was also true, but not documented.</li>
<li>Atomicfu version is updated to 0.23.1, and Kotlin/Native atomic transformations are enabled, reducing the footprint of coroutine-heavy code (<a href="">#3954</a>).</li>
<li>Added a workaround for miscompilation of <code>withLock</code> on JS (<a href="">#3881</a>). Thanks <a href="https://github.com/CLOVIS-AI"><code>@​CLOVIS-AI</code></a>!</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h3>Changelog relative to version 1.8.0-RC2</h3>
<ul>
<li><code>kotlinx-coroutines-debug</code> no longer requires manually setting <code>DebugProbes.enableCoroutineCreationStackTraces</code> to <code>false</code>, it's the default (<a href="">#3783</a>).</li>
<li>Fixed a bug that caused <code>Flow</code> operators that limit cancel the upstream flow to forget that they were already finished if there is another such operator upstream (<a href="">#4035</a>, <a href="">#4038</a>)</li>
<li>Small documentation fixes.</li>
</ul>
<h2>Version 1.8.0-RC2</h2>
<ul>
<li>Fixed a bug introduced in 1.8.0-RC where <code>Mutex.onLock</code> would not unlock if a non-local return was performed (<a href="">#3985</a>).</li>
<li>Fixed a bug introduced in 1.8.0-RC where depending on kotlinx-coroutines in Native code failed with a compilation error <code>Could not find &quot;org.jetbrains.kotlinx:atomicfu-cinterop-interop&quot;</code> (<a href="">#3968</a>).</li>
<li>Small documentation fixes.</li>
</ul>
<h2>Version 1.8.0-RC</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>cd696d3</code></a> Version 1.8.1</li>
<li><a href=""><code>c1ba5af</code></a> Fix the ticker channel example giving wrong results on the website (<a href="">#4109</a>)</li>
<li><a href=""><code>2430d9a</code></a> Fix broken API reference links to the Project Reactor Javadoc (<a href="">#4111</a>)</li>
<li><a href=""><code>f22b229</code></a> fix the link to <code>Thread.uncaughtExceptionHandler</code></li>
<li><a href=""><code>515308d</code></a> fix: get rid of horizontal scrolling by splitting the comment and show more c...</li>
<li><a href=""><code>f8d1821</code></a> Fix typo in coroutine-context-and-dispatchers.md (<a href="">#3941</a>)</li>
<li><a href=""><code>20707d3</code></a> fix: remove <code>sampleStart</code> and <code>sampleEnd</code> comments from example in coroutine-...</li>
<li><a href=""><code>0148534</code></a> chore: fix identation in example loadContributorsBlocking() (<a href="">#4085</a>)</li>
<li><a href=""><code>74774df</code></a> Docs: reference to The Hitchhiker's Guide to the Galaxy (<a href="">#4082</a>)</li>
<li><a href=""><code>d106ac7</code></a> Docs: avoid scrolling sample code; fix test description; add () to functions ...</li>
<li>Additional commits viewable in <a href="https://github.com/Kotlin/kotlinx.coroutines/compare/1.7.2...1.8.1">compare view</a></li>
</ul>
</details>
<br />

Updates `org.jetbrains.kotlinx:kotlinx-coroutines-play-services` from 1.7.2 to 1.8.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/Kotlin/kotlinx.coroutines/releases">org.jetbrains.kotlinx:kotlinx-coroutines-play-services's releases</a>.</em></p>
<blockquote>
<h2>1.8.1</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Introduce a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li><code>Flow.timeout</code> throws the exception with which the channel was closed (<a href="">#4071</a>).</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.8.1-Beta</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Attempt a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li>Small tweaks.</li>
</ul>
<h2>1.8.0</h2>
<ul>
<li>Implement the library for the Web Assembly (Wasm) for JavaScript (<a href="">#3713</a>). Thanks <a href="https://github.com/igoriakovlev"><code>@​igoriakovlev</code></a>!</li>
<li>Major Kotlin version update: was 1.8.20, became 1.9.21.</li>
<li>On Android, ensure that <code>Dispatchers.Main != Dispatchers.Main.immediate</code> (<a href="">#3545</a>, <a href="">#3963</a>).</li>
<li>Fixed a bug that caused <code>Flow</code> operators that limit cancel the upstream flow to forget that they were already finished if there is another such operator upstream (<a href="">#4035</a>, <a href="">#4038</a>).</li>
<li><code>kotlinx-coroutines-debug</code> is published with the correct Java 9 module info (<a href="">#3944</a>).</li>
<li><code>kotlinx-coroutines-debug</code> no longer requires manually setting <code>DebugProbes.enableCoroutineCreationStackTraces</code> to <code>false</code>, it's the default (<a href="">#3783</a>).</li>
<li><code>kotlinx-coroutines-test</code>: set the default timeout of <code>runTest</code> to 60 seconds, added the ability to configure it on the JVM with the <code>kotlinx.coroutines.test.default_timeout=10s</code> (<a href="">#3800</a>).</li>
<li><code>kotlinx-coroutines-test</code>: fixed a bug that could lead to not all uncaught exceptions being reported after some tests failed (<a href="">#3800</a>).</li>
<li><code>delay(Duration)</code> rounds nanoseconds up to whole milliseconds and not down (<a href="">#3920</a>). Thanks <a href="https://github.com/kevincianfarini"><code>@​kevincianfarini</code></a>!</li>
<li><code>Dispatchers.Default</code> and the default thread for background work are guaranteed to use the same context classloader as the object containing it them (<a href="">#3832</a>).</li>
<li>It is guaranteed that by the time <code>SharedFlow.collect</code> suspends for the first time, it's registered as a subscriber for that <code>SharedFlow</code> (<a href="">#3885</a>). Before, it was also true, but not documented.</li>
<li>Atomicfu version is updated to 0.23.1, and Kotlin/Native atomic transformations are enabled, reducing the footprint of coroutine-heavy code (<a href="">#3954</a>).</li>
<li>Added a workaround for miscompilation of <code>withLock</code> on JS (<a href="">#3881</a>). Thanks <a href="https://github.com/CLOVIS-AI"><code>@​CLOVIS-AI</code></a>!</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.8.0-RC2</h2>
<ul>
<li>Fixed a bug introduced in 1.8.0-RC where <code>Mutex.onLock</code> would not unlock if a non-local return was performed (<a href="">#3985</a>).</li>
<li>Fixed a bug introduced in 1.8.0-RC where depending on kotlinx-coroutines in Native code failed with a compilation error <code>Could not find &quot;org.jetbrains.kotlinx:atomicfu-cinterop-interop&quot;</code> (<a href="">#3968</a>).</li>
<li>Small documentation fixes.</li>
</ul>
<h2>1.8.0-RC</h2>
<ul>
<li>Implement the library for the Web Assembly (Wasm) for JavaScript (<a href="">#3713</a>). Thanks <a href="https://github.com/igoriakovlev"><code>@​igoriakovlev</code></a>!</li>
<li>On Android, ensure that <code>Dispatchers.Main != Dispatchers.Main.immediate</code> (<a href="">#3545</a>, <a href="">#3963</a>).</li>
<li><code>kotlinx-coroutines-debug</code> is published with the incorrect Java 9 module info (<a href="">#3944</a>).</li>
<li>Major Kotlin version update: was 1.8.20, became 1.9.21.</li>
<li><code>kotlinx-coroutines-test</code>: set the default timeout of <code>runTest</code> to 60 seconds, added the ability to configure it on the JVM with the <code>kotlinx.coroutines.test.default_timeout=10s</code> (<a href="">#3800</a>).</li>
<li><code>kotlinx-coroutines-test</code>: fixed a bug that could lead to not all uncaught exceptions being reported after some tests failed (<a href="">#3800</a>).</li>
<li><code>delay(Duration)</code> rounds nanoseconds up to whole milliseconds and not down (<a href="">#3920</a>). Thanks <a href="https://github.com/kevincianfarini"><code>@​kevincianfarini</code></a>!</li>
<li><code>Dispatchers.Default</code> and the default thread for background work are guaranteed to use the same context classloader as the object containing it them (<a href="">#3832</a>).</li>
<li>It is guaranteed that by the time <code>SharedFlow.collect</code> suspends for the first time, it's registered as a subscriber for that <code>SharedFlow</code> (<a href="">#3885</a>). Before, it was also true, but not documented.</li>
<li>Atomicfu version is updated to 0.23.1, and Kotlin/Native atomic transformations are enabled, reducing the footprint of coroutine-heavy code (<a href="">#3954</a>).</li>
<li>Added a workaround for miscompilation of <code>withLock</code> on JS (<a href="">#3881</a>). Thanks <a href="https://github.com/CLOVIS-AI"><code>@​CLOVIS-AI</code></a>!</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.7.3</h2>
<ul>
<li>Disabled the publication of the multiplatform library metadata for the old (1.6 and earlier) KMP Gradle plugin (<a href="">#3809</a>).</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Changelog</summary>
<p><em>Sourced from <a href="https://github.com/Kotlin/kotlinx.coroutines/blob/master/CHANGES.md">org.jetbrains.kotlinx:kotlinx-coroutines-play-services's changelog</a>.</em></p>
<blockquote>
<h2>Version 1.8.1</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Introduce a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li><code>Flow.timeout</code> throws the exception with which the channel was closed (<a href="">#4071</a>).</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h3>Changelog relative to version 1.8.1-Beta</h3>
<ul>
<li><code>Flow.timeout</code> throws the exception with which the channel was closed (<a href="">#4071</a>).</li>
<li>Small documentation fixes.</li>
</ul>
<h2>Version 1.8.1-Beta</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Attempt a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li>Small tweaks.</li>
</ul>
<h2>Version 1.8.0</h2>
<ul>
<li>Implement the library for the Web Assembly (Wasm) for JavaScript (<a href="">#3713</a>). Thanks <a href="https://github.com/igoriakovlev"><code>@​igoriakovlev</code></a>!</li>
<li>Major Kotlin version update: was 1.8.20, became 1.9.21.</li>
<li>On Android, ensure that <code>Dispatchers.Main != Dispatchers.Main.immediate</code> (<a href="">#3545</a>, <a href="">#3963</a>).</li>
<li>Fixed a bug that caused <code>Flow</code> operators that limit cancel the upstream flow to forget that they were already finished if there is another such operator upstream (<a href="">#4035</a>, <a href="">#4038</a>)</li>
<li><code>kotlinx-coroutines-debug</code> is published with the correct Java 9 module info (<a href="">#3944</a>).</li>
<li><code>kotlinx-coroutines-debug</code> no longer requires manually setting <code>DebugProbes.enableCoroutineCreationStackTraces</code> to <code>false</code>, it's the default (<a href="">#3783</a>).</li>
<li><code>kotlinx-coroutines-test</code>: set the default timeout of <code>runTest</code> to 60 seconds, added the ability to configure it on the JVM with the <code>kotlinx.coroutines.test.default_timeout=10s</code> (<a href="">#3800</a>).</li>
<li><code>kotlinx-coroutines-test</code>: fixed a bug that could lead to not all uncaught exceptions being reported after some tests failed (<a href="">#3800</a>).</li>
<li><code>delay(Duration)</code> rounds nanoseconds up to whole milliseconds and not down (<a href="">#3920</a>). Thanks <a href="https://github.com/kevincianfarini"><code>@​kevincianfarini</code></a>!</li>
<li><code>Dispatchers.Default</code> and the default thread for background work are guaranteed to use the same context classloader as the object containing it them (<a href="">#3832</a>).</li>
<li>It is guaranteed that by the time <code>SharedFlow.collect</code> suspends for the first time, it's registered as a subscriber for that <code>SharedFlow</code> (<a href="">#3885</a>). Before, it was also true, but not documented.</li>
<li>Atomicfu version is updated to 0.23.1, and Kotlin/Native atomic transformations are enabled, reducing the footprint of coroutine-heavy code (<a href="">#3954</a>).</li>
<li>Added a workaround for miscompilation of <code>withLock</code> on JS (<a href="">#3881</a>). Thanks <a href="https://github.com/CLOVIS-AI"><code>@​CLOVIS-AI</code></a>!</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h3>Changelog relative to version 1.8.0-RC2</h3>
<ul>
<li><code>kotlinx-coroutines-debug</code> no longer requires manually setting <code>DebugProbes.enableCoroutineCreationStackTraces</code> to <code>false</code>, it's the default (<a href="">#3783</a>).</li>
<li>Fixed a bug that caused <code>Flow</code> operators that limit cancel the upstream flow to forget that they were already finished if there is another such operator upstream (<a href="">#4035</a>, <a href="">#4038</a>)</li>
<li>Small documentation fixes.</li>
</ul>
<h2>Version 1.8.0-RC2</h2>
<ul>
<li>Fixed a bug introduced in 1.8.0-RC where <code>Mutex.onLock</code> would not unlock if a non-local return was performed (<a href="">#3985</a>).</li>
<li>Fixed a bug introduced in 1.8.0-RC where depending on kotlinx-coroutines in Native code failed with a compilation error <code>Could not find &quot;org.jetbrains.kotlinx:atomicfu-cinterop-interop&quot;</code> (<a href="">#3968</a>).</li>
<li>Small documentation fixes.</li>
</ul>
<h2>Version 1.8.0-RC</h2>
<!-- raw HTML omitted -->
</blockquote>
<p>... (truncated)</p>
</details>
<details>
<summary>Commits</summary>
<ul>
<li><a href=""><code>cd696d3</code></a> Version 1.8.1</li>
<li><a href=""><code>c1ba5af</code></a> Fix the ticker channel example giving wrong results on the website (<a href="">#4109</a>)</li>
<li><a href=""><code>2430d9a</code></a> Fix broken API reference links to the Project Reactor Javadoc (<a href="">#4111</a>)</li>
<li><a href=""><code>f22b229</code></a> fix the link to <code>Thread.uncaughtExceptionHandler</code></li>
<li><a href=""><code>515308d</code></a> fix: get rid of horizontal scrolling by splitting the comment and show more c...</li>
<li><a href=""><code>f8d1821</code></a> Fix typo in coroutine-context-and-dispatchers.md (<a href="">#3941</a>)</li>
<li><a href=""><code>20707d3</code></a> fix: remove <code>sampleStart</code> and <code>sampleEnd</code> comments from example in coroutine-...</li>
<li><a href=""><code>0148534</code></a> chore: fix identation in example loadContributorsBlocking() (<a href="">#4085</a>)</li>
<li><a href=""><code>74774df</code></a> Docs: reference to The Hitchhiker's Guide to the Galaxy (<a href="">#4082</a>)</li>
<li><a href=""><code>d106ac7</code></a> Docs: avoid scrolling sample code; fix test description; add () to functions ...</li>
<li>Additional commits viewable in <a href="https://github.com/Kotlin/kotlinx.coroutines/compare/1.7.2...1.8.1">compare view</a></li>
</ul>
</details>
<br />

Updates `org.jetbrains.kotlinx:kotlinx-coroutines-test` from 1.7.2 to 1.8.1
<details>
<summary>Release notes</summary>
<p><em>Sourced from <a href="https://github.com/Kotlin/kotlinx.coroutines/releases">org.jetbrains.kotlinx:kotlinx-coroutines-test's releases</a>.</em></p>
<blockquote>
<h2>1.8.1</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Introduce a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li><code>Flow.timeout</code> throws the exception with which the channel was closed (<a href="">#4071</a>).</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.8.1-Beta</h2>
<ul>
<li>Remove the <code>@ExperimentalTime</code> annotation from usages of <code>TimeSource</code> (<a href="">#4046</a>). Thanks, <a href="https://github.com/hfhbd"><code>@​hfhbd</code></a>!</li>
<li>Attempt a workaround for an Android bug that caused an occasional <code>NullPointerException</code> when setting the <code>StateFlow</code> value on old Android devices (<a href="">#3820</a>).</li>
<li>No longer use <code>kotlin.random.Random</code> as part of <code>Dispatchers.Default</code> and <code>Dispatchers.IO</code> initialization (<a href="">#4051</a>).</li>
<li>Small tweaks.</li>
</ul>
<h2>1.8.0</h2>
<ul>
<li>Implement the library for the Web Assembly (Wasm) for JavaScript (<a href="">#3713</a>). Thanks <a href="https://github.com/igoriakovlev"><code>@​igoriakovlev</code></a>!</li>
<li>Major Kotlin version update: was 1.8.20, became 1.9.21.</li>
<li>On Android, ensure that <code>Dispatchers.Main != Dispatchers.Main.immediate</code> (<a href="">#3545</a>, <a href="">#3963</a>).</li>
<li>Fixed a bug that caused <code>Flow</code> operators that limit cancel the upstream flow to forget that they were already finished if there is another such operator upstream (<a href="">#4035</a>, <a href="">#4038</a>).</li>
<li><code>kotlinx-coroutines-debug</code> is published with the correct Java 9 module info (<a href="">#3944</a>).</li>
<li><code>kotlinx-coroutines-debug</code> no longer requires manually setting <code>DebugProbes.enableCoroutineCreationStackTraces</code> to <code>false</code>, it's the default (<a href="">#3783</a>).</li>
<li><code>kotlinx-coroutines-test</code>: set the default timeout of <code>runTest</code> to 60 seconds, added the ability to configure it on the JVM with the <code>kotlinx.coroutines.test.default_timeout=10s</code> (<a href="">#3800</a>).</li>
<li><code>kotlinx-coroutines-test</code>: fixed a bug that could lead to not all uncaught exceptions being reported after some tests failed (<a href="">#3800</a>).</li>
<li><code>delay(Duration)</code> rounds nanoseconds up to whole milliseconds and not down (<a href="">#3920</a>). Thanks <a href="https://github.com/kevincianfarini"><code>@​kevincianfarini</code></a>!</li>
<li><code>Dispatchers.Default</code> and the default thread for background work are guaranteed to use the same context classloader as the object containing it them (<a href="">#3832</a>).</li>
<li>It is guaranteed that by the time <code>SharedFlow.collect</code> suspends for the first time, it's registered as a subscriber for that <code>SharedFlow</code> (<a href="">#3885</a>). Before, it was also true, but not documented.</li>
<li>Atomicfu version is updated to 0.23.1, and Kotlin/Native atomic transformations are enabled, reducing the footprint of coroutine-heavy code (<a href="">#3954</a>).</li>
<li>Added a workaround for miscompilation of <code>withLock</code> on JS (<a href="">#3881</a>). Thanks <a href="https://github.com/CLOVIS-AI"><code>@​CLOVIS-AI</code></a>!</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.8.0-RC2</h2>
<ul>
<li>Fixed a bug introduced in 1.8.0-RC where <code>Mutex.onLock</code> would not unlock if a non-local return was performed (<a href="">#3985</a>).</li>
<li>Fixed a bug introduced in 1.8.0-RC where depending on kotlinx-coroutines in Native code failed with a compilation error <code>Could not find &quot;org.jetbrains.kotlinx:atomicfu-cinterop-interop&quot;</code> (<a href="">#3968</a>).</li>
<li>Small documentation fixes.</li>
</ul>
<h2>1.8.0-RC</h2>
<ul>
<li>Implement the library for the Web Assembly (Wasm) for JavaScript (<a href="">#3713</a>). Thanks <a href="https://github.com/igoriakovlev"><code>@​igoriakovlev</code></a>!</li>
<li>On Android, ensure that <code>Dispatchers.Main != Dispatchers.Main.immediate</code> (<a href="">#3545</a>, <a href="">#3963</a>).</li>
<li><code>kotlinx-coroutines-debug</code> is published with the incorrect Java 9 module info (<a href="">#3944</a>).</li>
<li>Major Kotlin version update: was 1.8.20, became 1.9.21.</li>
<li><code>kotlinx-coroutines-test</code>: set the default timeout of <code>runTest</code> to 60 seconds, added the ability to configure it on the JVM with the <code>kotlinx.coroutines.test.default_timeout=10s</code> (<a href="">#3800</a>).</li>
<li><code>kotlinx-coroutines-test</code>: fixed a bug that could lead to not all uncaught exceptions being reported after some tests failed (<a href="">#3800</a>).</li>
<li><code>delay(Duration)</code> rounds nanoseconds up to whole milliseconds and not down (<a href="">#3920</a>). Thanks <a href="https://github.com/kevincianfarini"><code>@​kevincianfarini</code></a>!</li>
<li><code>Dispatchers.Default</code> and the default thread for background work are guaranteed to use the same context classloader as the object containing it them (<a href="">#3832</a>).</li>
<li>It is guaranteed that by the time <code>SharedFlow.collect</code> suspends for the first time, it's registered as a subscriber for that <code>SharedFlow</code> (<a href="">#3885</a>). Before, it was also true, but not documented.</li>
<li>Atomicfu version is updated to 0.23.1, and Kotlin/Native atomic transformations are enabled, reducing the footprint of coroutine-heavy code (<a href="">#3954</a>).</li>
<li>Added a workaround for miscompilation of <code>withLock</code> on JS (<a href="">#3881</a>). Thanks <a href="https://github.com/CLOVIS-AI"><code>@​CLOVIS-AI</code></a>!</li>
<li>Small tweaks and documentation fixes.</li>
</ul>
<h2>1.7.3</h2>
<ul>
<li>Disabled the publication of the multiplatform library metadata for the old (1.6 and earlier) KMP Gradle plugin (<a href="">#3809</a>).</li>
</ul>
<!-- raw HTML omitted -->
</blockquote>
<p>... (trunc...

_Description has been truncated_

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3c13c535bf8e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.