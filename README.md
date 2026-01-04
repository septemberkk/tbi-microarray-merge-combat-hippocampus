# tbi-microarray-merge-combat-hippocampus

# Integrated rat TBI hippocampus microarray analysis (ComBat + limma)

## Datasets
All datasets are **Expression profiling by array (microarray)**.

- **GSE59645** — Whole hippocampus, 24h post-injury; includes naïve, sham, TBI, and several drug-treated TBI groups (JM6 / PMI-006 / E33). In this repo, only the **control (sham)** and **injury (TBI)** groups are used for the integrated TBI contrast. 
  - Platform: **GPL14746** (Agilent-028282 Whole Rat Genome Microarray 4x44K v3) 

- **GSE115614** — Whole hippocampus, 24h post-injury; contains sham, TBI, and TBI + antidepressant drug arms. This repo uses only **sham** and **TBI (untreated)** samples from the **mRNA** microarray platform (miRNA arm is not used here). 
  - Platforms: **GPL15084** (rat gene expression) and **GPL22696** (rat miRNA). Only **GPL15084** is used here.

## Analysis overview
### 1) Data preparation (gene-level)
- Download series matrix
- Map probes to gene symbols using platform annotation
- Collapse multiple probes per gene

### 2) Merge + batch correction
- Merge gene-level matrices by gene symbol 
- Batch correction: `sva::ComBat`
  - keep the main biological variable: **TBI vs Sham**

### 3) Differential expression (limma)
- Model: limma linear model + `eBayes`
- Threshold:
  - `adjustP < 0.05`
  - `|logFC| > 1` (FC > 2)

### 4) Plots
- Volcano plot
- Heatmap of top DEGs 

### 5) Enrichment
- GO enrichment
- KEGG pathway enrichment  

- logFoldChange cutoff: **1**
- adjusted P-value cutoff: **0.05**
- batch correction: **ComBat (sva)**
