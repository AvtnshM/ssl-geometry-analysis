# Jacobian-Regularized Contrastive Learning  
Controlling Representation Smoothness in Self-Supervised Learning

---

## Overview

This project studies a fundamental question in self-supervised learning (SSL):

> How do training objectives shape the sensitivity of learned representations, and can this be explicitly controlled?

We analyze the **input–representation Jacobian** as a measure of sensitivity and relate it to:
- robustness to perturbations  
- noise sensitivity  
- downstream linear probe performance  

In addition to comparing **SimCLR** (contrastive) and **BYOL** (non-contrastive), we study:

> **SimCLR+Jac** — a Jacobian-regularized variant of SimCLR that penalizes input sensitivity.

---

## Key Findings

### Geometry–Performance Trade-off
- **SimCLR** learns higher-sensitivity representations with stronger linear separability  
- **BYOL** learns smoother representations with reduced sensitivity  
- This reveals a consistent **smoothness vs discrimination trade-off**

---

### Controlling Representation Smoothness
- Jacobian regularization reduces sensitivity significantly  
- SimCLR+Jac moves toward BYOL-like smoothness  
- Maintains competitive accuracy with only minor loss on CIFAR-10  

---

### Stability Across Seeds
- SimCLR+Jac shows lower variance in accuracy across seeds  
- Indicates more consistent performance under different random initializations  

---

### STL-10 (In-Distribution Results)

| Method        | Accuracy |
|--------------|----------|
| BYOL         | 0.457    |
| SimCLR       | 0.560    |
| SimCLR+Jac   | 0.567    |

- SimCLR+Jac matches or slightly improves performance  
- No degradation from regularization  

Additionally, lower training time was observed in our runs (~21 vs ~43 minutes), though this is **implementation-dependent** and not claimed as an inherent property.

---

### Transfer and Generalization
- No degradation in transfer performance  
- Comparable results at 100-epoch probe  
- Slight improvement in low-data (20-epoch) regime  
- CIFAR-100 shows **positive effect size** for SimCLR+Jac  

---

### Temperature Effects
- Lower temperature → higher sensitivity  
- Results are consistent with temperature acting as an implicit regularizer  

---

### Architecture (ViT)
- SimCLR and SimCLR+Jac achieve similar performance  
- Jacobian regularization does **not consistently reduce sensitivity** in transformers  
- Suggests architecture-dependent behavior  

---

## Methods

We compare:

- **SimCLR** (contrastive learning)  
- **BYOL** (non-contrastive learning)  
- **SimCLR+Jac** (Jacobian-regularized contrastive learning)  

Controlled setup:
- Same backbone (ResNet-18 / ViT)  
- Same augmentations  
- Same optimizer (Adam, lr = 3e-4)  
- Same training schedule  

Jacobian regularization uses:
λ = 0.01


---

## Metrics

- Jacobian Frobenius norm (Hutchinson estimator)  
- Augmentation sensitivity  
- Noise sensitivity  
- Linear probe accuracy  

---

## Repository Structure
ssl-geometry-analysis/
├── README.md
├── LICENSE
│
├── data/
│ └── ssl_master_dataset.csv
│
├── analysis/
│ └── ssl-paper-analyses-plots-tables.ipynb
│
├── figures/
│ ├── fig1_core_accuracy.pdf
│ ├── fig2_geometry.pdf
│ ├── fig3_tau_jacobian.pdf
│ ├── fig4_tau_noise.pdf
│ ├── fig5_transfer100.pdf
│ └── fig7_cifar100.pdf
│
├── notebooks/
│ ├── cifar10/
│ ├── stl10/
│ └── cifar100/
│
└── paper/
└── ssl_geometry_analysis.pdf



---

## Reproducibility

### Training
Training notebooks are provided in `/notebooks/`  
GPU runs were conducted on Kaggle.

---

### Analysis
All results, statistics, and plots are generated via:
analysis/ssl-paper-analyses-plots-tables.ipynb


This notebook:
- Computes all metrics  
- Runs statistical tests  
- Produces LaTeX-ready tables  
- Generates all figures  

---

## Requirements
python >= 3.9
numpy
pandas
matplotlib
scipy
torch
torchvision
tqdm

## Contributions

- Empirical comparison of input Jacobian norms across SSL methods  
- Introduction of Jacobian-regularized SimCLR  
- Identification of a geometry–performance trade-off  
- Demonstration that representation smoothness is controllable  

---

## Limitations

- Experiments limited to small-scale datasets (CIFAR, STL)  
- Jacobian norm is a global metric (does not capture directional structure)  
- Hutchinson estimator introduces sampling noise  
- No causal claims — results are empirical  

---

## License

Apache 2.0 License  

---

## Citation

```bibtex
@article{malaviya2026sslgeometry,
  title={Jacobian-Regularized Contrastive Learning: Controlling Representation Smoothness in Self-Supervised Learning},
  author={Malaviya, Avatansh},
  year={2026}
}

