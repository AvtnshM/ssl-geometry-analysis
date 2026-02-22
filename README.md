# ssl-geometry-analysis
Empirical geometric study of representation smoothness in SSL.


# SSL Geometry Analysis: BYOL vs SimCLR

## Overview

This project investigates a mechanistic question in Self-Supervised Learning (SSL):

> Do non-contrastive methods (BYOL) produce smoother encoders than contrastive methods (SimCLR)?

We test this by measuring the input Jacobian norm of trained encoders and relating it to augmentation robustness.


## Research Hypothesis

1. BYOL produces encoders with lower input Jacobian norms than SimCLR under matched training conditions.
2. Lower Jacobian norm correlates with stronger augmentation invariance and robustness.
3. Smoothness may explain why non-contrastive SSL works without negative samples.

---

## Methods Compared

- BYOL (non-contrastive)
- SimCLR (contrastive)

Both trained with:

- Same encoder (ResNet-18)
- Same augmentations
- Same optimizer
- Same batch size
- Same number of epochs

---

## Metrics

- Input Jacobian Frobenius norm (Hutchinson estimator)
- Augmentation sensitivity
- Gaussian noise stability
- Linear probe accuracy

---

## Core Idea

The Jacobian measures how sensitive the representation is to small input perturbations.

If:

BYOL → lower Jacobian norm  
SimCLR → higher Jacobian norm  

Then representation smoothness may explain augmentation robustness.

## Status

Experimental prototype.  
Results require validation across multiple random seeds.
