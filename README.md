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

```bash
pip install ultralytics kaggle
