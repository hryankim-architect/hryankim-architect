# H. Ryan Kim, PhD

**Principal Bioinformatics Scientist · AI / Agentic Systems Architect**

[![ORCID](https://img.shields.io/badge/ORCID-0000--0002--1869--0412-green?logo=orcid)](https://orcid.org/0000-0002-1869-0412)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-hryankim-blue?logo=linkedin)](https://www.linkedin.com/in/hryankim/)
[![Citations](https://img.shields.io/badge/citations-~7%2C000-orange)](https://orcid.org/0000-0002-1869-0412)

17+ years delivering clinical bioinformatics across Gilead Sciences, MSKCC, Baylor / Texas Children's, and the NYU / Columbia Genome Centers. Publications in *Nature Medicine*, *Nature Genetics*, *Cancer Discovery*, *Molecular Cell*. Co-PI on a **$5.9M CPRIT** award.

This GitHub is my **self-funded R&D & capability-portrait lab** (04/2026 – present): methods and architecture from my industry tenures, shipped end-to-end as public, clone-and-run repos.

---

## 🔬 Flagship — `omniomics` v0.4.0

[![CI](https://github.com/hryankim-architect/omniomics/actions/workflows/ci.yml/badge.svg)](https://github.com/hryankim-architect/omniomics/actions/workflows/ci.yml)
[![Python](https://img.shields.io/badge/python-3.10–3.12-blue)](https://github.com/hryankim-architect/omniomics)
[![License: MIT](https://img.shields.io/badge/license-MIT-green)](LICENSE)

**Knowledge-anchored residual discovery**: anchor on a zero-parameter textbook prior; gate genome-wide data; mine orthogonal biology the textbook doesn't explain.

Reproduces and extends my [*Molecular Cell* 2015](https://doi.org/10.1016/j.molcel.2015.08.011) study.

| Validation | Result |
|---|---|
| LumA/B knowledge anchor | 20-gene proliferation prior AUROC **0.919 → 0.947** |
| Residual biology | Basal/keratinization axis (Reactome **p≈8e-11**) |
| METABRIC external | Reproduces independently 20/30 genes (**p≈7e-27**) |
| 7-cohort cross-cancer | AUROC ≥ 0.91 squamous vs 0.52–0.61 adeno-only (**30–40 pp bifurcation**) |
| NSCLC anti-PD-1 | Cross-domain replication (p = 0.038) |

**9 external validation datasets · 82 CI-gated tests · PyPI-ready · bioRxiv manuscript in preparation**

```python
from omniomics.multiomics import anchored_residual_discovery
hits = anchored_residual_discovery(prior_score, X_genome_wide, gene_names, y)
```

---

## 🤖 Agentic AI Substrate

**5-node distributed lab** (Apple Silicon + x86 + ARM) running Ollama / LangGraph / ChromaDB / BioMCP / Nextflow + GATK4 / Scanpy.

Closed-loop **Prompt-to-Pill** active-learning loop surfaced **erlotinib as top-1 EGFR candidate** in 0.3 s across a 2,000-compound screen. Regulated-AI primitives (hash-chained NDJSON audit, 4-pattern HITL gates, MLflow + AgentOps cross-reference) designed for FDA / CLIA transfer. Hot-vector p95 = 2 ms · RAG accuracy 100% on 15-question golden set · safety-guard FP 0%.

---

## 📂 Portfolio (11 repos, all CI-green)

| Repo | Domain | Key result |
|---|---|---|
| [`omniomics`](https://github.com/hryankim-architect/omniomics) | Multi-omics engine | 9-cohort cross-cancer validation, bioRxiv-ready |
| [`dmoi-brca-poc`](https://github.com/hryankim-architect/dmoi-brca-poc) | RNA + methylation multi-omics | Cross-cohort METABRIC AUROC **0.9254**, 4-axis reusability |
| [`tp53-aml-hrd-severity`](https://github.com/hryankim-architect/tp53-aml-hrd-severity) | Clinical genomics / survival | Cox HR **8.39**, ~59% HRD-mediated via TP53 |
| [`hnscc-time-multimodal`](https://github.com/hryankim-architect/hnscc-time-multimodal) | Multimodal survival | **55% MAE reduction** vs unimodal baseline |
| [`sc-tumor-annotator`](https://github.com/hryankim-architect/sc-tumor-annotator) | Single-cell CNV | Tumor cell annotation from scRNA-seq |
| [`spatial-niche-mapper`](https://github.com/hryankim-architect/spatial-niche-mapper) | Spatial transcriptomics | Niche mapping ARI **0.921** |
| [`perturb-response-poc`](https://github.com/hryankim-architect/perturb-response-poc) | Perturb-seq | Response prediction F1 **0.989** |
| [`healthomics-lab-orchestrator`](https://github.com/hryankim-architect/healthomics-lab-orchestrator) | Regulated platform engineering | Nextflow DSL2 + hash-chained NDJSON audit |
| [`cdx-clinical-reporter`](https://github.com/hryankim-architect/cdx-clinical-reporter) | CDx reporting | **21 CFR Part 11**-style signed reporting |
| [`multiqc-foundation-gate`](https://github.com/hryankim-architect/multiqc-foundation-gate) | ML on QC telemetry | Sample-inclusion gate from MultiQC metrics |
| [`bioinformatics-repo-scaffold-template`](https://github.com/hryankim-architect/bioinformatics-repo-scaffold-template) | Shared scaffold | v0.5 — CI / MLflow / audit / canary baseline |

All repos share a unified scaffold: shared audit / MLflow / canary substrate, MIT license, English-only docs, reproducible entry points.

---

## 📄 Selected Publications

| Paper | Journal | Citations |
|---|---|---|
| Zehir et al. (*MSK-IMPACT 10,000 patients*) — co-author | *Nature Medicine* 2017 | ~3,210 |
| Jordan\* & **Kim\*** et al. — **co-first author** (*lung adenocarcinoma*) | *Cancer Discovery* 2017 | ~630 |
| Austin et al. (*caveolin-1, pulmonary hypertension*) | *Circ Cardiovascular Genetics* 2012 | ~470 |
| Noh, Wang, **Kim** et al. (*Dnmt3a2 / histone recognition*) | *Molecular Cell* 2015 | ~105 |

Full list: [ORCID 0000-0002-1869-0412](https://orcid.org/0000-0002-1869-0412)

---

> *These repos are capability portraits: end-to-end methods and engineering substrate built from my industry work, validated on public data subsets. Production-scale work at Gilead and MSKCC operated on proprietary cohorts I cannot share — what I can show is the method, the engineering, and the clinical reasoning.*
