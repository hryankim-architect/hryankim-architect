# Developing Safe, Regulated, and Reproducible Infrastructure for Clinical Bioinformatics

Principal Bioinformatics Scientist with 17+ years across academia, NIH-funded research, and industry, including 5 years leading regulated clinical bioinformatics in oncology (CAR-T, immune checkpoint, companion diagnostics, FDA submissions, multi-vendor CDx partnerships).

Several thousand citations across computational oncology, precision medicine, and chromatin / RNA biology publications. Co-first author on a landmark precision-oncology molecular-characterization study; co-author on the prospective sequencing cohort whose published dataset is now a training corpus for oncology AI models industry-wide.

*Prior chapters: lead and architect. This chapter: also ship.*

**TL;DR** — one engineering principle (*pick the smallest representation that could carry the signal, measure it against an honest baseline, report the verdict faithfully*) applied across **eleven clinical-bioinformatics problems (twelve repos) plus six AI-safety eval harnesses** — all MIT-licensed and clone-and-run on a single laptop. The through-line is one idea: **the discipline that tells me a biomarker is *real* rather than flattering is the same discipline that tells me a model capability is real rather than a flattering benchmark** — clinical-bio capability *and* the measured oversight of it.

**Start here** → [`omniomics`](https://github.com/hryankim-architect/omniomics) **v0.4.0** (the new marquee — knowledge-anchored residual discovery validated across **9 external datasets and a 7-cohort cross-cancer series**; bioRxiv manuscript in preparation), then [`dmoi-brca-poc`](https://github.com/hryankim-architect/dmoi-brca-poc) (the methodology flagship — a parameter-free design beats a trainable variant across cohort, task, and split), then one safety harness, [`sycophancy-eval`](https://github.com/hryankim-architect/sycophancy-eval) (the one carried to real models: naive sycophancy is a small-model artifact, while appeal-to-authority survives scale).

---

## One principle, eleven biological problems and a shared substrate

Most public bioinformatics repos show you an analysis. The twelve below — plus the shared substrate they all inherit — show you a *principle*, applied until it's unmistakable:

> **Pick the smallest, most interpretable representation of the biology that could carry the signal — then measure it against a stronger alternative or a trivial baseline, and report the verdict honestly, whether the compact choice wins, ties, or loses.**

*Representation → baseline → faithful verdict.* That discipline is the portable skill behind every repo here — and it is, precisely, why AI safety is needed. The central safety question is not "can the model do this?" but "do we *know* the capability is real, rather than a flattering benchmark?" The **representation** decides what is even being measured, the **baseline** forces the number to mean something relative to an honest comparison, and the **faithful verdict** reports the unfavorable result — *the compact version only tied, the trainable variant was refuted, the null stands* — instead of burying it. That last step is the whole of alignment and evals in miniature, and it is exactly the posture the AI-safety repos below make explicit.

Every repo also runs on one agentic AI-safety substrate (~9,500 LOC): hash-chained NDJSON audit, a three-pattern HITL approval queue, MLflow + drift monitoring, a deterministic canary. Its end-to-end smoke test is a chr20 NA12878 GATK deployment producing 62,466 variants with full stage-by-stage audit traceability. So the discipline isn't only analytical — it's the audit-and-evidence rigor a regulated clinical environment actually requires.

## The principle, repo by repo

Each repo is MIT-licensed, clone-and-run on a single workstation, with the engineering evidence visible rather than narrated. Read each row as *representation → baseline → honest verdict*.

| Repo | Compact representation | Baseline / bigger alternative | Verdict, reported honestly |
|---|---|---|---|
| [`omniomics`](https://github.com/hryankim-architect/omniomics) **v0.4.0 ★** | a **zero-parameter textbook prior** as anchor; genome-wide data gated as a non-negative residual; residual mined for orthogonal biology | random gene panels (null); direct data models (no anchor) | **textbook prior wins, then the residual names what it doesn't explain.** 20-gene proliferation prior AUROC 0.919 → 0.947; residual recovers basal/keratinization axis (Reactome p≈8e-11); replicated across **9 external datasets** — METABRIC (p≈7e-27), **7-cohort cross-cancer series** (AUROC ≥ 0.91 squamous vs 0.52–0.61 adeno, **30–40 pp bifurcation**), NSCLC anti-PD-1 (p=0.038). **82 CI-gated tests. bioRxiv manuscript in preparation.** |
| [`dmoi-brca-poc`](https://github.com/hryankim-architect/dmoi-brca-poc) **(methodology flagship)** | pole-feature views + a 1-scalar disagreement signal; **parameter-free** attention masks | a **trainable** pathway-attention variant | **trainable variant refuted.** Parameter-free design held across cohort, task, and split (LumA-vs-LumB TCGA AUROC 0.968 / METABRIC 0.909; Luminal-vs-Basal 5-fold AUROC 1.0000 ± 0.0000) and transferred to a **third task axis** HER2-vs-Luminal (v0.14: TCGA 0.892 ± 0.056 / METABRIC 0.893) — the richer interface didn't help |
| [`multiomics-cnv-conditioned-poc`](https://github.com/hryankim-architect/multiomics-cnv-conditioned-poc) | a third **CNV pole-conditioned modality** (amplicon-masked) added to DMOI's RNA + methylation | the same model on **RNA + methylation only** | **axis-specific, with a transfer law.** Within-cohort, CNV helps the ERBB2-defined HER2 axis (**+0.125** AUROC) and not proliferation; cross-platform, a per-gene **amplicon-strength → transfer law** holds (pooled Spearman **+0.84**, externally validated **+0.89** on a third cohort), while a gated-fusion "fix" is reported as an honest null |
| [`hnscc-time-multimodal`](https://github.com/hryankim-architect/hnscc-time-multimodal) | a shared **4-density TIME schema** reconciling IHC + bulk RNA-seq | intercept-only (predict-the-mean) | **compact wins.** Cross-cohort LOO MAE **0.210 vs 0.466** (55% reduction); 6,725 nuclei segmented via Cellpose 4.x on DeepLIIF ROIs |
| [`multiqc-foundation-gate`](https://github.com/hryankim-architect/multiqc-foundation-gate) | a **28-feature engineered vector** + linear/tree model | an MLP (~1.5k params) | **compact wins.** sklearn baselines (LogReg **0.80**, RandomForest **0.84**) beat the MLP's **0.40** at n=50 — capacity without data hurts, narrated honestly |
| [`sc-tumor-annotator`](https://github.com/hryankim-architect/sc-tumor-annotator) | a single interpretable **CNV scalar** (chromosome-length-normalized) | a **30-PC expression embedding** | **compact ties big.** 0.94 vs 0.986 macro-F1 (within ~4 pts) — value is interpretability, not accuracy |
| [`spatial-niche-mapper`](https://github.com/hryankim-architect/spatial-niche-mapper) | a **neighbourhood-composition vector** (spatial k-NN) | per-spot proportions / raw expression | **compact wins.** Niche **ARI 0.921**; per-spot proportions re-find cell types, not regions |
| [`perturb-response-poc`](https://github.com/hryankim-architect/perturb-response-poc) | a low-dim **perturbation embedding** → ridge map | a mean-response baseline (nonlinear GEARS/CPA is the next step) | **linear suffices for now.** Held-out perturbation corr **0.60 vs 0.05** (lift +0.55) |
| [`tp53-aml-hrd-severity`](https://github.com/hryankim-architect/tp53-aml-hrd-severity) | a **bounded composite** (tier+VAF, HRD-norm), nothing learned | a many-parameter / learned Cox | **by design.** Nothing to over-fit at n=15; Cox HR 8.39 (p=0.024) emitted but labeled descriptive |
| [`cdx-clinical-reporter`](https://github.com/hryankim-architect/cdx-clinical-reporter) | a single **256-bit content hash** as the report's integrity representation | the report itself (tamper-evidence is the test) | **tamper-evident.** Any edit changes the hash; a 21 CFR Part 11-style signature ledger binds authored + approved sign-offs to it |
| [`healthomics-lab-orchestrator`](https://github.com/hryankim-architect/healthomics-lab-orchestrator) | a **hash-linked NDJSON record** as the representation of run provenance | an unverifiable run log | **end-to-end verifiable.** One append-only chain represents a whole Nextflow DSL2 pipeline's audit state (22-entry chain across orchestrator + 4 processes) |
| [`bioinformatics-repo-scaffold-template`](https://github.com/hryankim-architect/bioinformatics-repo-scaffold-template) | the **shared substrate scaffold** every repo inherits | ad-hoc, unaudited demos | **makes the principle reproducible.** Audit + MLflow + canary + honest-scope README, ~820 LOC |

Every repo carries an explicit honest-scope note in the same spirit (wording tailored per repo, in the README and each `docs/what-is-out-of-scope.md`) — clean-room or synthetic / intentionally-subsetted public data, framed as an engineering demo rather than a research publication or benchmark:

> *These are self-contained engineering demos, not research publications. Public data is subsetted to keep each demo small and fast.*

## The pattern, stated once

1. **Compact + interpretable first.** A zero-parameter textbook prior, a CNV scalar, a neighbourhood vector, a pole-masked view, a 28-feature vector, a content hash — each the smallest representation that could carry the signal.
2. **Always a baseline or a bigger alternative.** The number only means something *relative to* the honest comparison.
3. **Report the verdict faithfully** — "compact ties big," "compact wins," "linear suffices for now," "the trainable variant was refuted," "the null stands." Nulls and ties are kept, not buried.

No single result carries the portfolio. The repeated principle does — across the axes a clinical-bioinformatics principal is expected to own end to end: knowledge-anchored multi-omics discovery with cross-cancer validation (`omniomics`, the marquee), hypothesis-conditioned multi-omics interpretability (`dmoi-brca-poc`, the methodology flagship) and its cross-platform CNV-transfer extension (`multiomics-cnv-conditioned-poc`), pipeline orchestration (`healthomics-lab-orchestrator`), machine learning on operational QC telemetry (`multiqc-foundation-gate`), clinical genomics with survival modeling (`tp53-aml-hrd-severity`), multimodal tumor-microenvironment inference (`hnscc-time-multimodal`), single-cell tumor annotation with copy-number inference (`sc-tumor-annotator`), regulated CDx reporting with 21 CFR Part 11-style electronic signatures (`cdx-clinical-reporter`), spatial-transcriptomics deconvolution and niche mapping (`spatial-niche-mapper`), and single-cell perturbation-response prediction (`perturb-response-poc`), all built on one shared substrate scaffold (`bioinformatics-repo-scaffold-template`).

---

## The second thread — measured oversight (AI-safety eval suite)

Alongside the bioinformatics repos, a parallel AI-safety suite *measures oversight itself* — six focused, public, clean-room eval harnesses, one per research pillar, in the same house style as the bio repos: hash-chained audit of every decision, a transparent mock/synthetic responder (no live model or tools required), a pure scorer, CI, an explicit `what-is-out-of-scope.md`, and honest reporting where the metric must be *able* to look bad. The suite spans oversight → robustness → red-teaming → alignment → control → fairness.

| Repo | Pillar | What it measures | Headline |
|---|---|---|---|
| [`honesty-rubric-eval`](https://github.com/hryankim-architect/honesty-rubric-eval) **v0.2** | Scalable oversight | judge–expert agreement on a procedure-not-position honesty rubric | a 7B judge does *not* match experts out of the box but improves as leakage-free experience accumulates (κ **0.41 → 0.61**, K=0→3) |
| [`cot-faithfulness-audit`](https://github.com/hryankim-architect/cot-faithfulness-audit) **v0.2** | Robustness (CoT faithfulness) | does stated reasoning match the actual tool calls / decision? | planted-unfaithful recall **1.00** (4/4 controls — too few for a CI); counterfactual flip-rate **1.00** |
| [`agent-refusal-eval`](https://github.com/hryankim-architect/agent-refusal-eval) **v0.3** | Evals & red-teaming | does a screening gate refuse abstract dual-use intent without over-refusing? | refusal-recall **1.00** @ false-refusal **0.00** on a synthetic set (+ real-model gate adapter) |
| [`sycophancy-eval`](https://github.com/hryankim-architect/sycophancy-eval) **v1.1** | Alignment (pressure-robustness) | does a correct answer flip under social pressure? | **real-model live result:** a 0.5B model caves **0.75**, but a 7B model fully resists plain insistence (**0.000**) while appeal-to-**authority still flips it 43%** — naive sycophancy is a small-model artifact, authority framing is not |
| [`sandbagging-eval`](https://github.com/hryankim-architect/sandbagging-eval) **v0.4** | Alignment & control | does accuracy drop when the model knows it's evaluated? | sandbagging_gap **0.60** (mock); real-model adapter + pluggable LLM-judge grader |
| [`fairness-audit`](https://github.com/hryankim-architect/fairness-audit) **v0.2** | Fairness & bias | demographic parity **vs** equalized odds + the cost of each mitigation | the two fairness metrics *cannot both* be satisfied; calibration fixes a measurement-bias cohort with no trade-off |

The aggregator [`ai-safety-evals`](https://github.com/hryankim-architect/ai-safety-evals) **v0.1** runs all six offline and emits one `SCORECARD.md` with **no single aggregate score** — the heterogeneous metrics and their trade-offs are the point, not a number to game.

The two threads meet at **calibration**: the flagship perturbs the *world* (cohort shift) and `sycophancy-eval` perturbs the *conversation* (a confident wrong push), and the non-obvious payoff is that calibration and pushback-robustness are *distinct* trust axes — one does not imply the other. Honest evaluation also runs through the bio repos directly: calibration reported as a **null** where it doesn't transfer (`dmoi-brca-poc` cross-cohort), a gate calibration diagnostic (`multiqc-foundation-gate`, RF ECE 0.05), a per-gene amplicon-strength→transfer law externally validated alongside two honest fusion nulls (`multiomics-cnv-conditioned-poc`), and feature-attribution validated against ground truth (`perturb-response-poc`). That pairing — clinical-bio capability **and** the measured oversight of it — is the portfolio's core differentiator.

---

## Substrate philosophy

All the public repos above run on the same substrate. **What every public repo inherits — and what you can clone and run — is the audit / canary / observability / honest-scope layer** (the first bullet below). **The heavier control machinery — the Constitutional-AI critic, the HITL approval queue, drift monitoring, the GATK pipeline — lives in the *internal* substrate; it is described here for context, not shipped in the public repos.**

- **Audit ledger**: tamper-evident NDJSON, each entry chained to the previous. All public repos emit the same format, so one audit consumer handles any of them.
- **HITL substrate**: three-pattern approval queue (kickoff / intermediate / commit) designed around clinical decision points.
- **Drift monitor**: MLflow run cross-reference, plus a critic that applies seven explicit principles to every verdict.
- **GATK chr20 NA12878**: full small-variant pipeline producing 62,466 variants with ti/tv 2.19 and stage-by-stage audit traceability.
- **~132 engineering lessons captured** in root-cause format since April 2026, the kind of judgment usually left in private post-mortems.

Closed-loop discipline: every substrate fix is itself logged to the audit chain, and the post-fix state is verified by a fresh canary run before the fix is marked complete.

---

## Engagement

Open to Principal / Senior Principal IC roles in regulated clinical bioinformatics, computational oncology, or AI-for-biology platform engineering. The repos above are the starting point; a GitHub Issue on any of them is a fine way to begin a conversation.
