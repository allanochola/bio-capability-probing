# Cross-Model Comparison: Generalization of Biological Task Separability

## Executive Summary

This analysis tests whether separability between benign and harmful biological prompts generalizes across different transformer models and architectures.

**Key Finding:** Separability persists across models of different sizes (125M vs. 410M parameters) and architectures, both achieving ROC-AUC = 1.0 on controlled vocabulary prompts (56% overlap).

**Interpretation:** Perfect separability across models suggests signal may be robust to architectural variation, though both models are from the same family (EleutherAI). Generalization across diverse model families (biological vs. general-purpose) would constitute stronger evidence.

## Motivation

Prior phases tested robustness to confounds (vocabulary, paraphrasing, scaffolding) but were limited to a single model (Pythia-410m). 

Critical question: **Is separability an artifact of Pythia-410m's specific architecture, or does it generalize to other models?**

Cross-model testing addresses:
1. **Architectural robustness** — Does signal persist across different transformer designs?
2. **Scale generalization** — Does signal scale with model size?
3. **True transferability** — Can probes trained on one model transfer to another?

## Methodology

### Models Tested

1. **Pythia-410m** (baseline)
   - Parameters: 410M
   - Layers: 25
   - Hidden size: 1024
   - Architecture: GPT-NeoX (decoder-only transformer)

2. **GPT-Neo-125m** (smaller, different architecture)
   - Parameters: 125M
   - Layers: 12
   - Hidden size: 768
   - Architecture: GPT-Neo (decoder-only transformer)

### Evaluation Protocol

- **Prompts:** Controlled vocabulary (56% overlap) for fair comparison
- **Methodology:** Independent logistic regression probes per layer
- **Data:** N=10 (5 benign + 5 harmful)
- **Metric:** ROC-AUC across all layers

## Results

Layer  0 | ROC-AUC: 1.0000
Layer  5 | ROC-AUC: 1.0000
Layer 10 | ROC-AUC: 1.0000
Layer 15 | ROC-AUC: 1.0000
Layer 20 | ROC-AUC: 1.0000
Layer 24 | ROC-AUC: 1.0000
Mean ROC-AUC: 1.0000

**GPT-Neo-125m (125M parameters, 13 layers):**

Layer  0 | ROC-AUC: 1.0000
Layer  2 | ROC-AUC: 1.0000
Layer  4 | ROC-AUC: 1.0000
Layer  6 | ROC-AUC: 1.0000
Layer  8 | ROC-AUC: 1.0000
Layer 10 | ROC-AUC: 1.0000
Layer 12 | ROC-AUC: 1.0000
Mean ROC-AUC: 1.0000

### Summary

| Model | Parameters | Layers | Mean ROC-AUC | Range |
|---|---|---|---|---|
| Pythia-410m | 410M | 25 | 1.0000 | 1.0-1.0 |
| GPT-Neo-125m | 125M | 12 | 1.0000 | 1.0-1.0 |

**Key Observation:** Perfect separability persists across both models and all layers.

## Interpretation

### Evidence for Generalization

✅ **Separability is not model-specific** — Signal persists across different EleutherAI models
✅ **Scale-invariant** — Both 125M and 410M parameter models show identical separability
✅ **Architectural consistency** — Different layer counts, hidden sizes still show perfect ROC-AUC
✅ **Layer-level robustness** — Every tested layer achieves perfect separability

### Evidence Against Strong Generalization Claims

❌ **Same model family** — Both models are EleutherAI (GPT-Neo and GPT-NeoX)
❌ **Not tested on biological models** — No Evo 2, ESM, or ProteinMPNN comparison
❌ **Sample size still trivial** — N=10 in 768-1024 dimensional space
❌ **No transfer evaluation** — Didn't test if probes trained on Pythia transfer to GPT-Neo

## What This Tells Us

### Positive Signal

The consistency across two different models suggests:
- Signal is not an artifact of Pythia-410m's specific weights or architecture
- Semantic task distinction may encode in a representation-level way that generalizes
- Perfect separability across layers suggests signal is distributed throughout representations

### Limitations

- Both models are from the same EleutherAI family
- No biological foundation models tested (Evo, ESM, etc.)
- Perfect metrics across all conditions still point to overfitting as primary explanation
- N=10 remains statistically trivial in both dimensionalities

## What Would Strengthen This Claim

To claim robust cross-model generalization, we would need:

1. **Biological models** — Test on Evo 2, ProteinMPNN, ESM-family models
2. **Different model families** — Compare EleutherAI vs. Meta vs. other architectures
3. **Transfer evaluation** — Train probes on Pythia, evaluate on GPT-Neo (and vice versa)
4. **Larger sample size** — N ≥ 100+ to validate signal vs. overfitting
5. **Mechanistic alignment** — Identify which features/circuits drive separability in each model

## Conclusion

Separability across two different models suggests the signal is not model-specific, strengthening the hypothesis that semantic task distinction encodes robustly in transformer representations.

However, both models are from the same architectural family. True generalization would require validation on diverse model families (particularly biological foundation models) and larger datasets.

## Next Steps

1. **Test on biological models** (Evo 2, ESM-family)
2. **Implement transfer evaluation** (cross-model probe application)
3. **Expand to larger dataset** with proper cross-validation
4. **Mechanistic investigation** via sparse autoencoders or circuit analysis
### Layer-wise Separability

**Pythia-410m (410M parameters, 25 layers):**
