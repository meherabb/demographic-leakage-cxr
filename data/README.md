# Data

This repository does not redistribute any raw medical images. Both datasets are publicly accessible via Kaggle and should be obtained directly from their original sources, respecting each dataset's license and data-use terms.

## NIH ChestX-ray14

- **Source institution:** NIH Clinical Center
- **Kaggle mirror:** [`nih-chest-xrays/data`](https://www.kaggle.com/datasets/nih-chest-xrays/data)
- **Original release:** Wang et al., *ChestX-ray8: Hospital-scale Chest X-ray Database and Benchmarks*, CVPR 2017.
- **Scale:** 112,120 frontal radiographs from 30,802 unique patients (after deduplication by Patient ID).
- **Labels used:** Patient Age, Patient Gender, Finding Labels (binarized to any-pathology-present vs. no-finding).
- **Disease prevalence (full dataset):** 31.5% (any finding).
- **Sampling used in this work:** 15,000 patients, stratified-subsampled to balance disease prevalence, deduplicated to one image per patient (youngest available scan kept on tie).

## CheXpert-v1.0-small

- **Source institution:** Stanford Hospital
- **Kaggle mirror:** [`ashery/chexpert`](https://www.kaggle.com/datasets/ashery/chexpert) — a third-party Kaggle mirror of the original CheXpert release, which normally requires a Stanford AIMI data-use agreement.
- **Original release:** Irvin et al., *CheXpert: A Large Chest Radiograph Dataset with Uncertainty Labels and Expert Comparison*, AAAI 2019.
- **Scale:** 191,023 frontal+lateral radiographs from 64,530 unique patients; this work uses **frontal views only**, deduplicated by patient ID.
- **Labels used:** Sex, Age, No Finding (binarized to any-pathology-present vs. no-finding), Frontal/Lateral (filtered to Frontal only).
- **Disease prevalence (full dataset):** 84.5% (any finding) — substantially higher than NIH, which is part of why this dataset serves as a genuinely independent replication target (different hospital, different scanner fleet, different labeling pipeline, no patient overlap with NIH).
- **Sampling used in this work:** 15,000 patients, stratified-subsampled to balance disease prevalence.

## Why two datasets

NIH and CheXpert differ in hospital system, scanner fleet, disease prevalence, and labeling pipeline. Findings that replicate across both (see `results/tables/main/` and `results/figures/fig7_crossdataset_replication.*`) are substantially less likely to be artifacts of a single institution's imaging protocol or labeling conventions.

## Reproducing the exact sample

The notebook (`notebooks/reproducibility_notebook.ipynb`) performs all loading, filtering, deduplication, age-median-split binarization, and stratified subsampling deterministically under `SEED = 42`. Re-running Cells 1–5 against the same Kaggle dataset versions will reproduce the exact same 15,000-patient sample for each dataset.
