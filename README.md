# Regulated clinical bioinformatics + AI safety substrate

Principal Bioinformatics Scientist with 18+ years across academia, NIH-funded research, and industry — including 5 years leading regulated clinical bioinformatics in oncology (CAR-T, immune checkpoint, companion diagnostics, FDA submissions, multi-vendor CDx partnerships).

Several thousand citations across computational oncology, precision medicine, and chromatin / RNA biology publications. Co-first author on a landmark precision-oncology prospective sequencing cohort; its published dataset is now a training corpus for oncology AI models industry-wide.

The five repositories below are a **capability-portrait portfolio**: each one is a single, public, clone-and-run slice of regulated clinical bioinformatics, built on the same agentic AI safety substrate (~9,500 LOC). The substrate provides hash-chained NDJSON audit, a three-pattern HITL approval queue, and MLflow integration; its end-to-end smoke test is a chr20 NA12878 GATK deployment producing 62,466 variants with full stage-by-stage audit traceability.

*Prior chapters: lead and architect. This chapter: also ship.*

---

## Capability-portrait portfolio (5 public repos)

Each repo is one capability claim, MIT-licensed, runnable end-to-end on a single workstation, with the engineering evidence visible rather than narrated.

| Repo | Capability | Climax |
|---|---|---|
| [`tp53-aml-hrd-severity`](https://github.com/hryankim-architect/tp53-aml-hrd-severity) | TP53-driven HRD severity scoring + survival on TCGA-LAML | **v0.3** · Cox HR **8.39** (p=0.024) for TP53 axis · Telli 2016 HRD-scar mediation path-a **p=0.0005, ~59% mediated** |
| [`hnscc-time-multimodal`](https://github.com/hryankim-architect/hnscc-time-multimodal) | IHC + bulk RNA-seq cross-cohort calibration for HNSCC Tumor Immune Microenvironment | **v0.3** · 3-arm pipeline on real public data · 50 TCGA-HNSC patients · **6,725 nuclei segmented via Cellpose 4.x** on DeepLIIF ROIs · LOO MAE **0.210 vs 0.466 intercept-only — 55% MAE reduction** |
| [`multiqc-foundation-gate`](https://github.com/hryankim-architect/multiqc-foundation-gate) | ML gate on MultiQC report metrics (sample include/exclude classifier) | **v0.1** · 3-classifier comparison **LogReg 0.860 / RF 0.840 / MLP 0.400** (honest sklearn-beats-MLP under-fit at n=50, narrated in the README) · 215-entry hash-chained audit · 49 tests |
| [`healthomics-lab-orchestrator`](https://github.com/hryankim-architect/healthomics-lab-orchestrator) | Nextflow DSL2 RNA-seq orchestration with audit-chained substrate hooks | **v0.1** · 22-entry audit chain across an outer Python orchestrator + 4 inner Nextflow processes · macOS-Nextflow tooling lessons captured |
| [`bioinformatics-repo-scaffold-template`](https://github.com/hryankim-architect/bioinformatics-repo-scaffold-template) | Shared substrate scaffold inherited by all four capability portraits | **v0.1** · audit + MLflow + canary + English-only CI + honest-scope README template · ruff-clean, lint-strict, ~674 LOC |

Every repo carries the same honest-scope preamble:

> *Capability portrait, not a research result. Public data is intentionally subsetted to keep the demo small and reproducible on a single workstation.*

Most public bioinformatics repos focus on the analysis. The differentiator here is doing the same analysis with the engineering substrate that a regulated clinical environment would actually require — audit chain, HITL, drift monitor, deterministic canary, English-only enforced commits.

---

## Active work — DMOI POC (private, in development)

`dmoi-brca-poc`: Dialectical Multi-Omics Integration on TCGA-BRCA RNA-seq + DNA methylation. Week-1 complete (6 commits, all CI-green).

Cohort selection landed an honest negative finding: H+ luminal vs H- basal/TN saturated at AUROC = 1.0 across every classifier × feature-set combination. The discrimination target was empirically re-scoped to within-luminal LumA vs LumB (437 LumA / 198 LumB, 417 dual-modality patients).

The new target's baseline headroom map — RNA-only AUROC 0.96, methylation AUROC 0.82–0.88, naive early-fusion concat barely beating RNA-only — is the comparison anchor for the hypothesis-conditioned encoder. Hallmark gene set priors (ESTROGEN_RESPONSE for the LumA pole; E2F_TARGETS / G2M_CHECKPOINT / MYC_TARGETS_V1 for the LumB pole) load with 93–98% feature overlap on the cohort's RNA-seq space.

Will surface publicly when the hypothesis-conditioned encoder lands.

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
