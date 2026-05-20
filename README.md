# Bio Capability Probing: Exploratory Activation-Space Monitoring for Biological Task Domains

**Author:** Allan Ochola | **Date:** May 2026 | **Status:** Published (Zenodo DOI: 10.5281/zenodo.20244912)

---

## Quick Summary

Exploratory research investigating whether activation-space probing methodologies developed in deception-detection research can transfer to biological capability monitoring in language models.

**Key Finding:** Separability between benign and harmful biological prompts persists across **ALL adversarial attack types** (vocabulary control, paraphrasing, scaffolding), achieving ROC-AUC = 1.0 in all cases. This suggests semantic task framing encodes robustly, but tiny sample size (N=10) makes perfect separability statistically trivial.

**Primary Contribution:** Methodological framework for systematic confound analysis and honest limitation documentation in small-sample interpretability research.

---

## Project Structure

bio-capability-probing/
├── README.md (this file)
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
│   └── complete_adversarial_robustness_grid.png
├── results/
│   └── baseline_metrics.json
└── writeups/
├── baseline_replication.md
├── vocabulary_control_analysis.md
├── adversarial_robustness_analysis.md
├── scaffold_attacks_analysis.md
└── RESEARCH_SUMMARY.md

---

## Research Phases

### Phase 1: Apollo Behavioral Baseline ✅
Reconstructed deception classifier from Apollo Research rollout annotations.

**Results:** ROC-AUC = 0.64, Accuracy = 0.67, Precision = 0.74, Recall = 0.83

---

### Phase 2: Hidden-Layer Analysis ✅
Extracted mean-pooled representations from all 25 transformer layers.

**Results:** ROC-AUC = 1.0 (all layers, 29% vocabulary overlap)

---

### Phase 3: Vocabulary Control Analysis ✅
Compared original (29% overlap) vs. controlled (56% overlap) prompts.

**Results:** ROC-AUC = 1.0 (separability persists under vocabulary control)

---

### Phase 4: Adversarial Robustness Testing ✅

#### 4a: Paraphrase Attacks (62% vocab overlap)
**Results:** ROC-AUC = 1.0 (all layers)

#### 4b: Scaffold Attacks (45% vocab overlap)  
**Results:** ROC-AUC = 1.0 (all layers)

---

## Complete Adversarial Robustness Summary

| Attack Type | Vocab Overlap | Mean ROC-AUC |
|---|---|---|
| Original Prompts | 29% | 1.0000 |
| Vocabulary Control | 56% | 1.0000 |
| Paraphrase Attack | 62% | 1.0000 |
| Scaffold Attack | 45% | 1.0000 |

**Key Finding:** Perfect separability persists across all attack types and all layers.

---

## Critical Analysis: Why Perfect Metrics Are Red Flags

Perfect ROC-AUC = 1.0 across all conditions appears to validate robustness. However:

**Sample size problem:**
- N=10 samples in 1024-dimensional space
- Dimensionality ratio: 102.4:1
- Statistical overfitting is most parsimonious explanation
- Perfect separability is mathematically trivial at this ratio

**Evidence for semantic signal:**
✅ Separability persists under vocabulary control  
✅ Separability survives paraphrasing  
✅ Separability survives realistic scaffolding  
✅ Consistent across all 25 layers  

**Evidence for overfitting:**
❌ N=10 too small for 1024-D space  
❌ No cross-validation  
❌ Single model only  
❌ Perfect metrics = overfitting in ML  

---

## Honest Limitations

1. **Sample Size (CRITICAL):** N=10 is far too small
2. **No Cross-Validation:** Training/eval on same data
3. **Single Model:** Pythia-410m only; no biological models tested
4. **Manual Prompts:** Not representative of realistic workflows
5. **No Adversarial Optimization:** Passive attacks only
6. **No Circuit Analysis:** No mechanistic investigation

### What We Cannot Claim
✗ Robust biological threat detection  
✗ Deployment-ready capability  
✗ Generalizable signal across models  

### What We Can Claim
✓ Separability persists under confound control  
✓ Semantic signal likely contributes  
✓ Signal not purely lexical  
✓ Methodologically rigorous analysis  
✓ Reproducible pipeline  

---

## How to Reproduce

```bash
git clone https://github.com/allanochola/bio-capability-probing.git
cd bio-capability-probing
pip install -r requirements.txt

# Run experiments
jupyter notebook notebooks/01_apollo_baseline.ipynb
jupyter notebook notebooks/02_biological_probing.ipynb
jupyter notebook notebooks/03_hidden_layer_analysis.ipynb
```

---

## Validation Roadmap

To move from exploratory to validated research:

1. Expand dataset to N ≥ 100+ examples
2. Implement k-fold cross-validation
3. Test adversarial robustness with active optimization
4. Evaluate cross-model transfer (biological foundation models)
5. Investigate mechanistic basis (circuit analysis)

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

**Zenodo DOI:** https://doi.org/10.5281/zenodo.20244912

---

## Contact

**Author:** Allan Ochola  
**Email:** allanochola4@gmail.com  
**GitHub:** github.com/allanochola  

---

**Status:** ✅ Exploratory Research Complete | ✅ Published to Zenodo | ⏳ Validation Phase

**Last Updated:** May 2026
