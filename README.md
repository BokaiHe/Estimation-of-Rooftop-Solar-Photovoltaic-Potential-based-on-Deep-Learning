# Rooftop Solar Photovoltaic Potential Estimation with Deep Learning  
*Pina Pi, Tiancheng Gu, Bokai He*  
*Department of Earth and Environmental Engineering, Columbia University*

## Overview

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

- Zhong, T., Zhang, Z., Chen, M., Zhang, K., Zhou, Z., Zhu, R., Wang, Y., Lü, G., & Yan, J. (2021). A city-scale estimation of rooftop solar photovoltaic potential based on deep learning. *Applied Energy*, 298, 117132. https://doi.org/10.1016/j.apenergy.2021.117132

- Liu, C., Albrecht, C. M., Wang, Y., & Zhu, X. X. (2024). Task specific pretraining with noisy labels for remote sensing image segmentation. *IEEE International Geoscience and Remote Sensing Symposium (IGARSS)*. https://arxiv.org/abs/2402.16164

- Li, Y., Ding, D., Liu, C., & Wang, C. (2016). A pixel-based approach to estimation of solar energy potential on building roofs. *Energy and Buildings*, 129, 563–573. https://doi.org/10.1016/j.enbuild.2016.08.025

- Lukač, N., Seme, S., Žlaus, D., Štumberger, G., & Žalik, B. (2014). Buildings roofs photovoltaic potential assessment based on LiDAR (Light Detection And Ranging) data. *Energy*, 66, 598–609. https://doi.org/10.1016/j.energy.2013.12.066

- Assouline, D., Mohajeri, N., & Scartezzini, J. L. (2017). Quantifying rooftop photovoltaic solar energy potential: A machine learning approach. *Solar Energy*, 141, 278–296. https://doi.org/10.1016/j.solener.2016.11.045

- Nelson, J. R., & Grubesic, T. H. (2020). The use of LiDAR versus unmanned aerial systems (UAS) to assess rooftop solar energy potential. *Sustainable Cities and Society*, 61, 102353. https://doi.org/10.1016/j.scs.2020.102353

---

*This project was developed as part of Columbia University's Earth and Environmental Engineering Department.*
