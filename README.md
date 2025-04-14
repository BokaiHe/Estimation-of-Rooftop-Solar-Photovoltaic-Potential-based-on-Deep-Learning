# Rooftop Solar Photovoltaic Potential Estimation with Deep Learning  
*Pina Pi, Tiancheng Gu, Bokai He*  
*Department of Earth and Environmental Engineering, Columbia University*

## 📌 Overview

This project estimates rooftop solar photovoltaic (PV) potential using deep learning-based semantic segmentation. A U-Net model was trained on RGB and Near-Infrared (NIR) imagery to identify suitable rooftop areas for solar installation, promoting clean energy development and sustainability in urban environments.

## Methodology

### 1. Semantic Segmentation with U-Net

- **Architecture Details**:
  - Each encoder/decoder block contains:
    - Two 3×3 convolution layers
    - BatchNorm2d
    - ReLU activation (inplace = True)
  - Skip connections via `torch.cat`
  - Decoder input = upsampled features + encoder outputs

- **Training Configuration**:
  - Optimizer: Adam (`lr = 1e-5`)
  - Loss: Binary Cross Entropy (`BCELoss`)
  - Batch Size: 8
  - Early Stopping: `patience = 10`

### 2. Solar Potential Estimation Pipeline

- **Rooftop Geometry**:
  - Slope and aspect calculated to assess installation viability

- **Suitability Scoring**:
  - Factors: slope, aspect, thermal characteristics
  - Combined into a final suitability score

- **Energy and Economic Estimation**:
  - Panel layout simulation
  - Daily & annual energy production (kWh)
  - Estimated annual economic benefit (USD)

## Results

### Model Evaluation on Test Set

| Metric     | Value   |
|------------|---------|
| IoU        | 0.6139  |
| Dice       | 0.7593  |
| Precision  | 0.7852  |
| Recall     | 0.7370  |
| F1 Score   | 0.7593  |

### Installation Potential Comparison

| Metric                         | Ground Truth (B) | Predicted Mask (A) |
|-------------------------------|------------------|---------------------|
| Identified Roofs              | 3                | 6                   |
| Suitable Roofs                | 3                | 5                   |
| Total Solar Panels            | 108              | 181                 |
| Annual Energy (kWh)           | 45,490.1         | 76,207.7            |
| Annual Economic Benefit (USD) | 22,745.0         | 38,103.8            |

### Observed Challenges

- Smoothed building edges due to shadows/occlusions
- Loss of detail in small or complex rooftops
- Closely spaced buildings may be merged
- Scale bias towards large structures

## Future Work

- **Dataset Expansion**: Scale from 1,000 to 30,000+ images
- **Data Diversity**: Include seasonal imagery and meteorological info
- **Model Improvements**: Add attention, pretrained backbones, multi-scale fusion
- **Advanced Assessment**: Consider roof materials, building age, and other practical constraints

## Key References

- Zhong et al., 2021. *A city-scale estimation of rooftop solar photovoltaic potential based on deep learning.* [Applied Energy](https://doi.org/10.1016/j.apenergy.2021.117132)
- Liu et al., 2024. *Task specific pretraining with noisy labels for remote sensing image segmentation.* [arXiv](https://arxiv.org/abs/2402.16164)
- Li et al., 2016. *Pixel-based estimation of solar energy potential.* [Energy and Buildings](https://doi.org/10.1016/j.enbuild.2016.08.025)
- Lukač et al., 2014. *LiDAR-based rooftop PV assessment.* [Energy](https://doi.org/10.1016/j.energy.2013.12.066)
- Assouline et al., 2017. *Quantifying PV potential via ML.* [Solar Energy](https://doi.org/10.1016/j.solener.2016.11.045)
- Nelson & Grubesic, 2020. *LiDAR vs UAS for rooftop PV.* [Sustainable Cities and Society](https://doi.org/10.1016/j.scs.2020.102353)

---

*This project was developed as part of Columbia University's Earth and Environmental Engineering Department.*
