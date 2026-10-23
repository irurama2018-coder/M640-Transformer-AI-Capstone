# QM640 Transformer AI Capstone

**Project title:** Developing a Multimodal AI Decision-Support Framework for Predictive Maintenance, Electrical Energy-Loss Reduction, and CAPEX Prioritization in Indian Power Utilities  
**Course:** QM640 — Data Analytics Capstone  
**Research stage:** Preliminary RQ1–RQ2 DGA analysis and scenario-based RQ3–RQ4 distribution-transformer analysis completed; OEM/utility validation and separate power-transformer modeling pending.

## Project overview

This academic capstone examines how transformer dissolved gas analysis (DGA), explainable machine learning, engineering energy-loss models, and constrained financial optimization may support transformer maintenance and capital-investment decisions in Indian power utilities. The current analyses are **separate research modules**, not a validated integrated multimodal deployment. RQ1–RQ2 use public DGA observations; RQ3–RQ4 use distribution-transformer loss benchmarks combined with explicitly hypothetical economic inputs. Results should not be interpreted as observed utility performance.

## Research questions and progress

| Question | Scope | Current status |
| --- | --- | --- |
| **RQ1 — Fault classification** | Compare supervised classifiers using DGA gas concentrations and six fault categories | Preliminary model comparison completed |
| **RQ2 — Explainability** | Assess permutation importance, SHAP attributions, and global feature-ranking stability | Preliminary explainability analysis completed |
| **RQ3 — Energy-loss reduction** | Infer simplified loss components from distribution-transformer benchmark ceilings and estimate annual loss reduction across loading scenarios | Six-rating scenario analysis completed; field validation pending |
| **RQ4 — CAPEX prioritization** | Evaluate energy-only NPV, cost scenarios, Monte Carlo uncertainty, and budget-constrained selection | Scenario optimization completed; actual investment validation pending |

## Repository guide

| File | Purpose |
| --- | --- |
| [`QM640_Interim_Report_RQ1_RQ2_Final.ipynb`](QM640_Interim_Report_RQ1_RQ2_Final.ipynb) | Executed RQ1–RQ2 classification and explainability notebook |
| [`QM640_Public_DGA_Fault_Dataset.xlsx`](QM640_Public_DGA_Fault_Dataset.xlsx) | Preliminary DGA data (provenance/license still to be verified) |
| [`QM640_Interim_Report_RQ3_RQ4_Final.ipynb`](QM640_Interim_Report_RQ3_RQ4_Final.ipynb) | Executed RQ3–RQ4 engineering and economic scenario notebook |
| [`QM640_RQ34_Distribution_Benchmark_Inputs.csv`](QM640_RQ34_Distribution_Benchmark_Inputs.csv) | Six distribution-transformer loss-benchmark records plus hypothetical CAPEX inputs |
| [`QM640_RQ3_RQ4_Analysis.ipynb`](QM640_RQ3_RQ4_Analysis.ipynb) | Additional RQ3–RQ4 analysis notebook; **use the interim final notebook above as the principal reporting version** |
| [`QM640_RQ3_RQ4_Expanded_Analysis.xlsx`](QM640_RQ3_RQ4_Expanded_Analysis.xlsx) | Supporting sensitivity and financial scenario workbook |
| [`QM640_RQ3_RQ4_Public_Data_Starter.xlsx`](QM640_RQ3_RQ4_Public_Data_Starter.xlsx) | Earlier public-data starter workbook; not the authoritative final result set |
| `QM640_RQ4_Reproducible_Monte_Carlo_Draws.csv` (if present) | Supporting simulated draws; inspect the version and assumptions before comparing with the final notebook |
| `README.md` | Research scope, instructions, findings, sources, and limitations |

**Version control note:** Some earlier workbooks/notebooks contain alternative benchmark or scenario assumptions. Do not combine results from different versions without reconciling input values, financial assumptions, and simulation settings. The two *Interim_Report* notebooks above are the primary documented interim analyses.

## RQ1 — DGA fault classification

### Dataset and approach

The preliminary DGA dataset has **589 observations** with five predictors (`H2`, `CH4`, `C2H6`, `C2H4`, `C2H2`) and target `故障类型` (fault type). Classes: **D1, D2, PD, T1, T2, T3**. Initial checks found no missing values and two exact duplicate rows. The analysis uses an 80:20 stratified split (471 training, 118 holdout), four baseline classifiers, and training-only five-fold cross-validation for Random Forest.

| Classifier | Holdout accuracy | Balanced accuracy | Macro-F1 |
| --- | ---: | ---: | ---: |
| Random Forest | 0.7712 | 0.7342 | 0.7405 |
| Gradient Boosting | 0.7203 | 0.6918 | 0.6965 |
| Logistic Regression | 0.5000 | 0.4007 | 0.3444 |
| Support Vector Machine | 0.2542 | 0.2358 | 0.1791 |

Random Forest had the strongest **exploratory baseline** results. Training-only five-fold cross-validation mean macro-F1 was **0.7731** (sample SD **0.0451**). Holdout recall was relatively low for **T2 (0.42)** and **D1 (0.56)**. These findings do not establish external transformer-level generalization or readiness for operational fault diagnosis.

## RQ2 — Explainability

Permutation importance (drop in macro-F1 when a gas is shuffled) and SHAP (model-attribution magnitude) produced the same global feature ordering:

1. **C2H2** — acetylene
2. **C2H4** — ethylene
3. **H2** — hydrogen
4. **C2H6** — ethane
5. **CH4** — methane

Across five retrained Random Forest fits, the evaluated global rankings were identical (mean pairwise Spearman rank correlation **1.0000**; top-three Jaccard similarity **1.0000**). This is **internal global-ranking stability** on the evaluated sample—not causal inference, perfect classification, individual-explanation stability, or external replication. Permutation and SHAP scores have different units and should not be directly compared in magnitude.

## RQ3 — Distribution-transformer energy-loss modeling

### Inputs and engineering model

The scenario compares six distribution-transformer ratings (**16, 25, 63, 100, 160, 200 kVA**) using tabulated **3-star versus 5-star total-loss benchmark ceilings** at 50% and 100% rated loading. The model infers simplified no-load and rated-load loss components:

\[
P_{LL}=\frac{P_{100}-P_{50}}{0.75},\qquad P_0=P_{100}-P_{LL}
\]

\[
P_{loss}(x)=P_0+x^2P_{LL},\qquad
E_{annual}=8760\,[P_{loss,3\star}(x)-P_{loss,5\star}(x)]
\]

Here, losses are expressed in **kW** when computing annual energy in **kWh**, and \(x\) is the per-unit load. The reported base case assumes **constant 60% loading, 8,760 hours/year**, and an illustrative **₹7/kWh** energy value. The inferred components are **not independently measured OEM factory-test losses**. Results assume constant voltage and simplified load-squared losses; temperature, varying load profiles, auxiliary losses, and field measurements are not represented.

### Modeled annual energy savings (60% constant load)

| Transformer rating | Annual loss reduction (kWh) | Annual energy value at ₹7/kWh (approx.) |
| --- | ---: | ---: |
| 16 kVA | 237.92 | ₹1,665 |
| 25 kVA | 343.74 | ₹2,406 |
| 63 kVA | 593.23 | ₹4,153 |
| 100 kVA | 862.57 | ₹6,038 |
| 160 kVA | 1,066.85 | ₹7,468 |
| 200 kVA | 1,282.35 | ₹8,976 |

These are **modeled benchmark-ceiling comparisons**, not guaranteed savings from a particular manufacturer's transformer or measured utility energy-loss reductions. The notebook also evaluates loading sensitivity.

## RQ4 — Financial analysis and CAPEX prioritization

### Base assumptions

| Parameter | Base scenario |
| --- | --- |
| Investment interpretation | Hypothetical **full replacement CAPEX** |
| CAPEX per unit | ₹50,000 to ₹300,000 across the six ratings (illustrative, not quotations) |
| Electricity value | ₹7/kWh (assumed) |
| Discount rate | 8% annually (assumed) |
| Evaluation horizon | 15 years (assumed) |
| Example budget | ₹8,00,000 (assumed) |
| Benefit scope | Energy-loss savings only in the base case; no verified reliability benefit |

For constant annual financial savings \(B\), initial capital cost \(C\), annual discount rate \(r\), and horizon \(T\), the simplified net present value is:

\[
NPV=-C+\sum_{t=1}^{T}\frac{B}{(1+r)^t}
\]

This omits unverified outage avoidance, maintenance costs, residual values, tax effects, energy-price escalation, and other project-specific factors. **Full replacement cost and incremental efficiency-upgrade premium are distinct investment questions** and must not be conflated.

### Scenario results

- Under the modeled **full-replacement, energy-only** assumptions, all six individual NPVs are **negative**.
- Exact enumeration of **64 binary portfolios** (\(2^6\)) identifies **no replacements** as the NPV-maximizing *optional* portfolio under the ₹8 lakh budget, with portfolio **NPV = ₹0**.
- This does **not** imply that maintenance or replacement is never warranted. Mandatory safety replacements, failure risk, avoided outages, and the incremental cost of purchasing a higher-efficiency unit require separate evaluation.
- The analysis also includes hypothetical **incremental-premium** scenarios; any favorable outcomes are conditional on their specified premium assumptions, not actual procurement quotes.

### Monte Carlo sensitivity

The reproducible scenario runs **5,000 draws per rating** (**30,000 draws total**) using documented triangular uncertainty assumptions for loading, energy value, and capital-cost multipliers, with a fixed random seed. In the saved **full-replacement** simulation, the observed fraction of positive-NPV draws is **0% for each rating**. This is an outcome **within the chosen distributions**, not a measured real-world probability or proof that profitable replacement is impossible. Report the exact distribution parameters and seed from the executable notebook when presenting results.

## Reproduce the analysis in Google Colab

**RQ1–RQ2:**

1. Open [`QM640_Interim_Report_RQ1_RQ2_Final.ipynb`](QM640_Interim_Report_RQ1_RQ2_Final.ipynb) in [Google Colab](https://colab.research.google.com/).
2. Check that the data-loading cell points to the intended [`QM640_Public_DGA_Fault_Dataset.xlsx`](QM640_Public_DGA_Fault_Dataset.xlsx) file. An earlier `IEEE_STANDARD.xlsx` path may appear in exploratory cells; its name does **not** verify IEEE provenance.
3. Run all cells, install missing dependencies as needed, and compare outputs against the RQ1/RQ2 tables above.

**RQ3–RQ4:**

1. Open [`QM640_Interim_Report_RQ3_RQ4_Final.ipynb`](QM640_Interim_Report_RQ3_RQ4_Final.ipynb) in [Google Colab](https://colab.research.google.com/).
2. The notebook reads the input CSV from this repository's raw GitHub URL: [`QM640_RQ34_Distribution_Benchmark_Inputs.csv`](https://raw.githubusercontent.com/irurama2018-coder/M640-Transformer-AI-Capstone/main/QM640_RQ34_Distribution_Benchmark_Inputs.csv).
3. Run all cells. Verify that **six ratings** load, that the annual savings match the RQ3 table, and that **64 portfolios** are evaluated for each applicable budget scenario.
4. Check that the financial assumptions, Monte Carlo settings, and output filenames match the notebook before using generated figures or CSVs in a report.

Saved notebook outputs demonstrate prior execution but do not replace a fresh reproducibility run. GitHub file paths and dependencies must remain accessible.

## Public sources and provenance requiring verification

- **Bureau of Energy Efficiency (BEE):** Distribution-transformer star-labeling schedules and applicable Gazette amendments. [BEE distribution-transformer schedule (public reference)](https://www.beestarlabel.com/Content/Files/Schedule4_DT.pdf). **Confirm the controlling notification, effective period, equipment category, and exact 50%/100% loss table before citing these inputs as official 2026 requirements.**
- **Central Electricity Authority (CEA):** [Failures of power equipment](https://cea.nic.in/failure-type/failures-of-power-equipment/?lang=en) — contextual source for failure reporting, **not** a substitute for asset-specific reliability probabilities.
- **Bureau of Indian Standards (BIS):** Applicable IS 1180 distribution-transformer and IS 2026 power-transformer requirements should be checked against current official standards and amendments.
- **DGA data:** The original dataset creator, measurement units, labeling process, and license remain to be verified. Repository file names are not proof of source endorsement or redistribution rights.

The CSV includes **benchmark-style loss ceilings combined with assumed CAPEX**; it is not an OEM measurement dataset or a utility asset register. Where the original source license does not permit redistribution, replace copied source material with a citation and a reproducible extraction procedure.

## Research limitations and next steps

1. **Validate data provenance and permissions:** Verify DGA and BEE source documents, benchmark periods, units, and reuse rights.
2. **Strengthen RQ1/RQ2 validity:** Investigate duplicate records and detection limits, use training-only tuning, and seek independent transformer-level test data with asset identifiers and timestamps.
3. **Obtain OEM specifications:** Collect rated capacity, separately tested no-load/load losses, reference temperature, replacement alternatives, and quotations under authorized data-sharing terms.
4. **Obtain utility measurements:** Collect anonymized loading profiles, metering, maintenance/failure history, and cost/budget inputs with appropriate approvals.
5. **Separate power-transformer model:** Develop a distinct power-transformer engineering/financial dataset under appropriate specifications; **do not reuse distribution-transformer star-loss tables as power-transformer evidence**.
6. **Integrate cautiously:** Only after data alignment and validation should the four modules be assessed as a combined decision-support framework.

## Responsible use, governance, and academic disclaimer

This repository contains **preliminary academic research** and **illustrative financial simulations**, not a certified transformer-monitoring, electrical-safety, or investment-decision product. Qualified engineers and utility decision-makers must retain oversight of safety-critical judgments. Do not publish confidential OEM/utility records, personally identifiable information, credentials, or unlicensed third-party datasets. Clearly distinguish source values, engineering assumptions, and simulated outputs in any academic presentation.
