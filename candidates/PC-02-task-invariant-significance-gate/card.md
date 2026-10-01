# Paper Candidate PC-02
## Task- and Invariant-Aware Significance Gate for Multi-Mode State Updates

**Date:** 2026-09-13  
**Paper cluster:** adaptive state representation / synchronization  
**Related idea IDs:** I-003, I-006, I-008, I-009, I-011  
**Publication role:** **paper core / development paper**  
**Literature status:** **screened → novelty-threatened**  
**Publication decision:** **explore → experiment after PC-01 prototype**

## One-sentence thesis

Replace a scalar “send-on-delta” threshold with a significance policy that estimates the **expected downstream value of an update** and chooses among multiple update modes while enforcing constraints on physical/dynamical validity.

## Research question

What is the cheapest update sufficient to preserve the receiver's ability to make the same scientifically/operationally relevant decision?

The key shift is:

\[
\text{importance} \neq \|x_t-\hat x_t\|
\]

but approximately

\[
\text{importance}
=
\Delta \mathbb E[\text{task loss}]
+\text{risk of invariant/dynamics violation}.
\]

## Publication hypothesis

> **If** update significance is evaluated by task loss / value of communication plus explicit physical/dynamical constraints rather than raw state error, **then** a multi-mode gate can reduce bytes, inference work, and update frequency at equal downstream quality relative to fixed-threshold and reconstruction-oriented policies.

## Closest known paper

**Closest threat:** Mostaani et al., *Task-Oriented Communication Design at Scale* [1].

It already combines:
- task-oriented communication;
- Value of Information;
- multi-agent systems;
- quantization policy;
- RL;
- explicit task-performance vs communication trade-off.

A second major threat is Luo et al.'s Pareto/value-of-communication formulation [2], which asks almost exactly “what minimum communication is required to achieve the goal?”

Therefore **“send only important information” and “learn VoI” are not novelty claims.**

## Novelty map

| Dimension | Prior art already covers | Candidate contribution | Scientific or engineering? | Threat |
|---|---|---|---|---|
| Task-oriented communication | Extensive literature [1–3] | Not novel | — | **closed** |
| Value of Information trigger | Explicitly used in MAS [1], Pareto formulation [2] | Not novel | — | **closed** |
| Agent decides what/when/why to communicate | Explicit current research agenda [3] | Not novel as vision | — | **closed** |
| Joint choice of *representation mode* and timing | Typical work optimizes transmit/not-transmit, quantization, bandwidth; our action space includes silence/latent/exact/checkpoint | Unified multi-mode state-update policy | scientific if formalized and benchmarked | **open-ish** |
| Physical invariant constraints | Not central in closest task-oriented communication papers | Add hard/soft scientific-state validity constraints | scientific | **open** |
| Long-horizon dynamics-aware utility | Semantic comm usually evaluates downstream task; scientific trajectory fidelity adds another layer | Value function includes future dynamical distortion | scientific | **open** |
| Cross-domain common gate | Usually application-specific | Same criterion tested on physical simulation and micro-agent decision tasks | generalization result | medium |

## Candidate objective

\[
\min_{\pi}
\mathbb E[
L_{\rm task}
+\lambda_B B
+\lambda_C C_{\rm compute}
+\lambda_L L_{\rm latency}
]
\]

subject to, where relevant,

\[
E_{\rm invariant} \le \epsilon_I,\qquad
E_{\rm dynamics}(H) \le \epsilon_D,\qquad
Age \le A_{\max}.
\]

The policy chooses

\[
a_t \in \{0,\,z\text{-update},\,x\text{-exact},\,checkpoint\}.
\]

## Three implementation levels

1. **Analytic gate** — handcrafted VoI approximation; simplest and best for interpretation.
2. **Supervised gate** — learn whether omitting an update changes the future task outcome.
3. **RL/MDP gate** — optimize long-run rate–quality–compute objective.

Do not begin with RL. First determine whether the signal contains exploitable structure.

## Target evidence

**Baselines**
- periodic;
- fixed state-error threshold;
- dynamic ETM;
- AoI/AoII-style trigger;
- binary VoI trigger;
- multi-level heuristic trigger.

**Metrics**
- task success / control loss;
- bytes and packets;
- energy/CPU/inference time;
- invariant violation;
- long-horizon trajectory/statistics;
- false-silence events: update suppressed but task output changes.

**Ablations**
- state error only;
- task loss only;
- invariant only;
- task + invariant;
- learned vs analytic gate;
- binary vs multi-mode actions.

**Key figure**
Rate–quality Pareto front plus “false silence” rate.

## Cheapest falsification experiment

Generate a nonlinear time series with an explicit downstream classifier/control action. For each timestep, compute the counterfactual outcome with and without the update; train a tiny gate to predict whether transmission changes the outcome. Compare against \(\|x-\hat x\|\)-thresholding.

If a simple numerical threshold performs equally well, the learned-significance idea has little value.

## Main risks

1. Task-oriented/semantic communication is crowded.
2. An RL gate is easy to dismiss as “another policy network.”
3. If the task is too simple, “significance” collapses to state-error magnitude.
4. Combining physical invariants and agentic tasks may make the paper incoherent; one domain should be primary.

## What would make it publishable

A defensible scientific contribution is **not** “we train a gate.” It is one of:
- a new significance functional with interpretable components;
- a formal connection between update omission and future task/dynamics error;
- a multi-mode policy shown to dominate binary/event-triggered policies across budgets;
- constrained task-aware communication where invariant preservation changes the optimal policy in a measurable way.

## Fit to 1.2.2

**5/5** if framed as optimization / numerical method for distributed computational systems.  
Drops toward **3–4/5** if framed primarily as wireless semantic communication.

## References from Consensus reconnaissance

1. [Task-Oriented Communication Design at Scale](https://consensus.app/papers/taskoriented-communication-design-at-scale-mostaani-vu/f04cd7953033508c80a4a9e0aaaddde6/?utm_source=chatgpt) — Arsham Mostaani, T. Vu, Hamed Habibi, S. Chatzinotas, Björn E. Ottersten; 2023/2024; IEEE Transactions on Communications; citations in Consensus: 13; DOI: 10.1109/TCOMM.2024.3416898.
2. [Value of Communication in Goal-Oriented Semantic Communications: A Pareto Analysis](https://consensus.app/papers/value-of-communication-in-goaloriented-semantic-luo-li/36cc553a6e5e577180263400faa4702b/?utm_source=chatgpt) — Jiping Luo, Bowen Li, Nikolaos Pappas; 2025; arXiv; citations in Consensus: 3; DOI: 10.48550/arXiv.2512.01454.
3. [Towards reasoning-empowered task-oriented communication for agent networks](https://consensus.app/papers/towards-reasoningempowered-taskoriented-communication-xie-li/3a13f9df2e7d57a5afa9084fd06c9b30/?utm_source=chatgpt) — Songjie Xie, Hongru Li, Zixin Wang, Shenghui Song, Jun Zhang, K. B. Letaief; 2026; npj Wireless Technology; citations in Consensus: 2; DOI: 10.1038/s44459-026-00028-z.