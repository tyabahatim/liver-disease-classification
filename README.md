# Liver Disease Classification (ILPD)

Binary classification of liver disease on the **Indian Liver Patient Dataset (ILPD)**, built as a full data-science pipeline for the Data Science module at FH Aachen (Medizintechnik, summer semester 2026).

## Overview

The project takes the ILPD dataset from raw patient records to a validated classifier that predicts whether a patient has liver disease from routine blood markers, age and sex. Rather than chasing a single accuracy number, it asks a sharper question: **how much of the remaining error is fixable by a better model, and how much is a ceiling in the data itself?**

## Dataset

- **Indian Liver Patient Dataset (ILPD)** — UCI Machine Learning Repository (ID 225). 583 patient records (4 dropped for a missing Albumin/Globulin ratio → 579 used).
- **Features:** age, sex, and standard liver-function blood markers (total & direct bilirubin, ALP, AST, ALT, total protein, albumin, A/G ratio).
- **Target:** liver disease vs. no liver disease (imbalanced classes).

## Approach

- Full pipeline in **Python** (pandas, scikit-learn, matplotlib): cleaning, exploratory analysis, modelling and evaluation.
- **Four models** compared in a 2×2 design (model family × intervention type), including **logistic regression** and **random forest**.
- **Leakage-safe methodology:** resampling applied only *inside* training folds (never before the train/test split), `StandardScaler` fit on training data only.
- **Evaluation under class imbalance** via **ROC-AUC** and **macro-F1** rather than raw accuracy.
- **Feature analysis:** dropping Direct Bilirubin (r = 0.87 with Total Bilirubin) left performance unchanged (AUC slightly up, ≈ 0.72), confirming redundancy.

## Key result

All four models converge on **AUC ≈ 0.70**. The 2×2 experiment shows the performance ceiling lies in the **data, not the model** — more complex models don't break through it. The strongest predictors (**ALP, AST, ALT, age**) align with established clinical markers for liver disease.

## Repository contents

- `Project work.ipynb` — the full analysis notebook (pipeline, models, evaluation).
- `ilpd+indian+liver+patient+dataset/` — the ILPD dataset.
- `fig6_confusion_matrix.png` — example result figure.

## Running it

1. Install dependencies: `pip install pandas scikit-learn matplotlib jupyter`
2. Open `Project work.ipynb` in Jupyter or PyCharm and run the cells top to bottom.

---
*Data Science module project · FH Aachen (Medizintechnik) · summer semester 2026.*
