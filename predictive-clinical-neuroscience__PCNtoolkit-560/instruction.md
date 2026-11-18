# Issue

**Title:** Possibility to model the pairwise interactions between covariates with composite basis

## Description

#### AI assistance

I used ChatGPT to help develop the tests and documentation. I reviewed and applied the changes and ran the tests locally.

#### Reference issue (if any)

No dedicated issue linked.

#### What does this implement/fix?

Adds optional pairwise interactions to `CompositeBasisFunction`, allowing models to represent effects such as different nonlinear age trajectories by sex.

- `interactions=[(i, j)]` refers to indices in `parts`. Each pair appends all products between the two components’ transformed basis columns.
- Interaction columns follow the main-effect columns, and `dimension` includes the interaction terms.
- Dictionary serialization preserves interactions while retaining upstream’s version propagation to component bases.
- Older dictionaries without an `interactions` field continue to load without interactions.

Tests cover interaction values, dimensions, component ordering, multidimensional basis products, and dictionary loading. All basis-function tests pass locally.

#### To reproduce

This example combines a B-spline age effect, a binary sex effect, and their interaction:

```python
import numpy as np

from pcntoolkit.math_functions.basis_function import (
    BasisFunction,
    BsplineBasisFunction,
    CompositeBasisFunction,
    LinearBasisFunction,
)

age = np.linspace(10, 80, 20)
sex = np.tile([0.0, 1.0], 10)
X = np.column_stack([age, sex])

age_basis = BsplineBasisFunction(
    basis_column=0,
    degree=3,
    nknots=5,
)
basis = CompositeBasisFunction(
    parts=[
        age_basis,
        LinearBasisFunction(basis_column=1),
    ],
    interactions=[(0, 1)],
)

basis.fit(X)
Phi = basis.transform(X)

n_age_terms = age_basis.dimension
age_terms = Phi[:, :n_age_terms]
interaction_terms = Phi[:, -n_age_terms:]

assert Phi.shape == (len(X), 2 * n_age_terms + 1)
np.testing.assert_allclose(
    interaction_terms,
    age_terms * sex[:, None],
)
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c77f550a36e1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.