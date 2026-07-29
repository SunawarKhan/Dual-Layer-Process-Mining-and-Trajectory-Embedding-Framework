
# DPTEM — Dual-Layer Process-mining and Trajectory-Embedding Model

**Process Mining + Patient-Trajectory Analysis for ICU Clinical-Pathway Discovery and Risk Prediction (MIMIC-III)**

DPTEM is an end-to-end framework that fuses two complementary views of an ICU admission — the **process view** (how care events follow one another) and the **trajectory view** (how a patient's physiology evolves over time) — into a single representation, the **Temporal Process-aware Clinical Trajectory Graph (TP-CTG)**, and uses it to predict clinical outcomes.

The notebook runs top-to-bottom on the open-access **MIMIC-III Clinical Database Demo v1.4** and produces every table and figure with real numbers. The demo is used for structural and computational validation; full-MIMIC hooks are marked throughout with `# FULL-MIMIC`.

---

## Authors

- **Sunawar Khan**1
- **Rahma Zayoud**
- **Ibrahim Alreshidi**
- **Sghaier Guizani**
- **Habib Hamam**

> ¹ Corresponding author. *(Sunawar Khan, National College of Business Administration and Economics, Lahore, Pk)*

---

## Highlights

- **Dual-layer fusion** — process-mining features + trajectory embeddings + cluster assignment + static demographics, combined into one TP-CTG representation.
- **Three prediction heads** — in-hospital **mortality** (binary), **length-of-stay** (3-class: short / medium / long), and **deterioration** (binary early-warning proxy).
- **Reviewer-grade evaluation** — patient-grouped repeated stratified cross-validation, leakage audit, leave-one-block-out ablation with paired significance testing, calibration and recalibration.
- **Runs anywhere** — GPU optional; graceful fallbacks when `pm4py`, `tslearn`, `lifelines`, or `shap` are not installed.

---

## Pipeline

1. **Data loading** — MIMIC-III demo subset (`ADMISSIONS`, `PATIENTS`, `LABEVENTS`, `D_LABITEMS`); full-MIMIC tables auto-detected when present.
2. **Pre-processing & cohort construction** — one ICU admission (`HADM_ID`) = one process *case*; age corrected for MIMIC's 300-year shift.
3. **Event-log construction** — the canonical 5-tuple `(Case ID, Activity, Timestamp, Resource, Event Type)`.
4. **Process-mining module (PM4Py)** — directly-follows graph, inductive-miner Petri net, empirical transition matrix.
5. **Trajectory modeling** — hourly lab-value state tensor, BiLSTM/Transformer sequence embedding, DTW / soft-DTW k-means clustering.
6. **Fusion model (TP-CTG) & prediction** — gradient-boosted baseline and a small joint MLP for the three heads.
7. **Extended experiments** — survival analysis (Kaplan–Meier + Cox), readmission prediction, trace-variant & bottleneck analysis, process-miner comparison, diagnosis-based phenotyping.
8. **Enriched evaluation protocol** — patient-grouped CV, leakage audit, internal baselines on identical splits, calibration (Brier / ECE, Platt & isotonic recalibration).

---

## Repository structure

```
DPTEM_MIMIC3_repository/
├── Output/
│   ├── Figure/
│   └── Tables/
├── .gitset
├── DPTEM_MIMIC3_process_mining.ipynb
├── LICENSE
├── README.md
└── requirements.txt
```

---

## Requirements

- Python 3.9+
- Core: `numpy`, `pandas`, `scipy`, `scikit-learn`, `matplotlib`
- Deep learning: `torch`
- Process mining: `pm4py`
- Trajectories & survival: `tslearn`, `lifelines`
- Interpretability: `shap`

Install everything with:

```bash
pip install numpy pandas scipy scikit-learn matplotlib torch pm4py tslearn lifelines shap
```

---

## Getting started

### Option A — Google Colab (one click)
Open the notebook in Colab and run the first setup cell. It installs the process-mining libraries and downloads the four open-access MIMIC-III **demo** CSVs into `./data`. The rest of the notebook runs top-to-bottom.

### Option B — Local
```bash
git clone https://github.com/<your-username>/DPTEM.git
cd DPTEM
pip install -r requirements.txt   # or the pip line above
jupyter notebook DPTEM_MIMIC3_process_mining_trajectory_REVISED.ipynb
```

Place the MIMIC-III demo CSVs (`ADMISSIONS`, `PATIENTS`, `LABEVENTS`, `D_LABITEMS`) in `./data`, then run all cells.

---

## Scaling to full MIMIC-III

The notebook was built to grow from the demo to the full database. Search for the `# FULL-MIMIC` markers to enable extra event sources such as `ICUSTAYS` (`ICU_IN_<unit>`, `ICU_OUT`), `PRESCRIPTIONS` (`RX_<drug>`), and `CHARTEVENTS` vitals. Access to the full MIMIC-III database requires credentialing on [PhysioNet](https://physionet.org/) and completion of the required training.

---

## Data & ethics

This project uses the publicly available **MIMIC-III Clinical Database Demo v1.4**. No protected health information is redistributed in this repository. Users working with the full MIMIC-III database must comply with the PhysioNet Credentialed Health Data Use Agreement. Results on the demo subset are illustrative and are **not** presented as evidence of predictive superiority.

---

## Citation

If you use this work, please cite:

```bibtex
@article{khan_dptem,
  title   = {Dual-Layer-Process-Mining-and-Trajectory-Embedding-Framework},
  author  = {Khan, Sunawar and Zayoud, Rahma and Alreshidi, Ibrahim and
             Guizani, Sghaier and Hamam, Habib},
  year    = {2026}
}
```

*(Update the venue, volume, DOI, and year once the paper is published.)*

---

## Acknowledgements

Built on the [MIMIC-III](https://mimic.mit.edu/) database (Johnson et al.) and the [PM4Py](https://pm4py.fit.fraunhofer.de/) process-mining library.

## License

Add a license (e.g. MIT) in a `LICENSE` file. Note that any use of MIMIC data remains subject to the PhysioNet data use agreement.
