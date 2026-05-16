

# Bio Capability Probing

Exploratory experiments investigating whether probing methodologies inspired by deception-detection research transfer into biologically sensitive task domains.

---

# Project Overview

This repository contains two exploratory research components:

## 1. Apollo Behavioral Baseline

A lightweight reconstruction of a behavioral deception-classification pipeline using rollout annotations from the Apollo Research deception-detection repository.

The baseline experiment:
- reconstructs deception labels,
- trains a logistic regression classifier,
- evaluates separability,
- and analyzes linguistic correlates associated with deceptive outputs.

## 2. Biological Activation Probing

An exploratory activation-space probing experiment evaluating whether hidden-state representations contain partially separable signal associated with constrained biological task categories.

The experiment uses:
- lightweight open language models,
- hidden-state extraction,
- linear probing,
- and PCA visualization.

---
# Repository Structure

```text
bio-capability-probing/
│
├── notebooks/
├── datasets/
├── figures/
├── results/
└── writeups/


## Figures

### PCA Projection

![PCA Projection](figures/pca_projection.png)

## Figures

### PCA Projection

![PCA Projection](figures/confusion_matrix.png)

## Figures

### PCA Projection

![PCA Projection](figures/roc_curve.png)


