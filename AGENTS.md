# Research agent instructions

## Canonical state

This repository is the canonical research state for project «Кандидатская». Prefer repository content over stale chat attachments or old conversation summaries.

## Change workflow

- Do not make substantive changes directly to `main`.
- Create a branch and submit a pull request.
- Keep PRs coherent: one research update / literature review / experiment result per PR when practical.
- Never merge a PR automatically unless explicitly requested by AD.

## Research workflow

For every promising research direction:

1. Check `ideas/IDEA_INDEX.md` and existing `candidates/`.
2. Reuse existing IDs when the thought develops an existing idea; create a new ID only for an independent result.
3. Before substantial implementation, perform a literature kill-test.
4. Identify closest prior art and record why it threatens the candidate.
5. Separate engineering usefulness from scientific novelty.
6. Define the cheapest falsification experiment.
7. Trace evidence through `I → PC → H → EXP → R → C → P → DC`.

## Paper candidates

Closest papers are contextual: keep analytical closest-paper cards inside the relevant `PC-*` candidate. The global bibliography stores citations, not the contextual novelty comparison.

For promising candidates maintain:
- publication hypothesis;
- closest known paper(s);
- novelty gap;
- literature status;
- target evidence/baselines;
- falsification experiment;
- publication decision;
- role in dissertation.

## Experiments

Each experiment lives under `experiments/EXP-NNN-*` and should contain:

- `README.md` — hypothesis, protocol, baselines, metrics, linked IDs, conclusion;
- `src/` — experiment-specific code/scripts;
- `configs/` — exact configurations;
- `results/` — machine-readable raw/derived outputs when reasonably small;
- `figures/` — generated figures when appropriate;
- environment/reproducibility metadata;
- external implementation repository + exact commit SHA when code lives elsewhere.

Do not mix executable experiment code into research Markdown directories.

## Results and claims

A result (`R-*`) is an observed fact tied to evidence. A claim (`C-*`) is a generalizable scientific statement supported by one or more results. Do not promote a single favorable measurement directly into a dissertation claim.

## Novelty threats

Maintain `novelty/THREAT_REGISTER.md` and candidate-specific threat analysis. If prior art closes a claim, mark it `novelty-closed` and narrow, merge, park, or kill the candidate instead of defending it artificially.