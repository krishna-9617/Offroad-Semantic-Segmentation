# Offroad Semantic Scene Segmentation  
## Startathon Hackathon 2026 — Duality AI Challenge  

---

## 🚀 Project Overview  

This project trains a semantic segmentation model on synthetic desert scenes to maximize **Mean Intersection over Union (IoU)** on an unseen test environment.

### 🏆 Judging Criteria

| Component | Weightage |
|------------|------------|
| Mean IoU Score | 80% |
| Documentation & Reproducibility | 20% |

---

## 📊 Final Results  

| Metric                          | Value                 |
|----------------------------------|------------------------|
| Final Validation Mean IoU        | **0.2991**            |
| Best Validation IoU              | **0.2995 (Epoch 23)** |
| Final Validation Dice Score      | **0.4428**            |
| Final Validation Accuracy        | **70.58%**            |

---

## 🧠 Model Architecture  

| Component         | Details |
|------------------|----------|
| Backbone          | DINOv2 ViT-S/14 (Frozen) |
| Segmentation Head | Lightweight Convolutional Classifier |
| Loss Function     | CrossEntropyLoss |
| Optimizer         | SGD (momentum = 0.9) |
| Learning Rate     | 1e-4 |
| Epochs            | 30 |
| Batch Size        | 4 |

The backbone was frozen to reduce overfitting and ensure stable convergence while training only the segmentation head.

---

## 🗂 Dataset  

The dataset contains RGB desert images with pixel-level segmentation masks across 10 classes:

| Class ID | Class Name      |
|-----------|------------------|
| 0         | Background       |
| 100       | Trees            |
| 200       | Lush Bushes      |
| 300       | Dry Grass        |
| 500       | Dry Bushes       |
| 550       | Ground Clutter   |
| 700       | Logs             |
| 800       | Rocks            |
| 7100      | Landscape        |
| 10000     | Sky              |

Training and validation data come from one desert environment.  
Testing is performed on a different unseen location — making **generalization critical**.

---

## ⚙️ Environment Setup  

```bash
conda activate EDU
pip install -r requirements.txt
```

---

## 🏋️ Training  

```bash
python train_segmentation.py
```

### 📁 Training Outputs

| File | Description |
|-------|-------------|
| segmentation_head.pth | Trained model weights |
| train_stats/training_curves.png | Loss & accuracy curves |
| train_stats/iou_curves.png | IoU per epoch |
| train_stats/all_metrics_curves.png | Combined metrics |
| train_stats/evaluation_metrics.txt | Full metrics log |

---

## 🧪 Testing / Inference  

```bash
python test_segmentation.py
```

### 📁 Inference Outputs

| File / Folder | Description |
|----------------|-------------|
| predictions/evaluation_metrics.txt | Final IoU and evaluation metrics |
| predictions/per_class_metrics.png | Per-class IoU bar chart |
| predictions/comparisons/ | Input / Ground Truth / Prediction comparison images |
| predictions/masks/ | Raw predicted masks |
| predictions/masks_color/ | Colorized predicted masks |

---

## 📁 Repository Structure  

```
project/
│
├── train_segmentation.py
├── test_segmentation.py
├── segmentation_head.pth
│
├── train_stats/
│   ├── training_curves.png
│   ├── iou_curves.png
│   ├── all_metrics_curves.png
│   └── evaluation_metrics.txt
│
├── predictions/
│   ├── per_class_metrics.png
│   ├── evaluation_metrics.txt
│   └── comparisons/
│
├── README.md
├── requirements.txt
└── Report.pdf
```

---

## 📈 Experiment Summary  

| Version        | Learning Rate | Epochs | Batch Size | Mean IoU |
|----------------|---------------|--------|------------|----------|
| V1 (Baseline)  | 1e-4          | 10     | 2          | 0.2976   |
| V2             | 1e-4          | 25     | 4          | 0.2991   |
| V3             | 1e-4          | 10     | 2          | 0.3456   |

---

## 🔎 Key Observations  

| Observation |
|-------------|
| Large structures (Sky, Trees, Landscape) were segmented more accurately due to consistent appearance and scale. |
| Small objects (Logs, Ground Clutter) were harder to detect due to visual similarity. |
| A train–validation IoU gap of ~0.04 indicates mild overfitting caused by domain shift. |

---

## 📌 Submission Info  

This repository is submitted as part of the **Startathon Hackathon 2026** organized by **Duality AI**.
