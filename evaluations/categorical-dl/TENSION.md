# Tension Analysis: Categorical Deep Learning and TSM Theory

**Paper**: Gavranović et al. "Categorical Deep Learning is an Algebraic Theory of All Architectures" (arXiv:2402.15332v2)

**Evaluation Date**: 2025-12-26

---

## Executive Summary

While CDL provides strong theoretical foundations, significant tensions exist between its abstract algebraic framework and TSM's concrete linguistic commitments. The primary conflict: CDL is **architecture-agnostic** while TSM is **domain-specific**. CDL's generality is both a strength (wide applicability) and a limitation (no guidance on which monad to use for semantics).

---

## 1. Abstraction Level Mismatch

### CDL's Position

CDL operates at **maximum generality**:

```
"We give a unified theory of all neural network architectures"
Objects: Any category C (Set, Vect, Meas, ...)
Morphisms: Para(C) parametric maps
Structure: Any monad T
```

The paper is deliberately agnostic about:
- Which specific monad captures language
- What the base category should be
- How constraints arise from data

### TSM's Position

TSM operates with **concrete commitments**:

```
Types: {Entity, Process, Relation, Quantity, ...}
Base category: Measurable spaces (for probability)
Specific constraint: Type preservation under transformation
```

### The Tension

| Aspect | CDL | TSM | Conflict |
|--------|-----|-----|----------|
| Specificity | Any monad | Semantic type monad | CDL doesn't say which |
| Base category | Any C | Meas (measurable) | CDL allows too much |
| Domain | All architectures | NLP/semantic validation | CDL is broader |
| Derivation | Assumed constraints | Constraints from data | Methodological gap |

**Core Problem**: CDL provides the **form** of a solution (monad algebras preserve structure) but not the **content** (what monad captures semantics). TSM needs specific instantiation.

---

## 2. The "Which Monad?" Problem

### CDL's Framework

CDL shows that **given** a monad T, algebra homomorphisms preserve T-structure. But it doesn't address:
- How to discover T from data
- Whether T is unique or learnable
- What makes one monad better than another for semantics

### TSM's Need

TSM requires a **specific** semantic monad SemT where:

```
SemT-algebras = typed semantic units
SemT-homomorphisms = type-preserving transformations
```

But TSM doesn't yet formally specify SemT.

### The Tension

This creates a **chicken-and-egg problem**:
- CDL says: "If you have a monad, here's how to work with it"
- TSM says: "Here are the types, but what's the monad?"

Neither paper provides:
1. A procedure to derive SemT from linguistic data
2. Proof that TSM's types form a monad
3. Evidence that this monad is unique/canonical

---

## 3. Discrete Types vs. Continuous Parameters

### CDL's Framework

CDL's Para(C) construction assumes:
- **Continuous** parameter spaces (for gradient descent)
- Smooth composition of parametric maps
- Differentiable structure throughout

### TSM's Framework

TSM's type system is fundamentally **discrete**:

```
Type = {Entity, Process, Relation, Quantity, ...}
Type assignment τ: X → Type is a partition
Type compatibility is a finite relation
```

### The Tension

| Aspect | CDL | TSM | Conflict |
|--------|-----|-----|----------|
| Type space | Continuous P | Discrete Type | Fundamental incompatibility |
| Optimization | Gradient descent on P | Discrete type inference | Different optimization regimes |
| Composition | Smooth | Combinatorial | Different mathematical structure |

**Problem**: CDL's machinery assumes smooth structure for training. TSM's discrete types don't admit gradients. Bridging requires either:
- Softening TSM types to distributions (losing crispness)
- Restricting CDL to discrete parameter spaces (losing training)

---

## 4. Universal vs. Language-Specific

### CDL's Position

CDL claims **universality**:

```
"An algebraic theory of ALL architectures" (title)
Valid for: CNNs, RNNs, Transformers, GNNs, ...
Independent of: Domain, language, modality
```

### TSM's Position

TSM makes **language-specific** claims:

```
Types derived from: Case morphology (ALLATIVE, LOCATIVE, ...)
Linguistic structures: Nominal, verbal, prepositional
Cultural/grammatical patterns: Language-dependent variation
```

### The Tension

| Aspect | CDL | TSM | Conflict |
|--------|-----|-----|----------|
| Scope | All domains | Natural language | TSM is narrower |
| Types | Mathematical | Linguistic | Different ontologies |
| Variation | Architecture-dependent | Language-dependent | Different sources of variation |
| Universality | Category-theoretic | Linguistic (claimed) | Different universal claims |

**Problem**: CDL's universality comes from abstraction away from domain. TSM's claims depend on linguistic specifics. These pull in opposite directions—CDL loses linguistic detail, TSM loses architectural generality.

---

## 5. Constructive vs. Existential

### CDL's Position

CDL provides **existential** results:

```
"There exists a monad capturing this constraint"
"The algebra structure provides..."
"Universal properties guarantee..."
```

These are non-constructive—they prove existence without construction.

### TSM's Need

TSM requires **constructive** methods:

```
Given text, compute types
Given types, check preservation
Given violation, generate correction
```

### The Tension

| Aspect | CDL | TSM | Conflict |
|--------|-----|-----|----------|
| Existence proofs | ✓ Strong | Insufficient | Need constructive versions |
| Algorithms | Not provided | Required | Implementation gap |
| Complexity bounds | Not analyzed | Need polynomial | Feasibility unknown |
| Learning procedures | Theoretical | Practical | Different concerns |

**Problem**: CDL proves that structure exists categorically. TSM needs algorithms that compute this structure. The gap between "exists" and "computable" is significant.

---

## 6. Static vs. Dynamic Semantics

### CDL's Framework

CDL's algebras are **static** structures:

```
(A, α: TA → A) is a fixed structure
Homomorphisms preserve this fixed structure
No notion of structure changing over time
```

### TSM's Framework

TSM must handle **dynamic** semantics:

```
Discourse evolves: types depend on context history
Ambiguity resolution: types sharpen with context
Learning: type system updates with experience
```

### The Tension

| Aspect | CDL | TSM | Conflict |
|--------|-----|-----|----------|
| Structure | Fixed | Evolving | TSM needs dynamic types |
| Context | Parameter (static) | Discourse (dynamic) | Different treatment of context |
| Learning | Weight updates | Type updates | Different what's learned |
| Time | Implicit | Explicit | Different handling of dynamics |

**Problem**: CDL's coalgebras (Section 6) capture state, but as fixed transition systems. TSM needs the state space itself to evolve—types can be refined, extended, or revised during discourse. CDL doesn't address this meta-level dynamism.

---

## 7. Interpretation of Constraints

### CDL's Position

CDL treats constraints as **architectural**:

```
Constraint = property architecture must satisfy
Example: Equivariance, weight sharing, recurrence
Enforcement: By construction (architecture design)
```

### TSM's Position

TSM treats constraints as **semantic**:

```
Constraint = property meaning must satisfy
Example: Type preservation, dimensional conservation
Enforcement: By validation (type checking)
```

### The Tension

| Aspect | CDL | TSM | Conflict |
|--------|-----|-----|----------|
| Constraint source | Architecture design | Semantic requirements | Different origins |
| Enforcement time | Construction time | Validation time | Different phases |
| Violation handling | Impossible (by design) | Error + recovery | Different failure modes |
| Flexibility | Fixed once built | Checked at runtime | Different rigidity |

**Problem**: CDL's constraints are "baked in" at architecture design time. TSM's constraints are "checked" at inference time. These represent fundamentally different approaches to ensuring validity.

---

## 8. The Grounding Problem

### CDL's Framework

CDL assumes symbols are **given**:

```
Objects of C are primitive
Types are sets (or objects of a category)
No account of how symbols get meaning
```

### TSM's Framework

TSM must address **grounding**:

```
Tokens → Types requires interpretation
Types → Semantics requires grounding
Meaning emerges from use patterns
```

### The Tension

CDL is purely **syntactic**—it describes structure without addressing how structure connects to meaning. TSM's whole point is this connection.

| Aspect | CDL | TSM | Conflict |
|--------|-----|-----|----------|
| Symbol meaning | Assumed | Derived | Different starting points |
| Reference | Not addressed | Central concern | Major gap |
| Use patterns | Not considered | Constitutive | Different methodology |
| Embodiment | Abstract | Requires grounding | Philosophical gap |

---

## 9. Summary of Tensions

### Fundamental Tensions (Hard to Resolve)

1. **Abstraction level**: CDL's generality vs. TSM's specificity
2. **Discrete vs. continuous**: TSM's crisp types vs. CDL's smooth parameters
3. **Grounding**: CDL's syntactic vs. TSM's semantic orientation

### Methodological Tensions (Resolvable with Work)

4. **Which monad?**: Need specific instantiation for semantics
5. **Constructive methods**: Need algorithms, not just existence proofs
6. **Dynamic semantics**: Need evolving type structures

### Surface Tensions (Mostly Notational)

7. **Vocabulary**: Mathematical vs. linguistic terminology
8. **Examples**: Architecture-focused vs. language-focused

---

## 10. Implications for Integration

To integrate CDL and TSM, one must:

1. **Choose a monad**: Define SemT specifically (not generically)
2. **Bridge discrete/continuous**: Either soft types or discrete Para
3. **Construct algorithms**: Convert existence proofs to procedures
4. **Address grounding**: Connect categorical structure to meaning
5. **Handle dynamics**: Extend to evolving type structures

The tensions are significant but not fatal. CDL provides the **categorical skeleton**; TSM must provide the **semantic flesh**. Neither alone is complete, but together they might form a coherent theory.

---

## References

- Gavranović et al. (2024). arXiv:2402.15332v2
- Prior TSM evaluations: categorical-methods/*.md
- Lawvere (1963). Functorial Semantics (constructive vs. existential)
- Wittgenstein (1953). Meaning as use (grounding problem)
