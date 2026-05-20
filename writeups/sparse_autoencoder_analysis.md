
# Sparse Autoencoder Analysis: Identifying Interpretable Features

## Executive Summary

This analysis investigates which latent features in transformer hidden states drive separability between benign and harmful biological tasks.

**Key Finding:** Perfect separability (ROC-AUC = 1.0) is achievable with just **5 features**, suggesting task distinction encodes sparsely in representation space.

**Interpretation:** Task-relevant information may be concentrated in a small subset of interpretable dimensions rather than distributed across the full 1024-D hidden state. This is promising for mechanistic interpretability but concerning for the overfitting hypothesis — 5 features in 10 samples is even more trivial than 1024 features.

## Motivation

Prior analyses showed:
- Separability persists across confounds (vocabulary, paraphrasing, scaffolding)
- Separability generalizes across models
- All 1024 dimensions achieve perfect ROC-AUC = 1.0

**Question:** Which dimensions actually matter? Can we identify a sparse set of interpretable features?

This addresses two competing hypotheses:
1. **Genuine semantic signal** — Task distinction encodes sparsely and interpretably
2. **Statistical overfitting** — Perfect metrics on N=10 are trivial regardless of feature count

## Methodology

### Feature Extraction

- **Model:** Pythia-410m
- **Layer:** Layer 12 (middle of network, good balance of abstraction)
- **Hidden state dimensionality:** 1024
- **Data:** Controlled vocabulary prompts (N=5 benign + N=5 harmful)

### Feature Importance Ranking

For each of the 1024 features:
1. Compute mean activation for benign prompts
2. Compute mean activation for harmful prompts
3. Rank by absolute difference

### Sparsity Testing

Train logistic regression probes on:
- Top 1, 2, 3, 5, 10, 20, 50, 100 features
- All 1024 features (baseline)

Metric: ROC-AUC on training data

## Results

### Top 10 Most Discriminative Features (Layer 12)

| Rank | Feature | Difference | Benign Mean | Harmful Mean | Direction |
|---|---|---|---|---|---|
| 1 | 325 | 1.6865 | -0.8438 | 0.8428 | ↑ Harmful |
| 2 | 907 | 1.6094 | 0.8047 | -0.8047 | ↑ Benign |
| 3 | 867 | 1.6055 | -0.8037 | 0.8013 | ↑ Harmful |
| 4 | 68 | 1.5605 | 0.7803 | -0.7803 | ↑ Benign |
| 5 | 262 | 1.4629 | 0.7344 | -0.7290 | ↑ Benign |
| 6 | 762 | 1.4609 | 0.7310 | -0.7300 | ↑ Benign |
| 7 | 112 | 1.4160 | -0.7085 | 0.7080 | ↑ Harmful |
| 8 | 507 | 1.3926 | -0.6968 | 0.6963 | ↑ Harmful |
| 9 | 531 | 1.3662 | -0.6836 | 0.6826 | ↑ Harmful |
| 10 | 318 | 1.3125 | 0.6558 | -0.6567 | ↑ Benign |

### Feature Patterns

**Features with higher activation in benign prompts:**
- 907, 68, 262, 762, 318
- These may encode "legitimate research" semantics

**Features with higher activation in harmful prompts:**
- 325, 867, 112, 507, 531
- These may encode "weaponization" or "attack" semantics

### Separability with Sparse Features

| Feature Count | ROC-AUC | Implication |
|---|---|---|
| Top 5 | 1.0000 | Perfect with ~0.5% of dimensions |
| Top 10 | 1.0000 | Perfect with ~1% of dimensions |
| Top 20 | 1.0000 | Perfect with ~2% of dimensions |
| Top 50 | 1.0000 | Perfect with ~5% of dimensions |
| All 1024 | 1.0000 | Perfect with 100% of dimensions |

**Critical observation:** Perfect separability achieved with just 5 features.

## Interpretation

### What This Suggests (Optimistic View)

✅ **Task distinction encodes sparsely** — Not distributed across all dimensions
✅ **Interpretability possible** — Small set of features may be mechanistically understandable
✅ **Generalizable pattern** — Sparse representation may reflect fundamental task properties

### What This Reveals (Pessimistic View)

❌ **Extreme overfitting** — 5 features on 10 samples is even more trivial than 1024 features on 10 samples
❌ **Dimensionality ratio absurd** — 5:10 is 1 feature per 2 samples (the ultimate overfitting scenario)
❌ **No real signal validation** — Perfect metrics at any feature count suggest N=10 sample size is completely inadequate

## Critical Analysis

### The Overfitting Paradox

Perfect separability with **fewer** features actually **strengthens the overfitting hypothesis**:

- With N=10 samples and 1024 features, logistic regression has many degrees of freedom
- With N=10 samples and 5 features, it has even fewer degrees of freedom
- Yet both achieve perfect separability
- This suggests the model is memorizing the training data regardless of feature count

**If signal were real:**
- Fewer features should hurt performance (information loss)
- We'd expect ROC-AUC to decline with sparsity
- Instead, perfect metrics persist at all sparsity levels

**Conclusion:** Sparse feature structure is evidence **against** real signal, not for it.

### What Would Validate Sparse Signal

To claim interpretable sparse features actually encode task distinction:

1. **Cross-validation** — Sparsity benefits should appear in test performance, not training
2. **Larger dataset** — Performance on N ≥ 100+ examples
3. **Feature consistency** — Same features should emerge across different random seeds
4. **Mechanistic interpretation** — What do features 325, 867, 112 actually compute?
5. **Transfer learning** — Do top features from Pythia transfer to other models?

## Conclusion

Sparse autoencoder analysis reveals that perfect separability is achievable with just 5 dimensions out of 1024, suggesting task-relevant information concentrates in a small feature subset.

However, this finding **reinforces rather than refutes** the overfitting hypothesis. Perfect metrics at extreme sparsity (1 feature per 2 samples) indicate the N=10 dataset is too small to draw any conclusions about real signal.

The appropriate response is: collect more data and implement proper cross-validation before claiming mechanistic interpretability.

## Next Steps

1. **Larger dataset** — Expand to N ≥ 100+ examples
2. **Proper cross-validation** — k-fold evaluation on held-out test set
3. **Feature stability** — Do top features emerge consistently?
4. **Mechanistic investigation** — What do top features compute?
5. **Cross-model feature transfer** — Do features generalize to other models?
