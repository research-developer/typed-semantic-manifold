# Synthesis: Neural Collapse Insights for TSM Theory Development

**Paper**: "Asymptotic Analysis of Shallow and Deep Forgetting in Replay with Neural Collapse" (arXiv:2512.07400)

---

## Core Insight

The paper's central finding—that neural networks preserve deep (feature-space) structure even when shallow (classifier) outputs fail—provides the most important theoretical grounding for TSM's type-level / token-level distinction.

**Key equation for TSM**: The "replay efficiency gap" shows structure preservation is cheaper than output accuracy. TSM should exploit this asymmetry.

---

## 1. Formalizing the Type-Token Hierarchy

### The Paper's Framework

The paper operationalizes two distinct levels:

| Level | Measure | What It Captures |
|-------|---------|------------------|
| Deep | Linear probe accuracy A*_ij | Feature-space structure |
| Shallow | Classifier accuracy A_ij | Output predictions |

The gap `A*_ij - A_ij` quantifies preserved-but-unutilized structure.

### TSM Translation

| Neural Collapse | TSM Concept | Interpretation |
|-----------------|-------------|----------------|
| Deep structure | Type-level representation | Semantic position on manifold |
| Shallow output | Token-level generation | Surface form production |
| Linear probe | Type-aware decoder | Structure-respecting output layer |
| Replay buffer | Type annotations | Minimal structural anchors |

**Actionable insight**: TSM could operationalize "type preservation" as linear separability of semantic categories in hidden states.

---

## 2. The Geometry of Type Violations

### Neural Collapse Formalization

The paper defines forgetting geometrically:
- **In-distribution**: Features in subspace S (spanned by active class means)
- **Out-of-distribution**: Features drifting toward S⊥ (orthogonal complement)

Forgetting = drift from S toward S⊥.

### TSM Application

TSM's Meta-Model violations (deletion, distortion, generalization) can be formalized as:

| Meta-Model Pattern | Geometric Interpretation |
|-------------------|-------------------------|
| **Deletion** | Projection from S_full → S_reduced (dimensions removed) |
| **Distortion** | Non-orthogonal transformation in S |
| **Generalization** | Collapse of distinct positions toward shared mean |
| **Nominalization** | Process-space → Entity-space projection |

**Concrete test**: Measure whether nominalized sentences have features closer to entity-class means than process-class means, validating the "dimension collapse" interpretation.

---

## 3. Buffer Size ↔ Type Annotation Density

### The Paper's Finding

| Buffer Size | Deep Forgetting | Shallow Forgetting |
|-------------|----------------|-------------------|
| 1% | Nearly zero | Very high |
| 10% | Zero | High |
| 100% | Zero | Near zero |

**Interpretation**: Minimal anchors preserve structure; accurate boundaries require full statistics.

### TSM Design Principle

This suggests a **tiered type annotation strategy**:

| Annotation Level | Analogous to | Expected Effect |
|-----------------|--------------|-----------------|
| Coarse types (Entity/Process/Relation) | 1% buffer | Preserve semantic structure |
| Medium types (Person/Object/Location) | 10% buffer | Improve type-level accuracy |
| Fine types (full case morphology) | 100% buffer | Match surface-level precision |

**Design recommendation**: TSM's typed tokenizer should support **progressive type refinement**, starting with coarse categories that anchor geometry, with optional fine-grained types for precision-critical applications.

---

## 4. Avoiding Strong Collapse

### The Paper's Warning

> "Strong collapse induced by small buffers leads to rank-deficient covariances and inflated class means."

This occurs when:
1. Training data is too sparse (small buffer)
2. Optimization converges to buffer-optimal solutions that don't generalize

### TSM Corollary

**Aggressive morphological fusion risks "strong collapse":**

| Fusion Level | Token Count | Risk |
|--------------|-------------|------|
| None | Baseline | No collapse |
| Light (prepositions) | ~30% reduction | Low risk |
| Heavy (full fusion) | ~60% reduction | Potential collapse |
| Extreme | ~80% reduction | Strong collapse likely |

**Recommendation**: Establish empirical bounds on compression ratio. The paper suggests any non-zero replay preserves linear separability—analogously, any non-zero token granularity should preserve expressiveness. But the **optimal** compression may be moderate, not maximal.

### Testable Prediction

Train models with varying morphological fusion levels. Measure:
1. Feature covariance rank (should not decline pathologically)
2. Class mean norms (should not inflate beyond population estimates)
3. Linear probe vs classifier gap (strong collapse = large gap despite full data)

---

## 5. Connecting TSM to OOD Detection

### The Paper's Insight

> "We reconceptualize deep forgetting as a geometric drift toward out-of-distribution subspaces."

This bridges continual learning and OOD detection.

### TSM Application

**Type violations as OOD detection problems:**

| Type Violation | OOD Interpretation |
|----------------|-------------------|
| Missing argument | Input in null-pointer region of manifold |
| Unresolved anaphora | Pointer target in S⊥ |
| Nominalization without grounding | Process features projected to Entity region |
| Prompt injection | System-scope features drifted to User-scope region |

**Concrete method**: Use OOD detection techniques (Mahalanobis distance, energy-based methods) to detect type violations:
```
D(x, type) = distance from x's features to expected type region
if D > threshold: TYPE_VIOLATION
```

This operationalizes TSM's static decidability using established OOD machinery.

---

## 6. Multi-Head Architecture Suggestion

### The Paper's Finding

Multi-head architectures (TIL) show smaller deep-shallow gaps than single-head (CIL, DIL).

### TSM Architectural Implication

TSM's type system might benefit from **type-specific heads**:

```
Input: [STORE.ALLATIVE] "groceries"

Type Head for ALLATIVE → specialized processing for motion-toward
Type Head for Entity → specialized processing for physical objects

Combined: Motion-toward(groceries, STORE)
```

This is analogous to:
- Task-incremental learning's separate heads per task
- Mixture-of-experts with type-routed experts
- Modular networks with type-specific modules

**Architecture recommendation**: Explore type-conditioned attention or type-specific output projections.

---

## 7. Revised TSM Postulates Based on Neural Collapse

### Postulate I (Manifold Structure) — Strengthened

**Original**: "Meaning is position, coherence is continuous path."

**Revised with NC grounding**: "Meaning is position in a geometric manifold that, under sufficient training, converges to a structured configuration (simplex ETF for classification, analogous structure for generation). Coherence is continuity within the active subspace S; incoherence is drift toward S⊥."

### Postulate II (Typed Addressability) — Operationalized

**Original**: "Linguistic units carry typed signatures."

**NC operationalization**: "Type signatures correspond to localized regions in feature space, characterized by class means μ_c and covariances Σ_c. Type-checking is distance computation to these regions."

### Postulate III (Categorical Conservation) — Geometrized

**Original**: "Dimension-collapsing transformations are type errors."

**NC formalization**: "Dimension collapse manifests as rank reduction in covariance matrices and projection of features from higher-dimensional S_full to lower-dimensional S_reduced. Detectable via singular value analysis of feature covariances."

### Postulate IV (Static Decidability) — Enabled by OOD

**Original**: "Semantic validity is decidable pre-inference."

**NC method**: "Use OOD detection on feature representations to identify type violations before generation. Linear probes can recover valid type structure even when classifier fails."

### Postulate V (Tokenization Commitment) — Bounded

**Original**: "Type assignment must occur at tokenization."

**NC warning**: "Type assignment at tokenization is valid but must avoid 'strong collapse' from over-compression. Optimal fusion ratio is empirical, not maximal."

---

## 8. Experimental Roadmap

Based on Neural Collapse insights, TSM validation should include:

### Phase 1: Manifold Geometry Verification
1. Measure NC metrics (NC1, NC2, NC3) for language models on semantic categories
2. Test whether typed tokens produce tighter NC than BPE tokens
3. Validate ETF-like structure for linguistic type categories

### Phase 2: Type Violation Detection via OOD
1. Develop OOD detectors for semantic type regions
2. Test correlation between OOD scores and hallucination/error rates
3. Build type-violation classifier using Mahalanobis distance

### Phase 3: Compression Bound Identification
1. Train models with progressive morphological fusion
2. Measure feature covariance rank at each compression level
3. Identify threshold where "strong collapse" begins

### Phase 4: Architecture Exploration
1. Implement type-conditioned attention heads
2. Compare single-head vs multi-type-head architectures
3. Measure deep-shallow gap reduction from type-aware architecture

---

## Summary: Top 5 Takeaways for TSM

1. **The deep/shallow distinction is real and robust** — This validates TSM's core intuition about layered semantic structure.

2. **Minimal type anchors may suffice** — Like small replay buffers, coarse type annotations might preserve most of the semantic structure.

3. **Beware of strong collapse** — Aggressive typed tokenization could cause pathological geometry. Moderate compression is likely optimal.

4. **OOD detection enables type checking** — The paper's OOD framework provides concrete methods for implementing TSM's static decidability.

5. **Architecture may matter as much as tokenization** — Multi-head and type-conditioned architectures may be needed to fully realize TSM's benefits.

---

## Key Open Question

The paper's deepest challenge to TSM:

> If deep structure (types) is naturally preserved by learned representations, why impose explicit types rather than exploit implicit structure?

**Possible answers**:
1. **Interpretability**: Explicit types are human-readable; implicit structure requires probing
2. **Efficiency**: Typed tokenization reduces sequence length; implicit structure doesn't compress
3. **Robustness**: Explicit types constrain the model; implicit structure can be overridden
4. **Compositionality**: Explicit types support algebraic operations; implicit structure is entangled

The strongest argument may be **controllability**: explicit types let humans intervene in the semantic structure, while implicit types require post-hoc interpretation.

---

## Citation

This evaluation based on:

```bibtex
@article{lanzillotta2025asymptotic,
  title={Asymptotic analysis of shallow and deep forgetting in replay with Neural Collapse},
  author={Lanzillotta, Giulia and Meier, Damiano and Hofmann, Thomas},
  journal={arXiv preprint arXiv:2512.07400},
  year={2025}
}
```
