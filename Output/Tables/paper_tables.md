
### T_leakage_audit

| Mortality, fusion features | OOF AUROC |
|---|---|
| Admission-level CV (leaky) | 0.744 |
| Patient-grouped CV (correct) | 0.742 |
| Optimism attributable to patient leakage | 0.002 |

### T_deterioration_leak

| Deterioration head (patient-grouped OOF) | AUROC | AUPRC | F1 |
|---|---|---|---|
| All fusion features (as published) | 0.884 | 0.947 | 0.85 |
| Proxy constituents removed | 0.539 | 0.685 | 0.712 |

### T_baselines_mortality

| Model | n_feat | AUROC | AUPRC | F1 | BalAcc | Brier |
|---|---|---|---|---|---|---|
| Prevalence (no features) | 2 | 0.364 [0.245–0.497] | 0.256 | 0.0 | 0.5 | 0.222 |
| Demographics only (LR) | 2 | 0.479 [0.352–0.586] | 0.328 | 0.364 | 0.469 | 0.255 |
| Process-mining only (LR) | 5 | 0.579 [0.439–0.744] | 0.39 | 0.466 | 0.581 | 0.263 |
| Process-mining only (GBT) | 5 | 0.742 [0.628–0.860] | 0.637 | 0.639 | 0.737 | 0.172 |
| Trajectory only (LR) | 36 | 0.537 [0.425–0.644] | 0.347 | 0.356 | 0.509 | 0.301 |
| Trajectory only (GBT) | 36 | 0.582 [0.467–0.688] | 0.444 | 0.41 | 0.576 | 0.283 |
| Trajectory cluster only (LR) | 1 | 0.424 [0.318–0.579] | 0.315 | 0.4 | 0.475 | 0.254 |
| DPTEM fusion (RF) | 44 | 0.735 [0.618–0.830] | 0.637 | 0.441 | 0.629 | 0.181 |
| DPTEM fusion (GBT) | 44 | 0.742 [0.639–0.838] | 0.633 | 0.582 | 0.698 | 0.203 |

### T_baselines_deterior

| Model | n_feat | AUROC | AUPRC | F1 | BalAcc | Brier |
|---|---|---|---|---|---|---|
| Prevalence (no features) | 2 | 0.372 [0.279–0.486] | 0.567 | 0.777 | 0.5 | 0.243 |
| Demographics only (LR) | 2 | 0.365 [0.266–0.505] | 0.599 | 0.604 | 0.428 | 0.256 |
| Process-mining only (LR) | 5 | 0.815 [0.737–0.878] | 0.913 | 0.797 | 0.805 | 0.171 |
| Process-mining only (GBT) | 5 | 0.916 [0.871–0.961] | 0.963 | 0.907 | 0.881 | 0.106 |
| Trajectory only (LR) | 36 | 0.533 [0.431–0.659] | 0.664 | 0.679 | 0.585 | 0.314 |
| Trajectory only (GBT) | 36 | 0.526 [0.444–0.639] | 0.676 | 0.71 | 0.513 | 0.314 |
| Trajectory cluster only (LR) | 1 | 0.423 [0.344–0.532] | 0.588 | 0.598 | 0.448 | 0.252 |
| DPTEM fusion (RF) | 44 | 0.873 [0.818–0.928] | 0.936 | 0.85 | 0.784 | 0.143 |
| DPTEM fusion (GBT) | 44 | 0.884 [0.829–0.931] | 0.947 | 0.85 | 0.808 | 0.15 |

### T_ablation_loo

| Configuration | n_feat | AUROC | dAUROC | p_wilcoxon | p_corrected_t |
|---|---|---|---|---|---|
| DPTEM fusion (all blocks) | 44 | 0.735 ± 0.089 | — | — | — |
| − process block | 39 | 0.613 ± 0.145 | +0.122 | 0.000 | 0.122 |
| − trajectory block | 8 | 0.792 ± 0.110 | -0.057 | 0.008 | 0.306 |
| − cluster block | 43 | 0.742 ± 0.085 | -0.007 | 0.192 | 0.653 |
| − demographics block | 42 | 0.740 ± 0.091 | -0.005 | 0.244 | 0.754 |

### T_calibration

| Calibration | AUROC | Brier | Reliability | Resolution | Uncertainty | ECE |
|---|---|---|---|---|---|---|
| Uncalibrated | 0.742 | 0.203 | 0.0395 | 0.049 | 0.2139 | 0.184 |
| Platt (sigmoid) | 0.712 | 0.188 | 0.0076 | 0.0279 | 0.2139 | 0.079 |
| Isotonic | 0.784 | 0.168 | 0.0108 | 0.0558 | 0.2139 | 0.092 |

### T_operating_points

| Operating point | Threshold | Sensitivity | Specificity | PPV | NPV | Alert rate |
|---|---|---|---|---|---|---|
| high-sensitivity screen | 0.011 | 0.9 | 0.258 | 0.353 | 0.852 | 0.791 |
| default | 0.5 | 0.575 | 0.82 | 0.59 | 0.811 | 0.302 |
| high-specificity escalation | 0.738 | 0.475 | 0.91 | 0.704 | 0.794 | 0.209 |

### T_subgroups

| Stratum | n | Prevalence | AUROC | AUPRC | Brier | Mean predicted |
|---|---|---|---|---|---|---|
| sex = Female | 59 | 0.356 | 0.704 | 0.628 | 0.25 | 0.361 |
| sex = Male | 70 | 0.271 | 0.774 | 0.655 | 0.163 | 0.275 |
| age band = <50 | 16 | 0.562 | 0.54 | 0.648 | 0.331 | 0.587 |
| age band = 50–64 | 21 | 0.048 | 0.55 | 0.1 | 0.114 | 0.14 |
| age band = 65–79 | 46 | 0.217 | 0.833 | 0.689 | 0.13 | 0.255 |
| age band = ≥80 | 46 | 0.435 | 0.669 | 0.686 | 0.273 | 0.358 |
| cluster = 0 | 44 | 0.341 | 0.628 | 0.572 | 0.274 | 0.273 |
| cluster = 1 | 80 | 0.262 | 0.769 | 0.602 | 0.176 | 0.311 |

### T_seed_stability

| seed | fusion | process_only |
|---|---|---|
| 42 | 0.742 | 0.742 |
| 43 | 0.716 | 0.754 |
| 44 | 0.731 | 0.736 |
| 45 | 0.692 | 0.664 |
| 46 | 0.724 | 0.757 |
| mean ± sd | 0.721 ± 0.019 | 0.731 ± 0.038 |

### T_cluster_sensitivity

| K | Fusion OOF AUROC | Silhouette | p (cluster vs mortality) |
|---|---|---|---|
| 2.0 | 0.742 | 0.151 | 0.1984 |
| 3.0 | 0.742 | 0.132 | 0.0776 |
| 4.0 | 0.742 | 0.137 | 0.0636 |
| 5.0 | 0.741 | 0.112 | 0.1029 |
| 6.0 | 0.752 | 0.046 | 0.1302 |