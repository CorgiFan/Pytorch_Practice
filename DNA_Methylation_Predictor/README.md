# DNA Methylation Predictor

A PyTorch implementation of a feedforward neural network for predicting DNA methylation status from biological features. This project was built to practice applying deep learning to epigenetic datasets while developing a complete machine learning workflow in PyTorch.

---

## Overview

DNA methylation is an epigenetic modification in which methyl groups are added to DNA, often affecting gene expression without altering the DNA sequence itself. Aberrant methylation patterns have been linked to numerous diseases, including cancer and neurological disorders.

This project demonstrates how a neural network can be trained to classify methylation status from tabular biological data using PyTorch.

---

## Features

- Data preprocessing with **Pandas**
- Dataset splitting into training and testing sets
- Custom PyTorch neural network
- Binary classification using **CrossEntropyLoss**
- Model training with the **Adam optimizer**
- Accuracy evaluation on unseen test data
- GPU-compatible training (when available)

---

## Technologies Used

- Python
- PyTorch
- Pandas
- NumPy
- Matplotlib (optional visualization)

---

## Model Architecture

The model is a fully connected feedforward neural network consisting of multiple linear layers with ReLU activations.

Example architecture:

```
Input Features
      ↓
Linear Layer
      ↓
ReLU
      ↓
Hidden Layer(s)
      ↓
ReLU
      ↓
Output Layer
      ↓
Softmax / CrossEntropyLoss
```

The exact layer sizes can be found within the notebook.

---

## Project Workflow

1. Load the methylation dataset
2. Separate features and labels
3. Convert data into PyTorch tensors
4. Create DataLoaders for batching
5. Define the neural network architecture
6. Train the model over multiple epochs
7. Evaluate performance on the testing set
8. Report classification accuracy

---

## Learning Objectives

This project was created to strengthen my understanding of:

- Building neural networks from scratch in PyTorch
- Working with biological tabular datasets
- Training and evaluating classification models
- Managing the complete machine learning workflow
- Applying deep learning techniques to computational biology problems

---

## Future Improvements

Potential extensions include:

- Hyperparameter optimization
- Batch normalization
- Dropout regularization
- ROC-AUC evaluation
- Precision, recall, and F1-score metrics
- Cross-validation
- Feature importance analysis
- Comparison with traditional machine learning models (Random Forest, XGBoost, Logistic Regression)

---

## Dataset

The notebook uses a publicly available DNA methylation dataset downloaded from Kaggle. The dataset is not included in this repository due to licensing and file size considerations.

---

## Disclaimer

This project was developed for educational purposes to learn PyTorch and explore applications of deep learning in computational biology. It is not intended for clinical or diagnostic use.

---

## Author

**Jeffrey Ding**

Interested in computational neuroscience, bioinformatics, and machine learning applications in biology.
