# Transfer Learning on Intel Image Classification Dataset

**Transfer Learning • PyTorch • ResNet-18 • Computer Vision • Data Augmentation**

---

## Overview

This repository demonstrates two transfer-learning strategies—fixed feature extraction and full fine-tuning—applied to the Intel Image Classification Dataset. Using a pre-trained ResNet-18 backbone, you’ll see how small‐ and large-scale adaptations affect performance on a six-class outdoor scene classification task.

---

## Dataset

- **Intel Image Classification Dataset**  
  ~25 000 RGB images (150×150×3) across six categories: `building`, `forest`, `glacier`, `mountain`, `sea`, `street`.  
- **Splits**  
  - Train: 14 000 images (further split 80/20 for train/validation)  
  - Test: 3 000 images  
- **Preprocessing**  
  - Resize to 224×224 for ResNet-18 compatibility  
  - Normalize channels using ImageNet mean & standard deviation
 
> **Note:** Augmentations were mistakenly applied to validation data as well; future pipelines will restrict them to the training split only.

---

## Methods

1. **Fixed Feature Extractor**  
   - Freeze all convolutional layers; only retrain the final fully connected layer.  
   - Learning rate: 1 × 10⁻³  
   - Faster convergence and fewer trainable parameters.

2. **Full Fine-Tuning**  
   - Unfreeze the entire network and fine-tune all layers.  
   - Learning rate: 1 × 10⁻⁴  
   - Better domain adaptation at the cost of longer training.

### Data Augmentation

- Random horizontal & vertical flips (50% probability each)  
- Color jitter (brightness, contrast, saturation)  

---

## Experiments

- **Reproducibility:** Seeded PyTorch and NumPy for deterministic runs.  
- **Training:** 10 epochs per method using the Adam optimizer.  
- **Metric:** Top-1 validation accuracy.

---

## Results

| Method                      | Validation Accuracy |
| --------------------------- | ------------------- |
| Random Baseline (1/6 classes) | 16.67%            |
| Fixed Feature Extractor     | 12%                 |
| Full Fine-Tuning            | 20%                 |

> **Insight:** Full fine-tuning shows a steeper accuracy gain across epochs despite the limited 10-epoch budget.
