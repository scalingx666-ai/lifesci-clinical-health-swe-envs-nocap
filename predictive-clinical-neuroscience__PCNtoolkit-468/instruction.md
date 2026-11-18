# Issue

**Title:** feat: better dp for computing gradient of kv

## Description

#### What does this implement/fix?

In order to use NUTS, all components of the computation graph have to be differentiable. The SHASHb distribution uses the scipy.special.kv function, but scipy does not provide the derivative (yet). We work around this by approximating the gradient using a finite difference method (shash.Kv.grad), which is parameterized by dp. The value of dp has been set at 1e-16 for some time now, but that's actually smaller than can be reliably represented using python floats. This PR sets dp to 1e-8.

A sweep on several values of dp showed this has the following effects:

1. A 5-fold speedup of MCMC sampling with SHASHb models
<details>

<summary>Plot of fit duration vs dp</summary>

<img width="1050" height="750" alt="fit_duration" src="https://github.com/user-attachments/assets/41d221c3-efa1-429c-a5b9-367de5f7a86e" />

</details>

2. Better chain mixing, visible as a lower Rhat

<details>

<summary>Plot of Rhat vs dp</summary>

<img width="1050" height="750" alt="r_hat" src="https://github.com/user-attachments/assets/d210c5f5-7ad4-4c7b-9903-849b422d918e" />


</details>

3. Stability of all evaluation metrics across the spectrum

<details>

<summary>Plots of all evaluation metrics vs dp</summary>

<img width="1050" height="750" alt="MACE" src="https://github.com/user-attachments/assets/b517d419-baa3-4378-b37a-cfd72242d549" />
<img width="1050" height="750" alt="MAPE" src="https://github.com/user-attachments/assets/bbab8c51-2c90-45ca-a70a-41c7cb48c3cf" />
<img width="1050" height="750" alt="test_MSLL" src="https://github.com/user-attachments/assets/f233f804-8860-4564-965f-02616b798674" />
<img width="1050" height="750" alt="train_MSLL" src="https://github.com/user-attachments/assets/36616320-bc5a-4ed6-ae22-d76726638f50" />
<img width="1050" height="750" alt="test_MLL" src="https://github.com/user-attachments/assets/9eed6290-a9e1-4ed1-b996-185370e21874" />
<img width="1050" height="750" alt="train_MLL" src="https://github.com/user-attachments/assets/0cc05601-c7b3-4899-8c5f-5fd1a0ce0bb6" />
<img width="1050" height="750" alt="test_shapW" src="https://github.com/user-attachments/assets/c280d83d-5e35-4077-817c-bcf6be2a5f8a" />
<img width="1050" height="750" alt="train_shapW" src="https://github.com/user-attachments/assets/7c85c79a-d5b1-4258-94ff-5ea0c5f5e7e9" />


</details>

4. Model comparisons show no meaningful difference in elpd_loo.

<details>

<summary>Model comparisons</summary>

Error bars indicate standard deviation of results.

<img width="1800" height="1500" alt="CortexVol_comparison" src="https://github.com/user-attachments/assets/479f940b-79c1-4a82-b6c8-5eaa072d0f8e" />
<img width="1800" height="1500" alt="Right-Lateral-Ventricle_comparison" src="https://github.com/user-attachments/assets/5c6d02a8-ce5f-4264-8986-c86185171177" />
<img width="1800" height="1500" alt="Right-Amygdala_comparison" src="https://github.com/user-attachments/assets/c42571f5-f6fa-4aeb-b87f-7acba4a1ff9a" />
<img width="1800" height="1500" alt="WM-hypointensities_comparison" src="https://github.com/user-attachments/assets/68924dec-f659-4a8b-bef8-4d667afabd7a" />

</details>


<details>

<summary>Pickled results and comparisons</summary>

[pickled_dp_sweep_results.zip](https://github.com/user-attachments/files/28193441/pickled_dp_sweep_results.zip)

</details>

#### To reproduce

Place this script in a new directory called `scripts` in the project root. 
[dp_sweep.py](https://github.com/user-attachments/files/28193527/dp_sweep.py)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `db07b9eff5f4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.