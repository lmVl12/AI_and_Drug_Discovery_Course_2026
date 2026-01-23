# Assignment 2: QSAR Data Curation and Preprocessing for FLT3

### Bioactivity Data Retrieval and Curation for QSAR Modeling.

### **Selected Target**
* **Target Name:** Receptor-type tyrosine-protein kinase FLT3 (FMS-like tyrosine kinase 3)
* **ChEMBL ID:** [CHEMBL1974](https://www.ebi.ac.uk/chembl/target_report_card/CHEMBL1974/)
* **UniProt ID:** P36888
* **Organism:** *Homo sapiens*

### **Dataset Statistics**
* **Initial records collected:** 7096 records 
* **Final preprocessed records:** 4647 records 

### **Data Curation Workflow**
The following diagram and description outline the step-by-step process used to curate the dataset:

```mermaid
flowchart TD
    subgraph Stage1 [Data Retrieval]
    A[Mount Google Drive] --> B[Install ChEMBL Web Service]
    B --> C[Search Target: FLT3]
    C --> D[Retrieve IC50 bioactivity data]
    D --> E[Save: bioactivity_raw_data.csv]
    end

    subgraph Stage2 [Preprocessing]
    E --> F[Handle IC50 values & Unit filtering]
    F --> G[Deduplication by molecule ID]
    G --> H[Assign bioactivity classes]
    H --> I[SMILES validation & structural deduplication]
    I --> J[Save: bioactivity_preprocessed_data.csv]
    J --> K[Analyze class balance]
    end
```
#### **Data Curation Workflow Description**
The data curation process was executed in two primary stages:

#### I. Data Retrieval:
After establishing a connection between Google Colab and Google Drive, the ChEMBL web service client was utilized to identify the FLT3 target (CHEMBL1974). Bioactivity records specifically reported as IC50 values in nanomolar (nM) units were retrieved.
#### II. Data Preprocessing:
* Data Cleaning: Records with missing or null IC50 values were identified and removed. A units check was performed to ensure only nanomolar (nM) values remained to maintain dataset quality.

* Activity Classification: Compounds were categorized into three distinct classes—Active (IC50 ≤ 1000 nM), Inactive (IC50 ≥ 10000 nM), and Intermediate—to provide a structured basis for QSAR modeling.

* Structural Validation & Deduplication: A rigorous check of chemical structures was performed using RDKit for salt removal and canonization. This step allowed for the identification and collapsing of 57 hidden chemical duplicates where different ChEMBL IDs shared identical structures.

* Class Balance Analysis: The final distribution was analyzed, revealing a 3-part ratio of 4.01 : 1.34 : 1.00 (Active : Inactive : Intermediate), indicating an "Active-heavy" dataset.

* File Management: The raw data and the final preprocessed dataset were exported as CSV files to the designated /data folder on Google Drive.
