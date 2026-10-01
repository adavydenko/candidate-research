# Master Novelty Map — Candidate Paper Cluster

**Date:** 2026-09-13  
**Scope:** ideas I-001–I-016 after first Consensus reconnaissance  
**Purpose:** decide where to spend implementation effort before a deep literature review.

## Proposed publication sequence

| Order | Candidate | Role in research line | Novelty status | Current decision |
|---|---|---|---|---|
| **P1** | PC-01 Predictive Latent Innovation | base method | threatened but plausible | **EXPERIMENT FIRST** |
| **P2** | PC-02 Task-/Invariant-Aware Significance Gate | development / smarter policy | threatened but plausible | **EXPLORE after P1** |
| **P3** | PC-03 Temporal Latent-State Sync for SLM Micro-Agents | complex/application setting | generic thesis closed; narrow temporal gap possible | **PARK until P1 works** |
| **P0/support** | PC-04 Dynamics-Preserving Benchmark | evidence/benchmark layer | broad novelty largely closed | **MERGE/SUPPORT** |

This sequence matches the desired dissertation strategy:

**problem/benchmark → base synchronization method → adaptive decision policy → constrained edge/agent application.**

## Cross-paper novelty map

| Mechanism / claim | Status after recon | Evidence / interpretation |
|---|---|---|
| Lossless float delta/bit packing as scientific novelty | **closed/weak** | mature compression space; use FLLC as baseline/fallback |
| Preserve QoIs rather than raw floats | **closed as broad claim** | QoI-preserving compression already formalized |
| Preserve structure/invariants in latent ROM | **closed as broad claim** | active structure-preserving MOR literature |
| Preserve temporal dynamics under compression | **closed as broad claim** | dynamics-preserving compression exists |
| Skip unimportant updates | **closed as broad claim** | event-triggered communication/estimation is mature |
| Cumulative innovation | **closed** | explicit cumulative-innovation event-triggered work exists |
| DNN predictor + event-triggered estimation | **closed** | prior IEEE TAC work |
| Value-of-information communication | **closed as principle** | task-oriented MAS and Pareto/value-of-communication work |
| Agents communicate in latent space | **novelty-closed** | Interlat, LatentMAS, other 2025–2026 work |
| Compress latent agent messages | **novelty-closed** | Interlat and related work |
| Edge SLM/LLM share semantic/KV intermediate states | **novelty-threatened/mostly closed** | CE-LSLM and adjacent systems |
| **Receiver-aware latent innovation after skipped timesteps** | **potentially open** | not closed by first recon; needs deep review |
| **Unified silence/latent/exact/checkpoint action space** | **potentially open** | closest work often separates scheduling/quantization/estimation |
| **Long-horizon invariant/dynamics constraints inside state-sync policy** | **potentially open** | bridge between event-triggered estimation and structure-preserving scientific computing |
| **Temporal persistent-state sync for SLM micro-agents** | **potentially open, fast-moving** | distinguish from per-turn hidden/KV transfer |
| **Joint decision of whether to send and at what representation level** | **potentially open** | promising if formulated as optimization, not heuristic |
| **Error decomposition: integrator vs representation vs skipped-update vs predictor** | **potentially useful** | could become methodological contribution/benchmark |

## Strongest candidate scientific claim today

> A distributed computational system can reduce communication by maintaining a shared predictive model and transmitting **receiver-aware innovations at an adaptively selected representation level**, while explicitly constraining long-horizon dynamical or task error.

This is narrower and safer than:
- “semantic communication”;
- “latent agent communication”;
- “QoI-aware compression”;
- “event-triggered estimation.”

## Recommended dissertation/paper cluster

### Cluster C1 — Adaptive state synchronization

**Core IDs:** I-004, I-005, I-006, I-009  
**Support:** I-003, I-007, I-008, I-011, I-012  
**Application:** I-010  
**Baseline:** I-001

Potential dissertation logic:

1. Define receiver-aware state/anchor model and error decomposition.
2. Introduce predictive latent innovation.
3. Introduce adaptive multi-mode significance policy.
4. Establish criteria/limits for drift, resynchronization and task/dynamics equivalence.
5. Validate on N-body; optionally a second physical system.
6. Validate the same mechanism in resource-constrained micro-agents.

## Immediate research priority

Before substantial implementation, perform a **deep review** of the citation neighborhoods around:
- cumulative innovation-driven event-triggering;
- dynamic event-triggered estimation with implicit information from silence;
- semantic/task-oriented communication with VoI;
- latent communication surveys and hidden/KV state transfer.

The key kill question is:

> Is there already a method that simultaneously maintains a receiver-side predictive latent state, suppresses intermediate updates, sends innovation relative to receiver belief, adaptively selects correction fidelity, and controls downstream/dynamical error?

If yes, PC-01 must be narrowed or killed. If no, this is the strongest current gap.

## Index updates recommended

- **I-003:** keep perspective, but `literature status = novelty-threatened`; publication role `supporting result / benchmark`.
- **I-004:** strengthen; `paper cluster = C1`; literature status `screened`; decision `experiment`.
- **I-005:** strongest current core; literature status `screened`; decision `paper candidate`.
- **I-006:** paper-core candidate but defer until I-005 prototype; literature status `screened`.
- **I-009:** principle itself not novel; merge conceptually into I-006 as theoretical basis rather than separate novelty claim.
- **I-010:** generic latent communication novelty closed; retain narrowed `persistent temporal state synchronization for SLM micro-agents`.
- **I-011:** keep as theoretical question; likely supports I-006.
- **I-012:** strong benchmark role, not novelty by itself.

## Current rankings

| Candidate | Scientific novelty potential | 1.2.2 fit | Cheap falsifiability | Publication risk | Overall |
|---|---:|---:|---:|---:|---:|
| PC-01 | 4/5 | 5/5 | 5/5 | medium-high | **4.5/5** |
| PC-02 | 4/5 | 5/5 | 4/5 | high | **4.2/5** |
| PC-03 | 3/5 | 4/5 | 4/5 | very high / fast-moving | **3.4/5** |
| PC-04 | 2.5/5 standalone; 4/5 as support | 5/5 | 5/5 | medium | **3.5/5 support** |

## Bottom line

The literature search **did not kill the overall research line**, but it killed several broad novelty claims. The most defensible surviving gap is not “compression,” “event triggering,” “VoI,” or “latent agent communication” separately. It is their narrower intersection around **receiver-aware temporal latent innovation with adaptive fidelity and dynamics/task guarantees**.