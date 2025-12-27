# SYNTHESIS: Manifold Capacity as Semantic Coherence Metric

**Paper**: "Generalized Category Discovery via Token Manifold Capacity Learning" (arXiv:2505.14044)
**Framework**: Typed Semantic Manifold (TSM)

---

## The Central Question

Can MTMC's **manifold capacity** serve as a quantitative metric for TSM's notion of **semantic coherence as path continuity**?

TSM claims:
> "Coherence is continuous path... drift along the manifold surface is semantically meaningful."

MTMC provides:
> "Manifold capacity of class tokens to preserve the diversity and complexity of data."

**Synthesis Goal**: Adapt MTMC's geometric measures to quantify TSM's path-based coherence.

---

## From Points to Paths: The Required Transformation

### MTMC's Current Formulation
MTMC measures capacity of a **point cloud** (CLS tokens from a batch):

$$\mathcal{L}_{MTMC} = -\|\mathbf{CLS}\|_* = -\sum_i \sigma_i$$

This captures: *How much of the representation space is occupied by the distribution of inputs?*

### TSM's Requirement
TSM needs measures of **path properties**:

- Does a token sequence trace a continuous curve?
- Does the path stay within typed regions?
- Is the path geodesic (shortest valid route between semantic positions)?

**Transformation Needed**: Convert point-cloud capacity to path-capacity.

---

## Proposed Synthesis: Path Manifold Capacity (PMC)

### Definition
For a token sequence $\{t_1, t_2, ..., t_n\}$ with embeddings $\{e_1, e_2, ..., e_n\}$:

**Step 1: Form the Path Matrix**
$$\mathbf{P} = [e_1, e_2, ..., e_n] \in \mathbb{R}^{d \times n}$$

This is analogous to MTMC's CLS matrix, but within a single sequence rather than across a batch.

**Step 2: Compute Path Nuclear Norm**
$$\|\mathbf{P}\|_* = \sum_i \sigma_i(\mathbf{P})$$

**Step 3: Normalize by Path Length**
$$\text{PMC} = \frac{\|\mathbf{P}\|_*}{n}$$

### Interpretation
- **High PMC**: The path "uses" many dimensions—the sequence visits semantically diverse positions
- **Low PMC**: The path is dimensionally collapsed—tokens cluster in a low-dimensional subspace

---

## Path Manifold Capacity and TSM Coherence

### Hypothesis: PMC Measures Semantic Richness of Discourse

| PMC Level | Semantic Interpretation | TSM Diagnosis |
|-----------|------------------------|---------------|
| Very Low | Repetitive, stuck in single semantic region | Potential loop/stagnation |
| Low | Limited semantic movement | Constrained discourse |
| Medium | Balanced exploration within structure | Coherent discourse |
| High | Covers many semantic dimensions | Rich, exploratory discourse |
| Very High | Erratic movement across space | Potential incoherence (?) |

**Critical Question**: Does high PMC correlate with coherence or incoherence?

---

## The Coherence-Capacity Relationship

### MTMC's Claim: Higher Capacity → Better Discrimination
For classification, more capacity means better separation of categories.

### TSM's Constraint: Coherence Requires Continuity
For generation, valid paths must be *continuous*—you can't teleport across the manifold.

**Synthesis Insight**: Coherence requires **structured capacity**:
- The path should span multiple dimensions (high capacity)
- But transitions should be smooth (continuity)

This suggests a **modified PMC** that penalizes discontinuous jumps:

$$\text{PMC}_\text{coherent} = \frac{\|\mathbf{P}\|_*}{n} - \lambda \sum_{i=1}^{n-1} \|e_{i+1} - e_i\|^2 / \sigma^2$$

where the second term penalizes large jumps relative to expected step size $\sigma$.

---

## Connecting to TSM's Type System

### Manifold Capacity Within Type Regions
TSM partitions the manifold into typed regions. We can compute **type-conditional PMC**:

For tokens of type $\tau$:
$$\text{PMC}_\tau = \|\mathbf{P}_\tau\|_* / |\{t : \text{type}(t) = \tau\}|$$

This measures: *How much capacity is used within each type category?*

### Cross-Type Path Capacity
Transitions between types should also preserve capacity:

$$\text{PMC}_\text{transition} = \text{Capacity of } \{e_i : \text{type}(t_i) \neq \text{type}(t_{i+1})\}$$

High transition capacity indicates rich type-boundary crossings; low capacity indicates stereotyped transitions.

---

## Empirical Metrics Derived from Synthesis

### Metric 1: Sequence Manifold Capacity (SMC)
$$\text{SMC}(s) = \|\mathbf{E}_s\|_* / \text{len}(s)$$

where $\mathbf{E}_s$ is the embedding matrix for sequence $s$.

**Predicts**: Semantic richness of generated text.

### Metric 2: Local Capacity Gradient (LCG)
$$\text{LCG}(i) = \text{SMC}(s_{1:i+1}) - \text{SMC}(s_{1:i})$$

**Predicts**: Whether adding token $i$ increases or decreases path capacity.
- Positive LCG: Token expands semantic coverage
- Negative LCG: Token is redundant or collapsing

### Metric 3: Type-Weighted Capacity (TWC)
$$\text{TWC} = \sum_\tau w_\tau \cdot \text{PMC}_\tau$$

where $w_\tau$ weights types by semantic importance (from TSM's type hierarchy).

**Predicts**: Typed semantic coherence combining capacity and structure.

---

## Connection to MAS (Morphological Alignment Score)

TSM's MAS measures tokenization efficiency:
$$\text{MAS} = 1 / (\text{BPE tokens per semantic unit})$$

**Synthesis Hypothesis**: MAS and PMC are related:

| MAS | PMC | Interpretation |
|-----|-----|----------------|
| High MAS, High PMC | Efficient tokens, rich semantics | Optimal |
| High MAS, Low PMC | Efficient tokens, shallow semantics | Precise but limited |
| Low MAS, High PMC | Scattered tokens, rich semantics | Redundant but expressive |
| Low MAS, Low PMC | Scattered tokens, shallow semantics | Poor all around |

**Joint Metric**:
$$\text{Semantic Efficiency} = \text{MAS} \times \text{PMC}$$

This captures both tokenization quality (MAS) and representational richness (PMC).

---

## Von Neumann Entropy as Coherence Signal

MTMC proves nuclear norm maximization increases von Neumann entropy. For TSM:

$$\hat{H}(\mathbf{P}) = -\sum_j \lambda_j \log \lambda_j$$

where $\lambda_j$ are normalized eigenvalues of $\mathbf{P}\mathbf{P}^T$.

**Interpretation**:
- **Low entropy**: Path concentrated in few dimensions → limited semantic exploration
- **High entropy**: Path uniformly distributed across dimensions → maximal semantic richness

**TSM Application**: Track $\hat{H}(\mathbf{P})$ during generation. Entropy collapse signals dimensional collapse, which by Postulate III is a type error.

---

## Algorithmic Application: Capacity-Aware Decoding

### Standard Decoding
Next token = argmax $P(t | \text{context})$

### Capacity-Aware Decoding
Next token = argmax $P(t | \text{context}) + \alpha \cdot \Delta\text{PMC}(t)$

where $\Delta\text{PMC}(t)$ is the capacity change from adding token $t$.

**Effect**: Bias generation toward tokens that maintain or increase manifold capacity, preventing dimensional collapse during generation.

---

## Synthesis Summary

| MTMC Concept | TSM Application | Synthesized Metric |
|--------------|-----------------|-------------------|
| Nuclear norm of CLS batch | Within-sequence path richness | Sequence Manifold Capacity (SMC) |
| Manifold capacity | Semantic exploration per type | Type-Weighted Capacity (TWC) |
| Von Neumann entropy | Dimensional collapse detection | Path entropy tracking |
| Dimensional collapse | Type error (Postulate III) | LCG < 0 as warning signal |

**Core Insight**: MTMC's manifold capacity, adapted from point-cloud to path-based measurement, provides quantitative grounding for TSM's qualitative claims about semantic coherence.

---

## Future Directions

1. **Empirical Validation**: Correlate SMC with human coherence judgments
2. **Capacity-Guided Training**: Add PMC as auxiliary loss for language models
3. **Type-Conditioned Capacity**: Measure whether type boundaries correlate with capacity shifts
4. **Cross-Modal Extension**: Apply path capacity to multimodal manifolds (text + vision)

The synthesis of MTMC's geometric measures with TSM's typed semantics opens a path toward **measurable semantic coherence**—moving TSM from theoretical framework to empirically testable system.
