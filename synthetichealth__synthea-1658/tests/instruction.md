# Issue

**Title:** Cache parsed range bounds in Demographics to avoid repeated regex/parseInt per patient

## Description

## Summary

Caches the parsed integer bounds from demographic range strings (e.g., `"0..4"` → `[0, 4]`) 
to avoid redundant regex splitting and `Integer.parseInt()` on every call to `pickAge()` 
and `pickIncome()`.

## Motivation

Addresses the TODO comments in `Demographics.java` lines 89 and 284:
> "this seems like it would benefit from better caching"

These methods are called for every generated patient. The set of range strings is small 
and fixed (defined by the demographics CSV), so parsing them repeatedly is wasteful.

## Changes

- Added a static `ConcurrentHashMap<String, int[]>` cache (`RANGE_CACHE`)
- Added `parseRange(String)` helper that uses `computeIfAbsent` for thread-safe lazy caching
- Replaced inline `split("\\.\\.") + parseInt` calls with `parseRange()` lookups
- Removed the TODO comments since the caching is now implemented

## Impact

For a typical 10,000 patient run, this eliminates ~20,000 redundant regex operations 
and ~40,000 `Integer.parseInt` calls. The cache is thread-safe for parallel generation.

No behavioral change — same output, just faster.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c48eac705e15`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.