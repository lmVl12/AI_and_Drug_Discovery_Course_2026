# Stage 2: Exploratory Data Analysis and Feature Engineering

This sub-project focuses on the statistical validation and molecular encoding of the FLT3 bioactivity dataset prepared in Stage 1. The goal is to transform chemical structures into high-quality, filtered datasets ready for Machine Learning.

## 📋 Task Overview
The workflow is divided into three main phases based on the implemented Python pipeline:

### 1. Exploratory Data Analysis (EDA)
* **Bioactivity Normalization:** IC50 values were converted to **pIC50** to stabilize variance and ensure a uniform scale for modeling.
* **Activity Re-assignment:** Compounds were classified into **Active** (pIC50 ≥ 6) and **Inactive** (pIC50 < 6) based on pharmacological potency.
* **Lipinski Descriptors:** Molecular Weight, LogP, H-Bond Donors, and H-Bond Acceptors were calculated to map the chemical space.
* **Statistical Testing:** The **Mann-Whitney U Test** followed by some visualizations was applied to confirm that all physicochemical properties significantly differentiate between activity classes ($p < 0.05$).

### 2. 2D Molecular Descriptor Calculation
* **Tool:** PaDEL-Descriptor was utilized to generate 1,444 topological indices.
* **Refinement:** A **Variance Threshold** filter was implemented to remove constant and non-informative features.
* **Outcome:** A cleaned set of **1,209 unique 2D descriptors** was integrated with pIC50 labels for supervised learning.

### 3. Molecular Fingerprinting (PubChem)
* **Encoding:** Molecules were converted into **881-bit PubChem binary vectors**, capturing specific structural fragments.
* **Feature Selection:** After removing zero-variance bits, **599 informative bits** were retained to reduce dimensionality and noise.
* **Final Deliverable:** A finalized fingerprint dataset (`QSAR_dataset_fp.csv`) optimized for binary classification and regression tasks.

---

## 🛠️ Reproduction Guide (Technical Setup)

To reproduce the analysis, follow this file sequence:

1. **Phase 1 Input:** Use `bioactivity_preprocessed_data.csv` (output from Stage 1) to run the EDA and Lipinski calculations.
2. **Phase 2 Input:** The resulting `df_lipinski.csv` is then used as the primary input for PaDEL-Descriptor calculations and fingerprint generation.
3. **Installation:** Run the following command to install specialized tools:
   ```bash
   pip install rdkit padelpy
