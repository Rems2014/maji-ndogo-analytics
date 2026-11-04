# Understanding the Shortfall — Part B

Five city temperatures explain only 6.82% of the observed variance in Spain's 3-hourly energy shortfall. On the prescribed random 80/20 split, R² is 0.07185 and RMSE is 5,098.73. This is a completed training baseline, unsuitable for operational forecasting without further development.

## Method and evidence

The supplied Module 2 archive contains notebook.py, df_train.csv and df_test.csv. Training data were loaded with the first column as index; time was removed, encoded Valencia wind direction and Seville pressure were converted to numbers, and rows with any missing values were dropped. The resulting analysis has 6,695 rows and 47 columns. The supplied external test file was not used for evaluation.

Ordinary least squares uses Madrid, Seville, Valencia, Bilbao and Barcelona temperatures. The holdout uses test_size=0.2 and random_state=42.

| Measure | Result |
|---|---:|
| Full-data R² | 0.0682061 |
| Full-data RMSE | 5091.7260 |
| Holdout R² | 0.0718491 |
| Holdout RMSE | 5098.7257 |
| Holdout mean residual | -145.1826 |
| Holdout residual standard deviation (ddof=0) | 5096.6583 |
| Durbin–Watson in shuffled holdout order | 1.9733091 |

## Diagnostic findings

The course's VIF calculation omits an intercept. Positive Kelvin means inflate the uncentered results. Conventional VIF calculated with an intercept gives a more appropriate measure for this model:

| City | Course uncentered VIF | Centered VIF |
|---|---:|---:|
| Madrid | 7006.73 | 10.09 |
| Seville | 9105.43 | 6.76 |
| Valencia | 14491.98 | 8.44 |
| Bilbao | 8624.93 | 5.00 |
| Barcelona | 12796.33 | 7.21 |

Redundancy remains material, but the uncentered thousands overstate the conventional diagnostic. Do not infer independent causal effects from these coefficients.

Durbin–Watson near two in randomly shuffled order does **not** establish temporal independence. A chronological holdout, timestamp checks and appropriately ordered residual diagnostics are needed. Similar random-holdout and full-data performance also does not establish future forecasting performance.

The residual plot shows substantial scatter without a clear monotonic funnel; constant variance and absence of conditional bias are not proven. The holdout mean residual indicates average overprediction of about 145.18 target units on this split.

## Reflection

More predictors help only when they contribute information beyond existing features. Temperatures share seasonal and national weather patterns. The Part A comparison is also not a clean nested comparison: its stated baseline uses humidity, while this model uses temperatures.

Madrid has the highest centered VIF and is a candidate for a removal sensitivity check, followed by recomputing VIF and validation metrics. Valencia has the highest course uncentered VIF, but that alone is not a sufficient deletion rule. No city was dropped from the required five-feature model.

Wind, cloud cover, solar radiation, demand/calendar effects, generation availability and appropriately lagged measurements could add different information. Availability at prediction time must be checked. Diagnose redundancy first because it makes individual coefficients sensitive to feature choices and sampling variation.

## Deliverables and scope

See [model card](MODEL_CARD.md) and [development log](DEV_LOG.md). The completed Python notebook, original CSV companions, residual plot and verification log are delivered locally. This repository retains documentation only, following its source policy. This Spain training exercise is distinct from the Maji Ndogo agricultural audit elsewhere in the portfolio.
