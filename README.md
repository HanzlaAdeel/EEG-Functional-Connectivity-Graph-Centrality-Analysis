# EEG Functional Connectivity & Graph Centrality Analysis

This repository contains a neuroimaging pipeline implemented in Python for analyzing electroencephalogram (EEG) functional brain networks[cite: 1]. It computes phase-based connectivity, extracts topological graph centralities, maps them across anatomical brain regions, and conducts statistical comparisons across clinical cohorts[cite: 1].

---

## 📊 Dataset: OpenNeuro `ds004504`
The project utilizes the **OpenNeuro ds004504** dataset[cite: 1], a BIDS-standardized resting-state EEG dataset with eyes-closed recordings (`sub-*_task-eyesclosed_eeg.set`)[cite: 1]. 

The cohort comprises subjects across three groups[cite: 1]:
- **AD**: Alzheimer's Disease[cite: 1]
- **FTD (F)**: Frontotemporal Dementia[cite: 1]
- **HC (C)**: Healthy Controls[cite: 1]

Associated clinical metadata includes **Age**, **Gender**, and **MMSE** (Mini-Mental State Examination) cognitive scores[cite: 1].

---

## ⚙️ What Was Done (Pipeline Overview)

1. **Cohort & BIDS Integration**
   - Loaded and cleaned subject demographics (`participants.tsv`), harmonizing labels for Alzheimer’s (`AD`), Frontotemporal Dementia (`F`), and Controls (`C`)[cite: 1].

2. **Standard 10–20 Channel & Regional Mapping**
   - Configured 19 standard scalp channels:  
     `Fp1`, `Fp2`, `F3`, `F4`, `C3`, `C4`, `P3`, `P4`, `O1`, `O2`, `F7`, `F8`, `T3`, `T4`, `T5`, `T6`, `Fz`, `Cz`, `Pz`[cite: 1].
   - Organized electrodes into anatomical and topographical subdivisions:
     - **Lobes / Regions**: Frontal, Temporal, Parietal, Occipital[cite: 1]
     - **Hemispheres**: Left vs. Right[cite: 1]
     - **Topography**: Anterior, Posterior, Central[cite: 1]

3. **Functional Connectivity (Phase Lag Index - PLI)**
   - Utilized Hilbert transform analytic signal extraction to capture instantaneous phase angles across all channels[cite: 1].
   - Computed pairwise **Phase Lag Index (PLI)** to generate weighted, undirected adjacency matrices invariant to linear volume conduction[cite: 1].

4. **Network Topology & Graph Centralities**
   - Constructed weighted graphs via `networkx` and computed key topological centrality metrics[cite: 1]:
     - **Leverage Centrality**: Evaluates node dominance relative to its immediate neighborhood[cite: 1].
     - **Weighted Leverage Centrality**: Incorporates eigenvector centrality weighting into neighborhood influence[cite: 1].
     - **Betweenness Centrality**: Evaluates shortest communication paths using inverted distance weights[cite: 1].
     - **Closeness Centrality**: Measures mean geodesic distance from a node to all other nodes[cite: 1].
   - Aggregated node centralities across anatomical lobes, hemispheres, and anteroposterior regions[cite: 1].

5. **Statistical Analysis & Clinical Correlations**
   - **One-Way ANOVA**: Assessed regional network metric differences across the three diagnostic groups (`AD`, `C`, `F`)[cite: 1].
   - **Post-hoc Pairwise T-Tests**: Conducted pairwise contrasts with **Benjamini–Hochberg False Discovery Rate (FDR)** correction for multiple comparisons[cite: 1].
   - **Clinical Correlations**: Evaluated Pearson correlation coefficients ($r$) between regional graph metrics and clinical variables (**Age** vs. Temporal Leverage; **MMSE** vs. Central Betweenness)[cite: 1].

---

## 🛠️ Requirements
- `python >= 3.9`
- `mne`[cite: 1]
- `networkx`[cite: 1]
- `scipy`[cite: 1]
- `statsmodels`[cite: 1]
- `numpy`[cite: 1]
- `pandas`[cite: 1]
