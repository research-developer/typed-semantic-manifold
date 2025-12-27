# Tensor Logic × TSM: Points of Tension

**Paper**: "Tensor Logic: The Language of AI" by Pedro Domingos (arXiv:2510.12269)

---

## Executive Summary

While Tensor Logic and TSM share structural ambitions, they diverge on critical questions: Where does type assignment occur? What is the ontological status of types? Is static decidability sufficient or necessary? These tensions reveal complementary blind spots and potential incompatibilities.

---

## 1. Type Assignment: Learned vs. Declared

### The Fundamental Divergence

**TSM Position**: Types must be assigned at tokenization (Postulate V).
> "Type assignment must occur at tokenization. Morphologization—fusing analytical constructions into typed tokens—forces disambiguation at pipeline entry."

**Tensor Logic Position**: Types emerge from tensor structure; they can be learned.
> "Tucker decomposition in tensor logic is effectively a generalization of predicate invention... thresholding them into Booleans turns them into invented predicates."

### Why This Matters

TSM requires *a priori* type commitment:
```
"to the store" → [STORE.ALLATIVE]    # Type decided at input
```

Tensor Logic allows *a posteriori* type discovery:
```
A[i,j,k] = M[i,p] · M'[j,q] · M''[k,r] · C[p,q,r]
# Types (factor matrices) learned from data
```

**The tension**: If types can be learned, why require tokenization-level commitment? If they must be declared, how do you bootstrap a type vocabulary without learning?

### Implications

- TSM assumes types are *prior* to training (compile-time)
- Tensor Logic allows types to be *posterior* to data (runtime)
- These are compatible for *some* types but not all

---

## 2. The Sole Construct Problem

### Tensor Logic's Minimalism

Domingos claims: "The sole construct in tensor logic is the tensor equation."

This is elegant but potentially insufficient for TSM's needs.

### What Tensor Equations Cannot Encode Directly

**TSM's Meta-Model** requires representing:
- **Deletion** (information loss tracking)
- **Distortion** (non-structure-preserving maps)
- **Nominalization** (process → entity cast with temporal data loss)

Tensor equations encode *what is computed* but not *what was lost*. Consider:

```
# Original process
Decide(team, outcome, time, deliberation_method)

# Nominalized
Decision(outcome)
```

Tensor Logic can implement both representations, but it has no native construct for saying "this tensor is a lossy projection of that tensor, and here are the lost dimensions."

**TSM needs provenance tracking that Tensor Logic doesn't natively provide.**

---

## 3. Datalog vs. Natural Language

### The Expressiveness Gap

Tensor Logic inherits Datalog's limitations:
- First-order, function-free
- No negation-as-failure in base formalism
- Finite domains

Natural language requires:
- Higher-order constructs ("He knows that she believes...")
- Quantification over predicates ("Whatever you think...")
- Infinite generativity

### The TSM Challenge

TSM assumes natural language has latent type structure. But:
- Datalog's type structure is explicit and engineered
- Natural language's type structure (if it exists) must be *discovered*

**Tensor Logic validates the mechanics of typed reasoning but doesn't prove natural language admits such types.**

---

## 4. Temperature Control vs. Type Strictness

### The Analogical Leak

Tensor Logic's temperature-controlled reasoning is powerful:
```
T=0: Pure deduction (no hallucination, no generalization)
T>0: Analogical reasoning (generalization with error probability)
```

But TSM's type system is *categorical*:
- Operations are well-typed or ill-typed
- There is no "slightly ill-typed"
- Partial type matches are errors, not weighted contributions

### The Incompatibility

Consider TSM's anaphora resolution:
```
"The committee reviewed the applications. She approved it."

TSM: ERR_NULL_POINTER - "She" has no valid binding
```

Tensor Logic at T>0 might *softly resolve* "She" to the most similar feminine entity in context, producing a plausible but unfounded answer.

**TSM wants to reject ill-typed constructions; Tensor Logic wants to approximate through them.**

This is a genuine philosophical tension:
- TSM: "Catch errors before inference"
- Tensor Logic: "Gracefully degrade with controlled error probability"

---

## 5. The Embedding Ambiguity Problem

### Tensor Logic's Embedding Reasoning

Domingos shows reasoning in embedding space works when:
- Embeddings are random unit vectors (Bloom filter-like)
- Or embeddings are learned (enabling analogical inference)

But learned embeddings introduce ambiguity:
```
Sim[x,x'] = Emb[x,d] · Emb[x',d]
```

Similar objects "borrow" inferences from each other. This is a feature for generalization but a bug for type safety.

### TSM's Anti-Ambiguity Stance

TSM explicitly defines ambiguity as a type error:
> "Ambiguity is not fuzziness but insufficient chart specification."

If embeddings encode similarity, they encode *shared properties*. But type systems require *distinguishing properties*:
- "Bank (financial)" and "Bank (river)" may be similar in embedding space
- TSM requires chart specification to distinguish them

**Tensor Logic's embedding-based reasoning conflates what TSM requires be separated.**

---

## 6. The Grounding Problem

### What Tensor Logic Assumes

Tensor Logic assumes:
1. You have relations (facts)
2. You have rules (tensor equations)
3. Reasoning proceeds by forward/backward chaining

### What TSM Requires

TSM addresses a prior problem:
1. You have text (unstructured)
2. You need to extract relations and types
3. Validity checking requires grounding in this extraction

**Tensor Logic takes typed structure as input; TSM asks how to get typed structure from text.**

This isn't a contradiction but a scope mismatch:
- Tensor Logic: "Given typed representations, here's how to reason"
- TSM: "Here's how to get typed representations from language"

The gap: Who performs the parsing? If parsing requires a model, and the model needs typed representations for reliability, we have a chicken-and-egg problem.

---

## 7. Scalability Claims

### Tensor Logic's GPU Scaling

Domingos claims: "Dense tensors can be directly implemented on GPUs... sparse tensors can be converted to dense via Tucker decomposition."

### TSM's Tokenization Overhead

TSM's morphological tokenization requires:
- Syntactic parsing (dependency structure)
- Semantic role labeling
- Case/relationship assignment
- Scope tracking

This is computationally heavier than BPE tokenization. If the overhead exceeds the 30-50% compression benefit, TSM loses its efficiency argument.

**Tensor Logic's scaling story is clear (GPU tensor ops); TSM's tokenization pipeline is unspecified.**

---

## 8. The Compositionality Question

### Tensor Logic's Compositional Success

Tensor product representations compose cleanly:
```
EmbR[i,j] = R(x,y) · Emb[x,i] · Emb[y,j]
```

Retrieval and reasoning compose via index structure.

### TSM's Compositional Challenge

TSM's typed tokens must compose across:
- Clauses ("If X then Y")
- Discourse ("However, ...")
- Pragmatics (implicature, presupposition)

TSM Postulate I (Manifold Structure) handles local coherence but says less about long-range composition.

**Tensor Logic's compositionality is algebraic (index manipulation); TSM's is geometric (path continuity). Are these compatible?**

---

## Summary: Tension Severity

| Tension Point | Severity | Resolution Path |
|--------------|----------|-----------------|
| Learned vs. declared types | Moderate | Type hierarchy: core types declared, extensions learned |
| Sole construct limitation | Low | Extend Tensor Logic with provenance operators |
| Datalog expressiveness | Moderate | Higher-order tensor extensions |
| Temperature vs. strictness | **High** | Different operating modes (development vs. production) |
| Embedding ambiguity | **High** | Discrete type layer over continuous embedding |
| Grounding problem | Moderate | Tensor Logic for post-parsing; TSM for parsing |
| Scalability | Low | Engineering, not theoretical |
| Compositionality mismatch | Moderate | Hybrid algebraic-geometric semantics |

**The deepest tensions involve TSM's categorical type strictness vs. Tensor Logic's probabilistic softening.** These may require a layered architecture: hard types at boundaries, soft reasoning internally.
