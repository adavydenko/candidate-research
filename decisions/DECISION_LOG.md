# Research Decision Log

This log records decisions that materially narrow, merge, park, or kill research directions.

## D-001 — Treat FLLC as baseline/fallback, not dissertation novelty
**Decision:** Use FLLC as exact baseline / fallback and reproducible engineering artifact.  
**Reason:** Delta/bit-packing lossless float compression is mature; independent implementation and portability are valuable engineering results but insufficient novelty by themselves.  
**Affected:** I-001, PC-04.

## D-002 — Move broad QoI/invariant-preserving claim to supporting role
**Decision:** Do not claim “preserve physical quantities instead of raw floats” as core novelty.  
**Reason:** QoI-preserving scientific compression and structure-preserving ROM already cover the broad claim.  
**Affected:** I-003, PC-04.

## D-003 — Focus C1 on receiver-aware temporal innovation
**Decision:** Current strongest line is receiver-aware temporal latent innovation with adaptive correction fidelity and explicit dynamics/task constraints.  
**Reason:** First literature reconnaissance did not close this exact intersection, while adjacent broad ideas are established.  
**Affected:** I-004, I-005, I-006, PC-01, PC-02.

## D-004 — Narrow edge/SLM work to temporal persistent-state synchronization
**Decision:** Do not position generic latent agent communication as novelty.  
**Reason:** Interlat, LatentMAS, AgentComm and adjacent 2025–2026 work already establish latent/semantic agent communication.  
**Affected:** I-010, PC-03.

## D-005 — Use pull requests for all substantive repository changes
**Decision:** Keep `main` as accepted canonical state. Research updates are proposed through branches and pull requests.  
**Reason:** Preserve provenance, reviewability, and safe multi-agent collaboration.
