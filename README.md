# Eulerian Video Magnification (EVM) – Heart Rate Estimation Demo (MATLAB)

This repository is a **portfolio-friendly, reproducible refactor** of my B.Sc. project work on estimating heart rate from facial video signals, and comparing the result to ECG-derived heart rate.

It includes:
- ECG preprocessing + HR estimation
- Video ROI signal extraction + HR estimation (rPPG-style processing)
- Alignment + error metrics + plots (including Bland–Altman)
- A single entry script (`run_evm_demo.m`) that produces a `results/` folder


---

## How this repo relates to the final report

The submitted final report describes a workflow that used an **Eulerian Video Magnification (EVM)** implementation (“face/face2”) to produce **magnified videos**, and then performed ROI extraction, filtering, peak detection, and statistical comparison.

This repo focuses on making the **analysis pipeline reproducible and easy to run**:
- It can run directly on **original videos** (MP4/AVI), or
- It can run on **pre-generated magnified videos** (AVI) if you provide them.

In other words:
- The report documents the original academic submission workflow.
- This repo is a cleaned-up engineering refactor that supports both “original” and “magnified” inputs, and reproduces the evaluation + visualization steps.

---

## Requirements

- MATLAB (tested on recent versions)

---

## Project Structure

run_evm_demo.m # main entry point
src/ # helper functions
data/ # input files (NOT tracked in git)
results/ # generated outputs (plots + summary.csv)
legacy/ # original scripts (optional / reference)

---

## Data: my demo files vs. bring your own

This project is designed to work in two modes:

### Mode 1 — Local demo data (for my own runs)
I keep my real input data locally (ECG + videos) under `data/`, but **the data folder is excluded from git** for privacy and file size reasons.

Expected filenames (default; you can change these in `run_evm_demo.m`):
- ECG: `restHR.txt`, `activeHR.txt`
- Video (original): `restHR1.mp4`, `activeHR1.mp4`
- Video (magnified, optional): `rest_mag.avi`, `active_mag.avi`

### Mode 2 — Bring Your Own Data (for anyone else)
If you want to try the pipeline on your own recordings:
1) Run `run_evm_demo.m`
2) Set `cfg.videoMode = "prompt"` to select videos via file dialog
3) (Optional) Update ECG file paths to your own text files

You can also drop your files into the `data/` folder locally (not committed) and update the filenames in the config section.

**Notes**
- Videos should be stable, well-lit, and include a clear face ROI.
- If using cloud-synced folders (iCloud/OneDrive), make sure files are available offline so MATLAB can read them.

---

## Quickstart

1) Put your inputs into the `data/` folder (excluded from git):

Required ECG:
- `restHR.txt`
- `activeHR.txt`

Required Video (choose one of the options below):
- Original videos (MP4/AVI): e.g. `restHR1.mp4`, `activeHR1.mp4`
- Magnified videos (AVI): e.g. `rest_mag.avi`, `active_mag.avi` (optional)

2) Open MATLAB, set the current folder to the repo, and run:

```matlab
run_evm_demo