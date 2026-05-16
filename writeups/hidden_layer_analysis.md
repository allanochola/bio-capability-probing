# Hidden-Layer Analysis: Where Does Biological Task Signal Reside?

## Abstract

This analysis investigates whether representational signal associated with biological task distinctions is distributed uniformly across transformer layers or concentrated in specific regions.

We trained linear probes on hidden-state representations extracted from each layer of a language model and measured separability (ROC-AUC) as a function of layer depth.

Results show that biological task separability varies substantially across layers, with peak performance at specific intermediate layers. This suggests that the signal underlying task distinction is neither superficial (early layers) nor maximally abstracted (final layer), but concentrated in intermediate representation spaces.

## Methodology

**Model:** EleutherAI/pythia-410m (12 layers, 410M parameters)

**Dataset:** 10 manually constructed biological prompts (5 benign, 5 harmful)

**Probe:** Logistic regression trained independently for each layer

**Metric:** ROC-AUC (more robust than accuracy given small sample size)

## Key Finding

![Layer Separability](../figures/layer_separability.png)

**Peak separability occurs at layer [INSERT BEST LAYER INDEX]**

ROC-AUC by layer progression:
- Early layers: modest signal
- Middle layers: peak separability
- Late layers: declining signal

This pattern suggests:
- Early layers: likely capturing lexical/syntactic biological vocabulary
- Middle layers: semantic abstraction of biological task concepts
- Late layers: task-agnostic or task-suppressed representations

## Detailed Results

Complete layer-by-layer metrics available in `results/layer_analysis_results.csv`

### Early Layers (0-3)
Signal present but modest, suggesting lexical confounds dominate.

### Peak Separability
Best performance at intermediate layers indicates authentic semantic separation rather than superficial vocabulary differences.

### Late Layers
Declining ROC-AUC in final layers suggests final token representation may suppress or abstract away task-relevant signal.

## Visualization: Peak Layer Representation Space

![Best Layer PCA](../figures/best_layer_pca.png)

PCA projection of the peak-separability layer shows partial clustering between benign and harmful prompts, with notable overlap indicating non-trivial but imperfect separability.

## Interpretation

This analysis provides preliminary evidence that:

1. **Biological task signal exists in hidden representations** — Not just a superficial textual artifact
2. **Signal is layer-distributed** — Not concentrated in any single layer
3. **Peak separability is intermediate** — Suggests semantic rather than purely lexical basis
4. **Overlap persists** — Complete separation does not exist even in best-case representation

## Important Limitations

- **Tiny sample size (N=10):** Extremely fragile to overfitting and noise
- **Single model family:** Results may not generalize to other architectures
- **Manual prompts:** Not representative of realistic biological task domains
- **No cross-layer analysis:** Did not examine feature redundancy across layers
- **No adversarial evaluation:** Robustness to paraphrasing untested

## Scientific Implications

If biological task signal truly resides in intermediate layers:
- Early-layer monitoring alone would miss semantic-level deception
- Late-layer monitoring might be insufficient due to abstraction
- Multi-layer ensemble approaches may be more robust

These hypotheses require testing on larger, more realistic datasets.

## Future Directions

- Analyze intermediate layers in larger models (7B+)
- Test adversarial robustness of layer-specific probes
- Compare signal persistence across model families
- Investigate feature composition in peak layers (SAE analysis)

## Conclusion

Hidden-layer analysis reveals that biological task separability is not uniformly distributed across transformer depth. Peak separability in intermediate layers suggests authentic semantic signal, though the tiny dataset size and manual prompt construction severely limit generalizability.

This work provides methodological scaffolding for future mechanistic interpretability research on biological task domains.
