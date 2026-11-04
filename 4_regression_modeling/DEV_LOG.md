# Development log

## 2026-11-04 — Module 2 Part B

Completed all five required functions while preserving cell count and function signatures. Used imports inside solution functions so each cell declares its own dependencies. Resolved CSV paths relative to the notebook file.

Reproduced the supplied full-data and holdout metrics, residual mean and standard deviation, and shuffled-order Durbin–Watson. Executed every cell body in source order, including the readiness cell; all five functions were present with the expected signatures. Checked expected numerical outputs with floating-point tolerances and verified unchanged cell count. Inspected the generated residual plot.

The installed statsmodels VIF function defaults to standardizing inputs. Added signature-based compatibility so standardize=False reproduces the course's uncentered expected output, while older versions use their original interface. Separately calculated centered VIF with an intercept.

Added interpretation notes within existing markdown cells to distinguish uncentered from conventional VIF and avoid claiming temporal independence from shuffled residuals. Raw data and the completed notebook remain local under the repository's documentation-first source policy.

The marimo command-line check/export did not finish in this session; source-order cell execution passed, but a native interactive run/export was not verified. No chronological validation or deployment was performed.
