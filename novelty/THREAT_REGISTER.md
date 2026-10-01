# Novelty Threat Register

| ID | Prior work / line | Threatens | Severity | Current impact | Status |
|---|---|---|---|---|---|
| TH-001 | Bian et al. — cumulative innovation-driven event-triggered estimation | PC-01, I-004, I-005 | HIGH | Cumulative innovation + event triggering cannot be claimed as novel | analyzed |
| TH-002 | Zegers et al. — DNN distributed state estimation with event-triggered communication | PC-01, I-005 | HIGH | Learned nonlinear predictor + event trigger is prior art | analyzed |
| TH-003 | Jiao et al. — QoI-preserving lossy scientific compression | PC-04, I-003 | CRITICAL | “Preserve QoI instead of raw floats” is not a novelty claim | novelty narrowed |
| TH-004 | Structure-preserving neural/model-order reduction literature | PC-04, I-003 | CRITICAL | Invariant/structure-preserving latent reduction is established | novelty narrowed |
| TH-005 | Glazkov & Schmid — dynamics-preserving compression | PC-04 | HIGH | “Preserve temporal dynamics under compression” is already explicit | novelty narrowed |
| TH-006 | Mostaani et al. — task-oriented communication + VoI | PC-02, I-006, I-009 | CRITICAL | VoI/task-aware triggering is established | novelty narrowed |
| TH-007 | Luo et al. — minimum/value of communication Pareto formulation | PC-02, I-009, I-011 | HIGH | Minimum communication for a task is not new as a broad question | analyzed |
| TH-008 | Interlat — latent communication between agents | PC-03, I-010 | CRITICAL | Generic “agents communicate in latent space” novelty is closed | novelty closed |
| TH-009 | LatentMAS — shared latent working memory | PC-03, I-010 | CRITICAL | Shared latent working memory is prior art | novelty closed |
| TH-010 | AgentComm — importance-aware semantic agent communication | PC-03, I-010 | HIGH | Importance-aware semantic reduction is prior art | analyzed |
| TH-011 | CE-LSLM — cloud-edge LLM/SLM intermediate-state sharing | PC-03, I-010 | HIGH | Edge LLM/SLM semantic/KV state sharing is already explored | analyzed |

## Surviving gap after reconnaissance

The first reconnaissance did **not** identify prior work that simultaneously combines:

- persistent receiver-side predictive state;
- suppression of intermediate updates;
- innovation relative to the receiver belief rather than the immediately previous sender state;
- adaptive choice among silence / latent correction / exact correction / checkpoint;
- explicit long-horizon dynamical, invariant, or downstream-task constraints.

This gap is provisional until a deep citation-neighborhood review of PC-01 is complete.
