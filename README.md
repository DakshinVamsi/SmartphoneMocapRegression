# Joint Angle Estimation from MoCap and Video-Derived Pose Data

This repository contains code, models, and pipelines for regressing joint angles from 3D joint coordinates acquired from both ground-truth MoCap systems and simplified 3D joint coordinates obtained from smartphone video (e.g., via MediaPipe or similar pose estimation models).

---

## 📌 Project Highlights

- Trained LSTM-based regression model using MoCap 3D XYZ coordinates  
- Joint angles predicted include **36 biomechanical DOFs** (e.g., hip flexion, knee angle, etc.)  
- Raw MoCap format (42 joints × 3D = 126D input) is supported  
- MediaPipe-style reduced joint input (33 joints × 3D = 99D input) is supported by:
  - Engineering simplified joint representations from raw MoCap
  - Training a second model compatible with real-time video inputs  
- Streaming inference and visualization support (real-time predictor + plotter)

---

## 🧠 Model Architecture

- **Input**: Sequences of 3D joint coordinates (`126D` or `99D`)
- **Model**: 2-layer LSTM with 256 hidden units
- **Output**: 36 joint angles per timestep
- **Loss**: Mean Squared Error (MSE)
- **Window size**: 500 timesteps

---

## 🗂 Directory Structure

