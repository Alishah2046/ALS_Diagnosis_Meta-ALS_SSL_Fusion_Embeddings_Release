# ALS SSL Fusion Embeddings (Korean Speech)

This repository contains **utterance-level embedding matrices** extracted from frozen self-supervised speech models for multi-class ALS diagnosis experiments, together with **anonymized metadata** and a **subject-disjoint split (seed 42)**.

It is designed to support the paper contribution:
> We release the extracted multi-layer fusion embeddings across four self-supervised speech models together with the subject-disjoint split information to support reproducible evaluation.

## What is included

### Embeddings (`embeddings/`)
Four SSL backbones:
- `hubert_xlarge/`
- `wav2vec2_large/`
- `data2vec_audio_large/`
- `wavlm_large/`

Each backbone folder contains five fusion settings:
- `X_acoustic.npy`
- `X_stability.npy`
- `X_middle.npy`
- `X_last3.npy`
- `X_multi_depth.npy`

All matrices are shaped `(6926, D)` where 6,926 is the number of utterances; `D` depends on the backbone and fusion (concatenation of pooled layer vectors).

### Metadata (`metadata/`)
- `label_map.json` (class name → integer label)
- `embedding_spec.json` (high-level spec of what’s inside)
- `utterances.csv` (one row per utterance: `utterance_id`, `subject_id`, `label`, `label_name`, `gender`)
- Per-backbone `.npy` arrays:
  - `utterance_ids.npy` (synthetic IDs `U000000...`)
  - `subject_ids.npy` (anonymized IDs `S000...`)
  - `labels.npy` (0/1/2)
  - `gender.npy` (`F`/`M`)

### Split (`splits/seed42/`)
Subject-disjoint split lists:
- `train_subject_ids.txt`
- `test_subject_ids.txt`
- `split_info.json`

## Privacy / data-use note
This repo **does not include raw audio** and **does not include original filenames**.
Only anonymized subject IDs and synthetic utterance IDs are provided.



## GitHub file-size note
The `.npy` matrices in `embeddings/` are **>100 MB** each, so normal git pushes to GitHub will fail unless you:
- use **Git LFS**, or
- upload the `.npy` files as **GitHub Release assets** (recommended), or
- host the arrays on an external archive (Zenodo/OSF/HuggingFace) and link here.

See `PUBLISHING.md`.

## Quick usage (Python)
```python
import numpy as np
X = np.load("embeddings/wav2vec2_large/X_stability.npy")  # (6926, 3072)
```

