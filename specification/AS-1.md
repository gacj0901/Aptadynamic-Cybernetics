# Aptadynamic Cybernetics Specification
## AS-1, Version 1.0

**Author:** G.A.C.J. — ORCID 0009-0009-5649-1359
**Brand / Program:** AptadynamiK
**Discipline:** Aptadynamic Cybernetics
**Status:** Normative. This document defines what any implementation must satisfy to be called *aptadynamic*. It supersedes all prior specification drafts, which are retained as historical material only.

**References (non-normative):**
- *Systemic Foundation* — the program's conceptual technical reference. Source of the framework's vocabulary and principles.
- *Logical–Mathematical Corpus* — the formal reference. Full axiomatization, theorems, and proofs. DOI: 10.5281/zenodo.20369325.
- *Aptadynamic-Electrical-Grid* — the reference implementation and first empirical validation (BPA 1999–2017; NYISO 2008–2021).

Neither reference is required to implement this specification. They are required to *extend* it.

**Conformance language.** The key words MUST, MUST NOT, SHOULD, and MAY are to be interpreted as in RFC 2119.

---

# 1. Purpose

Aptadynamics is the study of structural viability: the capacity of a system to keep being what it is while everything around it — and within it — varies. This specification defines the **PRAMA Protokol** (short form: *the Protokol*), a domain-independent method for evaluating the structural viability of any system from its observable behavior alone.

The Protokol answers one question: **is this system sustaining itself, or merely appearing to?** A system may operate normally — produce output, meet demand, show no visible fault — while continuously consuming the structural margin that makes its operation possible. The Protokol detects this condition, called *latent collapse*, before it manifests as visible failure.

The claim of the framework is universality: the same evaluation kernel, unmodified, applies to an electrical grid, an institution, a market, an organism, or a conversation. Only the way each domain is *observed* changes. This claim is not rhetorical; it is an architectural constraint (§4) with a defined empirical test (§8).

---

# 2. Core Principles

These eight principles constitute the framework. An implementation that violates any of them is not aptadynamic, whatever else it computes. Each principle is normative here; its formal statement and proof context live in the Corpus.

**P1 — Single viability condition.**
Viability is a property of trajectories, not states. A system is structurally viable at time *t* if and only if its accumulated tension remains below its endogenous threshold:

> Ξ(t) ≤ Θ(λ(t))

Every regime classification, alert, and diagnostic MUST derive from this condition. There is no second criterion.

**P2 — History is never erased (non-Markovian memory).**
Structural cost that is not paid does not disappear; it is displaced onto the future. The tension accumulator MUST integrate past decoupling through a causal memory kernel:

> Ξ(t) = ∫₀ᵗ K(t−τ) Δ(τ) dτ,  K causal, K ≥ 0

Memoryless (Markovian) evaluation is expressly non-conformant. *Empirical signature:* on BPA data, the memory-bearing accumulator discriminated conditional severity at ratio 16.0 where the best strictly causal Markovian baseline reached 3.16.

**P3 — The threshold contracts with history (endogeneity).**
What a system can tolerate is not fixed: past excess reduces future absorption capacity. The threshold Θ MUST be an increasing function of historical permissivity λ(t), and λ MUST be eroded by accumulated excess (Ξ−Θ)⁺. Fixed numeric thresholds (e.g. 0.75 / 0.50 / 0.25) are the negation of this principle and MUST NOT be used.

**P4 — Asymmetric recovery (non-reincarnation).**
Permissivity may recover; accumulation never does. Recovery dynamics MUST satisfy:

> dλ/dt ≤ r(λ_eq − λ),  with ∂Ξ/∂λ = 0

Recovery MUST NOT modify, discount, or reset the accumulated tension Ξ.

**P5 — Decoupling, never raw activity.**
The framework measures a system's deviation from *its own causally expected behavior*, never the raw amplitude of its activity:

> Δ(t) = |ω(t) − ω̂(t)| / (ω̂(t) + 1),  ω̂(t) = E[ω(t) | past only]

A Δ that correlates strongly with raw activity has degenerated and invalidates the study (§8). *Empirical signature:* on NYISO data, a degenerate intensity-based Δ produced ratio 0.55 (failure); genuine causal decoupling produced ratio 1.90 — same kernel, unchanged. The failure belonged to the observation, not the kernel. This episode is the operational proof that P5 is not optional.

**P6 — Latent collapse: operation is not persistence.**
The most dangerous phase of a system's life is the one in which it still functions while consuming what makes its functioning possible. Latent collapse is defined by the simultaneous conditions:

> σ_op(t) = 1  ∧  M(t) ≥ 0  ∧  G(t) < 0

(operational, margin still positive, margin generation negative). Implementations MUST compute and expose this condition. *Empirical signature:* inside latent-collapse periods on BPA data, P(severe cascade) = 0.091 vs 0.006 outside.

**P7 — Kernel / observation separation (universality).**
The protocol is the composition

> Domain 𝒟 → O_𝒟 → Ω → π → Γ

Exactly one component, the observation interface O_𝒟, depends on the domain. The projection kernel π MUST be mathematically identical across all domains and MUST NOT contain any domain knowledge — no topology, no mechanism, no causal model of the phenomenon. Domain adaptation happens exclusively in O_𝒟.

**P8 — Discarding is constitutive (development frontier).**
Persistence is not retaining everything; it is discarding what would prevent continued being. The Corpus proves (no-go theorem) that under long memory no fixed-rate forgetting stabilizes the accumulator: discarding must eventually become a dynamic field α(t), not a parameter. Current conformant implementations realize P8 only as fixed kernel decay. Dynamic prescindence is the declared development frontier of the framework (Corpus, Conjecture C1); implementations MAY explore it and MUST NOT claim it as validated.

---

# 3. The Aptadynamic Coordinates

The kernel projects any observable stream onto six coordinates:

> Γ(t) = (Δ, Ξ, λ, Θ, M, G)

| Coordinate | Name | Meaning |
|---|---|---|
| Δ(t) | Structural decoupling | Instantaneous deviation from the system's own causally expected behavior (P5). |
| Ξ(t) | Tension accumulator | Historically weighted integral of decoupling; the system's unpaid structural debt (P2). |
| λ(t) | Historical permissivity | Remaining absorption capacity; eroded by excess, recoverable but never at the expense of Ξ (P3, P4). |
| Θ(λ) | Endogenous threshold | The viability frontier; contracts as history accumulates (P3). |
| M(t) | Viability margin | Θ(λ) − Ξ. Distance to the frontier. |
| G(t) | Margin generation power | D⁺M (upper Dini derivative). Whether margin is being produced or consumed. |

**Semantic invariance.** Because π is universal (P7), the meaning of Γ is identical in every domain. "M is shrinking while operation looks normal" means the same thing for a power grid and for an institution.

---

# 4. Engine Architecture

A conformant implementation — a **PRAMA Protokol Engine** — consists of four separable components:

```
┌─────────────────────────────────────────────────────┐
│                PRAMA Protokol Engine                │
│                                                     │
│  Observation Interface (O_𝒟)   ← the ONLY domain-   │
│    raw measurements → normalized  specific part     │
│    causal observables Ω                             │
│                                                     │
│  Reference Kernel (π)          ← universal, fixed,  │
│    Ω → Γ = (Δ,Ξ,λ,Θ,M,G)         identical across   │
│                                   domains           │
│                                                     │
│  Runtime Engine                ← orchestration:     │
│    ingest → omega → projection    streaming,        │
│    → regimes → alerts             batching, replay  │
│                                                     │
│  Compliance Module             ← verification that  │
│    conformance checks, study      P1–P7 hold in     │
│    discipline, audit records      this deployment   │
└─────────────────────────────────────────────────────┘
```

**Separation requirement.** The code path that computes Γ MUST have no read access to domain-internal state; its input closure MUST be a subset of Ω. This makes P7 mechanically auditable rather than declared.

---

# 5. Observation Interface Contract

An observation interface O_𝒟 is conformant if and only if it satisfies all of the following. These conditions were not designed a priori; they were extracted from what empirical validation showed to be necessary.

**C1 — Strict observability.** Only externally observable events enter the protocol. No hidden state, no internal variables, no mechanism assumptions. Input is a temporally ordered stream Ω = {ω_t}.

**C2 — Strict causality.** The expectation ω̂(t) MUST depend exclusively on the strict past of the stream. Truncating the stream at *t* MUST leave every ω̂(s), s ≤ t, unchanged. Any predictor, normalization, or running scale that touches the future is non-conformant — including baselines used for comparison.

**C3 — Genuine decoupling.** Δ MUST measure deviation from causal self-expectation (P5), never normalized activity. Degeneration is detectable: if the correlation |corr(Δ_t, ω_t)| approaches 1, Δ has collapsed into activity and the study is invalid.

**C4 — Scale invariance.** Raw measurements MUST pass through an explicit normalization making the observable stream dimensionless, such that rescaling all raw inputs by any constant c > 0 leaves the Γ-trajectory unchanged, with no re-tuning of threshold parameters.

**C5 — No retro-fitting.** Kernel parameters MUST be fixed across domains. Per-domain adjustment targets the fidelity of O_𝒟 only. Parameters MUST NOT be tuned against outcome labels, and negative results MUST be reported as found. If O_𝒟 is revised after outcome exposure, the revised study MUST be labeled as a new study citing the superseded one; silent replacement is prohibited.

---

# 6. Regimes and Alerts

Regime stratification is defined on the (M, G) plane — position relative to the frontier, and direction of travel:

| Regime | Condition (informal) | Reading |
|---|---|---|
| **S₁ — Viable** | Ample margin, margin sustained or growing | The system pays its cost and regenerates. |
| **S₂ — Tension** | Margin positive but under pressure | Perturbation is being absorbed at increasing cost. |
| **S₃ — Critical** | Margin thin and being consumed | Correction is still possible; the window is closing. |
| **S₄ — Collapse** | Margin exhausted (M < 0) | The viability condition (P1) is violated. |

**Latent-collapse alert.** Orthogonal to stratification, the condition of P6 (operational ∧ M ≥ 0 ∧ G < 0) MUST be continuously evaluated and exposed. It is the framework's distinctive early signal: the system looks fine and is not.

Regime boundaries are functions of (M, G) and therefore inherit the endogeneity of Θ; they are never fixed cutoffs on a synthetic score (P3).

---

# 7. What the Kernel Never Does

For clarity of scope, a conformant kernel:

- does **not** model the phenomenon (no physics, no topology, no propagation mechanism);
- does **not** forecast event occurrence — empirically, short-horizon occurrence forecasting remains better served by Markovian baselines; the Protokol's contribution is *conditional severity* and *latent-state detection*;
- does **not** produce point predictions of collapse time; it measures distance to, and consumption rate of, the viability frontier;
- does **not** interpret. Γ is a measurement space. Domain meaning is reconstructed on the far side of the projection, by the domain expert.

Claiming more than this on behalf of the framework is non-conformant communication.

---

# 8. Compliance and the Universality Test

**Conformance of an implementation.** An implementation is Protokol-conformant when: (i) its kernel satisfies P1–P7 and §4's separation requirement; (ii) its observation interface satisfies C1–C5; (iii) it ships a compliance module able to demonstrate both mechanically (dependency audit, causality truncation test, degeneration statistic, rescaling test).

**Conformance of a study.** A domain study is conformant when it was executed under C5 discipline: interface declared before outcome exposure, parameters frozen, negative results retained. Conformance is a property of a *study*, not only of a codebase — the same engine can yield conformant and non-conformant studies.

**The universality claim and its test.** Each new domain study runs the *identical* kernel behind a newly written observation interface. Every conformant study that discriminates adds evidence of universality; a conformant study that fails to discriminate — where the interface passed all checks and the data was informationally sufficient — is evidence *against* the framework, and MUST be published as such. The framework stakes its credibility on this asymmetry being real.

**Current evidential status (July 2026).** One validated domain (electrical transmission: BPA confirmatory-grade discrimination at ratio 16.0; NYISO 1.90 after interface correction, both above permutation nulls). The NYISO failure-and-correction episode is part of the public record by design: it demonstrates that the kernel/observation separation localizes failure where the architecture says it should. Studies predating this specification are classified *exploratory*; the first fully disciplined multi-domain study is the program's declared next milestone.

---

# 9. Terminology

Public materials of the program use the following canonical terms. The complete conceptual mapping is maintained in the program's *Translation Glossary* (Systemic Foundation → technical terminology).

| Canonical term | Refers to |
|---|---|
| **AptadynamiK** | The brand / umbrella program. May host future programs, protocols, or technologies beyond the PRAMA Protokol. |
| **Aptadynamic Cybernetics** | The scientific discipline: the study of structural viability in observable systems. Comprises the Systemic Foundation, the Logical–Mathematical Corpus, this specification, and the PRAMA Protokol. |
| **Aptadynamics / aptadynamic** | The framework of structural viability (adjective for all technical artifacts). |
| **Systemic Foundation** | The discipline's conceptual technical reference. |
| **PRAMA Protokol** | The discipline's operational protocol, specified by this document. Comprises the Engine, the Observation Interfaces, the Domain Implementations, and the Validation Studies. |
| **PRAMA Protokol Engine** | A conformant implementation (§4). |
| **Structural decoupling, tension accumulator, historical permissivity, endogenous threshold, viability margin, margin generation** | The six coordinates of Γ (§3). |
| **Latent collapse** | The condition of P6. |
| **Structural pruning / dynamic prescindence** | The P8 operation; its dynamic form is the development frontier. |

**Denomination rule.** The protocol is always referred to as **PRAMA Protokol** in full; the admissible short form is **the Protokol**. The token "PRAMA" MUST NOT be used in isolation in any public material of the program.

---

# 10. Versioning and Change Control

- This specification is versioned AS-*n*. Breaking changes to P1–P8, Γ, or C1–C5 increment *n*.
- The Reference Kernel is versioned independently and semantically; a study record MUST cite both the specification version and the kernel version it ran.
- Amendments follow the C5 discipline: no silent replacement, superseded versions remain public.

---

*Aptadynamic Cybernetics Specification AS-1 v1.0 — AptadynamiK. The Corpus remains the sole formal authority for proofs; this document is the sole normative authority for implementations.*
