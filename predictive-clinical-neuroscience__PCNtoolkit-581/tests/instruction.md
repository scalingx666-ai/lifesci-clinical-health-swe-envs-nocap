# Issue

**Title:** enh: compute SHASH P once per repeated value

## Description

Part of #576 (row 3). Based on `dev`. It does not need #572 or #577–#580.

**Review 5 commits:** b4078db (the change), 3a571da (empty arrays), and the review changes f2fc1b1 (move helpers to `pcntoolkit/util/data_utils.py`), 41a9290 (first cache, of values) and 4320066 (cache of positions, replaces the first cache).

## What it does

The SHASH likelihoods need the mean and variance of the SHASH distribution (`m1m2`). `m1m2` calls the function `P`, and `P` calls the Bessel function `scipy.special.kv` 4 times per value. In HBR `predict`, the inputs have one value per observation and posterior sample: for example 20 000 × 400 = 8 million values. `kv` is the slowest part of SHASHb predict.

But delta usually has few distinct values:

| How delta is modelled | Distinct values | Example |
|---|---|---|
| Fixed | 1 per posterior sample | 400 instead of 8 million |
| Random effect (one value per batch level) | levels × samples | 20 levels → 8 000 |
| Linear in the covariates | all distinct | no saving |

A new helper, `dedupe` in `pcntoolkit/util/data_utils.py`, computes `P` only on the distinct values and then copies the results back:
1. **Same value along an axis** (fixed delta): keep one slice. This check takes about 4 ms for 10 million values.
2. **Few distinct values** (random effect): use `np.unique`. First, a sample of 100 000 values estimates how many values are distinct. If more than half are distinct, skip `np.unique`, so linear delta does not pay for a full sort.
3. **Otherwise:** compute every value, as before.

`P`, `K` and `m1m2` work value by value, so the result is **bit-identical**. Scalar inputs return the same types as before.

## Cache

`compute_centiles` calls `backward` once per centile, and each call computes `m1m2` of the same delta again. For a random-effect delta, `np.unique` then sorts the same values each time (about 0.7 s for 8 million values).

`dedupe` keeps the positions of the distinct values from the last call (1 slot: shape, index of the first copy of each distinct value, inverse indices). The next array often has new values in the same grouping, for example delta of the next response variable. Cached positions are used only if `arr[index][inverse]` gives back `arr` bit for bit (about 0.09 s for 8 million values, compared to about 1.5 s for `np.unique`). Thus a wrong grouping is never used, and it is not necessary to clear the cache when a new model graph is made. `clear_dedupe_cache()` frees the memory. The bit comparison also keeps `-0.0` and `0.0` apart. The inverse indices use the smallest unsigned type (uint16 for 8 000 values, 16 MB for 8 million values).

The 5 ms all-distinct sample check stays: for linear delta, `np.unique` with `return_index` costs 2.3 s and saves nothing.

`compute_centiles`, SHASHb with delta random over 20 sites, 3 response variables (N = 20 000, 400 draws, 5 centiles): **about 80 s → 55 s** (machine with other load), centiles bit-identical. The cache does not help for fixed delta (already fast), linear delta (all values distinct) or `harmonize` (the two calls use different batch effects).

The constants (`UNIQUE_SAMPLE_SIZE`, `MAX_UNIQUE_FRACTION`, `CHUNK_SIZE`) are public and are the defaults of keyword parameters. `use_cache=False` turns the cache off.

## Tests

New `test/test_util/test_data_utils.py` (dedupe, elementwise, cache, cache content check) and `test/test_math/test_shash.py` (`m1m2`, `P`, `K` bit-identical to direct `scipy.special.kv`).

## Threads

The old `K` ran on dask threads. I kept dask for large arrays in a new `elementwise` helper (also in `data_utils.py`, so `data_utils` now imports dask; dask is not a new dependency). `m1m2` now computes both `P` terms in one dask call. Without dask, linear delta was 2.5× slower than the old code on 8 cores.

dask uses all cores the process may use. It ignores `SLURM_CPUS_PER_TASK` and the `n_jobs` workers from #577. This was already so before this PR. #587 (row 8) replaces dask.

## Speed

8-core laptop.

**`NormativeModel.predict`**, saved SHASHb benchmark model (fixed epsilon and delta, 400 posterior samples, 1 response variable). Best of 2 runs after a warm-up:

| N | Before | After | Speed-up |
|---|---|---|---|
| 1 000 | 2.23 s | 0.70 s | 3.2× |
| 20 000 | 12.4 s | 3.32 s | 3.7× |

**`m1m2` alone**, 10 000 × 1 000 arrays, 2 runs each:

| delta | Before (dask, 8 threads) | Before (1 thread) | After |
|---|---|---|---|
| Fixed | 3.3–3.9 s | 7.6–8.1 s | 0.80–0.91 s |
| Random effect (20 levels) | 3.3–4.2 s | 8.2–8.5 s | 1.6–2.2 s |
| Linear (all distinct) | 3.0–4.0 s | 8.3–8.5 s | 2.5–2.7 s |

`shash.m1m2_fixed` in the #572 benchmark script (`--size medium`): 5.2 s before, 1.6 s after.

## Results

Z, centiles, logp, Yhat and all `m1m2` outputs above are **bit-identical** to the old code.

## Validation

I checked and timed this PR with the benchmark and validation code in #572. This PR does not include that code.

## AI use

Claude Opus 5.5 (Claude Code) wrote the code and this description, and ran the benchmarks and the equivalence checks. It also made the review changes (f2fc1b1, 41a9290, 4320066) and the rebase on `dev`. A human set the rules in #576 and reviews this PR.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01Mr7sVWVWnqWZUEYkYUaeLy

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5b0cf44e57bf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.