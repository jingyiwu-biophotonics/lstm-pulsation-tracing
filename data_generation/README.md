# Data Generation for Synthetic Pulsation Dataset

This folder contains MATLAB scripts and functions for generating synthetic data that was used in training the LSTM-based pulsation tracing model. The scripts allow users to generate clean pulse signals, add realistic artifacts and noise, and prepare datasets for model training.


## Folder Structure

### `data/`
- Contains a small set of example data (20 samples for each pulse type) for demonstration.
- Generated using `generate_training_data.m`.

### `generate_artifacts/`
- Functions for **artifact generation**, including:
  - Amplitude modulation (Gaussian, Sigmoid)
  - Random oscillations
  - Spikes
  - Baseline shifts & drifts
  - Perlin and colored noise

### `generate_pulses/`
- Functions for generating **clean synthetic signals** based on skewed normal waveforms.
- Implements different pulse morphologies (e.g., single peak, closer/further double peaks).
- **Note:** Routines here are adapted from ECGSYN and are therefore licensed under GNU GPL v3.0 (see Licensing below).

### `utils/`
- Helper functions for filtering, signal processing, and visualization:
  - FFT and spectrogram utilities
  - Butterworth filters
  - Custom plotting functions


## Key Scripts

### `generate_training_data.m`
- Main script for generating large-scale training datasets.
- Produces **clean** and **noisy** pairs of signals.
- Saves data as `.mat` files with dimensions `[num_signals × time × 3]`:
  - Channel 1: Preprocessed noisy signal
  - Channel 2: Clean signal (ground truth)
  - Channel 3: Raw noisy signal

### `visualize_synthetic_signal.m`
- Demonstrates generation of a single synthetic signal.
- Adds artifacts sequentially and visualizes both time traces and spectrograms.

### `visualize_artifact.m`
- Demonstrates specific artifact types (e.g., modulation, drift, spikes).
- Plots clean vs. artifact-distorted signals for clear comparison.


## Notes

- The example data in `data/` is small and lightweight for demonstration.
- For full-scale training, run `generate_training_data.m` to create large datasets (several GBs).
- Pulse morphology generation is adapted from [ECGSYN](https://physionet.org/content/ecgsyn/1.0.0/).


## Licensing
This folder contains components under three different licenses:
1. **GNU General Public License v3.0 (GPL-3.0)**
    - The following files/functions in the `generate_pulses/` folder were derived from or adapted based on ECGSYN, and are licensed under GPL-3.0:
      - `generate_signal.m`
      - `odenirs_2SN.m`
      - `rrprocess.m`
2. **MIT License**
    - Applies to all other original code in this repository.
3. **Creative Commons Attribution (CC BY 4.0)**
    - Applies to all example data provided in the `data/` folder.


## Contact
Jingyi Wu — jingyiwu@andrew.cmu.edu
