# Synthetic Data

This folder contains small synthetic datasets used to evaluate the LSTM framework for pulsation tracing. These datasets were generated with controlled noise and artifacts, allowing benchmarking of model performance under known ground truth.


## Datasets

- **`synthetic_dataset1.mat`**  
  - *Used in the paper.*  
  - Contains noisy synthetic data with **medium colored noise**.  
  - Served as the ground-truth benchmark dataset for additional analyses in the study.

- **`synthetic_dataset2.mat`**  
  - *Not used in the paper.*  
  - Same signals as `synthetic_dataset1`, but with **higher colored noise**.  

- **`synthetic_dataset3.mat`**  
  - *Not used in the paper.*  
  - Same signals as `synthetic_dataset1`, but with **no colored noise**.  


## Data Format

Each dataset has the following structure:  

- Dimensions: **8 × 3000 × 3**  
  - **8 samples**  
  - **3000 time points** (corresponding to 60 seconds at 50 Hz sampling rate)  
  - **3 channels:**  
    - Preprocessed noisy signal  
    - Clean ground truth signal  
    - Raw noisy signal  

## Visualization

- **`plot_dataset_signal.m`**  
  A MATLAB script for visualizing signals in the synthetic datasets.  


## Contact
Jingyi Wu — jingyiwu@andrew.cmu.edu
