# QM640 Transformer AI Capstone

**Project:** Developing a Multimodal AI Decision-Support Framework for Predictive Maintenance, Electrical Energy-Loss Reduction, and CAPEX Prioritization in Indian Power Utilities  
**Course:** QM640 — Data Analytics Capstone  
**Status:** Preliminary RQ1 and RQ2 analyses completed; RQ3 and RQ4 pending authorized utility/OEM data.

## Project overview

This academic capstone explores how transformer condition data, explainable machine learning, engineering-economic assessment, and budget-constrained optimization could inform maintenance and capital investment decisions in Indian power utilities. The current repository documents **preliminary** dissolved gas analysis (DGA) experiments for RQ1 and RQ2. It does not yet validate a deployed predictive-maintenance or CAPEX decision system.

## Research questions

- **RQ1 — Fault classification:** How effectively can supervised machine-learning models classify transformer fault categories from DGA measurements?
- **RQ2 — Explainability:** Which DGA features contribute most strongly to predictions, and how stable are global importance rankings across retraining?
- **RQ3 — Energy-loss reduction:** How can transformer operating measurements and specifications support estimates of energy-loss reduction and maintenance economics? **Pending data access.**
- **RQ4 — CAPEX prioritization:** How can condition, expected benefits, costs, and budget constraints inform capital investment priorities? **Pending data access.**

## Repository files

| File | Purpose |
| --- | --- |
| `QM640_Interim_Report_RQ1_RQ2_Final.ipynb` | Google Colab analysis, saved results, figures, and interpretation for RQ1 and RQ2 |
| `QM640_Public_DGA_Fault_Dataset.xlsx` | DGA fault-classification dataset used in the preliminary analyses |
| `README.md` | Project description, methods, findings, limitations, and reproduction guidance |

## Dataset and scope

The dataset contains **589 observations**, **five gas predictors** (`H2`, `CH4`, `C2H6`, `C2H4`, `C2H2`), and **one target column** (`故障类型`, meaning fault type). The six target classes are **D1, D2, PD, T1, T2, and T3**. Initial inspection found **zero missing values** and **two exact duplicate rows**; whether the duplicates represent repeated records or valid separate observations remains unresolved.

**Provenance and licensing:** Original source attribution, authorship, measurement units, labeling methodology, and permission to redistribute the spreadsheet have **not yet been independently verified**. The prior filename `IEEE_STANDARD.xlsx` does not establish IEEE authorship, endorsement, or a dataset standard. Repository publication is not evidence that third-party redistribution is authorized.

## RQ1 — Methods and preliminary results

Four baseline classifiers were compared using a stratified training/test split: Random Forest, Gradient Boosting, Logistic Regression, and Support Vector Machine. Five-fold stratified cross-validation was also performed on the training partition for Random Forest.

| Baseline model | Holdout accuracy | Balanced accuracy | Macro-F1 |
| --- | ---: | ---: | ---: |
| Random Forest | 0.7712 | 0.7342 | 0.7405 |
| Gradient Boosting | 0.7203 | 0.6918 | 0.6965 |
| Logistic Regression | 0.5000 | 0.4007 | 0.3444 |
| Support Vector Machine | 0.2542 | 0.2358 | 0.1791 |

Random Forest had the highest holdout performance **among these evaluated baselines**. Its training-only five-fold cross-validation yielded mean macro-F1 **0.7731** (sample SD **0.0451**). Holdout recall was relatively low for **T2 (0.42)** and **D1 (0.56)**, requiring attention before considering operational use. These results do not establish that Random Forest would outperform tuned alternatives or generalize to previously unseen transformers.

## RQ2 — Explainability and stability

Permutation importance and SHAP gave the same global ordering of the five gases:

1. `C2H2` — acetylene
2. `C2H4` — ethylene
3. `H2` — hydrogen
4. `C2H6` — ethane
5. `CH4` — methane

Across five retrained Random Forest fits, the evaluated global feature rankings were identical, giving mean pairwise **Spearman rank correlation = 1.0000** and mean **top-three Jaccard similarity = 1.0000**. These results concern **global ranking stability within this evaluation**, not perfect prediction, causal effects, individual-explanation stability, or external validity.

## Reproduce the notebook

1. Open `QM640_Interim_Report_RQ1_RQ2_Final.ipynb` in [Google Colab](https://colab.research.google.com/).
2. Confirm that its data-loading cell points to `QM640_Public_DGA_Fault_Dataset.xlsx` in this repository.
3. Install any missing packages if Colab requests them.
4. Select **Runtime → Restart and run all**.
5. Check that the dataset loads with shape **(589, 6)** and that model metrics and figures execute without errors.
6. Compare the fresh outputs with the numerical findings above. Update the reported values if they differ.

The published notebook may include saved outputs from a prior Colab run. A saved output is not independent verification that the notebook will reproduce unchanged under every future environment or package version.

## Limitations and next steps

- Verify the dataset's original publication, license, units, and fault-label definitions.
- Investigate exact/near duplicates and potential measurement-limit substitutions.
- Select and tune models using training data only; assess class-wise uncertainty and potential leakage.
- Seek independent utility records with transformer identifiers and dates for equipment-level external validation.
- Conduct RQ3 energy-loss/economic analysis and RQ4 budget-constrained CAPEX analysis **only after authorized access to suitable utility and OEM data**.

## Responsible use and data governance

All findings are **preliminary academic research**. Fault classifications and explanations require qualified engineering judgment before maintenance actions. The repository must not contain confidential utility/OEM records, personal information, credentials, or proprietary documents. Public release of the dataset should occur only where its redistribution rights are confirmed.

## Academic disclaimer

This repository is an educational research artifact and is not a validated operational transformer-monitoring, electrical safety, or investment decision system.
