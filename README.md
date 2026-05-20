# Bio Capability Probing: Exploratory Activation-Space Monitoring for Biological Task Domains

**Author:** Allan Ochola | **Date:** May 2026 | **Published:** Zenodo DOI: 10.5281/zenodo.20244912

---

## Quick Summary

Exploratory research investigating whether activation-space probing methodologies transfer to biological capability monitoring in language models.

**Key Finding:** Separability between benign and harmful biological prompts persists across ALL adversarial attack types and generalizes across models (ROC-AUC = 1.0). Sparse autoencoder analysis reveals task distinction encodes in just 5 dimensions—but this reinforces the overfitting hypothesis at N=10 sample size.

**Contribution:** Comprehensive 6-phase methodology with systematic confound analysis, adversarial robustness testing, cross-model validation, and honest documentation of why perfect metrics on tiny datasets are red flags.

---

## Research Overview

### Phases Completed

**Phase 1: Apollo Behavioral Baseline**
- Reconstructed deception classifier from Apollo Research annotations
- ROC-AUC = 0.64 (modest behavioral signal)

**Phase 2: Hidden-Layer Analysis**
- Mean-pooled representations from all 25 transformer layers
- ROC-AUC = 1.0 across all layers (29% vocabulary overlap)

**Phase 3: Vocabulary Control Analysis**
- Isolated semantic signal from lexical confounds
- ROC-AUC = 1.0 (56% vocabulary overlap)

**Phase 4: Adversarial Robustness Testing**
- Paraphrase attacks: ROC-AUC = 1.0 (62% overlap)
- Scaffold attacks: ROC-AUC = 1.0 (45% overlap)

**Phase 5: Cross-Model Comparison**
- Pythia-410m (410M params, 25 layers): ROC-AUC = 1.0
- GPT-Neo-125m (125M params, 12 layers): ROC-AUC = 1.0

**Phase 6: Sparse Autoencoder Analysis**
- Top 5 features achieve ROC-AUC = 1.0
- Top 10, 20, all 1024 features also achieve ROC-AUC = 1.0
- Sparsity paradox: Perfect metrics at extreme sparsity = overfitting

---

## Complete Evaluation Summary

| Phase | Test Type | Result | Key Metric |
|---|---|---|---|
| 1 | Behavioral baseline | ✅ | ROC-AUC = 0.64 |
| 2 | Hidden-layer (all 25) | ✅ | ROC-AUC = 1.0 |
| 3 | Vocabulary control | ✅ | ROC-AUC = 1.0 (56% overlap) |
| 4a | Paraphrase attacks | ✅ | ROC-AUC = 1.0 (62% overlap) |
| 4b | Scaffold attacks | ✅ | ROC-AUC = 1.0 (45% overlap) |
| 5a | Cross-model (Pythia) | ✅ | ROC-AUC = 1.0 (25 layers) |
| 5b | Cross-model (GPT-Neo) | ✅ | ROC-AUC = 1.0 (12 layers) |
| 6 | Sparse features | ✅ | ROC-AUC = 1.0 (5 features) |

---

## Why Perfect Metrics Are Red Flags

Perfect ROC-AUC = 1.0 appears validating but raises critical concerns:

**Sample Size Problem:**
- N=10 samples in 1024-dimensional space (102.4:1 ratio)
- Logistic regression trivially overfits at this ratio
- Statistical overfitting most parsimonious explanation

**Sparsity Paradox:**
- Perfect separability with 5 features MORE suspicious than 1024
- 5 features on 10 samples = 1 feature per 2 samples
- This is extreme overfitting, not real signal

**Evidence For Semantic Signal:**
✅ Separability persists under vocabulary control  
✅ Separability survives paraphrasing  
✅ Separability survives realistic scaffolding  
✅ Separability generalizes across models  
✅ Task distinction encodes sparsely  

**Evidence For Overfitting:**
❌ N=10 too small for validation  
❌ Perfect metrics at ALL sparsity levels  
❌ No cross-validation performed  
❌ Single model family tested  
❌ Perfect metrics = overfitting in ML  

---

## Critical Limitations

1. **Sample Size (CRITICAL):** N=10 is far too small for any statistical claims
2. **No Cross-Validation:** Training/evaluation on same data
3. **Single Model Family:** EleutherAI only; no biological models
4. **Manual Prompts:** Not representative of realistic workflows
5. **Passive Attacks Only:** No active adversarial optimization
6. **No Circuit Analysis:** Which neurons drive features unknown
7. **Sparsity Is Suspicious:** Perfect metrics at extreme sparsity reinforce overfitting

### What We Cannot Claim
- Robust biological threat detection
- Deployment-ready capability
- Generalizable signal across diverse models
- Mechanistic interpretability without validation

### What We Can Claim
- Separability persists under confound control
- Semantic signal likely contributes information
- Signal not purely lexical
- Methodologically rigorous analysis across 6 phases
- Reproducible, transparent pipeline

---

## Project Structure

bio-capability-probing/
├── README.md
├── requirements.txt
├── notebooks/
│   ├── 01_apollo_baseline.ipynb
│   ├── 02_biological_probing.ipynb
│   └── 03_hidden_layer_analysis.ipynb
├── datasets/
│   └── biological_prompts.csv
├── figures/
│   ├── confusion_matrix.png
│   ├── roc_curve.png
│   ├── vocabulary_control_comparison.png
│   ├── adversarial_robustness_comparison.png
│   ├── complete_adversarial_robustness_grid.png
│   ├── complete_adversarial_summary.png
│   └── sparse_autoencoder_analysis.png
├── results/
│   └── baseline_metrics.json
└── writeups/
├── baseline_replication.md
├── vocabulary_control_analysis.md
├── adversarial_robustness_analysis.md
├── scaffold_attacks_analysis.md
├── cross_model_comparison.md
├── sparse_autoencoder_analysis.md
└── RESEARCH_SUMMARY.md


---

## Reproducing Results

```bash
git clone https://github.com/allanochola/bio-capability-probing.git
cd bio-capability-probing
pip install -r requirements.txt

jupyter notebook notebooks/01_apollo_baseline.ipynb
jupyter notebook notebooks/02_biological_probing.ipynb
jupyter notebook notebooks/03_hidden_layer_analysis.ipynb
```

---

## Validation Roadmap

To move from exploratory to validated research:

1. Expand dataset to N ≥ 100+ biological prompts
2. Implement k-fold cross-validation
3. Test adversarial robustness with active optimization
4. Evaluate on biological models (Evo 2, ProteinMPNN, ESM-family)
5. Investigate mechanistic basis (which neurons drive separability?)

---

## Citation

```bibtex
@software{ochola2026biocapabilityprobing,
  author = {Ochola, Allan},
  title = {Bio Capability Probing: Exploratory Activation-Space Monitoring for Biological Task Domains},
  year = {2026},
  url = {https://github.com/allanochola/bio-capability-probing},
  doi = {10.5281/zenodo.20244912}
}
```

**Zenodo:** https://doi.org/10.5281/zenodo.20244912

---

## Contact

**Author:** Allan Ochola  
**Email:** allanochola4@gmail.com  
**GitHub:** github.com/allanochola  

---

**Status:** ✅ Exploratory Research Complete | ✅ Published to Zenodo | ⏳ Validation Phase (Requires larger dataset + cross-validation)

**Last Updated:** May 2026
