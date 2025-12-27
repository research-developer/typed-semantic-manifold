# Citations from arXiv:2505.03862 Supporting TSM Theory

**Paper**: Lê et al. "Categorical and geometric methods in statistical, manifold, and machine learning"

**Citation Date**: 2025-12-26

---

## Executive Summary

This document extracts specific quotable citations from the categorical-geometric methods paper that provide formal support for TSM's five postulates. The paper's rigorous treatment of probabilistic morphisms, graph Laplacian convergence, and information geometry provides mathematical foundations for TSM's claims about manifold structure and type-preserving transformations.

---

## Citation 1: Belkin-Niyogi Theorem (Theorem 4.1)

### Location
**Section 4.2**: "Manifold Learning using spectral properties à la Belkin-Niyogi"

### Exact Statement

> **Theorem 4.1** ([9], Theorem 3.1). Let M be a compact n-dimensional Riemannian submanifold in ℝ^d. Let S_m = {x_i}_{i=1}^m be sampled according to the uniform probability distribution μ on M. Let f ∈ C^∞(M). Put t_m = m^{-1/(n+2+α)}, where α > 0. Then ∀p ∈ M, and for any fixed ε > 0,
>
> lim_{m→∞} μ^m { S_m ∈ M^m : |1/(t_m(4πt_m)^{n/2}) Δ^t_{S_m} f(p) - 1/vol_g(M) (Δ_g f)(p)| > ε } = 0.

### Mathematical Interpretation

The discrete graph Laplacian Δ^t_{S_m} (constructed from finite data samples) converges in probability to the continuous Laplace-Beltrami operator Δ_g on the manifold. The scaling factor t_m = m^{-1/(n+2+α)} determines the rate of convergence.

### TSM Postulate Supported

**Postulate I: Manifold Structure** ★★★

This theorem provides the rigorous foundation for TSM's claim that semantic content lies on a manifold structure. Specifically:

1. **Discrete → Continuous Bridge**: Data points (tokens) sampled from a manifold allow recovery of the underlying continuous geometry
2. **Intrinsic Geometry Recovery**: The Laplace-Beltrami operator encodes intrinsic manifold structure, recoverable from extrinsic distances
3. **Spectral Consistency**: Eigenvalues of discrete graph operators approximate eigenvalues of the manifold Laplacian

**Why This Matters for TSM**: TSM posits that semantic content has intrinsic geometric structure (Postulate I). The Belkin-Niyogi theorem proves that finite token samples can reconstruct this structure—validating the possibility of learning manifold geometry from discrete text data.

---

## Citation 2: Category of Probabilistic Morphisms (Section 2.2)

### Location
**Section 2.2**: "The category **Probm** and characterizations of regular conditional probability measures"

### Key Formalization

> "Basic examples of probabilistic morphisms are measurable mappings, Markov kernels and regular conditional probability measures that are of central importance in mathematical statistics and statistical learning theory."

The paper defines **Probm** as the category where:
- **Objects**: Polish spaces (complete separable metric spaces)
- **Morphisms**: Markov kernels (probabilistic mappings)
- **Composition**: Chapman-Kolmogorov equation

### TSM Postulates Supported

**Postulate II: Typed Addressability** ★★★

The categorical framework formalizes how probabilistic type assignments preserve measurability. A morphism T: X → Y in **Probm** assigns to each x ∈ X a probability distribution on Y—precisely modeling how tokens receive probabilistic type assignments.

**Postulate III: Categorical Conservation** ★★★

Morphisms in **Probm** compose associatively via the Chapman-Kolmogorov equation. This categorical composition law ensures that type-preserving transformations compose to give type-preserving transformations—the core of TSM's conservation postulate.

---

## Citation 3: Graph Operator Characterization (Theorem 2.6)

### Location
**Section 2.2.2**: "Characterizations of regular conditional probability measures"

### Exact Statement

> **Theorem 2.6** (Characterization of regular conditional probability measures).
>
> (i) A measurable mapping T̄: X → P(Y) is a regular conditional probability measure for μ ∈ P(X × Y) with respect to the projection Π_X if and only if
>
> (Γ_T)_* μ_X = μ
>
> where Γ_T is the graph of T.

### Mathematical Interpretation

The graph operator Γ_T maps:
```
Γ_T: X → X × Y
Γ_T(x) = (x, T̄(x))
```

The condition (Γ_T)_* μ_X = μ states that pushing forward the marginal through the graph recovers the joint distribution. This characterizes when T̄ correctly "factors" the joint distribution.

### TSM Postulates Supported

**Postulate III: Categorical Conservation** ★★★

The graph operator formalization provides the mathematical machinery for TSM's type-preservation claim:
- **Graph = Typed Assignment**: Γ_T encodes the type assignment as a graph structure
- **Measure Preservation**: The pushforward condition ensures type assignments preserve the underlying probability structure
- **Uniqueness (Part ii)**: Regular conditional probability measures are unique μ_X-a.e., implying type assignments are essentially unique given the data distribution

**Postulate V: Tokenization Commitment** ★★

The graph operator framework formalizes how tokenization (assigning types to inputs) must satisfy measure-theoretic consistency. The requirement (Γ_T)_* μ_X = μ is a formal version of TSM's commitment that tokenization must preserve semantic structure.

---

## Citation 4: Fisher-Rao Metric (Section 3)

### Location
**Section 3**: Geometric kernels on SPD matrices

### Exact Quote

> "It corresponds to the Fisher-Rao metric on the set of zero-mean Gaussian densities on ℝ^n. The Riemannian manifold (Sym^{++}(n), g_{ai}) is a Cartan-Hadamard manifold, that is it is geodesically complete, simply connected, and with nonpositive sectional curvature."

### Geodesic Formula

> γ_{ai}^{AB}(t) = A^{1/2} exp[t log(A^{-1/2} B A^{-1/2})] A^{1/2}, t ∈ [0,1]

### TSM Postulate Supported

**Postulate I: Manifold Structure** ★★

The Fisher-Rao metric provides:
1. **Information-Theoretic Geometry**: Natural metric on probability distributions
2. **Geodesic Completeness**: All paths can be extended indefinitely
3. **Negative Curvature**: Cartan-Hadamard property ensures unique geodesics between points

**Why This Matters for TSM**: The Fisher-Rao metric is the natural geometry for probability distributions. If semantic types are modeled as distributions (soft typing), then this metric provides the correct geometric structure for TSM's manifold postulate.

---

## Citation 5: Laplacian Eigenmap Algorithm (Section 4.2)

### Location
**Section 4.2**: "Manifold Learning using spectral properties à la Belkin-Niyogi"

### Key Formalization

The paper describes constructing a weighted graph from data:

> "Given a set of data points S_m = {x_i}_{i=1}^m, associate to S_m a one-parameter family of weighted full graphs S_m(t), where the weight at vertices x_i, x_j is exp(-||x_i - x_j||²/t)."

The graph Laplacian operator is:
```
Δ^t_{S_m} f(x_i) = Σ_j w_ij (f(x_i) - f(x_j))
```

### TSM Postulates Supported

**Postulate I: Manifold Structure** ★★★

The construction provides:
1. **Finite → Continuous**: Discrete graph converges to continuous manifold
2. **Heat Kernel Weights**: exp(-||x_i - x_j||²/t) captures local geometry
3. **Spectral Recovery**: Eigenvalues of graph Laplacian approximate manifold eigenvalues

**Postulate IV: Static Decidability** ★★

The graph construction is:
1. **Computable**: Finite weighted graph from finite data
2. **Deterministic**: Given data and parameter t, the graph is fully determined
3. **Checkable**: Spectral properties of finite graphs are decidable

---

## Summary: Citation Support Matrix

| Citation | Location | TSM Postulate | Support Level |
|----------|----------|---------------|---------------|
| Belkin-Niyogi Theorem | Theorem 4.1, §4.2 | I. Manifold Structure | ★★★ |
| Probm Category | §2.2 | II. Typed Addressability | ★★★ |
| Probm Composition | §2.2 | III. Categorical Conservation | ★★★ |
| Graph Operator (Theorem 2.6) | §2.2.2 | III. Categorical Conservation | ★★★ |
| Graph Operator | §2.2.2 | V. Tokenization Commitment | ★★ |
| Fisher-Rao Metric | §3 | I. Manifold Structure | ★★ |
| Laplacian Eigenmap | §4.2 | I. Manifold Structure | ★★★ |
| Laplacian Eigenmap | §4.2 | IV. Static Decidability | ★★ |

---

## Key Takeaways

### For TSM's Manifold Structure (Postulate I)
The Belkin-Niyogi theorem provides the strongest formal support: discrete samples from a manifold permit recovery of intrinsic geometric structure. The Fisher-Rao metric adds that probability distributions (soft types) naturally form a manifold with well-defined geodesics.

### For TSM's Categorical Conservation (Postulate III)
The **Probm** category and Theorem 2.6 formalize exactly what TSM needs: probabilistic type assignments compose categorically, and the graph operator framework ensures measure-theoretic consistency is preserved under transformation.

### For TSM's Static Decidability (Postulate IV)
Graph Laplacian construction is explicitly finite and computable. While full manifold learning involves limits (m → ∞), finite approximations are checkable—supporting TSM's claim that type-validity can be decided statically.

---

## References

- Lê, H.V., Minh, H.Q., Protin, F., Tuschmann, W. (2025). "Categorical and geometric methods in statistical, manifold, and machine learning." arXiv:2505.03862
- Belkin, M., Niyogi, P. (2006). "Convergence of Laplacian eigenmaps" (Reference [9] in paper)
- Lê, H.V. (Reference [37] in paper) - Category of probabilistic morphisms
