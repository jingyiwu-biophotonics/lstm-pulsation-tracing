# LSTM Pulsation Tracing — Testing

Scripts and notebooks for **evaluating trained LSTM models** on experimental and synthetic datasets.  
This folder demonstrates how to load models, run inference, compare with classical signal processing baselines, and visualize results.


## Folder Layout

```
testing/
├── experimental_data/                  # Experimental .mat datasets for evaluation
├── models/                             # Pre-trained model weights (see README in this folder)
├── synthetic_data/                     # Synthetic datasets with ground truth
├── utils/                              # Helper modules used by notebooks/scripts
│
├── ablation_study_compare_LSTM_models.ipynb
├── benchmark_LSTM_with_DWT_and_TDDR.ipynb
├── testing_pulsation_tracing_nirs_ecg_hr_comparison.ipynb
├── testing_pulsation_tracing_nirs_ppg_dcs.ipynb
├── testing_pulsation_tracing.ipynb     # General end-to-end demo (interactive)
├── testing_pulsation_tracing.py        # Script version of the demo
│
├── README_testing.md                   # This file
└── requirements_test.txt               # Python dependencies for testing
```


## What Each Notebook Does

- **`testing_pulsation_tracing.ipynb`** — End-to-end demo on experimental data (LSTM inference → comparisons → visualizations → pulse segmentation and averaging).  
- **`testing_pulsation_tracing_nirs_ecg_hr_comparison.ipynb`** — HR extraction accuracy: compares LSTM-derived HR from NIRS against ECG.  
- **`testing_pulsation_tracing_nirs_ppg_dcs.ipynb`** — Pulse shape tracing (segmentation + averaging) on NIRS/PPG/DCS examples.  
- **`benchmark_LSTM_with_DWT_and_TDDR.ipynb`** — Baseline comparison on synthetic data with ground truth (DWT, TDDR vs. LSTM).  
- **`ablation_study_compare_LSTM_models.ipynb`** — Ablation analyses (reduced dataset, no colored noise models) on synthetic data.


## Typical Workflow

1. **Select a pre‑trained model**  
   Place the weights in `testing/models/`. Recommended filenames:
   - `lstm_full_dataset.pt` (primary model used in the paper)  
   - `lstm_reduced_dataset.pt`  
   - `lstm_reduced_no_colored_noise.pt`  
   - `lstm_single_peak.pt` (not used in paper; useful for HR tracking)

2. **Choose a dataset**
   - **Experimental**: in `testing/experimental_data/` (NIRS, PPG, DCS).  
   - **Synthetic**: in `testing/synthetic_data/` (with known ground truth).

3. **Preprocess**  
   Convert raw intensity to ΔOD (if applicable), resample to **50 Hz**, and normalize to ~**[−1, 1]**.

4. **Run LSTM inference**  
   Window the signal (3000‑sample windows, overlap configurable), run the model on each segment, and stitch via overlap‑averaging.

5. **Compare with baselines** (optional)  
   - **Temporal Derivative Distribution Repair (TDDR)**  
   - **Discrete Wavelet Transform (DWT)**  
   - (Optionally) Savitzky–Golay, NeuroKit2 `ppg_clean`

6. **Analyze & visualize**  
   Time‑trace overlays, spectrograms, low‑SNR region highlighting, pulse segmentation/averaging, and HR/IBI metrics (where applicable).


## Running the Script Demo

From the repo root:

```bash
cd testing
python testing_pulsation_tracing.py
```

- The script opens multiple Matplotlib figures; **execution finishes after all figure windows are closed**.
- For interactive Plotly figures in a browser, ensure this line is set in the script:  
  ```python
  import plotly.io as pio
  pio.renderers.default = "browser"
  ```

### Run notebooks
```bash
jupyter notebook testing_pulsation_tracing.ipynb
```
Or open any of the other notebooks for the specific analyses listed above.


## Installation

Install Python dependencies for testing:

```bash
pip install -r requirements_test.txt
```


## Notes

- The testing notebooks rely on helper utilities in `testing/utils/` (imported as `from utils import ...`).  
- Experimental datasets and device details are documented in `testing/experimental_data/README_experimental_data.md`.  
- Synthetic datasets (with ground truth) are documented in `testing/synthetic_data/README_synthetic_data.md`.  
- If you use your own data, ensure **sampling rate = 50 Hz** or resample accordingly, and scale pulses to ~[−1, 1] for best results.


## Contact

Jingyi Wu — <jingyiwu@andrew.cmu.edu>
