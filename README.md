# Brain Tumor Classification with PyTorch

A CNN built in PyTorch to classify brain tumor types (glioma, meningioma, 
pituitary tumor, or no tumor) from MRI scans.

## Motivation
Built this to get hands-on experience writing PyTorch from the ground up — 
custom model architecture, training loop, and evaluation — rather than relying 
on high-level fit()-style APIs.

## Dataset
[Brain Tumor MRI Dataset](https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset) 
(Kaggle) — ~7,000 MRI images across 4 classes (glioma, meningioma, pituitary, no tumor).

## Approach
- 3-block CNN (Conv2d → ReLU → MaxPool2d, channels 32→64→128) with a fully 
  connected classifier head
- Custom PyTorch training loop (manual forward/backward/optimizer steps)
- Data augmentation (random flip, rotation) on training data only
- ImageNet normalization
- Adam optimizer with ReduceLROnPlateau scheduling
- Early stopping + checkpointing on best validation accuracy

## Results
Best validation accuracy: **93.9%**

## What I'd improve with more time
- Try transfer learning with a pretrained ResNet/EfficientNet backbone
- Add Grad-CAM visualization to see what regions the model is focusing on
- Cross-validation instead of a single train/test split for more robust accuracy estimates

## How to run
Built and trained in Google Colab (T4 GPU). Open `TorchTumorDetection.ipynb` 
and run all cells — dataset downloads automatically via `kagglehub`.
