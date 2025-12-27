# Quotable Citations: Neural Collapse Paper → TSM Theory

**Paper**: "Asymptotic Analysis of Shallow and Deep Forgetting in Replay with Neural Collapse" (arXiv:2512.07400)
**Authors**: Lanzillotta, Meier, Hofmann (ETH Zürich, 2025)

---

## Citations Supporting Postulate I: Manifold Structure

> *"Meaning is position, coherence is continuous path."*

### Citation 1.1 — Simplex ETF Geometry (Section 3.1)

**Quote**:
> "𝒩𝒞2 (Simplex ETF). Centered class means form a simplex Equiangular Tight Frame (ETF). They attain equal norms and maximal pairwise separation."

**Formalization**:
```
lim(t→∞) ⟨μ̃_c(t), μ̃_c'(t)⟩ = {
  β_t        if c = c'
  -β_t/(K-1) if c ≠ c'
}
```

**Section**: Section 3.1, NC2 Definition

**TSM Relevance**: Validates that meaning is literally encoded as position (class mean μ_c) on a structured geometric manifold with maximal separation—the ETF structure TSM's manifold postulate requires.

---

### Citation 1.2 — OOD as Geometric Drift (Contribution 4)

**Quote**:
> "We reconceptualize deep forgetting as a geometric drift toward out-of-distribution subspaces."

**Section**: Section 1, Contribution 4

**TSM Relevance**: Chart incompatibility in TSM (when semantic continuity breaks) is formalized as drift from active subspace S toward orthogonal complement S⊥. Coherence = staying within S; incoherence = drift to S⊥.

---

### Citation 1.3 — OOD Definition via Orthogonality (Definition 1)

**Quote**:
> "Let S_t = span{μ̂̃_1(t), ..., μ̂̃_K(t)} the active subspace spanned by the centered class means of the training data at time t. We say that X_c is *out-of-distribution* for φ_t if the average representation of X_c is orthogonal to S_t."

**Section**: Section 4.2.1, Definition 1

**TSM Relevance**: Provides a precise geometric criterion for "semantic discontinuity"—TSM's chart transitions fail when representations move toward S⊥.

---

## Citations Supporting Postulate II: Typed Addressability

> *"Linguistic units carry typed signatures corresponding to localized regions in feature space."*

### Citation 2.1 — Variability Collapse (Section 3.1)

**Quote**:
> "𝒩𝒞1 (Variability Collapse). Within-class variability vanishes as features collapse to their class means: φ_t(x) → μ_c(t), ∀x ∈ X_c, implying the within-class covariance approaches **0**."

**Section**: Section 3.1, NC1 Definition

**TSM Relevance**: Validates that semantic types correspond to tight, addressable regions—the collapse to class means is precisely the localization that typed addressability requires.

---

### Citation 2.2 — Self-Duality (Section 3.1)

**Quote**:
> "𝒩𝒞3 (Neural Duality). Classifier weights align with the class means up to scaling, i.e., W_h^⊤(t) ∝ Ũ(t)."

**Section**: Section 3.1, NC3 Definition

**TSM Relevance**: Classifier weights literally point to type positions—reading weights reveals type structure. This is interpretability by construction, enabling typed addressability to be verified.

---

## Citations Supporting Postulate III: Categorical Conservation

> *"Dimension-collapsing transformations are type errors."*

### Citation 3.1 — Strong Collapse Warning (Abstract)

**Quote**:
> "The 'strong collapse' induced by small buffers leads to rank-deficient covariances and inflated class means, effectively blinding the classifier to true population boundaries."

**Section**: Abstract

**TSM Relevance**: **Critical warning**: Aggressive compression (analogous to heavy morphological fusion) causes pathological geometry. "Rank-deficient covariances" = dimension collapse = type error per Postulate III.

---

### Citation 3.2 — Geometric Simplification as Pathology (Contribution 3)

**Quote**:
> "We demonstrate that shallow forgetting arises because classifier optimization on buffers is under-determined—a condition structurally exacerbated by Neural Collapse. The resulting geometric simplification (covariance deficiency and norm inflation) blinds the classifier to the true population boundaries."

**Section**: Section 1, Contribution 3

**TSM Relevance**: "Geometric simplification" (dimension reduction) causes failure. TSM's nominalization warning—that collapsing process-space to entity-space loses information—is validated as a general principle.

---

### Citation 3.3 — Rank Reduction in Multi-Head (Section 3.2.2)

**Quote**:
> "Rank reduction. We find that local normalization induces a dimensionality reduction in the feature space. The global feature space attains a maximal rank of n(K-1) for n tasks, which is strictly lower than the nK-1 rank observed in single-head settings."

**Section**: Section 3.2.2, Finding 3

**TSM Relevance**: Dimensional collapse is measurable as rank reduction. TSM can operationalize Postulate III by monitoring covariance matrix rank.

---

## Citations Supporting Postulate IV: Static Decidability

> *"Semantic validity is decidable via pre-inference analysis."*

### Citation 4.1 — Deep vs Shallow Distinction (Section 1)

**Quote**:
> "A persistent observation in the literature is that neural networks retain substantially more information about past tasks in their internal representations than in their output predictions. This phenomenon, first demonstrated through *linear probe evaluations*, shows that a linear classifier trained on frozen last-layer representations achieves markedly higher accuracy on old tasks than the network's own output layer."

**Section**: Section 1, paragraph 2

**TSM Relevance**: Linear probes can detect preserved type structure even when outputs fail. This suggests type violations are statically detectable by probing the feature space before generation.

---

### Citation 4.2 — Linear Separability Preserved (Abstract)

**Quote**:
> "A persistent paradox in continual learning (CL) is that neural networks often retain linearly separable representations of past tasks even when their output predictions fail."

**Section**: Abstract, opening sentence

**TSM Relevance**: The core insight: deep structure (types) survives when shallow structure (tokens) fails. Type-level validity can be checked independently of output accuracy.

---

### Citation 4.3 — SNR as Separability Measure (Section 4.1)

**Quote**:
> "To analyse deep forgetting, we require a mathematically tractable measure of linear separability in feature space... we use the *signal-to-noise ratio* (SNR) between class distributions, defined as SNR(c₁,c₂) = ‖μ₁−μ₂‖² / Tr(Σ₁+Σ₂). Higher SNR values imply greater separability."

**Section**: Section 4.1, Linear Separability subsection

**TSM Relevance**: Provides a concrete formula for type decidability: compute SNR between type regions. If SNR exceeds threshold, types are distinguishable; below threshold indicates potential type confusion.

---

## Citations Supporting Postulate V: Tokenization Commitment

> *"Type assignment must occur at tokenization but must avoid 'strong collapse' from over-compression."*

### Citation 5.1 — Replay Efficiency Gap (Section 1)

**Quote**:
> "We reveal a critical asymmetry in Experience Replay: while minimal buffers successfully anchor feature geometry and prevent deep forgetting, mitigating shallow forgetting typically requires substantially larger buffer capacities."

**Section**: Abstract / Section 1, Contribution 1

**TSM Relevance**: Minimal type annotations (like small replay buffers) are sufficient to anchor semantic structure. Typed tokenization need not be maximally detailed—coarse types may preserve geometry.

---

### Citation 5.2 — Minimal Anchoring Suffices (Section 2)

**Quote**:
> "Our analysis reveals a critical efficiency gap: *even small buffers are sufficient to preserve feature separability and prevent deep forgetting*, whereas mitigating shallow forgetting requires substantially larger buffers. Thus, while replay robustly preserves representational geometry, it often fails to maintain alignment between the learned head and the true data distribution."

**Section**: Section 1, paragraph 4

**TSM Relevance**: Validates that minimal type commitment at tokenization is sufficient to preserve type-level structure, even if full context is needed for surface accuracy.

---

### Citation 5.3 — Compression Bound Warning (Section 3.2.1)

**Quote**:
> "When past classes are under-represented in the training dataset, they act as minority classes: their features collapse toward a degenerate distribution centered near the origin, and their classifier weights converge to constant vectors."

**Section**: Section 3.2.1, CIL analysis

**TSM Relevance**: Warning for TSM: if type categories become too sparse (over-compressed morphologization), they may suffer "minority collapse"—the typed tokens would lose their discriminative geometry.

---

## Key Formalizations

### Formalization F1: Deep vs Shallow Forgetting (Section 1.1)

**Definition**:
```
Shallow forgetting = A_ij − A_jj  (classifier accuracy drop)
Deep forgetting    = A*_ij − A*_jj (linear probe accuracy drop)

where:
  A_ij  = accuracy on task j after session i
  A*_ij = linear probe accuracy on frozen features
```

**TSM Mapping**: Deep forgetting ↔ Type structure corruption; Shallow forgetting ↔ Token output failure

---

### Formalization F2: Hypothesis 1 — OOD Equivalence (Section 4.2.1)

**Statement**:
> "Forgotten samples behave analogously to samples that were never learned, i.e., they are effectively *out-of-distribution* (OOD) with respect to the current model."

**TSM Interpretation**: Semantic discontinuity (chart incompatibility) = OOD behavior = orthogonality to active subspace

---

### Formalization F3: ETF Structure (Section 3.1)

**Equation**:
```
lim(t→∞) ⟨μ̃_c(t), μ̃_c'(t)⟩ = {
  β_t        if c = c'    [same class: aligned]
  -β_t/(K-1) if c ≠ c'    [different classes: maximally separated]
}
```

**TSM Interpretation**: Types should occupy maximally separated positions on the semantic manifold—the ETF is the optimal geometry for K distinct types.

---

## Summary: Strongest Evidence by Postulate

| Postulate | Strongest Citation | Key Phrase |
|-----------|-------------------|------------|
| I (Manifold) | Citation 1.1 | "simplex Equiangular Tight Frame" |
| II (Addressability) | Citation 2.1 | "features collapse to their class means" |
| III (Conservation) | Citation 3.1 | "rank-deficient covariances" |
| IV (Decidability) | Citation 4.2 | "retain linearly separable representations" |
| V (Tokenization) | Citation 5.1 | "minimal buffers anchor feature geometry" |

---

## BibTeX

```bibtex
@article{lanzillotta2025asymptotic,
  title={Asymptotic analysis of shallow and deep forgetting in replay with Neural Collapse},
  author={Lanzillotta, Giulia and Meier, Damiano and Hofmann, Thomas},
  journal={arXiv preprint arXiv:2512.07400},
  year={2025}
}
```
