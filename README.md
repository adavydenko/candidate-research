# candidate-research

Canonical research repository for the project «Кандидатская».

The repository stores research state and evidence, not production software. Implementations that become independent software projects live in separate repositories and are referenced here by repository URL + commit SHA.

## Research traceability

`I → PC → H → EXP → R → C → P → DC`

- `I` — idea
- `PC` — paper candidate
- `H` — falsifiable hypothesis
- `EXP` — reproducible experiment
- `R` — observed result
- `C` — scientific claim supported by results
- `P` — manuscript/publication
- `DC` — dissertation/defense claim

## Repository areas

- `ideas/` — living idea index
- `candidates/` — publication candidates, novelty maps, closest prior art and literature kill-tests
- `novelty/` — cross-project novelty map and threat register
- `literature/` — global bibliography and topic-level reviews
- `experiments/` — reproducible experiment definitions/results; experiment code belongs under each experiment's `src/`
- `results/` — evidence statements extracted from experiments
- `claims/` — scientific claims supported by one or more results
- `manuscripts/` — actual publication drafts
- `dissertation/` — mapping of validated claims into dissertation chapters/defense claims
- `decisions/` — research decision log
- `templates/` — reusable research artifact templates

## Workflow

All substantive changes are made through pull requests. `main` is the canonical accepted research state.