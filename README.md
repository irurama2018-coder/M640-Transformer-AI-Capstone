# QM640 Transformer AI Capstone

**Project Title:** Developing a Multimodal AI Decision-Support Framework for Predictive Maintenance, Electrical Energy-Loss Reduction, and CAPEX Prioritization in Indian Power Utilities

**Course:** QM640 — Data Analytics Capstone  
**Research Status:** Interim analysis completed for RQ1 and RQ2; RQ3 and RQ4 pending utility and OEM data access.

## 1. Project Overview

This capstone investigates the potential of artificial intelligence and data analytics to support transformer condition assessment, predictive maintenance, electrical energy-loss reduction, and capital expenditure (CAPEX) prioritization in Indian power utilities.

The proposed framework integrates transformer fault classification, explainable machine learning, engineering-economic analysis, and investment optimization.

The project is organized into four research components. The current GitHub repository documents preliminary experimental work for RQ1 and RQ2 using a publicly sourced dissolved gas analysis (DGA) dataset.

## 2. Research Questions

**RQ1 — Transformer Fault Classification**

How effectively can supervised machine-learning models classify transformer fault categories using dissolved gas analysis measurements?

**RQ2 — Explainability and Stability**

Which DGA features contribute most strongly to model predictions, and how stable are global feature-importance rankings across model retraining?

**RQ3 — Electrical Energy-Loss Reduction**

How can transformer operating measurements, technical specifications, and maintenance information be used to estimate energy-loss reduction opportunities and their economic implications?

**RQ4 — CAPEX Prioritization**

How can transformer condition, expected benefits, investment costs, and budget constraints be integrated into a decision-support framework for capital investment prioritization?

RQ3 and RQ4 remain planned research components and will be developed using appropriately authorized utility and OEM datasets.

## 3. Repository Contents

| File | Description |
|---|---|
| `QM640_Interim_Report_RQ1_RQ2_Final.ipynb` | Google Colab notebook containing RQ1/RQ2 Python analyses, evaluation metrics, visualizations, and preliminary discussion |
| `QM640_Public_DGA_Fault_Dataset.xlsx` | DGA fault-classification dataset used for the preliminary analyses |
| `README.md` | Project overview, research methodology, results, limitations, and reproducibility instructions |

## 4. Dataset Description

The preliminary dataset contains **589 observations**, five DGA gas predictors, and one fault-category target variable.

| Variable | Description |
|---|---|
| `H2` | Hydrogen |
| `CH4` | Methane |
| `C2H6` | Ethane |
| `C2H4` | Ethylene |
| `C2H2` | Acetylene |
| `故障类型` | Transformer fault category |

Six fault classes are represented: D1, D2, PD, T1, T2, and T3.

Initial quality assessment identified no missing values and two exact duplicate rows.

**Dataset provenance notice:** The original publication, authorship, measurement units, labeling methodology, licensing conditions, and redistribution permission require further verification. The dataset should not be described as an officially endorsed IEEE dataset solely because an earlier file was named `IEEE_STANDARD.xlsx`.

## 5. Research Methodology

### RQ1: Supervised Machine Learning

Four baseline classifiers were evaluated:

- Random Forest
- Gradient Boosting
- Logistic Regression
- Support Vector Machine (SVM)

The preliminary evaluation used a stratified training/test split, classification metrics, confusion-matrix analysis, and five-fold stratified cross-validation on the training data.

Performance measures included accuracy, balanced accuracy, macro-F1 score, precision, and recall.

### RQ2: Explainable Artificial Intelligence

The explainability assessment included:

- Permutation feature importance
- SHAP feature-importance analysis
- Five-model retraining-based explanation stability
- Spearman rank correlation of global feature rankings
- Top-three Jaccard similarity

These methods examine global feature contributions and ranking consistency. They do not independently establish causal relationships, prediction reliability, or operational readiness.

## 6. Preliminary Research Results

### RQ1: Classification Performance

| Model | Accuracy | Balanced Accuracy | Macro-F1 |
|---|---:|---:|---:|
| Random Forest | 0.7712 | 0.7342 | 0.7405 |
| Gradient Boosting | 0.7203 | 0.6918 | 0.6965 |
| Logistic Regression | 0.5000 | 0.4007 | 0.3444 |
| SVM | 0.2542 | 0.2358 | 0.1791 |

Random Forest achieved the highest holdout performance among the evaluated baseline models.

Its five-fold cross-validation mean macro-F1 was **0.7731**, with a sample standard deviation of **0.0451**.

However, lower recall for T2 (0.42) and D1 (0.56) indicates the need for improved fault-specific detection and uncertainty analysis.

### RQ2: Explainability Results

Permutation importance and SHAP identified the same global feature-importance ordering:

1. Acetylene (`C2H2`)
2. Ethylene (`C2H4`)
3. Hydrogen (`H2`)
4. Ethane (`C2H6`)
5. Methane (`CH4`)

The retraining-based stability assessment produced a mean pairwise Spearman correlation of **1.0000** and mean top-three Jaccard similarity of **1.0000**.

These results indicate identical global feature rankings across the evaluated model fits. They do not imply perfect predictive accuracy or guaranteed stability under external operating conditions.

## 7. Reproducing the Analysis

The notebook is designed for Google Colab.

1. Open `QM640_Interim_Report_RQ1_RQ2_Final.ipynb` in Google Colab.
2. Confirm that the notebook loads `QM640_Public_DGA_Fault_Dataset.xlsx` from this repository.
3. Install any required Python dependencies that are not available in the Colab environment.
4. Select **Runtime → Restart and run all**.
5. Verify that the dataset loads with 589 rows and six columns.
6. Review the generated model-performance metrics, confusion matrix, feature-importance plots, and explanation-stability results.
7. Compare the newly generated results with the preliminary values documented above.

The notebook contains the analysis code and saved execution outputs. Results may vary if software versions, preprocessing, or model settings change.

## 8. Research Limitations

The current analysis has several limitations:

- Original dataset provenance and redistribution rights have not yet been fully established.
- Transformer identifiers and sampling dates are not available for verifying equipment-level independence.
- Two exact duplicate observations require further assessment.
- Random stratified splitting may not represent performance on previously unseen transformers.
- The baseline models have not undergone comprehensive training-only hyperparameter selection.
- Class-specific performance requires additional uncertainty analysis.
- Explanation stability was evaluated using overlapping training subsets and a fixed explanation sample.
- Independent external validation with utility operating records remains pending.

Consequently, these findings should be interpreted as **preliminary experimental evidence**, not as validation for autonomous maintenance or investment decisions.

## 9. Planned Research Extensions

The next phase will focus on validating dataset documentation, strengthening model evaluation, and obtaining authorized utility and OEM information.

For RQ3, the intended analysis will investigate transformer energy losses, operating characteristics, and maintenance economics.

For RQ4, the intended analysis will investigate budget-constrained investment prioritization using appropriate engineering-economic methods.

The final analytical design will depend on the quality, availability, and permitted use of the acquired data.

## 10. Responsible AI and Data Governance

The proposed framework emphasizes:

- Transparent model evaluation and documentation
- Engineering oversight of consequential maintenance decisions
- Protection of utility and OEM confidential information
- Explicit recognition of model limitations
- Traceability and reproducibility of analytical results
- Risk-aware interpretation of AI-supported recommendations

Publicly shared research materials must not contain confidential utility records, proprietary OEM information, credentials, or personal information.

## 11. Project Status

| Component | Status |
|---|---|
| RQ1 baseline classification | Preliminary analysis completed |
| RQ2 explainability and stability | Preliminary analysis completed |
| Dataset provenance verification | Pending |
| Training-only model tuning and uncertainty analysis | Planned |
| Independent utility validation | Pending |
| RQ3 energy-loss and economic modeling | Planned |
| RQ4 CAPEX optimization | Planned |

## 12. Academic Use Disclaimer

This repository supports an academic capstone research project. Reported findings are preliminary and should not be used as a substitute for qualified electrical engineering assessments, utility operating procedures, or independently validated investment analysis.

The repository's public availability does not establish the licensing status of third-party datasets.
