# Methodology and validity

## Original assignment design

Logistic Regression (scaled after median imputation), Decision Tree (maximum depth 5), Random Forest (300 trees), and Gradient Boosting were fitted to a binary stress label. An 80:20 stratified random split and 5-fold stratified random cross-validation were used in the primary reported comparison.

## Critical interpretation

The target is *defined* from current-period inflation, unemployment, GDP growth, current account and FX change. The original feature matrix contains these same inputs and engineered transformations. Consequently a tree can reproduce the threshold logic, producing artificially reassuring ~1.0 metrics **for the purported early-warning purpose**. This is not classic accidental leakage of unseen target values, but a **tautological target-feature construction**: the model learns a formula rather than predicts future shocks.

Repeated country-year observations in random folds also share country-specific and time-specific structures. Random folds do not test out-of-time prediction.

## Improved early-warning setup

1. Define `economic_stress` for year *t* using the original threshold definition, unchanged.
2. Generate predictors using indicators from year *t−1*, joined only for consecutive country years.
3. Train on target years through 2016; evaluate on 2017–2020. Avoid seeing holdout results during tuning.
4. Impute missing indicators on training samples only; scale Logistic Regression, not tree models.
5. Include a most-frequent-class baseline; evaluate accuracy, precision, recall, F1, ROC-AUC and confusion matrix. AUC is undefined if the holdout contains one class only.
6. Compare results to the contemporaneous baseline **without claiming that they estimate the same task**.

## Further validation recommended

- Rolling-origin / expanding-window validation with embargo if required by data publishing lags.
- Country-group holdouts to examine generalization to unseen countries.
- Sensitivity to stress thresholds, missingness and imputation strategy.
- True early-warning labels based on independently dated crises and reporting delays.
- Calibrated probabilities, PR-AUC, recall at an operational false-positive budget.
- Audit `economic_stress` construction and reject overlaps between aggregate countries and sovereign entities.

The repo's Colab notebook is a reference workflow and must be run against an actual user-controlled BigQuery table before any new scores are reported.
