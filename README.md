# Agreement-driven-multi-model-cross-valida-tion-for-reliable-polyp-detection-in-colorec-tal-imaging
The project presents a cross-validation framework for colorectal polyp detection and segmentation using multiple deep learning models:UNet, YOLOv8, PraNet, and Polyp-PVT.  The system evaluates each model and combines their outputs through consensus (AND, OR, and majority voting) to identify regions of interest with higher diagnostic confidence. 

![individual results](Images/1.png)


## Overview
This project implements a multi-model cross-validation framework for colorectal polyp detection and segmentation using deep learning.

The system integrates four state-of-the-art models:
- UNet
- YOLOv8 (segmentation/detection)
- PraNet
- Polyp-PVT (Transformer-based)

Each model is evaluated independently and then combined using consensus strategies to improve detection reliability and reduce false positives.

![sum of internet area](Images/3.png)
---

## Motivation
Colorectal cancer is one of the leading causes of cancer-related deaths worldwide. Early detection of polyps significantly increases survival rates.

However, single-model approaches often suffer from:
- Overfitting
- False positives
- Lack of generalization

This project proposes a **cross-model validation strategy** to increase robustness and clinical reliability.

---

## Methodology

### 1. Multi-Model Evaluation
Each model processes the same input image and generates:
- Segmentation masks
- Confidence scores

### 2. Cross-Validation Strategy
Predictions are combined using:

- **OR_ALL** → High sensitivity (detect anything possible)
- **AND_ALL** → High precision (only strong agreement)
- **MAJORITY_3OF4** → Balanced approach
- 
![comparison results](Images/tabla1.png)

### 3. Region of Interest (ROI)
Regions detected by multiple models are considered:
- Higher confidence
- Clinically more relevant

![interest areas](Images/2.png)

![comparison results](Images/tabla2.png)

### 4. Metrics
Evaluation includes:
- Dice Score
- IoU (Intersection over Union)
- Precision / Recall
- Accuracy
- True Polyp Detection %
- False Positive %
---
## Datasets

The framework supports multiple datasets:

- **PolypDB** (training)
- **Kvasir-SEG** (validation)
- **CVC-ClinicDB** (testing)

This ensures proper generalization across different imaging conditions.

---

## Notebooks Description

### 1. UNet Training
**File:** `1.Unet_PolypDB.ipynb`  
- Implements UNet architecture  
- Trains on PolypDB dataset  
- Outputs segmentation masks  
- Saves best model as: 'unet_polypdb_best.pt'

---

### 2. Polyp-PVT Training
**File:** `2.PolypPVT_PolypDB.ipynb`  
- Transformer-based segmentation model  
- Uses PVT backbone  
- High performance in complex structures  
- Saves model as:`polyp_pvt_real_like_best.pt`
---

### 3. PraNet Training
**File:** `3.PraNet_PolypDB.ipynb`  
- Reverse Attention Network  
- Focuses on boundary refinement  
- Strong performance in medical segmentation  
- Saves model as:`PraNet-19.pth`
---

### 4. YOLOv8 Training
**File:** `4.YOLOv8_PolypDB.ipynb`  
- Detection + segmentation model  
- Fast inference  
- Used for ROI detection  
- Saves model as: `best_detection.pt`


---

### 5. Cross-Validation and Evaluation
**File:** `5.Cross_Validation_4Models.ipynb`

This notebook integrates all trained models and performs:

#### Multi-model evaluation
- Each model predicts independently on the same dataset

#### Ensemble strategies
- **OR_ALL** → maximum sensitivity  
- **AND_ALL** → maximum precision  
- **MAJORITY_3OF4** → balanced decision  

#### Outputs
- Per-image evaluation
- Global metrics
- Agreement analysis between models
- CSV export with results

---

## Weights

All trained models must be placed in:

Required files:
- `unet_polypdb_best.pt`
- `best_detection.pt`
- `PraNet-19.pth`
- `polyp_pvt_real_like_best.pt`

---

## Methodology

The framework follows these steps:

1. Train each model independently on PolypDB
2. Evaluate each model separately
3. Apply cross-validation across models
4. Combine predictions using ensemble rules
5. Identify regions of interest based on agreement

---

## Key Idea

Instead of relying on a single model, this project uses:

> **Cross-model agreement as a confidence metric**

If multiple models detect the same region:
- Higher probability of true polyp
- Lower probability of false positive

---

## Metrics

The evaluation includes:

- Dice Score
- IoU (Intersection over Union)
- Precision
- Recall
- Accuracy
- True Positive Area %
- False Positive Area %

---

## How to Run

### Step 1 – Train Models
Run notebooks:
- `1 → 4`

### Step 2 – Place Weights
Ensure all weights are inside the folder


### Step 3 – Run Cross-Validation
Run: '5.Cross_Validation_4Models.ipynb'

---

## Results

- Polyp-PVT achieved the best individual performance
- YOLO provides strong detection capability
- UNet and PraNet improve segmentation consistency
- Ensemble methods significantly reduce false positives

---

## Future Work

- Real-time colonoscopy video analysis
- Clinical validation
- Integration with robotic systems
- Explainable AI (XAI)
- Deployment as medical diagnostic tool



## Author

Emmanuel Correa  
MSc Engineering Technology  
PHD robotics Technology

