# Paper Candidate PC-04
## Benchmark and Metrics for Dynamics-Preserving State Reduction

**Date:** 2026-09-13  
**Related idea IDs:** I-001, I-002, I-003, I-012, I-013  
**Publication role:** benchmark/tool or supporting result  
**Literature status:** screened → novelty-threatened  
**Publication decision:** merge/support unless a distinct metric/theorem emerges

## Thesis

Evaluate state reduction by whether it preserves physically and dynamically relevant behavior over time, not only pointwise reconstruction error.

## Kill-test result

The broad claim is already occupied:
- QoI-preserving scientific compression preserves downstream physical quantities;
- structure-preserving latent/model-order reduction preserves Hamiltonian/Lagrangian structure;
- dynamics-preserving compression for temporal flow analysis exists;
- time-varying vector-field compression can preserve critical-point trajectories.

Therefore “MSE is insufficient; preserve physics/dynamics instead” is **not** a novelty claim.

## Remaining gap

A useful contribution may still be a benchmark/evaluation protocol for **sparse state synchronization**, separating:

- numerical integrator error;
- representation/compression error;
- skipped-update error;
- predictor drift;
- downstream task error.

Candidate metric stack:

[
E_{state},\quad E_{invariant},\quad E_{dyn}(H),\quad E_{task},\quad R_{communication}
]

## Novelty map

| Dimension | Status | Candidate role |
|---|---|---|
| QoI preservation | closed as broad novelty | baseline / evaluation criterion |
| Structure-preserving latent ROM | closed as broad novelty | baseline |
| Temporal dynamics-preserving compression | closed as broad novelty | baseline |
| Joint state/invariant/dynamics/task/communication benchmark | potentially open | methodological/tool contribution |
| Error decomposition for skipped updates and predictor drift | potentially open | methodological contribution |
| N-body + SPH benchmark pair | not novel by itself | experimental design |
| FLLC | engineering baseline | exact fallback |

## Publication hypothesis

A method selected by pointwise reconstruction error alone can be Pareto-inferior when evaluated by long-horizon dynamical fidelity and communication cost; a benchmark including invariant drift, horizon-(H) divergence and task outcome can rank methods differently from MSE/PSNR alone.

## Target evidence

**N-body metrics**
- total energy error;
- linear/angular momentum error;
- center-of-mass drift;
- trajectory divergence;
- long-time structural/statistical observables.

**Baselines**
- FP64/FP32 raw state;
- FLLC and general lossless codecs;
- error-bounded lossy compression;
- PCA/POD;
- autoencoder / structure-preserving latent model;
- periodic thinning/interpolation;
- event-driven thinning.

## Cheapest falsification experiment

Create several perturbations of an N-body state with similar MSE but different directions in phase space, continue integration, and compare invariant/dynamics outcomes. If MSE predicts long-horizon quality equally well, the benchmark thesis weakens.

## Main risk

As a standalone paper this is incremental unless it contributes a new justified metric, a reusable benchmark/tool, a surprising empirical ranking reversal, or a formal error decomposition.

## Fit to 1.2.2

**5/5** as a supporting benchmark/tool for numerical methods and computational experiments.
