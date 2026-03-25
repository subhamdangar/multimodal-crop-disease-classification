# Multi-Modal Crop Disease Classification

## Overview
This project focuses on crop disease classification using multi-modal remote sensing data. The goal is to classify wheat crop patches into three categories:

- Healthy  
- Rust  
- Other  

The dataset consists of three modalities:
- RGB images (3 channels)  
- Multispectral images (5–6 channels)  
- Hyperspectral images (125 channels)  

Each modality captures different aspects of crop health. The long-term objective is to combine them using multi-modal learning.

---

## Current Progress

### 1. RGB Model
- **Architecture:** ResNet18 (pretrained)  
- **Techniques Used:**
  - Data augmentation (random crop, flip, rotation, color jitter, random erasing)
  - Transfer learning (fine-tuning all layers)
  - Differential learning rates (backbone vs classifier)
- **Result:**
  - ~62% validation accuracy  

---

### 2. Multispectral Model
- **Custom pipeline for spectral data**
- **Key Components:**
  - Spectral Attention Module (learns importance of each band)
  - Spectral Encoder for feature extraction
  - ResNet18 backbone for classification  
- **Data Handling:**
  - Band-wise normalization
  - Spectral augmentations:
    - Band scaling
    - Random band dropout  
- **Result:**
  - ~58–60% validation accuracy  

---

## Observations
- Overall performance is moderate (~60% accuracy)  
- Class-wise imbalance observed:
  - “Healthy” class is harder to classify  
- Indicates that learned features are not sufficiently discriminative  
- Different modalities produce different feature distributions  

---

## Current Challenge: Multi-Modal Fusion
The next step is to combine different modalities.

Challenges:
- RGB and spectral data have different distributions  
- Feature representations are not directly compatible  
- Naive fusion (e.g., concatenation) may reduce performance  

The goal is to design a fusion method that allows each modality to contribute complementary information.

---

## Dataset
- **Total samples:** 600  
- **Classes:** 3 (200 per class)  
- **Train/Validation split:**
  - Train: 480  
  - Validation: 120  

---

## Tech Stack
- Python  
- PyTorch  
- torchvision  
- rasterio (for spectral data)  
- NumPy  

---

## Future Work
- Implement hyperspectral model (125 channels)  
- Design feature-level fusion architecture  
- Improve class-wise performance (especially “Healthy”)  
- Perform detailed error analysis  

---

## Note
This is an ongoing project. The focus is on understanding model behavior and improving architecture design rather than only optimizing accuracy.