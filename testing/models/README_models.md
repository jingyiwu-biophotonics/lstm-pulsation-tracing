# Trained LSTM Models

This folder contains trained LSTM models using synthetic datasets of pulsatile signals with varying noise conditions.  
Each model corresponds to a different ablation or training configuration described in the paper.


## Available Models

- **`lstm_full_dataset.pt`**  
  Trained on the **full dataset** of 80,000 samples (40,000 single-peak pulses and 20,000 each for closely spaced and widely spaced double-peak pulses).  
  Includes all simulated noise and artifact types.

- **`lstm_reduced_dataset.pt`**  
  Trained on a **reduced dataset** of 6,000 samples (2,000 per archetype), with all noise and artifacts included.

- **`lstm_reduced_no_colored_noise.pt`**  
  Trained on the same **reduced dataset** of 6,000 samples, but **without colored noise**, to test the role of this noise component.

- **`lstm_single_peak.pt`**  
  Trained only on **single-peak pulsatile signals** (40,000 samples).  
  Useful for examining model performance when restricted to one pulse archetype.


## Notes

- The **primary model** used in the paper was `lstm_full_dataset.pt`.  
- Other models (`reduced` and `reduced_no_colored_noise`) were used in the **ablation analyses** to study training dataset size and noise characteristics.  
- The `single_peak` model was **not used in the paper**, but may be useful for tasks such as **heart rate tracking** when exact pulse morphology is less critical.  
- We may upload **new models trained on additional datasets** in the future as extensions of this work.  
