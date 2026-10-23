# Classifying TESS Objects of Interest with ~650 Labels: results and figure data

Results and the data behind Figure 1 of the Research Note of the AAS:

> Mouselimis, L. Sp. (2026), *Classifying TESS Objects of Interest with ~650 Labels: Kepler-Pretrained CNN and AutoML Models Benchmarked against ExoMiner++*, Research Notes of the AAS (submitted 2026 October 23).

This repository contains **results only**.

## Files

| File | Content |
|---|---|
| `figure1_data.csv` | The 182 TESS test signals of Figure 1: TFOPWG label and every model's score |
| `figure1.pdf`, `figure1.png` | Figure 1: test ROC-AUC with 95% Gaia-group bootstrap intervals |
| `results_summary.json` | All reported metrics: data counts (including the Kepler pretraining set), five-model test results with intervals, paired differences, top-N, operating thresholds, calibration, ExoMiner++ benchmark, transit-window detection, reproducibility rerun |
| `LICENSE` | Creative Commons Attribution 4.0 International (CC BY 4.0) |

## `figure1_data.csv` columns

| Column | Meaning |
|---|---|
| `toi` | TESS Object of Interest (ExoFOP-TESS snapshot of 2026-09-07) |
| `tic_id` | TESS Input Catalog ID |
| `planet_label` | 1 = TFOPWG confirmed or known planet (CP/KP); 0 = false positive or false alarm (FP/FA) |
| `toi_alerted_utc` | Date the TOI was alerted |
| `alerted_after_2024_01` | True if the TOI was alerted after 2024 January 31 (descriptive only; the ExoMiner++ v2.2.0 models were trained in 2026 May on SPOC two-minute signals from sectors 1–98, so this column does not mark signals unseen by ExoMiner++) |
| `cnn_score` | Kepler-pretrained dual-view CNN fine-tuned on TESS light curves and DV features |
| `autogluon_score` | AutoGluon ensemble on 18 SPOC Data Validation features |
| `blend_cnn_autogluon_rank_score` | Selected combination: rank average, 45% CNN / 55% AutoGluon (weight fixed on validation); ranks are computed within the full 183-signal test batch |
| `exominer_single_score` | NASA ExoMiner++ v2.2.0, single model (planet-validation task, two-minute data, stellar parameters from SPOC, optional Gaia renormalised unit weight error (RUWE) input set to unavailable) |
| `exominer_ensemble_score` | NASA ExoMiner++ v2.2.0, 10-model cross-validation ensemble (same settings) |

One test signal (TOI-1260.03) received no ExoMiner++ score and is not included; metrics on all 183 signals are in `results_summary.json`.

## Reproducibility

The full pipeline was rerun from the archived downloads with pinned software versions (2026-10-18/19). With the Kepler-pretrained weights held fixed, the test ROC-AUC of the selected blend was reproduced exactly (0.940). Repeating the GPU pretraining gave 0.932, within the 95% interval. ExoMiner++ retrieves its inputs from the Mikulski Archive for Space Telescopes (MAST) at run time, so its scores differ slightly between runs (ensemble 0.966 instead of 0.967). `figure1_data.csv` and Figure 1 use the original run; the rerun values are under `reproducibility_rerun` in `results_summary.json`.

## Data credits

Labels from ExoFOP-TESS (TFOPWG dispositions). Light curves and Data Validation products from the TESS Science Processing Operations Center via MAST. Kepler data from MAST and the NASA Exoplanet Archive. Star grouping with Gaia DR3 (ESA). ExoMiner++ scores produced by running NASA's public ExoMiner++ v2.2.0 container.

Dataset DOIs (as cited in the Research Note):

- TESS Light Curves – All Sectors (two-minute cadence), MAST: [10.17909/t9-nmc8-f686](https://doi.org/10.17909/t9-nmc8-f686)
- Kepler light curves, Q0–Q17, long cadence, MAST: [10.17909/T9488N](https://doi.org/10.17909/T9488N)
- Kepler Objects of Interest Cumulative Table, NASA Exoplanet Archive: [10.26133/NEA4](https://doi.org/10.26133/NEA4)
- Exoplanet Follow-up Observing Program (ExoFOP): [10.26134/ExoFOP5](https://doi.org/10.26134/ExoFOP5)

Note: the two IPAC DOIs (NEA4, ExoFOP5) resolve through doi.org to `catcopy.ipac.caltech.edu`, which was unreachable on 2026-10-23. The same DOI records are also at https://www.ipac.caltech.edu/doi/10.26133/NEA4 and https://www.ipac.caltech.edu/doi/10.26134/ExoFOP5.

## License and citation

Released under **CC BY 4.0**: you may share and adapt the material, including commercially, provided you give appropriate credit. Please cite the Research Note above (DOI to be added on publication).

Contact: Lampros Sp. Mouselimis, Monopteryx · [mouselimislampros@monopteryx.com](mailto:mouselimislampros@monopteryx.com) · ORCID [0000-0002-8024-1546](https://orcid.org/0000-0002-8024-1546)
