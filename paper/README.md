# Paper

**What Your CXR Reveals Beyond the Pathology: Causal Evidence for Demographic Leakage in Medical Foundation Model Embeddings and Its Calibration Fairness Consequences**

Submitted to the **ECCV 2026 Workshop on Medical Foundation Models and Benchmarks (MEDFMB)**.
Currently under anonymous review — author names and affiliations are withheld from this repository in accordance with double-blind review policy.

## Abstract

Foundation models are increasingly deployed in medical imaging pipelines where clinical predictions must be fair across patient demographic groups. We investigate whether frozen chest X-ray embeddings from five pretrained models — spanning four distinct pretraining paradigms — encode patient sex and age to a degree that translates into measurable downstream calibration unfairness. Using 15,000 patients from NIH ChestX-ray14 and 15,000 patients from CheXpert (Stanford Hospital), we establish three interconnected findings. First, all five models leak sex and age information significantly above chance, with 30 of 30 statistical tests surviving Benjamini–Hochberg false-discovery-rate correction across both datasets. Second, pretraining objective — not domain — governs the leakage magnitude: contrastive text-supervised models (BioMedCLIP, CLIP) leak substantially less than self-supervised (DINOv2-S/14) and fully-supervised (ResNet-50) models on identical images, regardless of whether the model was trained on medical or natural-image data. Third, and most critically, removing the age-decoding direction from each model's embedding space via iterative nullspace projection reduces the post-hoc age-axis calibration gap by 88–98% across all five models with the ablation sanity check passing in every case — converting what would otherwise be a purely correlational observation into an interventional one. These patterns replicate on both datasets and are stable across leave-one-out jackknife resampling and ten-seed stability checks. Our results suggest that the choice of pretraining loss function is a first-order lever for demographic leakage control, with direct implications for the safety evaluation of medical vision-language models.

## Contributions

1. A controlled, training-free audit of five foundation models spanning four pretraining paradigms on two independent CXR datasets, showing that pretraining objective explains the leakage ordering better than domain.
2. The first interventional evidence, via iterative nullspace projection (INLP) ablation, that the age-encoding direction in foundation model embedding spaces is a direct structural cause of the age-calibration gap, not merely a correlate.
3. A complete robustness suite — leave-one-out jackknife, multi-seed prevalence-matching stability, and age-quartile dose-response analysis — confirming the findings are not artefacts of threshold choices or specific model selections.

## Citation

This work is currently under anonymous review. A complete BibTeX citation will be added to this file upon de-anonymization or acceptance.
