# Cybersecurity Data Science – PBL Project

**Project Title**: Detecting Vulnerable Code Using CodeBERT and MLP  
**Course**: MSc Cybersecurity Data Science  
**Contributors**:
- Doğa Bahar | 645618
- Esra Duran | 641438

---

## Project Summary

This project explores automated detection of vulnerable code snippets using machine learning. We collected a dataset of known CVE fixes from the ProjectKB dataset and applied code embeddings using CodeBERT, followed by training a Multilayer Perceptron (MLP) classifier.

---

## Dataset

- **Source**: ProjectKB (structured YAMLs of GitHub commits for CVEs)
- **Filtering**:
  - Extracted commit-level function changes using PyDriller
  - Removed duplicates and empty samples
  - Final shape: `5988 rows × 2 columns` (function_code, label)
- **Label Distribution**:
  - Non-vulnerable (label 0): 4273 samples
  - Vulnerable (label 1): 3103 samples

---

## Architecture

- **Feature Representation**:
  - No hand-crafted features
  - Used **CodeBERT** to generate fixed-size embeddings of function code
- **Model**: Multilayer Perceptron (MLP)
  - Activation: ReLU
  - Dropout: 0.3
  - Optimizer: Adam (lr = 1e-4)
  - Loss: BCEWithLogitsLoss
  - Batch size: 32
  - Epochs: 50

---

## Training Procedure

- **Split**:
  - 80% train
  - 10% validation
  - 10% test
  - Stratified split to preserve label distribution
- No oversampling/undersampling or class weights applied

---

## Evaluation

| Metric      | Vulnerable (1) | Non-Vulnerable (0) |
|-------------|----------------|---------------------|
| Precision   | Low            | High                |
| Recall      | Low            | High                |
| F1-Score    | Low            | High                |
| ROC AUC     | 0.58           | —                   |

- The model struggled to classify vulnerable code correctly, likely due to:
  - Class imbalance
  - Noisy data
  - Simplicity of MLP model



