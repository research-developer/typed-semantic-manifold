# Tensor Logic Citations for TSM

**Source**: Domingos, P. (2025). "Tensor Logic: The Language of AI." arXiv:2510.12269v3

---

## Citation 1: Einsum = Logic (Core Equivalence)

**Section**: 3.1 Representation

**Quote**:
> "A Datalog rule is an einsum over Boolean tensors, with a step function applied elementwise to the result. (Specifically, the Heaviside step function, H(x)=1 if x>0 and 0 otherwise.)"

**Formalization**:
```
A_xz = H(S_xy P_yz) = H(∑_y S_xy P_yz)
```

**TSM Support**: **Postulate IV (Static Decidability)**

**Relevance**: This proves that logical validity checking reduces to tensor index compatibility checking. If semantic operations can be expressed as tensor equations, then validity is decidable by inspecting whether indices balance (shared indices get projected out, LHS indices appear in RHS). Type errors become dimension mismatches—detectable before evaluation.

---

## Citation 2: Index Compatibility as Type Checking

**Section**: 3.1 Representation

**Quote**:
> "The projection is onto the indices on the LHS."

**Formalization**:
```
(U ⨝ V)_αβγ = U_αβ V_βγ

where α is the subset of U's dimensions not in V and similarly for γ and V.
```

**Quote** (Tensor Join Definition):
> "The join of two tensors U and V along a common set of indices β is (U ⨝ V)_αβγ = U_αβ V_βγ... If the tensors are Boolean, tensor join reduces to database join."

**TSM Support**: **Postulate IV (Static Decidability)** + **Postulate II (Typed Addressability)**

**Relevance**: Operations are well-defined only when indices match. Two tensors with no shared indices → Kronecker product; tensors with mismatched indices → structurally undefined operation. This is exactly TSM's type checking: operations that attempt to cross incompatible type boundaries are structurally impossible.

---

## Citation 3: Temperature-Controlled Reasoning

**Section**: 5 Reasoning in Embedding Space

**Quote**:
> "If we apply a sigmoid to each equation, σ(x,T) = 1/(1+e^{-x/T}), setting its temperature parameter T to 0 effectively reduces the Gram matrix to the identity matrix, making the program's reasoning purely deductive. This contrasts with LLMs, which may hallucinate even at T=0."

**Formalization**:
```
σ(x, T) = 1/(1 + e^{-x/T})

T=0: Gram matrix → Identity (pure deduction)
T>0: Analogical reasoning with controlled error
```

**TSM Support**: **Postulate IV (Static Decidability)** + **Postulate III (Categorical Conservation)**

**Relevance**: At T=0, only exact type matches contribute to inference—no analogical "filling." This provides the mechanism for TSM's hallucination prevention: type-critical operations run at T=0, ensuring only grounded inferences reach outputs. Temperature bounds the degree of analogical extension.

---

## Citation 4: Sound Reasoning in Embedding Space

**Section**: 5 Reasoning in Embedding Space

**Quote**:
> "It's also exponentially more powerful than retrieval-augmented generation, since it effectively retrieves the deductive closure of the facts under the rules rather than just the facts."

**Quote** (Transparency):
> "The inferred tensors can be extracted at any point during inference. This makes reasoning highly transparent, in contrast with LLM-based reasoning models. It's also highly reliable and immune to hallucinations at sufficiently low temperature."

**TSM Support**: **Postulate I (Manifold Structure)** + **Postulate IV (Static Decidability)**

**Relevance**: TSM claims interpretability through representation. Tensor Logic proves this is achievable: the tensor structure *is* the reasoning trace. No post-hoc probing required—types are readable.

---

## Citation 5: Tucker Decomposition as Compression

**Section**: 2.2 Tensor Algebra + 5 Reasoning in Embedding Space

**Quote**:
> "The Tucker decomposition decomposes a tensor into a more compact core tensor of the same rank and k factor matrices, each expanding an index of the core tensor into an index of the original one."

**Formalization**:
```
A_ijk = M_ip M'_jq M''_kr C_pqr

where C is the core tensor and the M's are the factor matrices.
```

**Quote** (Predicate Invention):
> "Some ILP systems can also do predicate invention, i.e., discover relations that do not appear explicitly in the data, akin to hidden variables in neural networks."

**TSM Support**: **Postulate V (Tokenization Commitment)**

**Relevance**: Tucker decomposition parallels TSM's morphologization—fusing analytical constructions into typed tokens. The core tensor encodes semantic case structure; factor matrices are vocabulary embeddings. Both achieve compression by making relational structure explicit.

---

## Citation 6: Relation = Sparse Boolean Tensor

**Section**: 3.1 Representation

**Quote**:
> "A relation is a compact representation of a sparse Boolean tensor... a sparse Boolean tensor of rank n can be compactly represented by an n-ary relation with a tuple for each nonzero element, and the efficiency gain will typically increase exponentially with n."

**TSM Support**: **Postulate II (Typed Addressability)**

**Relevance**: This establishes the bijection between typed relations and tensor structure. TSM's typed tokens (entities, processes, relations) map directly to tensor indices and ranks. The type signature determines tensor shape.

---

## Citation 7: Learned Embeddings Enable Analogical Reasoning

**Section**: 5 Reasoning in Embedding Space

**Quote**:
> "The product of the embedding matrix and its transpose, Sim[x,x'] = Emb[x,d] Emb[x',d], is now the Gram matrix measuring the similarity of each pair of objects by the dot product of their embeddings. Similar objects 'borrow' inferences from each other, with weight proportional to their similarity."

**Quote** (Temperature Gradient):
> "Increasing the temperature makes reasoning increasingly analogical, with examples that are less and less similar borrowing inferences from each other. The optimal T will depend on the application, and can be different for different rules."

**TSM Support**: **Postulate I (Manifold Structure)** — but with tension

**Relevance**: This supports TSM's manifold geometry (similar meanings are nearby), but creates tension with TSM's anti-ambiguity stance. Embeddings conflate what types must distinguish. Resolution: discrete type layer over continuous embedding space.

---

## Citation 8: Sole Construct Minimalism

**Section**: Abstract + 3.1 Representation

**Quote**:
> "The sole construct in tensor logic is the tensor equation, based on the observation that logical rules and Einstein summation are essentially the same operation, and all else can be reduced to them."

**Quote**:
> "This is the entire definition of tensor logic. There are no keywords, other constructs, etc."

**TSM Support**: **Postulate II (Typed Addressability)**

**Relevance**: The minimalism enables TSM's meta-model. If all operations are tensor equations, then all type checking is index checking. However, Tensor Logic lacks native provenance tracking (deletion, distortion)—TSM's extension is needed.

---

## Summary Table

| Citation | Section | TSM Postulate(s) | Support Strength |
|----------|---------|------------------|------------------|
| Einsum = Logic | 3.1 | IV: Static Decidability | **Strong** |
| Index Compatibility | 3.1 | II + IV | **Strong** |
| Temperature Control | 5 | III + IV | **Strong** |
| Sound Reasoning | 5 | I + IV | **Strong** |
| Tucker Decomposition | 2.2 + 5 | V: Tokenization | Moderate |
| Relation = Tensor | 3.1 | II: Typed Addressability | **Strong** |
| Learned Embeddings | 5 | I: Manifold (with tension) | Moderate |
| Sole Construct | Abstract + 3.1 | II: Typed Addressability | Moderate |

---

## Key Formalizations for TSM Implementation

### 1. Type Checking as Index Compatibility

```
VALID:   A[x,z] = B[x,y] · C[y,z]    ✓ (y projected out)
INVALID: A[x,z] = B[x,y] · C[w,z]    ✗ (w unbound)
INVALID: A[x,z] = B[x,y] · C[y]      ✗ (y unprojected, rank mismatch)
```

### 2. Temperature-Bounded Deduction

```
T = 0:  σ(x, 0) → step function → Gram = Identity → Pure deduction
T > 0:  σ(x, T) → smooth sigmoid → Gram ≠ Identity → Analogical
```

### 3. Embedding with Type Boundaries

```
# Embedding space (continuous similarity)
Sim[x,x'] = Emb[x,d] · Emb[x',d]

# Type layer (discrete categories)
TypeMatch[x,x'] = Type[x,t] · Type[x',t]  # Boolean

# Combined: analog within type, blocked across types
Inference[x,x'] = Sim[x,x'] · TypeMatch[x,x']
```
