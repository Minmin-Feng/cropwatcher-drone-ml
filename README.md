# CropWatcher Drone ML

CropWatcher is an autonomous drone-based crop-health monitoring prototype developed for indoor greenhouse-style environments. The system uses a Crazyflie 2.1 mini-drone to collect position-tagged environmental data, process telemetry through a local data pipeline, and visualize crop-health risk through a web dashboard.

This repository focuses on the machine-learning and data-pipeline portion of the project, including crop-health risk prediction, time-series modeling, and integration with the drone telemetry workflow.

## Project Overview

The system combines:

- Crazyflie 2.1 mini-drone platform
- Lighthouse-based indoor positioning
- BMP388 temperature and pressure sensing
- Autonomous hover, lawnmower scan, and waypoint flight modes
- CSV-based telemetry logging
- Local API server and dashboard visualization
- Machine-learning-based crop-health risk estimation

The final prototype demonstrates an end-to-end workflow from drone-based environmental sensing to zone-level crop-health visualization.

## My Contributions

My main responsibilities focused on:

- Data pipeline development
- Machine-learning model optimization
- Model integration support
- Crop-health prediction logic
- Connecting sensor-based telemetry data with ML-based risk estimation

## Machine Learning Design

The ML component was designed as a binary time-series classification task. Given a sequence of observations from previous weeks, the model predicts whether a monitored fruit is likely to become diseased in the next observation period.

The model pipeline includes:

1. Image feature extraction using a frozen EfficientNet-B0 backbone
2. Environmental feature normalization using 11 sensor/weather variables
3. Feature concatenation into a 1,291-dimensional time-step representation
4. Temporal modeling using BiGRU and CfC/LNN architectures
5. Binary disease-risk prediction using a sigmoid classification head

## Model Performance

Two temporal models were evaluated:

| Model | Test AUC | Test F1 | Accuracy | Parameters |
|---|---:|---:|---:|---:|
| BiGRU | 0.861 | 0.767 | 76% | 215,361 |
| CfC / LNN | 0.870 | 0.837 | 81% | 239,681 |

The CfC / Liquid Neural Network model achieved the best overall performance and was selected as the final model checkpoint.

## Repository Contents

| File | Description |
|---|---|
| `pomegranate-tree-prediction_minmin.ipynb` | ML training and evaluation notebook |
| `best_lnn_stable.pt` | Trained CfC / LNN model checkpoint |
| `Project Final Report.pdf` | Final project report |
| `Owner's Manual.pdf` | Project user manual |

## Technical Highlights

- Built a sensor-based ML pipeline for crop-health risk prediction
- Compared BiGRU and CfC / Liquid Neural Network temporal models
- Used EfficientNet-B0 image embeddings with normalized environmental features
- Applied sequence augmentation, class-imbalance handling, gradient clipping, learning-rate scheduling, and early stopping
- Integrated model outputs with a dashboard-based zone health map
- Demonstrated a full prototype workflow from drone telemetry to predictive visualization

## Limitations

This project is a proof-of-concept system rather than a production-ready agricultural prediction model. The ML model was trained on an external pomegranate dataset, while the drone prototype collected indoor telemetry without ground-truth crop-health labels. A production version would require real greenhouse data collection, manual labeling, and model retraining.

## Summary

CropWatcher demonstrates how a small autonomous drone can collect environmental telemetry, map sensor readings to physical zones, and support machine-learning-based crop-health risk estimation. The project highlights practical experience in data pipelines, time-series modeling, sensor-data integration, and cyber-physical system prototyping.
