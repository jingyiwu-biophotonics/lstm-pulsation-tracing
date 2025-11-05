# Training LSTM Pulsation Tracing Models

This folder contains resources for **training** the LSTM-based cardiac pulsation tracing model.  

## Contents

- **`train_lstm_colab.ipynb`**  
  Main Google Colab notebook for training the LSTM model on synthetic pulsation data.  
  Includes data loading, preprocessing, model definition, training loops, and evaluation.  
  Launch directly in Colab:  
  [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jingyiwu-biophotonics/lstm-pulsation-tracing/blob/main/training/train_lstm_colab.ipynb)

- **`train_lstm_colab.py`** 
  Python script version of the notebook, auto-exported for convenience.

- **`requirements_train.txt`**  
  Python dependencies required for training. Install with:
  ```bash
  pip install -r requirements-train.txt
  ```

- **`data/convert_mat_to_npz.ipynb`**  
  Utility notebook for converting large `.mat` datasets into compressed `.npz` format for PyTorch training. Supports optional sharding for splitting very large datasets.  

## Data

- **Small example dataset (in repo):**  
  A small `.npz` dataset is included in this repository for demonstration.
  Shape: `(N, T, 2)`
  - `N` = number of samples (e.g., 750)
  - `T` = time samples per sample (e.g., 3000 for 60 s @ 50 Hz)
  - `2` = channels:
    - Channel 0: preprocessed (normalized) noisy signal
    - Channel 1: clean signal (ground truth)

- **Full dataset (on CMU KiltHub):**  
  For complete training, download the full dataset (`dataset_v0_training.npz`) hosted on [CMU KiltHub](https://doi.org/10.1184/R1/30090361).


## Workflow

1. **Prepare data**  
   - Convert `.mat` → `.npz` using `data/convert_mat_to_npz.ipynb`.  
   - If needed, large datasets can be split into shards.  
   - Store `.npz` files locally or on Google Drive for Colab access.  

2. **Train model**  
   - Open `train_lstm_colab.ipynb` in Colab.  
   - Load `.npz` dataset and create `Dataset`/`DataLoader`.  
   - Run the training loop; monitor loss and save the best checkpoint (`.pt`).  

3. **Use trained weights**  
   - Save `.pt` model weights (see testing folder).  
   - Use the testing notebook (`testing/testing_pulsation_tracing.ipynb`) to evaluate performance on new signals.  


## Notes 
- For details on inference and testing, see the `testing/` folder. 


## Contact
For questions:  
Jingyi Wu — jingyiwu@andrew.cmu.edu
