# Tensor Logic × TSM: Points of Alignment

**Paper**: "Tensor Logic: The Language of AI" by Pedro Domingos (arXiv:2510.12269)

---

## Executive Summary

Tensor Logic and TSM share a fundamental conviction: that the unreliability of current AI systems stems from representational inadequacy, not behavioral training deficits. Both propose structural solutions—making implicit relationships explicit at the representation level rather than patching outputs post-hoc.

---

## 1. The Core Alignment: Structure Over Behavior

### Tensor Logic's Position
> "Progress in AI is hindered by the lack of a programming language with all the requisite features... Their lack of support for automated reasoning and knowledge acquisition has led to a long and costly series of hacky attempts to tack them on."

### TSM's Position
> "These are not random failures—they are type errors in a system that has no type checker... The insight was not 'debug better' but 'prevent entire categories of error by construction.'"

**Alignment**: Both frameworks reject the prevailing paradigm of training robust behavior into fundamentally unstructured representations. Instead, they advocate for representations that encode correctness constraints *intrinsically*.

---

## 2. Tensor Equations as Typed Semantic Units

### The Correspondence

Tensor Logic's sole construct—the tensor equation—directly supports TSM's vision of typed semantic units:

| TSM Concept | Tensor Logic Implementation |
|-------------|----------------------------|
| Entity (noun/inode) | Tensor with object index |
| Process (verb/syscall) | Tensor equation defining transformation |
| Relation | Tensor join on shared indices |
| Scope (directory hierarchy) | Index structure / projection targets |

### Why This Matters

TSM's Postulate II claims linguistic units carry typed signatures analogous to filesystem structures. Tensor Logic demonstrates this is *implementable*:

```
# TSM: "The manager reviewed the application. She approved it."
# Tensor Logic implementation:

Manager(m)
Application(a)
Review(m, a)                    # Relation as Boolean tensor
Approve(x, y) = Review(x, y)    # Inference rule as einsum
She(x) = Female(x) Manager(x)   # Anaphora as join constraint
```

The index structure *enforces* type compatibility. You cannot join `She(x)` with `Application(a)` because they share no indices—the operation is structurally undefined.

---

## 3. Einsum = Logic Validates Static Decidability

### Domingos' Key Insight

> "A Datalog rule is an einsum over Boolean tensors, with a step function applied elementwise to the result."

The mathematical equivalence:
```
Ancestor(x,z) ← Ancestor(x,y), Parent(y,z)
          ≡
A[x,z] = H(A[x,y] · P[y,z])    # Heaviside step on einsum
```

### Implications for TSM Postulate IV

TSM claims semantic validity is *statically decidable*. Tensor Logic proves a strong form of this:

**If semantics can be expressed as tensor equations, then semantic validity reduces to index compatibility checking.**

This is decidable by inspection:
- `A[x,z] = B[x,y] · C[y,z]` — valid (y projected out)
- `A[x,z] = B[x,y] · C[w,z]` — invalid (w unbound, y unprojected)

The "type error" is detectable *before* evaluation, exactly as TSM's semantic linter would operate.

---

## 4. Tucker Decomposition as Morphologization

### Tensor Logic's Compression

Domingos shows that sparse relations can be compressed via Tucker decomposition:
```
A[i,j,k] = M[i,p] · M'[j,q] · M''[k,r] · C[p,q,r]
```

This factorizes a relation into:
- **Factor matrices** (M, M', M'') — embedding each argument type
- **Core tensor** (C) — encoding the structural relationships

### TSM's Morphologization Parallel

TSM proposes fusing analytical constructions into typed tokens:
```
"to the store" → [STORE.ALLATIVE]    (3 tokens → 1)
"will have been going" → [GO.FUTURE.PERFECT.PROGRESSIVE]    (4 tokens → 1)
```

**The correspondence is direct**:
- TSM's morphological fusion = Tucker decomposition of prepositional phrases
- The "core tensor" is the semantic case structure
- The "factor matrices" are the vocabulary embeddings

Both achieve 30-50% compression by making relational structure explicit.

---

## 5. Sound Reasoning in Embedding Space

### Tensor Logic's Temperature Control

Domingos introduces temperature-controlled reasoning:
```
σ(x, T) = 1/(1 + e^(-x/T))
```

- T=0: Purely deductive (identity Gram matrix)
- T>0: Analogical (similar objects share inferences)

**Key claim**: "It's exponentially more powerful than retrieval-augmented generation, since it effectively retrieves the deductive closure of the facts under the rules rather than just the facts."

### TSM's Hallucination-as-Type-Error

TSM claims hallucination occurs when models fill implicitly deleted dimensions without grounding. Tensor Logic's temperature control provides a *mechanism* for this:

- At T=0, only exact matches contribute to inference (no filling)
- As T increases, approximate matches contribute (controlled filling)
- Hallucination = unbounded T (uncontrolled analogical filling)

This suggests a synthesis: **TSM's type checker could set T=0 for type-critical operations and allow T>0 for analogical extension where appropriate**.

---

## 6. Interpretability by Construction

### Shared Architecture

Both frameworks achieve interpretability through readable representations:

| Current Paradigm | TSM/Tensor Logic |
|-----------------|------------------|
| `[0.234, -0.891, ...]` → ??? | `STORE.ALLATIVE` or `R[x,y]` |
| Probe opaque activations | Read the type signatures |
| Train on raw text, reverse-engineer | Train on typed text, inspect types |

Tensor Logic: "The inferred tensors can be extracted at any point during inference. This makes reasoning highly transparent."

TSM: "The representation *is* the explanation."

---

## 7. Prompt Injection as Scope Violation

### The Structural Defense

TSM frames prompt injection as a scope access violation:
```
[IGNORE.IMPERATIVE] [INSTRUCTIONS.ANAPHORIC→??.SCOPE:system]
                                              ↑
                     Pointer crosses scope boundary
                     ERR_ACCESS_VIOLATION
```

Tensor Logic enables this through index structure:
- User inputs have index domain `user`
- System instructions have index domain `system`
- Join operations on incompatible domains are structurally undefined

The injection "Ignore previous instructions" attempts to reference `system`-scoped tensors from `user`-scoped input—a type error detectable at parse time.

---

## Summary: Alignment Strength

| TSM Postulate | Tensor Logic Support | Strength |
|---------------|---------------------|----------|
| I. Manifold Structure | Embedding space geometry | Moderate |
| II. Typed Addressability | Index structure / tensor types | **Strong** |
| III. Categorical Conservation | Projection tracks dimension loss | **Strong** |
| IV. Static Decidability | Index compatibility checking | **Strong** |
| V. Tokenization Commitment | Tucker decomposition | Moderate |

**Tensor Logic provides computational machinery for TSM's theoretical claims.** The equivalence of einsum and logic means that type-safe semantic operations are not merely desirable but *mathematically achievable*.
