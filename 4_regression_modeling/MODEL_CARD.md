# Model card: five-temperature OLS baseline

- **Status:** Educational baseline; not deployed.
- **Target:** load_shortfall_3h from the supplied Spain energy/weather dataset.
- **Predictors:** Madrid_temp, Seville_temp, Valencia_temp, Bilbao_temp, Barcelona_temp.
- **Estimator:** scikit-learn LinearRegression with an intercept.
- **Evaluation:** Prescribed random 80/20 split, seed 42; R² 0.0718491, RMSE 5098.7257.
- **Full-data coefficients:** Madrid 121.5574; Seville -78.9912; Valencia -6.8158; Bilbao 29.1241; Barcelona 113.1248, per Kelvin conditional on the other temperatures. These are associations, not causal effects.
- **Missing values:** Complete-case deletion across all columns, including unused predictors; this can affect representativeness.
- **Limitations:** Low explanatory power, correlated predictors, shuffled residual ordering, no chronological evaluation, no formal constant-variance conclusion, and no operational validation. Dataset provenance and target-unit semantics are inherited from the course and have not been independently verified.
- **Intended use:** Learning multiple regression and diagnostic reasoning.
- **Next evaluation:** Chronological holdout, training-only preprocessing and feature selection, diverse predictors, and regularization compared with simple baselines.
