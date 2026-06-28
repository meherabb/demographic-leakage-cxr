# Embeddings

The frozen embeddings extracted by the five models (BioMedCLIP, CLIP ViT-B/16, CLIP ViT-B/32, DINOv2-S/14, ResNet-50) on both datasets are **not stored in this repository**.

## Why they're excluded

- Total size: ≈390 MB across 10 files (5 models × 2 datasets), which is too large for a clean, fast-to-clone research repository.
- They are fully deterministic given the pinned package versions and seed (`SEED = 42`) used in the notebook — anyone can regenerate them exactly.

## How to regenerate them

1. Open `notebooks/reproducibility_notebook.ipynb` in a Kaggle Notebook with a **T4 GPU** runtime.
2. Attach both datasets via **"+ Add Input"**:
   - `nih-chest-xrays/data`
   - `ashery/chexpert`
3. Run **Cell 1** through **Cell 7** (setup → dataset loading → embedding extraction). This alone takes roughly **15 minutes** on a T4 GPU for all five models on both datasets.
4. Embeddings are saved automatically to `outputs/embeddings/` as compressed NumPy archives (`.npz`), one file per model–dataset pair, e.g.:
   ```
   biomedclip_nih.npz
   resnet-50_chexpert.npz
   ```
   Each contains a single array `Z` of shape `(n_patients, embedding_dim)`.

## Expected output shapes

| Model | Embedding dimension |
|---|---|
| BioMedCLIP | 512 |
| CLIP ViT-B/16 | 512 |
| CLIP ViT-B/32 | 512 |
| DINOv2-S/14 | 384 |
| ResNet-50 | 2048 |

With `N_SAMPLES = 15000` (the default in the notebook), each `Z` array has shape `(15000, embedding_dim)`.

## Hosting a pre-computed copy (optional)

If you'd like to make the pre-computed embeddings available without requiring reviewers to re-run the pipeline, consider uploading `outputs/embeddings/` as a single archive to an anonymous, reviewer-accessible host (e.g., Zenodo's anonymous preview links, or OSF) and linking it here. No such link is currently provided.
