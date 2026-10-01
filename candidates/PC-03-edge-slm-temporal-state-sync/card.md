# Paper Candidate PC-03
## Temporal Latent-State Synchronization for Resource-Constrained SLM Micro-Agents

**Date:** 2026-09-13  
**Paper cluster:** edge micro-agents / application of synchronization core  
**Related idea IDs:** I-005, I-006, I-010, I-011, I-016  
**Publication role:** **development/application paper; possible standalone**  
**Literature status:** **screened → generic latent communication novelty-closed; narrowed hypothesis remains open**  
**Publication decision:** **park until PC-01 mechanism exists, then experiment**

## One-sentence thesis

A resource-constrained SLM agent should not repeatedly receive full text/context or full latent state; it should maintain a **persistent local state** and receive sparse temporal innovations only when they can change its next decision.

## What is explicitly *not* novel

The following claims are already closed:
- “agents can communicate in latent space”;
- “latent messages can be smaller/faster than text”;
- “shared latent working memory helps multi-agent reasoning”;
- “semantic communication can preserve task performance while reducing bandwidth”;
- “SLMs are useful on edge devices.”

Interlat [1], LatentMAS [2], AgentComm [3], current latent-communication surveys [4], and cloud-edge LLM/SLM intermediate-state sharing [5] make those claims unsafe as novelty.

## Narrowed research question

Can **temporal persistence** be exploited so that an SLM/micro-agent receives only the *innovation relative to what it is already expected to know*, rather than a newly encoded message/state at every interaction?

This differs from many latent-agent works conceptually:

\[
\text{message}_t = \Delta z_t \text{ relative to receiver belief}
\]

rather than

\[
\text{message}_t = z_t \text{ or hidden/KV state for the current turn}.
\]

The literature reconnaissance does **not yet establish** that this exact temporal/event-triggered formulation is absent; it needs deep review before implementation.

## Publication hypothesis

> **If** an edge SLM maintains persistent task/world state and receives only receiver-aware, event-triggered latent innovations, **then** it can preserve task success while lowering communication, prompt/token processing, KV/memory pressure and inference time compared with text, summarized-text and full-latent communication baselines.

## Closest known papers

**Interlat [1]** directly exchanges last-hidden-state latent representations and further compresses them.  
**LatentMAS [2]** uses shared latent working memory for lossless continuous collaboration.  
**AgentComm [3]** performs importance-aware semantic reduction with long-term knowledge.  
**CE-LSLM [5]** shares semantic intermediate states / KV-related context between cloud LLMs and edge SLMs.

Therefore the candidate must be about **temporal state synchronization**, not “latent communication.”

## Novelty map

| Dimension | Prior art already covers | Candidate contribution | Scientific or engineering? | Threat |
|---|---|---|---|---|
| Latent inter-agent communication | Explicitly demonstrated [1,2,4] | None | — | **closed** |
| Compression of latent communication | Interlat explicitly compresses latent messages [1] | None | — | **closed** |
| Shared latent working memory | LatentMAS [2] | None | — | **closed** |
| Importance-aware semantic selection | AgentComm [3] | None | — | **closed** |
| Edge LLM/SLM intermediate-state collaboration | CE-LSLM [5] | None | — | **closed** |
| Persistent receiver belief across environment time | Not established in closest records | Maintain state between invocations as a synchronized dynamical object | potentially scientific | **open but must deep-review** |
| Innovation relative to receiver belief | Not established in closest agent papers | Send only unpredicted temporal delta | potentially scientific | **open but must deep-review** |
| Event-triggered latent update | Current survey lists compression for edge as open; exact temporal trigger needs search | suppress messages entirely until decision-relevant deviation | scientific | **open-ish** |
| Joint savings: network + tokenization + KV + compute | Existing papers report some latency/token gains | systematic cost model for micro-agent state sync | engineering + empirical scientific result | medium |
| Failure/resync semantics | Latent protocols usually assume communication; our protocol includes silence/liveness/checkpoint | robust persistent-state protocol | mostly engineering unless formal guarantees | medium |

## Experimental setup

Start with **two CPU-only local processes**, not a distributed 6G simulator.

Agent A observes a streaming environment. Agent B is an SLM responsible for a narrow repeated decision/tool-selection task.

Compare:
1. full structured state each step;
2. natural-language summary;
3. embedding/full latent message each step;
4. persistent state + raw delta;
5. persistent state + latent innovation;
6. persistent state + task-aware event-triggered innovation.

## Metrics

- task success / action equivalence;
- bytes on wire;
- input tokens;
- KV/cache memory;
- peak RSS;
- CPU time;
- end-to-end latency;
- energy if measurement is available;
- update frequency;
- desynchronization/resync frequency.

## Key ablations

- persistent vs stateless receiver;
- text vs latent;
- full latent vs latent innovation;
- always-update vs event-triggered;
- same-model vs heterogeneous SLMs;
- deterministic vs nondeterministic inference.

## Cheapest falsification experiment

Use a tiny deterministic environment and a small local model. Keep the SLM state persistent in an external compact state vector rather than modifying model internals initially. Measure whether suppressing updates based on receiver-aware innovation lowers total cost at equal action accuracy.

If prompt/text summarization is equally cheap and accurate, or if maintaining synchronized latent state is unstable, this branch should remain an application demo rather than a paper core.

## Main risks

1. Extremely fast-moving literature.
2. Hidden-state/KV formats are architecture-specific.
3. “Latent state” of an SLM may not behave like a stable physical state variable.
4. Reproducibility across model versions may be poor.
5. Easy to drift from 1.2.2 into AI/communications.

## Fit to 1.2.2

**4/5.** Stronger if presented as an application of the general synchronization method and accompanied by formal state/error models. Weaker if the work is merely an LLM systems benchmark.

## References from Consensus reconnaissance

1. [Enabling Agents to Communicate Entirely in Latent Space](https://consensus.app/papers/enabling-agents-to-communicate-entirely-in-latent-space-du-wang/e77e8312d05b5c639a641b216da7ba5a/?utm_source=chatgpt) — Zhuo-Yun Du, Run-Ze Wang, Hui-Yu Bai, Zouying Cao, Xiaoyong Zhu, Bo Zheng, Wei Chen, Haochao Ying; 2025; arXiv; citations in Consensus: 26; DOI: 10.48550/arXiv.2511.09149.
2. [Latent Collaboration in Multi-Agent Systems](https://consensus.app/papers/latent-collaboration-in-multiagent-systems-zou-yang/0d19c2ecd274507e80887a8f734c7e62/?utm_source=chatgpt) — Jiaru Zou et al.; 2025; arXiv; citations in Consensus: 45; DOI: 10.48550/arXiv.2511.20639.
3. [AgentComm: Semantic Communication for Embodied Agents](https://consensus.app/papers/agentcomm-semantic-communication-for-embodied-agents-jiang-feng/1afc098e43e853379f1205b54473fa52/?utm_source=chatgpt) — Peiwen Jiang, Yushuo Feng, Jiajia Guo, Chao-Kai Wen, Shi Jin; 2026; IEEE Transactions on Cognitive Communications and Networking; citations in Consensus: 2; DOI: 10.1109/TCCN.2026.3729940.
4. [Beyond tokens: a unified framework for latent communication in LLM-based multi-agent systems](https://consensus.app/papers/beyond-tokens-a-unified-framework-for-latent-liu/4482eed8c14d504cb6d2ebbd60a04707/?utm_source=chatgpt) — Yingzhu Liu; 2026; arXiv; citations in Consensus: 3; DOI: 10.48550/arXiv.2606.05711.
5. [CE-LSLM: Efficient Large-Small Language Model Inference and Communication via Cloud-Edge Collaboration](https://consensus.app/papers/celslm-efficient-largesmall-language-model-inference-and-zhu-yang/2003465a2ccb59179e424f5e5f84da45/?utm_source=chatgpt) — Pengyan Zhu, Tingting Yang; 2025; arXiv; citations in Consensus: 3; DOI: 10.48550/arXiv.2505.14085.
6. [Small Language Models are the Future of Agentic AI](https://consensus.app/papers/small-language-models-are-the-future-of-agentic-ai-belcák-heinrich/bcacee1c9e3750b1983d604e28c9946a/?utm_source=chatgpt) — Peter Belcák, Greg Heinrich, Shizhe Diao, Yonggan Fu, Xin Dong, Saurav Muralidharan, Y. Lin, Pavlo Molchanov; 2025; arXiv; citations in Consensus: 359; DOI: 10.48550/arXiv.2506.02153.