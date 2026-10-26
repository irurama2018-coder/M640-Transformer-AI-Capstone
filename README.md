# QM640 Transformer AI Capstone

**Project:** Developing an AI-Based Decision-Support Framework for Transformer Predictive Maintenance and CAPEX Prioritization in Indian Power Utilities  
**Student:** Rama Devi Balakrishnan · **Group:** 3  
**Institution:** Walsh College · **Course:** QM640 Data Analytics Capstone  
**Interim report date:** October 23, 2026 · **Documentation updated:** October 26, 2026

## Project status and scope

This repository supports a **preliminary, modular capstone proof of concept**, not a deployed or field-validated transformer management system. Four research questions are examined using two different evidence bases:

- **RQ1–RQ2:** A publicly shared dissolved-gas-analysis (DGA) fault-label workbook, with original publisher, measurement units, labeling process, sample independence, and redistribution permission **not yet verified**.
- **RQ3–RQ4:** Six illustrative **distribution-transformer** rating alternatives, benchmark-based loss values, and **assumed** operating and financial inputs. These are **not** OEM factory-test measurements or utility procurement quotations.

**There is no verified asset-level join between the DGA and energy-loss/CAPEX datasets.** The analyses must not be represented as an integrated, field-validated asset recommendation system.

## Research questions and interim findings

| Module | Question / method | Preliminary finding | Interpretation |
|---|---|---|---|
| **RQ1** | Six-class transformer fault classification using five DGA gases; compare supervised classifiers | Deduplicated sensitivity analysis: **587 records**, Random Forest holdout **76.27% accuracy**, **72.12% balanced accuracy**, **72.62% macro-F1**; five-fold training-only CV approximately **76.12% ± 1.60%** | Internal evaluation only; class-level recall is uneven, and equipment-grouped validation is unavailable |
| **RQ2** | Model explanation with permutation importance and SHAP | **C₂H₂ and C₂H₄** ranked highly in the examined explanation analyses | Model-specific predictive association, **not engineering causation** |
| **RQ3** | Benchmark-based transformer loss reduction at assumed 60% loading and 8,760 h/year | Modeled savings range approximately **237.92–1,282.35 kWh/year** across six ratings | Illustrative distribution-transformer scenarios; **not metered energy savings** |
| **RQ4** | 15-year NPV, budget-constrained CAPEX selection, Monte Carlo sensitivity | Under the **energy-only full-replacement** assumptions, the optimum is **no investment** under the ₹800,000 budget | Scenario-specific; not a conclusion that replacements or upgrades are never justified |
| **Supplementary RQ4** | Traditional maintenance versus AI-assisted condition-based maintenance, sensitivity scenarios, and optional monitoring portfolio | Saved modeled scenarios report **negative incremental NPVs** under the stated assumptions | Hypothetical maintenance and monitoring costs/benefits; mandatory maintenance is not eliminated |

The earlier **589-row** RQ1 analysis is retained for transparency: its reported holdout accuracy was **77.12%**, balanced accuracy **73.42%**, and macro-F1 **74.05%**. These figures come from a different split/analysis and should **not** be substituted for the 587-record deduplicated results or described as a controlled estimate of the effect of deduplication.

### RQ3 base-case modeled energy savings

| Rating (kVA) | Annual modeled savings (kWh) | Annual value at ₹7/kWh (approx.) |
|---:|---:|---:|
| 16 | 237.92 | ₹1,665 |
| 25 | 343.74 | ₹2,406 |
| 63 | 593.23 | ₹4,153 |
| 100 | 862.57 | ₹6,038 |
| 160 | 1,066.85 | ₹7,468 |
| 200 | 1,282.35 | ₹8,976 |

The base financial case uses **₹7/kWh**, **8% discount rate**, **15 years**, and an **₹800,000** investment budget. Full replacement CAPEX is hypothetical. Separate incremental efficiency-premium cases must not be conflated with full-replacement economics. The loss benchmark's official edition, applicability, and effective period remain to be verified.

## Repository files

The following names are visible in the repository listing or documented in the interim report. **Check exact names, current paths, and notebook output status before submission.**

| File | Role |
|---|---|
| `QM640_Public_DGA_Fault_Dataset.xlsx` | Publicly shared DGA workbook; **original provenance and reuse terms unverified** |
| `QM640_RQ1_RQ2_Interim_Report.ipynb` | RQ1/RQ2 notebook in repository listing; verify that saved outputs match the final report |
| `QM640_RQ34_Distribution_Benchmark_Inputs.csv` | Six-rating benchmark and assumed CAPEX input table |
| `QM640_RQ3_RQ4_Interim_Report_.ipynb` | RQ3/RQ4 notebook in repository listing; verify exact filename and saved outputs |
| `QM640_RQ3_RQ4_Expanded_Analysis.xlsx` | Supporting scenario calculations |
| `QM640_RQ3_RQ4_Public_Data_Starter.xlsx` | Supporting input workbook |
| `QM640_RQ4_Maintenance_Cost_Data.xlsx` | Maintenance-cost scenario inputs |
| `QM640_RQ4_Maintenance_Cost_Scenario_Inter...` | Supplementary RQ4 notebook; **filename truncated in screenshot—verify actual name** |
| `QM640_RQ4_Reproducible_Monte_Carlo_Draw...` | Monte Carlo supporting output; **verify actual name** |
| `illustrative_maintenance_cost_comparison.csv` | Maintenance scenario output |
| `illustrative_sensitivity.csv` | Sensitivity scenario output |
| `README.md` | Repository documentation |

**Analysis record:** The interim report cites executed notebook copies named `QM640_RQ1_RQ2_Corrected_For_Colab (1).ipynb` and `QM640_RQ3_RQ4_Updated_For_Colab (1).ipynb`. The GitHub notebook names shown above differ. Confirm their content and saved results before claiming the repository reproduces the report exactly.

## Reproducibility procedure

1. Clone or download the repository and record the commit hash.
2. Verify the required input files exist, inspect their columns, and record file hashes.
3. Open the RQ1/RQ2 notebook in Google Colab or Jupyter. Run all cells, preserving its declared split, seed, preprocessing, model comparisons, evaluation metrics, and SHAP/permutation analysis.
4. Open the RQ3/RQ4 notebook. Check its input CSV path (including any GitHub raw URL), then run all cells. Confirm six ratings, the engineering arithmetic checks, NPV checks, 64 possible binary portfolios, and Monte Carlo outputs.
5. Open the supplementary maintenance-cost notebook. Check its workbook/CSV dependencies and rerun all scenarios.
6. Compare **freshly executed** results with the final interim report. Record Python/package versions, commit hash, input hashes, and any deviations. Do not overwrite original input data with generated outputs.

**Caution:** Notebook execution and saved outputs demonstrate computational reproducibility only. They do not authenticate the original data source, establish redistribution rights, or validate field performance. A clean-checkout reproduction has not been independently certified here.

## Data provenance and permissions register

| Data/source | Publisher and original title | Units / scope / period | Redistribution permission | Current status |
|---|---|---|---|---|
| Public DGA workbook | **Original publisher and source document not confirmed**; repository copy is not proof of authorship | Five gas variables and six fault labels; gas units, sampling period, transformer identity and labeling procedure require confirmation | **Not verified** | Use with explicit provenance caveat; request source confirmation |
| Distribution-transformer benchmark loss table | Official BEE/Indian notification, amendment, effective dates, and applicable transformer classes **to be verified** | Loss ceilings recorded in watts at 50% and 100% loading for six kVA ratings; not factory-tested individual asset losses | Verify original source/reuse terms | Illustrative engineering input pending authoritative source audit |
| Full replacement and maintenance costs | Researcher-defined illustrative scenarios, not an OEM or utility price schedule | INR, with stated scenario parameters | Project-generated assumptions | Not validated against quotations |

**Do not add an open-source license or assert third-party data redistribution permission unless the rights are established.** Source verification should record publisher, original title, edition/amendment, effective dates, equipment applicability, unit definitions, access date, and license or permission evidence. Where appropriate, replace copied third-party data with a documented retrieval procedure if redistribution is not authorized.

## Engineering, governance, and safety limitations

- Distribution-transformer benchmark calculations must **not** be applied automatically to power transformers.
- RQ1 does not have verified asset identifiers or timestamps for equipment-grouped or time-aware validation; repeated measurements across splits cannot be ruled out.
- RQ2 SHAP and permutation rankings depend on the fitted model, evaluation subset, and correlated gases; they are not causal evidence.
- RQ3 assumes constant loading and inferred loss components; actual losses require time-resolved load profiles and measured or guaranteed OEM test losses, including relevant temperature/test conditions.
- RQ4 excludes some potential lifecycle benefits (e.g., avoided outages, failure risk, reliability, residual value) from its energy-only base case. Negative scenario NPVs do not establish negative NPVs for every real investment.
- The supplementary RQ4 maintenance model uses assumed maintenance and monitoring costs and hypothetical risk reductions; mandatory inspection, engineering oversight, and safety requirements remain in force.
- This work is for **human-reviewed decision support**, not autonomous transformer operation or procurement approval.

## Next steps for final research

1. Audit original DGA and official benchmark sources, including units, applicability, licensing, and README/data-dictionary documentation.
2. Seek anonymized utility and OEM measurements: stable transformer ID, capacity, timestamps, load profiles, fault/maintenance history, tested losses, test temperature, tariff, procurement cost, and replacement requirements.
3. Repeat RQ1 with asset-grouped/time-aware validation, training-only model selection, class-sensitive costs, and uncertainty intervals; repeat RQ2 explanation-stability checks.
4. Recalculate RQ3 from measured or guaranteed losses and time-varying loads; update RQ4 using incremental CAPEX, verified lifecycle benefits, correlated uncertainty, and criticality/budget constraints.
5. Integrate modules only if a validated asset-level key connects diagnostic, engineering, and financial records. Reproduce from a clean checkout and seek mentor review.

## Report and citation

**Primary academic document:** *Developing an AI-Based Decision-Support Framework for Transformer Predictive Maintenance and CAPEX Prioritization in Indian Power Utilities: Interim Report*, Rama Devi Balakrishnan, Group 3, Walsh College, QM640, October 23, 2026 (55 pages).

**Repository:** https://github.com/irurama2018-coder/M640-Transformer-AI-Capstone

When citing external DGA records or transformer-loss standards, cite their **verified original sources**, not merely this repository. This repository and README do not certify ownership of third-party datasets.
