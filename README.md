# Aptadynamic Cybernetics

**The scientific discipline of structural viability in observable systems.**

G.A.C.J. — ORCID: [0009-0009-5649-1359](https://orcid.org/0009-0009-5649-1359)
Part of the **AptadynamiK** program.

---

## What this discipline studies

Aptadynamic Cybernetics studies one question across every kind of system: **what distinguishes a system that sustains itself from one that merely appears to?**

A power grid, an institution, a market, or an organism may operate normally — producing output, meeting demand, showing no visible fault — while continuously consuming the structural margin that makes its operation possible. The discipline provides the formal theory of that condition, the mathematics of its accumulation and thresholds, and an operational protocol that detects it from observable behavior alone.

Its central claims:

- **Viability is a property of trajectories, not states.** A system is viable while its accumulated tension Ξ(t) remains below an endogenous threshold Θ(λ(t)).
- **History is never erased.** Structural cost that is not paid is displaced onto the future; evaluation must carry genuine memory (non-Markovian).
- **The threshold contracts with history.** What a system can tolerate is not fixed; past excess reduces future absorption capacity.
- **Operation is not persistence.** The most dangerous phase — *latent collapse* — is the one in which a system still functions while consuming what makes its functioning possible.
- **The evaluation kernel is universal.** Only the way each domain is observed changes; the projection itself is mathematically identical across domains, and this claim carries a defined empirical test.

## Structure of the discipline

```
Aptadynamic Cybernetics
│
├── Systemic Foundation ............ conceptual technical reference
│                                    (source of the framework's vocabulary and principles)
│
├── Logical–Mathematical Corpus .... formal reference
│                                    (axiomatization, theorems, proofs)
│                                    DOI: 10.5281/zenodo.20369325
│
├── Aptadynamic Cybernetics
│   Specification (AS-1) ........... normative specification
│                                    (what any implementation must satisfy)
│
└── PRAMA Protokol ................. operational protocol
      ├── PRAMA Protokol Engine        (reference kernel, runtime,
      ├── Observation Interfaces        observation interface, compliance)
      ├── Domain Implementations
      └── Validation Studies
```

## Contents of this repository

| Path | Content |
|---|---|
| [`specification/AS-1.md`](specification/AS-1.md) | **Aptadynamic Cybernetics Specification (AS-1)** — the normative document. Defines the eight core principles (P1–P8), the aptadynamic coordinates Γ = (Δ, Ξ, λ, Θ, M, G), the Engine architecture, the Observation Interface contract (C1–C5), regime stratification, and the compliance regime. |
| [`glossary/translation-glossary.md`](glossary/translation-glossary.md) | **Translation Glossary** — the official bridge between the Systemic Foundation terminology and the technical language of cybernetics. |
| [`corpus/`](corpus/) | Pointer to the **Logical–Mathematical Corpus** (Zenodo, DOI above). The Corpus is the sole formal authority for proofs. |
| [`foundation/`](foundation/) | Reference note on the **Systemic Foundation**, the discipline's conceptual technical reference. |

## Relation to the PRAMA Protokol

The **PRAMA Protokol** is the discipline's operational protocol: the domain-independent method, specified in AS-1, for evaluating structural viability from observable event streams. Its engineering artifacts live in their own repositories:

- **Reference implementation and first empirical validation:** [`Aptadynamic-Electrical-Grid`](https://github.com/gacj0901/Aptadynamic-Electrical-Grid) — the PRAMA Protokol over Bonneville Power Administration transmission outage data (BPA 1999–2017; NYISO 2008–2021).

Key validated results: conditional severity discrimination at ratio 28.75 inside latent-collapse periods (vs 3.16 for the best strictly causal Markovian baseline, permutation p < 0.001); on NYISO, an initial negative result (0.55) was traced to a degenerate observation interface and corrected to 2.44 without touching the kernel — the operational demonstration that the kernel/observation separation localizes failure where the architecture says it should.

**Denomination.** The protocol is always referred to as **PRAMA Protokol** in full; the admissible short form is *the Protokol*.

## Authority hierarchy

| Question | Authority |
|---|---|
| What must an implementation satisfy? | **AS-1** (this repository) |
| Why is it mathematically true? | **Corpus** (Zenodo DOI) |
| What does each concept mean? | **Translation Glossary** (this repository) |
| Does it work on real data? | **Validation Studies** (domain repositories) |

## Citing

If you use or discuss this work, cite the Corpus:

> G.A.C.J. (2026). *Aptadinamia — Corpus Lógico-Matemático: Tratado de viabilidad estructural, persistencia y recursividad sincisional emergente.* Zenodo. https://zenodo.org/records/21270506

and, for the operational protocol, the AS-1 specification in this repository together with the relevant validation study.

## License

Documentation in this repository © 2026 G.A.C.J. — released under [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/) (attribution, non-commercial, no derivatives), unless otherwise noted. Code repositories of the PRAMA Protokol carry their own licenses (see each repository). Commercial licensing, industrial collaborations and academic research partnerships may be available separately.
