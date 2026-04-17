# VisDrone Detection with YOLOv8n

A compact Google Colab project for benchmarking and fine-tuning **YOLOv8n** on the **VisDrone** dataset for **small-object detection** in aerial images.

## Overview

This notebook:

- mounts Google Drive in Colab
- installs `ultralytics` and `kaggle`
- downloads the **VisDrone** dataset from Kaggle
- checks dataset structure and YAML config
- previews validation images
- evaluates a pretrained **YOLOv8n** model as a baseline
- fine-tunes YOLOv8n on VisDrone
- compares baseline vs fine-tuned metrics
- visualizes qualitative predictions before and after training

## Motivation

Models pretrained on COCO often struggle on aerial imagery because objects are:

- much smaller
- more crowded
- more heavily overlapped
- viewed from different scales and angles

This notebook tests how much a lightweight detector improves after short domain-specific training on VisDrone.

## Setup

Environment assumed by the notebook:

- **Google Colab**
- GPU runtime
- Google Drive mounted at `/content/drive`
- `kaggle.json` stored in Drive
- dataset downloaded with Kaggle CLI

Main packages:

    pip install ultralytics kaggle

## Dataset

The notebook uses the Kaggle VisDrone package:

- dataset root: `/content/VisDrone_Dataset`
- config file: `/content/VisDrone_Dataset/visdrone.yaml`

It checks the expected train/val/test folders before training.

## Model

- Model: **YOLOv8n**
- Initial weights: `yolov8n.pt` (COCO-pretrained)

## Training Configuration

Fine-tuning is run with:

- **epochs:** 10
- **imgsz:** 768
- **batch:** 4
- **device:** GPU (`device=0`)
- **workers:** 2
- **augmentation:** enabled
- **cache:** disabled

## Evaluation

The notebook first evaluates the pretrained model on the VisDrone validation split to establish a baseline, then evaluates the fine-tuned model on the same split for direct comparison.

Tracked metrics:

- Precision
- Recall
- mAP50
- mAP50-95

## Results

The notebook reports a clear improvement after fine-tuning:

- baseline **mAP50 ≈ 0.03**
- fine-tuned **mAP50 ≈ 0.28**

This shows that even a small model like YOLOv8n benefits substantially from adaptation to the VisDrone domain.

## Qualitative Analysis

The notebook also runs inference on a fixed validation image before and after training to show how detection quality changes visually.

Saved outputs include:

- baseline prediction images
- fine-tuned prediction images
- training run artifacts
- best weights
- validation comparison table

## Output Paths

Important paths used in the notebook:

- baseline predictions: `/content/runs/detect/baseline`
- latest synced training run: `/content/drive/MyDrive/EE428_results/latest`
- best model weights: `/content/drive/MyDrive/EE428_results/latest/weights/best.pt`

## Notes

- Paths are hardcoded for Colab and Google Drive.
- The workflow is designed as a lightweight experiment rather than a full production pipeline.
- Results come from a short 10-epoch run, so further tuning may improve performance.

## Summary

This project demonstrates a simple and practical pipeline for **small-object detection on VisDrone using YOLOv8n**.  
The pretrained model performs poorly out of the box, but short fine-tuning yields a strong improvement in validation performance and visibly better detections on aerial imagery.
