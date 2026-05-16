

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

## Quick Start

To reproduce the Apollo behavioral baseline:

```bash
pip install -r requirements.txt
jupyter notebook notebooks/01_apollo_baseline.ipynb
```

To explore activation-space probing on biological tasks:

```bash
pip install -r requirements.txt
jupyter notebook notebooks/02_biological_probing.ipynb
```

## Key Results

### Apollo Behavioral Baseline
- **Accuracy:** 0.67
- **Precision:** 0.74
- **Recall:** 0.83
- **ROC-AUC:** 0.64

**Interpretation:** Modest above-chance separability between deceptive and non-deceptive outputs. Classifier likely captures linguistic/social framing patterns rather than mechanistic deception representations.

**Top deceptive features:** just, really, sure, family, know, recently

**Top non-deceptive features:** honestly, discuss, focus, activities, track, foundation

### Biological Activation Probing
Exploratory hidden-state probing experiments suggest partial representational separability under constrained conditions.

**Important:** Results are highly preliminary and do not establish operational biological monitoring capability.

## Figures

### Confusion Matrix
![Confusion Matrix](figures/confusion_matrix.png)

### ROC Curve
![ROC Curve](figures/roc_curve.png)

## Data & Reproducibility

- **Apollo baseline dataset:** Reconstructed from [Apollo Research deception-detection repository](https://github.com/ApolloResearch/deception-detection/)
- **Biological prompts:** Manually constructed exploratory examples
- **Metrics:** See `results/baseline_metrics.json`
- **Dependencies:** See `requirements.txt`

## Important Limitations

This work does **NOT** establish:
- Robust deception detection
- Biological threat assessment
- Operational monitoring capability

The experiments are intentionally exploratory and susceptible to:
- Dataset imbalance
- Lexical confounds
- Topical separability
- Prompt artifacts
- Tiny sample sizes

## Future Directions

Potential extensions include:
- Larger biological prompt datasets
- Intermediate-layer probing
- Adversarial robustness evaluation
- Hidden-state transfer analysis
- Sparse autoencoder analysis
- Cross-model comparison

## Citation

```bibtex
@software{ochola2026biocapabilityprobing,
  author = {Ochola, Allan},
  title = {Bio Capability Probing: Exploratory Activation-Space Monitoring for Biological Task Domains},
  year = {2026},
  url = {https://github.com/allanochola/bio-capability-probing}
}
```

## License

MIT License - See LICENSE file for details

---

**Status:** Exploratory research artifact | **Last updated:** May 2026
