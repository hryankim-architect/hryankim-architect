# Regulated clinical bioinformatics + AI safety substrate

Principal Bioinformatics Scientist with 18+ years across academia, NIH-funded research, and industry — including 5 years leading regulated clinical bioinformatics in oncology (CAR-T, immune checkpoint, companion diagnostics, FDA submissions, multi-vendor CDx partnerships).

Several thousand citations across computational oncology, precision medicine, and chromatin / RNA biology publications. Co-first author on a landmark precision-oncology prospective sequencing cohort; its published dataset is now a training corpus for oncology AI models industry-wide.

The seven repositories below are a **capability-portrait portfolio**: each one is a single, public, clone-and-run slice of regulated clinical bioinformatics, built on the same agentic AI safety substrate (~9,500 LOC). The substrate provides hash-chained NDJSON audit, a three-pattern HITL approval queue, and MLflow integration; its end-to-end smoke test is a chr20 NA12878 GATK deployment producing 62,466 variants with full stage-by-stage audit traceability.

*Prior chapters: lead and architect. This chapter: also ship.*

---

## Capability-portrait portfolio (7 public repos)

Each repo is one capability claim, MIT-licensed, runnable end-to-end on a single workstation, with the engineering evidence visible rather than narrated.

| Repo | Capability | Climax |
|---|---|---|
| [`tp53-aml-hrd-severity`](https://github.com/hryankim-architect/tp53-aml-hrd-severity) | TP53-driven HRD severity scoring + survival on TCGA-LAML | **v0.3** · Cox HR **8.39** (p=0.024) for TP53 axis · Telli 2016 HRD-scar mediation path-a **p=0.0005, ~59% mediated** |
| [`hnscc-time-multimodal`](https://github.com/hryankim-architect/hnscc-time-multimodal) | IHC + bulk RNA-seq cross-cohort calibration for HNSCC Tumor Immune Microenvironment | **v0.3** · 3-arm pipeline on real public data · 50 TCGA-HNSC patients · **6,725 nuclei segmented via Cellpose 4.x** on DeepLIIF ROIs · LOO MAE **0.210 vs 0.466 intercept-only — 55% MAE reduction** |
| [`dmoi-brca-poc`](https://github.com/hryankim-architect/dmoi-brca-poc) | Hypothesis-conditioned multi-omics (RNA + HM450 methylation) on TCGA-BRCA, with calibration / cross-cohort / cross-task / 3-variant architecture validation -- four axes of framework reusability empirically confirmed AND split-invariant on both task axes | **v0.12-A** · LumA-vs-LumB TCGA test **AUROC 0.968** + METABRIC **0.909** (Jaccard 0.667 gene-level); v0.5/v0.6 Hallmark rollup showed LumA pole loads ER ~300× cell-cycle and LumB loads cell-cycle ~45× ER, finding survives full 50-set widening; **v0.7+v0.8 confirmed gene-level commitment is the right architectural level via 3-variant matched-basin convergence (richer interface didn't help); v0.9 transferred the same v0.6 architecture to Luminal-vs-Basal on TCGA (AUROC 1.000, 8/8 expected priors in per-pole IG top-5); v0.10 composed that with cross-cohort generalization: METABRIC Luminal-vs-Basal n=1,384 AUROC 0.965 with the SAME 8/8 priors hit AND identical per-pole IG top-3 to TCGA. v0.11 sealed the Luminal-vs-Basal four-axis result as split-invariant via 5-fold StratifiedKFold (every fold AUROC = 1.000, mean ± std = 1.0000 ± 0.0000; top-3 pairwise Jaccard = 1.0 on both poles). v0.12-A sealed the matching closure on LumA-vs-LumB via 5-fold TCGA cohort_v2 × full-METABRIC per fold (QN re-fit per fold): TCGA val AUROC 0.9702 ± 0.0122, METABRIC AUROC 0.9254 ± 0.0052 (std = 0.5 pp -- cross-cohort metric essentially deterministic), 2/2 LumA + 3/3 LumB expected priors hit 5/5 folds, LumB top-3 Jaccard = 1.0. The framework is simultaneously cohort-invariant, task-invariant, AND split-invariant on both task axes. v0.6 → v0.12-A reads as found → systematically tested → generalized across cohort → generalized across task → generalized across both → sealed under split perturbation on every measurable axis.** |
| [`multiqc-foundation-gate`](https://github.com/hryankim-architect/multiqc-foundation-gate) | ML gate on MultiQC report metrics (sample include/exclude classifier) | **v0.1** · 3-classifier comparison **LogReg 0.860 / RF 0.840 / MLP 0.400** (honest sklearn-beats-MLP under-fit at n=50, narrated in the README) · 215-entry hash-chained audit · 49 tests |
| [`healthomics-lab-orchestrator`](https://github.com/hryankim-architect/healthomics-lab-orchestrator) | Nextflow DSL2 RNA-seq orchestration with audit-chained substrate hooks | **v0.1** · 22-entry audit chain across an outer Python orchestrator + 4 inner Nextflow processes · macOS-Nextflow tooling lessons captured |
| [`sc-tumor-annotator`](https://github.com/hryankim-architect/sc-tumor-annotator) | Tree-based hierarchical tumor scRNA-seq annotation + expression-based CNV inference (chromosome-length-normalized malignant-cell score) + cancer subtype/grade prediction; clean-room, synthetic-data POC built from public methods only | **v0.2** · 4-stage annotator (compartment → stromal type → malignant call → subtype + grade) · v0.2 adds a hard subclonal-CNV regime + an honest **CNV-feature ablation**: a single interpretable CNV scalar reaches **0.94** malignant-call macro-F1 vs a 30-PC embedding's **0.99** (CNV-blind kNN baseline 0.92), adding it to the embedding is only marginally additive (+0.004) — framed as a compact-interpretable-channel result, not a large accuracy jump · 5-fold CV + independent-cohort harness · `adapter.py` Scanpy/AnnData bridge · deterministic, CPU-only, 17 tests, ruff + English-only CI |
| [`bioinformatics-repo-scaffold-template`](https://github.com/hryankim-architect/bioinformatics-repo-scaffold-template) | Shared substrate scaffold inherited by every capability portrait | **v0.1** · audit + MLflow + canary + English-only CI + honest-scope README template · ruff-clean, lint-strict, ~674 LOC |

Every repo carries the same honest-scope preamble:

> *Capability portrait, not a research result. Public data is intentionally subsetted to keep the demo small and reproducible on a single workstation.*

Most public bioinformatics repos focus on the analysis. The differentiator here is doing the same analysis with the engineering substrate that a regulated clinical environment would actually require — audit chain, HITL, drift monitor, deterministic canary, English-only enforced commits.

Across the portfolio the six capability portraits span the axes a clinical-bioinformatics principal is expected to own end to end: pipeline orchestration (`healthomics-lab-orchestrator`), machine learning on operational QC telemetry (`multiqc-foundation-gate`), clinical genomics with survival modeling (`tp53-aml-hrd-severity`), multimodal tumor-microenvironment inference (`hnscc-time-multimodal`), hypothesis-conditioned multi-omics interpretability (`dmoi-brca-poc`, the flagship), and single-cell tumor annotation with copy-number inference (`sc-tumor-annotator`) — all sharing the seventh repo's scaffold. No single project carries the portfolio; the span does.

---

## Substrate philosophy

The capability portraits all run on the same substrate. The substrate itself is internal, but every public repo above demonstrates a clone-and-run slice of it.

- **Audit ledger** — tamper-evident NDJSON, hash-chained per entry. Every public capability portrait emits in the same format, so a single audit consumer can read any of them.
- **HITL substrate** — three-pattern approval queue (kickoff / intermediate / commit) designed around clinical decision points.
- **Drift monitor** — MLflow run cross-reference, plus a critic that applies seven explicit principles to every verdict.
- **GATK chr20 NA12878** — full small-variant pipeline producing 62,466 variants with ti/tv 2.19, stage-by-stage audit traceability.
- **~132 engineering lessons captured** in Symptom / Cause / Fix / Generalizing form — the kind of judgment that's usually only documented in private post-mortems.

Closed-loop discipline: every substrate fix is itself logged to the audit chain, and the post-fix state is verified by a fresh canary run before the fix is marked complete.

---

## Engagement

Open to Principal / Senior Principal IC roles in regulated clinical bioinformatics, computational oncology, or AI-for-biology platform engineering. The portfolio above is the conversation starter; opening a GitHub Issue on any of the linked repos is the natural first thread.
