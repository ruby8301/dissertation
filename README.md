PDCADx Foundation 2025 – Multimodal MRI Pipeline

This repository contains a hybrid classification and segmentation pipeline for the PDCADx Foundation Challenge (MICCAI 2025). It integrates 3D ResNet deep features, handcrafted ROI features, and guided segmentation masks for Parkinson’s Disease (PD) vs. Healthy Control (HC) classification and deep gray matter (DGM) segmentation.

📂 Repository Structure

ResNet34_3D_prediction_files.ipynb

Runs 3D ResNet inference on multimodal MRI (NM, QSM, T1).

Produces per-subject resnet_prob scores saved as CSV.

hybrid_baseline.ipynb

Combines ResNet outputs with handcrafted ROI features.

Trains a baseline XGBoost classifier and reports accuracy, AUC, and confusion matrices.

pdcadx_classification_segmentation.ipynb

Implements the final leakproof pipeline.

Performs guided segmentation of NM and QSM (producing *_pred.nii.gz + PNG overlays).

Extracts region-wise features, merges with ResNet outputs, and retrains the tuned XGBoost model.

Generates submission files:

Segmentation masks (*_pred.nii.gz)

Classification predictions (label_predict.csv)

🚀 How to Run

Prepare Dataset
Ensure your dataset is organised as:

DATA_ROOT/
  train/ RJPD_xxx/ (NM.nii.gz, QSM.nii.gz, T1.nii.gz)
  val/   RJPD_xxx/
  test/  RJPD_xxx/
  train_cases.csv
  val_cases.csv


Step 1: ResNet Inference
Run ResNet34_3D_prediction_files.ipynb → generates resnet_train.csv, resnet_val.csv, resnet_test.csv.

Step 2: Baseline Classification
Run hybrid_baseline.ipynb → trains the hybrid XGBoost baseline, prints validation performance.

Step 3: Segmentation + Final Classification
Run pdcadx_classification_segmentation.ipynb →

Produces segmentation masks (*_pred.nii.gz)

Saves QC previews (*_preview.png)

Generates final label_predict.csv for challenge submission.
