
Tuberculosis (TB) remains one of the leading infectious disease killers worldwide, with over 10 million new cases annually. Automated chest X-ray analysis can support early screening, particularly in high-burden, low-resource settings where specialist radiologists are scarce.

This repository contains the full experimental pipeline for our paper:

**"Implementing Transformer Architectures for Tuberculosis Classification"**

We benchmark three modern vision transformer architectures against each other under identical, reproducible experimental conditions on the large-scale **TBX11K** chest X-ray dataset, with a focus on clinical metrics — particularly sensitivity (minimising missed TB cases) and specificity.

### Key contributions

- Controlled head-to-head comparison of **ViT-B/16**, **Swin-T**, and **DeiT-B** for TB classification
- Class-imbalance-aware training pipeline with **cost-sensitive weighted loss** and **PR-AUC-optimised early stopping**
- **Validation-set threshold optimisation** via F1-maximisation on the precision-recall curve
- Full reproducibility: fixed seed, saved split CSVs, per-model checkpoints and metric JSON files
- Google Colab notebook — **no local GPU required**

---

## Results

All models are evaluated on a held-out test set of **1,260 images** (1,140 Non-TB, 120 TB-positive).

| Model | ROC-AUC | PR-AUC | Sensitivity | Specificity | F1 | Bal. Acc. | MCC |
|---|---|---|---|---|---|---|---|
| ViT-B/16 | 0.994 | 0.954 | 0.908 | 0.992 | 0.916 | 0.950 | 0.910 |
| DeiT-B | 0.999 | 0.992 | 0.917 | **0.997** | 0.944 | 0.957 | 0.942 |
| **Swin-T** | **1.000** | **0.997** | **0.967** | 0.995 | **0.959** | **0.981** | **0.952** |

**Swin-T misses only 4 out of 120 TB-positive cases** (FN rate: 3.33%) — a 64% reduction in missed diagnoses compared to ViT-B/16.

### Confusion matrices

| | Swin-T | DeiT-B | ViT-B/16 |
|---|---|---|---|
| TP | 116 | 110 | 109 |
| FP | 6 | **3** | 9 |
| FN | **4** | 10 | 11 |
| TN | 1134 | 1137 | 1131 |
