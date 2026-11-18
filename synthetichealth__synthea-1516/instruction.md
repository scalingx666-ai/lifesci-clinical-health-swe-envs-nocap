# Issue

**Title:** Changes to hypertension onset to better align with statistics.

## Description

This set of module changes is designed to adjust the onset age of hypertension to be more in line with the following studies:

1. Ostchega Y, Fryar CD, Nwankwo T, Nguyen DT. Hypertension prevalence among adults aged 18 and over: United States, 2017–2018. NCHS Data Brief, no 364. Hyattsville, MD: National Center for Health Statistics. 2020.
2. Huang X, Lee K, Wang MC, Shah NS, Khan SS. Age at Diagnosis of Hypertension by Race and Ethnicity in the US From 2011 to 2020. JAMA Cardiol. 2022;7(9):986–987. doi:10.1001/jamacardio.2022.2345

# Real

- Age of Hypertension Onset

| Average (years) | Standard Deviation (years) |
|----:|----:|
| 46 | 15 |

- From source [2] above.

The data below was generated using the command `./run_synthea -p 10000` for the Before and After cohorts.


# Before

- Age of Hypertension Onset

| Average (years) | Standard Deviation (years) |
|----:|----:|
| 35.28 | 13.36 |

- Distribution
![image](https://github.com/user-attachments/assets/20bd7ae7-c5a3-490b-96ce-65c55163ca66)

# After
- Age of Hypertension Onset

| Average (years) | Standard Deviation (years) |
|----:|----:|
| 42.15 | 11.38 |

- Distribution
![image](https://github.com/user-attachments/assets/c624fd54-d9c1-40ca-9ef6-d8e00a4d2022)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2ca05dd2a01`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.