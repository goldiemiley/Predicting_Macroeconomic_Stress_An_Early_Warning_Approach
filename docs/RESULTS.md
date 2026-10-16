# Results and interpretation

**Source:** original uploaded 44-page project report and Colab notebook. These are reported values, not a fresh run of the new forward-warning notebook.

## Sample

- 5,423 country-year records, 1995–2020, 20 columns.
- No stress: 2,838 (52.33%). Stress: 2,585 (47.67%).
- Heavy tails: GDP growth range approximately −62.08% to 149.97%; inflation maximum approximately 4,145.11%. Large missing fractions in current-account and FX variables.

## Original same-year model comparison

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 0.8240 | 0.8410 | 0.7776 | 0.8080 | 0.8853 |
| Decision Tree | 0.9917 | 0.9922 | 0.9903 | 0.9913 | 0.9971 |
| Random Forest | 0.9972 | 0.9942 | 1.0000 | 0.9971 | 0.9999 |
| Gradient Boosting | 0.9982 | 0.9961 | 1.0000 | 0.9981 | 1.0000 |

![Reported model comparison](../figures/model_comparison.png)

## Confusion matrix counts (negative / positive)

| Model | TN | FP | FN | TP |
|---|---:|---:|---:|---:|
| Logistic Regression | 492 | 76 | 115 | 402 |
| Decision Tree | 564 | 4 | 5 | 512 |
| Random Forest | 565 | 3 | 0 | 517 |
| Gradient Boosting | 566 | 2 | 0 | 517 |

All rows total 1,085 held-out records. At the reported 0.5 default threshold, Gradient Boosting makes 2 false positives and 0 false negatives on this same-year holdout. The ROC curve reaching FPR=1 at its endpoint is mathematically normal and is **not** the operational false-positive rate at the selected threshold.

## Reported stratified random cross-validation

| Model | Mean F1 | Mean ROC-AUC |
|---|---:|---:|
| Logistic Regression | 0.7985 | 0.8863 |
| Decision Tree | 0.9942 | 0.9990 |
| Random Forest | 0.9988 | 1.0000 |
| Gradient Boosting | 0.9994 | 1.0000 |

## Economic interpretation

For the constructed label, the report describes strong influence from current-account balance, the misery index, GDP growth, unemployment and inflation. These patterns largely mirror variables used to **define** the label, so they cannot be interpreted as independent causal discoveries.

## Research conclusion

**Gradient Boosting scored highest on the original same-year classification exercise. This does not establish an operational early-warning system.** A true test is whether previous-year observations predict later stress in a chronological holdout. The repository includes a separate notebook for that experiment; no forward-warning results are asserted until it is executed.
