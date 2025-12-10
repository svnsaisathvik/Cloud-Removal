# 🌥️ Cloud-Free Satellite Imagery Generation: TimeGate & Multimodal Fine-Tuning

> Project implementing the TimeGate deep learning approach and extending it using high-resolution data and EO foundation model fine-tuning.

## 1. Project Overview

Optical satellite imagery (e.g., Sentinel-2) is often obscured by clouds, shadows, and missing data. This project generates clear, coherent images for a target date and region by leveraging time-series data through:
- TimeGate preprocessing
- Two fusion model pathways:
  - U-Net training
  - TerraMind foundation model fine-tuning

## 2. Core Methodology: TimeGate

### 2.1 — Time Extraction (Gating Mechanism)
- Input: image series T, cloud/missing indicators, temporal distance
- Goal: learn importance value per time step
- Gating: uses exponential decay over negated ReLU

### 2.2 — Aggregation
Produces:
- Composite image: Ẋ
- Abstract temporal features: Hᵃᵍᵍ

### 2.3 — Fusion Pathways

#### Pathway 1: U-Net
- Inputs: Ẋ + Hᵃᵍᵍ
- Encoder: MnasNet
- Decoder: Pixel-Shuffle + Self-Attention

#### Pathway 2: TerraMind Fine-Tuning
- Uses TimeGate outputs to fine-tune IBM/ESA TerraMind
- Improves cloud removal + missing region restoration

## 3. Training & Evaluation

### Data Enhancement

Landsat → Sentinel-2 (10m/20m/60m)
- Higher resolution output

### Metrics & Loss

- Metrics: MSE & SSIM (preferred)
- Loss: Feature Reconstruction Loss (FEAT)

## 4. Repository Structure

```
unet/
timegate/
terramind_finetuning/
data/
```

## Summary

TimeGate + Multimodal fine-tuning → High-resolution, cloud-free satellite images.
