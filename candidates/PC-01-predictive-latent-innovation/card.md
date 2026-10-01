# Paper Candidate PC-01
## Predictive Latent Innovation for Sparse Synchronization of Dynamical State

**Date:** 2026-09-13  
**Paper cluster:** adaptive state representation / synchronization  
**Related idea IDs:** I-004, I-005, I-007, I-008, I-012  
**Publication role:** **paper core / likely standalone paper**  
**Literature status:** **screened → novelty-threatened, but not closed**  
**Publication decision:** **experiment**

## One-sentence thesis

Maintain an approximate receiver-side state and transmit only a **receiver-aware latent innovation** when the predicted shared state becomes insufficient, with explicit correction/checkpoint modes that bound drift while reducing communication.

## Research question

Can a sender and receiver maintain sufficiently equivalent states of a nonlinear dynamical system while suppressing most intermediate updates, by combining:

1. a shared predictor;
2. innovation relative to the receiver's *predicted/anchored* state;
3. latent-space correction rather than raw-state correction;
4. adaptive escalation `silence → latent correction → exact correction → checkpoint`;
5. explicit control of long-horizon drift / invariant violation?

## Publication hypothesis

> **If** sender and receiver maintain a shared predictive state and transmit receiver-aware latent innovations only when a dynamics-aware error criterion is exceeded, **then** communication volume can be reduced relative to periodic/raw/event-triggered baselines while maintaining bounded long-horizon state divergence and physical invariant error, **because** predictable evolution is reconstructed locally and only unpredicted information is communicated.

This is falsifiable: if gains disappear after including predictor compute, metadata, resynchronization, and drift, the hypothesis fails.

## Closest known paper

**Closest threat:** Bian, Chen & Li — cumulative innovation-driven event-triggered remote estimation [1].

What it already does:
- remote state estimation;
- event-triggered communication;
- cumulative innovation;
- communication/performance optimization;
- MDP formulation.

What it does **not establish from the retrieved record**:
- learned/nonlinear latent state as the transmitted correction;
- a multi-mode exact/latent/checkpoint protocol;
- physical invariant / long-horizon trajectory preservation as the synchronization criterion;
- scientific-simulation state as the target rather than classical remote estimation.

## Novelty map

| Dimension | Prior art already covers | Candidate contribution | Scientific or engineering? | Threat |
|---|---|---|---|---|
| Event-triggered transmission | Mature field; dynamic ETMs reduce transmissions [2] | Not novel by itself | — | **closed** |
| Cumulative innovation | Explicitly present in close prior work [1] | Not novel by itself | — | **closed** |
| Learned nonlinear predictor + event trigger | DNN-based distributed estimation exists [3] | Not novel by itself | — | **closed** |
| Receiver-aware latent innovation | Prior work found here uses state/measurement innovation, not this exact latent synchronization framing | Define latent innovation against receiver belief, including skipped steps | potentially scientific | **open but threatened** |
| Multi-resolution correction modes | Not identified in this recon as a unified `silence/latent/exact/checkpoint` policy | Joint selection of update representation and timing | scientific if optimized/formalized; engineering if heuristic | **open** |
| Dynamics/invariant-bounded synchronization | ETM work focuses estimation error; our target includes physical/dynamical equivalence | Bound/control invariant drift and long-horizon divergence under sparse updates | scientific | **open** |
| Fault/loss recovery | Standard networking has checkpoints/sequence numbers | Anchor semantics integrated into estimator state | mostly engineering unless tied to formal guarantees | medium |

## Proposed method sketch

Let the true/sender state be \(x_t\), latent encoder \(E\), shared predictor \(F\), receiver belief \(\hat z_t^R\).

\[
z_t = E(x_t), \qquad \tilde z_t^R = F(\hat z_{t-1}^R, u_t)
\]

\[
e_t = z_t - \tilde z_t^R
\]

A policy chooses

\[
a_t \in \{\mathrm{silence},\mathrm{latent},\mathrm{exact},\mathrm{checkpoint}\}
\]

using error, uncertainty, age, resource budget, and optionally physical quantities of interest.

Key design constraint: the correction is always interpreted relative to an **explicit receiver belief/anchor**, never to an unsent intermediate state.

## Target evidence

**Baselines**
- periodic full-state transmission;
- send-on-delta / fixed threshold;
- periodic predictive residual;
- dynamic event-triggered estimator;
- cumulative-innovation event trigger;
- exact delta/FLLC as a lossless lower-level baseline.

**Systems**
- simple linear/Gaussian system for sanity and comparison to classical theory;
- Lorenz or another nonlinear chaotic system;
- N-body as primary scientific benchmark;
- SPH only after the method works.

**Metrics**
- bytes per simulated second / bits per state;
- transmission frequency;
- latency and sender/receiver CPU time;
- reconstruction error;
- energy / linear momentum / angular momentum drift for N-body;
- divergence after horizon \(H\);
- checkpoint frequency;
- failure recovery after packet loss.

**Key ablations**
- raw vs latent innovation;
- no predictor vs shared predictor;
- fixed threshold vs learned/adaptive threshold;
- no checkpoint vs checkpoint;
- MSE trigger vs dynamics/invariant-aware trigger.

**Key figure**
A Pareto front: **communication cost vs long-horizon dynamical error**, with invariant error as a second axis/table.

## Cheapest falsification experiment

Implement two processes sharing a deterministic N-body predictor. Compare:
1. full state every step;
2. fixed send-on-delta;
3. cumulative raw innovation;
4. latent innovation with a tiny autoencoder.

Force identical thresholds on receiver-state divergence. If latent innovation does not beat cumulative raw innovation after encoder cost and periodic resync are counted, this paper direction weakens sharply.

## Main risks

1. Classical event-triggered estimation is deep and mathematically mature; reviewers may view the work as relabeling.
2. A latent encoder may add more compute than the saved traffic is worth.
3. Chaotic systems can make long-horizon pointwise synchronization impossible; the target may need to be invariant/statistical equivalence rather than trajectory identity.
4. Formal guarantees may be hard for learned latent dynamics.

## What would make it publishable

At least one of:
- a new formal bound connecting communication policy to invariant/dynamics error;
- a new receiver-aware latent innovation representation with demonstrably superior rate–dynamics Pareto front;
- a principled multi-mode synchronization policy with provable or empirically robust resynchronization behavior.

Without one of these, this risks being an engineering integration.

## Fit to 1.2.2

**5/5.** The core is mathematical modeling + numerical state estimation/synchronization + algorithms + software experiment. Keep the framing on dynamical systems and computational complexes, not wireless PHY.

## References from Consensus reconnaissance

1. [Exploration into Optimal State Estimation with Event-triggered Communication](https://consensus.app/papers/exploration-into-optimal-state-estimation-with-bian-chen/0ce4c4f35d9558488f6246bb8ae479d3/?utm_source=chatgpt) — Xiaolei Bian, Huimin Chen, F. X. Rong Li; 2023; arXiv; citations in Consensus: 0; DOI: 10.48550/arXiv.2309.08070.
2. [Bounding Uncertainty in State Estimation Under Dynamic Event-Triggered Communication](https://consensus.app/papers/bounding-uncertainty-in-state-estimation-under-dynamic-perez-salesa-aldana-lópez/a669feda2e335cf1831ace224e5e4efc/?utm_source=chatgpt) — Irene Perez-Salesa, R. Aldana-López, Carlos Sagüés; 2025; IEEE Transactions on Systems, Man, and Cybernetics: Systems; citations in Consensus: 4; DOI: 10.1109/TSMC.2024.3465232.
3. [Distributed State Estimation With Deep Neural Networks for Uncertain Nonlinear Systems Under Event-Triggered Communication](https://consensus.app/papers/distributed-state-estimation-with-deep-neural-networks-zegers-sun/3640c7dc9fca5c9d930786f41eb0ba63/?utm_source=chatgpt) — Federico M. Zegers, Runhan Sun, Girish V. Chowdhary, W. Dixon; 2022; IEEE Transactions on Automatic Control; citations in Consensus: 26; DOI: 10.1109/TAC.2022.3217022.