# Issue

**Title:** [FIX][DOC] Limit pygments version

## Description

After #1666 
Code blocks in markdown not behaving as usual : `<p>` HTML element instead of `<pre>` in HTML rendering.

Root cause summary:

- Pygments 2.20.0 changed HtmlFormatter.__init__ to call html.escape() on the filename option
- pymdown-extensions was passing filename=None
- html.escape(None) → AttributeError
- The exception was silently swallowed by a bare except Exception in eval_fence()
- The fenced code block was never processed, falling through to the inline code parser → `<p><code>`

Fix: Downgrading to pygments==2.19.1.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `137e65f88f15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.