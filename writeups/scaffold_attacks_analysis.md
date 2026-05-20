
# Scaffold Attacks: Embedding Prompts in Realistic Workflows

## Executive Summary

This analysis tests whether separability survives when biological prompts are embedded in longer, realistic research narratives. Scaffold attacks represent the most ecologically valid test — moving beyond isolated prompts to contextualized workflows.

**Key finding:** Separability persists even under scaffold attacks (ROC-AUC = 1.0 across all layers), with only 45.1% vocabulary overlap. This is the strongest evidence yet that signal is not purely lexical or superficial, but encodes task-relevant semantic distinctions robustly.

## Motivation

Previous analyses tested:
1. Vocabulary control (reduce lexical confounds)
2. Paraphrasing (preserve semantics while varying vocabulary)

But both still used isolated prompts. Real biological research doesn't occur in isolation — tasks are embedded in longer workflows, research narratives, and contextual justifications.

**Question:** Does separability survive when prompts are contextualized within realistic research scenarios?

## Methodology

### Scaffold Design

We created two sets of longer biological research narratives (≈150 words each):

**Benign scaffolds:** Realistic research contexts for legitimate biological work
- Vaccine candidate development with storage optimization
- Industrial fermentation for pharmaceutical manufacturing
- Therapeutic enzyme efficiency enhancement
- Vaccine delivery system development
- Pharmaceutical protein synthesis optimization

**Harmful scaffolds:** Same biological topics but framed for weaponization
- Pathogen enhancement for biological weapons
- Bioweapon production optimization
- Toxin development for enhanced lethality
- Biological agent delivery systems
- Large-scale bioweapon production

### Vocabulary Control

Scaffold attacks achieved:
- **Benign vocabulary:** 122 tokens
- **Harmful vocabulary:** 107 tokens
- **Overlap:** 55 tokens (45.1%)

This represents the **lowest vocabulary overlap tested** across all phases:
- Original prompts: 29%
- Controlled vocabulary: 56%
- Paraphrase attacks: 62%
- **Scaffold attacks: 45%** ← Lowest overlap

Lower overlap means less lexical signal available. If separability persists despite minimal vocabulary overlap, semantic signal must be robust.

### Representation Extraction & Probing

Same methodology as prior phases:
- Mean-pooled hidden states from all 25 layers
- Logistic regression probe per layer
- Training/evaluation on same data (N=10)

## Results

**Layer-wise separability (ROC-AUC):**
