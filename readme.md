# 🌥️ Cloud-Free Satellite Imagery Generation: TimeGate & Multimodal Fine-Tuning

> **Implemented from scratch based on:** ["Creating Cloud-Free Satellite Imagery from Image Time Series with Deep Learning"](https://doi.org/10.1145/3423336.3429345) (Oehmcke et al., BIGSPATIAL 2020)

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
- Uses TimeGate outputs to fine-tune [IBM/ESA TerraMind](https://huggingface.co/ibm-esa-geospatial/TerraMind-1.0-base)
- Foundation model for Earth Observation (1.0B parameters)
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
unet/                       # U-Net fusion pathway
timegate/                   # TimeGate implementation
terramind_finetuning/       # TerraMind foundation model fine-tuning
data/                       # Dataset storage
```

## 5. Models Used

- **TimeGate Architecture:** Implemented from [BIGSPATIAL 2020 paper](https://doi.org/10.1145/3423336.3429345)
- **TerraMind Foundation Model:** [IBM/ESA TerraMind-1.0-base](https://huggingface.co/ibm-esa-geospatial/TerraMind-1.0-base)

## Summary

TimeGate + Multimodal fine-tuning → High-resolution, cloud-free satellite images.

