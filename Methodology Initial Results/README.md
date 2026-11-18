# Results: Open-Source LLMs for Requirements Prioritization with Hallucination Reduction

Experimental results for the paper *"Automated Software Requirements Prioritization Using Open-Source Large Language Models with Hallucination Reduction"* (Kamran Saeed, FAST-NUCES Islamabad).

## Experiment

| Item | Values |
|---|---|
| Models (Ollama, 4-bit) | `llama3.1:8b`, `mistral:7b`, `qwen2.5:7b` |
| Techniques | 100-Dollar, WSJF, AHP |
| Projects | S0 SDMP (Supplier Data Management Platform), S1 CWS (Courseware System), S2 HOM (DigitalHome) |
| Input conditions | clean, incomplete, ambiguous, changing (dynamic) |
| Methods | **B0** base-paper multi-agent method · **M1** fixed answer format (constrained output) · **M2** M1 + audit-and-repair |
| Hardware | Google Colab, NVIDIA T4 GPU |

## Headline results

| Method | Hallucination rate | LLM calls | Latency (s) |
|---|---|---|---|
| B0 | 17.6% | 4.0 | 447.0 |
| M1 | 1.7% | 1.0 | 59.4 |
| M2 | 1.2% | 1.58 | 94.2 |

## Files

| File | Contents |
|---|---|
| `runs.jsonl` | One record per prioritization run (raw model answer, parsed ranks, issues found, metrics, calls, latency) |
| `summary.json` | All summary tables in one file |
| `table_hallucination_by_method.csv` | Main results per method |
| `table_hallucination_by_method_technique.csv` | Results per technique |
| `table_hallucination_by_method_model.csv` | Results per model |
| `table_hallucination_by_scenario.csv` | Results per project |
| `table_hallucination_by_condition.csv` | Results per input condition |
| `table_dynamic.csv` | Changing-requirements condition (deleted requirements still ranked, urgent-requirement shift) |
| `table_technique_validity.csv` | AHP consistency ratio (CR) and 100-Dollar sum checks |
| `table_cost.csv` | LLM calls and latency per method |
| `table_statistics.csv` | Wilcoxon signed-rank tests with Holm correction |
| `table_agreement_consensus_clean.csv`, `table_consistency_clean.csv`, `table_stability_by_condition.csv` | Agreement and stability measures |
| `figures/` | Hallucination reduction, cost vs violation, stability plots |

## Metric columns

- `F`: fabricated requirement IDs (not in the input)
- `Om`: omitted requirements
- `Dup`: duplicated requirements
- `G`: deleted requirements still ranked (changing condition)
- `H`: hallucination rate (share of outputs with any of the above)
- `V`: share of outputs with any rule violation, including technique rules (100-Dollar total, AHP CR ≥ 0.10)
- `parse_ok`: share of answers that could be read as valid JSON
- `n_calls`, `latency_s`: LLM calls and seconds per prioritization

Note: CSV values are rounded to 3 decimals (e.g. M1 hallucination 0.0165 appears as 0.016; the paper reports 1.7%). Some tables contain an extra `M3` column from an exploratory variant; it is not reported in the paper.
