# Offroad-Semantic-Segmentation

Startathon Hackathon 2026 --- Duality AI Challenge

## Project Overview

This project trains a semantic segmentation model on a synthetic desert
dataset. The objective is to maximize Mean Intersection over Union (Mean
IoU) on an unseen test environment.

### Final Results

-   Final Validation Mean IoU: 0.2991
-   Best Validation IoU: 0.2995 (Epoch 23)
-   Final Validation Dice Score: 0.4428
-   Final Validation Accuracy: 0.7058

------------------------------------------------------------------------

## Model Architecture

-   Backbone: DINOv2 ViT-S/14 (Frozen)
-   Segmentation Head: Lightweight Conv-based head
-   Loss Function: CrossEntropyLoss
-   Optimizer: SGD (momentum=0.9)
-   Learning Rate: 1e-4
-   Epochs: 30
-   Batch Size: 4

The backbone was kept frozen to reduce overfitting and improve
stability.

------------------------------------------------------------------------

## Environment Setup

conda activate EDU pip install -r requirements.txt

------------------------------------------------------------------------

## Training

python train_segmentation.py

Outputs: - segmentation_head.pth - train_stats/ (training graphs and
metrics)

------------------------------------------------------------------------

## Testing

python test_segmentation.py

Outputs: - predictions/ - per_class_metrics.png -
evaluation_metrics.txt - comparison images

------------------------------------------------------------------------

## Folder Structure

project/ │ ├── train_segmentation.py ├── test_segmentation.py ├──
segmentation_head.pth ├── train_stats/ ├── predictions/ ├── README.md
├── requirements.txt └── Report.pdf

------------------------------------------------------------------------

## Key Observations

-   Large objects (Sky, Trees) were detected more accurately.
-   Small objects (Logs, Flowers) were more challenging.
-   Train and test environments differ, affecting generalization.

------------------------------------------------------------------------

This repository is submitted as part of Startathon Hackathon 2026.
