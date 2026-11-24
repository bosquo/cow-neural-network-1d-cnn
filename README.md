# CNN (Cow Neural Network): Predicting Livestock Movement Using 1D CNNs on Vector GPS Trajectories

![Research Paper](https://img.shields.io/badge/Research-GeoAI_%26_Trajectory_Forecasting-1B4332)
![Study Site](https://img.shields.io/badge/Study_Site-Vierkaseralm_(Untersberg%2C_Austria)-2D6A4F)
![Focus](https://img.shields.io/badge/Architecture-1D_CNN_(Raw_Vector_Sequences)-48584F)

> **Applied Geoinformatics Research Paper** (June 2025)  
> **Author:** Florian Herbst

---

## Overview

Precision livestock farming and alpine pasture management rely on GPS telemetry to understand grazing behavior and mitigate spatial conflicts between alpine agriculture, recreation, and returning wildlife.

While Convolutional Neural Networks (CNNs) are widely applied to pedestrian and vehicle trajectory forecasting, they typically convert raw coordinates into **rasterized heatmaps or grids**—generalizing away coordinate-level vector precision. This research paper evaluates whether a **pure 1D Convolutional Neural Network (1D CNN)** without recurrent (`LSTM`) layers can learn meaningful spatiotemporal patterns directly from **raw sequential vector GPS trajectories**.

---

## Methodology

1. **Case Study & Sensor Data**
   - Used real-world GPS collar telemetry recorded from cattle grazing on the **Vierkaseralm** alpine pasture at **Untersberg, Austria**.
   - Extracted sequential feature vectors containing **latitude, longitude, timestamp, speed, and course**.

2. **Sliding-Window Sequence Engineering**
   - Segmented continuous trajectories into overlapping sequences of **10 historical input steps (`X1–X10`)** paired with **10 target prediction steps (`Y1–Y10`)** to expand training volume without rasterization.
   - Split sequences into **70% training**, **15% validation**, and **15% test** subsets.

3. **Pure 1D CNN Architecture & Tuning**
   - Evaluated multiple 1D CNN depths and filter configurations (using sequence length `10`, kernel size `3`, and stride `1` as baseline) combined with a **learning-rate scheduler** and **early dropout** to prevent overfitting.
   - Deliberately excluded recurrent memory layers (LSTM/GRU) to isolate the standalone capability of 1D convolutions on vector coordinate sequences.

---

## Key Results & Conclusions

- **Architecture Trade-offs:** Shallower, simpler 1D CNN architectures outperformed deeper networks, capturing immediate short-term movement cues without collapsing generalization.
- **Quantitative Performance:** Across tuned configurations, error plateaued at a minimum **MSE of 0.44** and **MAE of 0.40**, corresponding to an average spatial prediction discrepancy of **~100 m** (ranging from **30 m to 200 m**) across 10-step forecast horizons.
- **Critical Finding:** Pure 1D CNNs capture local directional trends (e.g., gradual turns or resting pauses) but **lack temporal memory across irregular sampling intervals** and miss broader trajectory context. Coupled with single-animal training constraints due to GPS noise/outliers, the findings confirm why **hybrid CNN-LSTM / attention architectures** and multi-individual herd features are essential for reliable vector trajectory forecasting.

---

## Tech Stack

- **Deep Learning:** 1D Convolutional Neural Networks, Python
- **Geospatial Data:** Sequential Vector GPS Telemetry (Latitude, Longitude, Speed, Course, Timestamps)
- **Evaluation & Mapping:** MSE / MAE loss curves, spatial delta trajectory visualization

---

## Repository Structure

```text
cow-neural-network-1d-cnn/
├── docs/
│   └── report.pdf         # Full research paper with sequence diagrams, loss plots, and delta map
├── .gitignore
└── README.md
```

- **Full Research Paper:** [`docs/report.pdf`](docs/report.pdf)

---

<p align="center">
  Part of the <a href="https://bosquo.github.io/e-portfolio/"><strong>Florian Herbst — Geoinformatics &amp; Forestry e-Portfolio</strong></a>
</p>
