
# MoCap-to-EMG and Joint Angle and EMG envelope Regression

This repository contains code and datasets for training deep learning models to regress electromyography (EMG) signals and joint angles from 3D motion capture (MoCap) data. The project explores the relationship between biomechanical movement (captured as xyz joint coordinates) and physiological signals (EMG) using sequence models like LSTMs.

## Project Overview

Human motion involves complex neuromuscular coordination. This project builds regression models that take in MoCap joint coordinates and predict:

- EMG Envelopes
- Joint angles

## Dataset

eg: Subject_Data -> S5 -> Activity_Trials (contains the trials data)

Once this data is fed into pipeline.ipynb -> it is stored in sync_data as "/{SUBJECT_ID}_{action_name}_Synchronized.csv"

This dataset is again fed into emg_filtering.ipynb to produce the final dataset which will be present in sync_data -> imputed (this is what is used for training the data)

## Code File description

| Notebook                           | Description                                                                                                                                                                                            |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `pipeline.ipynb`                   | Merges and synchronizes multiple trials of a single activity based on frame alignment. Outputs are unified datasets ready for EMG and MoCap processing.                                                |
| `emg_filtering.ipynb`              | Applies signal processing to the raw EMG data: filtering, envelope extraction (linear EMG), and imputation. Outputs clean EMG envelopes aligned with the joint coordinate data.                        |
| `training_mocap_jointangles.ipynb` | Trains an LSTM model to regress from full 3D MoCap joint coordinates to joint angles. Useful for learning the biomechanical relationship between spatial motion and anatomical angles.                 |
| `training_mocap_emg.ipynb`         | Trains an LSTM model to regress from 3D MoCap joint coordinates to filtered EMG envelopes. Captures neuromuscular control patterns underlying observed motion.                                         |
| `training_mocap_mediapipe.ipynb`   | A variant of the joint angle regression model that uses a reduced set of joint coordinates (mimicking MediaPipe-style 3D inputs). This simulates real-world use cases where full MoCap is unavailable. |


## Model Architecture
- Input: 3D joint coordinates (42 joints × 3 = 126D, or MediaPipe-style 99D input)

- Model: LSTM-based sequence-to-sequence regression

- Output:

    -  36 joint angles (for joint angle model)

    - n-dimensional EMG envelope features (for EMG model)

## Training Details
- Sequence Length: 500 timesteps

- Loss Function: MSELoss

- Optimizer: Adam

- Regularization: Dropout = 0.3


