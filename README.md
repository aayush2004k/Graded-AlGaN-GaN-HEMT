# Simulation of Graded AlGaN/GaN HEMTs

A self-driven simulation study exploring how compositional grading of the AlGaN barrier layer affects 2DEG (two-dimensional electron gas) carrier concentration and threshold voltage in AlGaN/GaN HEMTs, using Gregory Snider's 1D Schrödinger-Poisson solver.

## Overview

Conventional AlGaN/GaN HEMTs use an abrupt AlGaN/GaN heterojunction to form the 2DEG channel. This project investigates whether **grading** the Al composition in the AlGaN barrier (instead of an abrupt step) can enhance 2DEG carrier concentration and tune the threshold voltage of a delta-doped HEMT structure.

Analytical models for electron concentration and threshold voltage were first derived for a delta-doped HEMT, after which several AlGaN grading profiles were explored:

- **Linear grading**
- **Parabolic grading**
- **Exponential grading**

Each profile was swept across grading percentage and grading layer thickness/position to study its effect on 2DEG confinement and carrier density. In total, **100+ simulations** were run across these grading configurations.

## Tool Used

Simulations were performed using **Gregory Snider's 1D Poisson/Schrödinger solver** (`1D Poisson Beta 8j`), a widely used academic tool for self-consistent 1D Schrödinger-Poisson calculations in compound semiconductor heterostructures.

## Repository Structure

```
Graded-AlGaN-GaN-HEMT/
│
├── greg_snider_1d_schrodinger_poisson_solver/
│   └── 1D Poisson Beta 8j PC Distribution/
│       └── Program_and_Input_Files/
│           └── [Simulation batches — see below]
│
├── PoissonWrapper_2016-10-23/        # Wrapper/utility scripts for the solver
├── ChangChujyh1990.pdf               # Reference paper used for model derivation
├── n_vs_normalised_grading.xlsx      # Consolidated results: carrier concentration vs. grading
└── README.md
```

### Simulation batches

The `Program_and_Input_Files` folder contains multiple sub-folders, each corresponding to a different stage/configuration of the grading study (20–30 input/output files per folder). Broadly, they are organized as:

| Folder (naming pattern) | What it represents |
|---|---|
| `1st try` | Initial baseline runs to validate the solver setup against the ungraded (abrupt) HEMT case |
| `1st layer graded (0%-25%)` | First AlGaN layer graded from 0% to 25% Al composition |
| `1st layer graded (grading ~ thickness)` | Grading profile swept as a function of layer thickness |
| `11 0–30% completely graded` | Full barrier graded from 0% to 30% Al composition |
| `12 30% not graded` | Control case — constant 30% Al composition, ungraded |

> Each folder contains the solver input deck(s) and corresponding output files for that configuration. File/folder names encode the grading range and condition being tested; refer to the input files inside each folder for exact parameters (grading profile type, layer thickness, doping).

## Key Files

- **`ChangChujyh1990.pdf`** — Reference paper used to validate/derive the analytical delta-doping and 2DEG confinement models.
- **`n_vs_normalised_grading.xlsx`** — Aggregated results across all simulation batches, plotting electron concentration (n) against normalized grading percentage.

## How to Run

1. Open the desired input file from a batch folder inside `Program_and_Input_Files` in the **1D Poisson (Beta 8j)** solver.
2. Run the self-consistent Schrödinger-Poisson solve.
3. Compare the output conduction band diagram / carrier concentration profile against the ungraded baseline case (`1st try`).
4. Aggregate results are tabulated in `n_vs_normalised_grading.xlsx`.

## Summary of Findings

- Grading the AlGaN barrier (linear, parabolic, or exponential) increases 2DEG carrier concentration relative to an abrupt AlGaN/GaN junction of the same average Al composition.
- The effect is sensitive to both the **grading profile shape** and the **grading layer thickness**, motivating the parameter sweep across 100+ simulation runs.

## Author

Aayush — Electrical Engineering, IIT Bombay

### Acknowledgements
- Gregory Snider (University of Notre Dame) for the 1D Poisson/Schrödinger solver.
- Chang & Chu (1990) reference paper for delta-doping model validation.
