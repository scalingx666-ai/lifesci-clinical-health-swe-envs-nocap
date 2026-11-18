# Issue

**Title:** Add ADVI, Laplace and Pathfinder as approximate inference methods for fitting HBR

## Description

Variational inference (VI) should make HBR _faster_ as it replaces MCMC sampling with optimization. From a quick search I see that [ADVI ](https://www.pymc.io/projects/docs/en/stable/api/generated/pymc.ADVI.html) and [Pathfinder ](https://www.pymc.io/projects/examples/en/latest/variational_inference/pathfinder.html) might be the best VI algorithms for HBR from PyMC to choose from.

What is reported online is that ADVI might underestimate posterior uncertainty, particularly for the hierarchical variance parameters that control between-site variability (e.g. `intercept_sigma`)

#### Important
pathfinder needs `pymc-extras` package. To allow   `pymc-extras >= 0.11.0 ` we should implement first this issue #450.

#### To reproduce
To see the results from the benchmark, see `04_HBR_SHASH_variational_inference_benchmark.ipynb` (make sure to install `pymc-extras == 0.10.0`  to run it)

#### Findings from the notebook run
- Pathfinder and ADVI are **~3 times faster** than MCMC for a sample of ~1000 subject with one response variable.
- Pathfinder performed better than ADVI at estimating z-scores and centiles. For pathfinder, divergences from MCMC are seen at the edges of the centile plots, probably because there are not many datapoints and there is extrapolation
- Pathfinder reported pareto-k around 2, which is a lot higher than the <0.7 which PyMC recommends. This means that the full posterior is poorly approximated. However this does not show in our centiles and zscores. Probably because z-scores and centiles depend only on posterior means, and not posterior widths (that were poorly estimated)
- we tried different configs for pathfinder but the default one performed the best.

Regarding the posterior parameters:
- in comparison to MCMC, both advi and pathfinder tend to underestimate most stds of posterior parameters, especially the std of `intercept_sigma`, `mu_intercept_mu`. `slope_mu`. 
- advi also struggles to estimate the mean of `epsilon `and `delta`

#### Conclusions
- HBR shash is faster with VI. 
- Pathfinder is better VI algorithm vs advi
- Pathfinder and MCMC diverge mostly in the edges (young and old ages) probably due to extrapolation


#### TODO
- check how much time improves with HBR normal
- check how much time improves with HBR shash with more subjects and response variables
- seems that default advi did not perform well due to lack of convergence. We could try [DADVI ](https://www.pymc.io/projects/extras/en/stable/generated/pymc_extras.inference.fit_dadvi.html) or use another optimizer like adam or adagrad_window (which in the notebook performed better than default advi)

#### question
is this convincing to go for pathfinder? The only problem is see is the high pareto k (=full posterior is poorly approximated) and the divergences from the MCMC in the edges (young and old ages). Other than that the centiles and zscores look good enough to me.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b207a6f0fec`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.