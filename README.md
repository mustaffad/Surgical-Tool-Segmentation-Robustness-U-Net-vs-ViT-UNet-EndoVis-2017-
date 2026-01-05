# Surgical Tool Segmentation Robustness: U-Net vs ViT-UNet (EndoVis 2017)

This repository contains my undergraduate course research project (Dec 2025) comparing a CNN-based U-Net and a Vision-Transformer-based segmentation model on **surgical tool segmentation**, with an emphasis on **robustness under realistic operating-room disturbances**.

## Paper
- [PDF](paper/Comparative_Evaluation_UNet_ViTUNet_EndoVis2017.pdf)

## Summary
- Dataset: EndoVis 2017 (tool masks), resized to 256×256, ImageNet normalization.
- Models: U-Net baseline vs a lightweight ViT-UNet-style model (ViT encoder + decoder).
- Training: Dice + BCE loss, Adam, lr=1e-4, 50 epochs (best checkpoint by validation Dice).
- Robustness: evaluate under Gaussian noise, motion blur, brightness reduction, and occlusion.

## Key Results

### Clean validation performance
| Model    | Dice   | IoU    | Precision | Recall |
|----------|--------|--------|----------|--------|
| U-Net    | 0.9445 | 0.9020 | 0.9576   | 0.9395 |
| ViT-UNet | 0.8941 | 0.8205 | 0.9153   | 0.8877 |

### Robustness (avg over 20 validation images)
| Distortion            | U-Net Dice | U-Net IoU | ViT-UNet Dice | ViT-UNet IoU |
|----------------------|-----------:|----------:|--------------:|-------------:|
| Gaussian Noise (σ=25)| 0.2742     | 0.1591    | 0.2177        | 0.1226       |
| Motion Blur (k=7)    | 0.2618     | 0.1510    | 0.2154        | 0.1212       |
| Brightness (×0.5)    | 0.2535     | 0.1460    | 0.1984        | 0.1105       |
| Occlusion (40×40)    | 0.2601     | 0.1498    | 0.2181        | 0.1228       |

**Takeaway:** In this from-scratch, limited-data setup, U-Net achieved higher clean accuracy and remained more stable under perturbations. Transformer-based models likely require pretraining, stronger augmentation, or hybrid designs to reach comparable robustness.

## Dataset

This project uses the EndoVis 2017 Robotic Instrument Segmentation dataset (MICCAI EndoVis 2017).

- Official Synapse files page (not redistributed in this repo):
  https://www.synapse.org/Synapse:syn22398986/files/

Notes:
- You may need a Synapse account and to agree to the dataset’s conditions for use / request access, depending on the file permissions.
- Please follow the dataset’s license/terms on Synapse. This repository contains only my paper and derived results, not the dataset.
