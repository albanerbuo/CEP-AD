# CEP-AD: Excess-Preserving Residual Calibration for Industrial Anomaly Detection

Official implementation of **CEP-AD** (Calibration with Excess Preservation for Anomaly Detection).

<!-- Replace with your overview figure, e.g. figures/overview.png -->
<!-- <p align="center"><img src="figures/overview.png" width="90%"></p> -->

## Overview

Industrial anomaly detection based on normal references treats the deviation of a query from these references as anomaly evidence. However, changes in acquisition conditions (illumination, viewpoint, background, pose) induce additional residual responses in normal regions, making anomaly scores computed against fixed normal references unreliable.

CEP-AD is a **training-free** method that calibrates the query residual at inference time. It models the query residual as the sum of normal, acquisition-shift, and anomaly components, and:

1. identifies positive-eigenvalue directions from the second-moment difference between support and query residuals;
2. estimates a normal residual baseline and a shift magnitude along each direction;
3. applies a bounded calibration that suppresses acquisition-related responses while preserving local excess responses.

The calibration rule is the unique closed-form solution of a strongly convex optimization problem, so it requires neither additional training nor reconstruction of the normal reference.

## Highlights

- **Training-free, 1-shot**, built on frozen DINOv2 ViT-G/14 features.
- **Best AU-PRO among 1-shot training-free methods** on all seven industrial benchmarks.
- **Robust to acquisition shifts**: compared with SubspaceAD, +20.57 I-AUROC on AeBAD-S and +5.34 AU-PRO on MVTec AD 2.
- **Plug-in module**: raises the AU-PRO of PatchCore and AnomalyDINO on AeBAD-S by 12.90 and 8.91 points, respectively.

## Benchmarks

| Type | Datasets |
| --- | --- |
| Acquisition-shift benchmarks | MVTec AD 2, AeBAD-S, RobustAD, PIAD |
| Standard IAD benchmarks | MVTec AD, VisA, Real-IAD |

Metrics: I-AUROC, P-AUROC, and AU-PRO.

## Default Setting

- Backbone: DINOv2 ViT-G/14 with registers (frozen)
- Input resolution: 672 × 672 (48 × 48 patch grid)
- Features: averaged over blocks 22–28 (0-indexed)
- Normal subspace: PCA with 0.99 cumulative explained variance
- Support set: 1-shot

## Code

Code and instructions for installation, data preparation, and evaluation will be released soon.

## Citation

The paper is currently under review. Citation information will be added upon publication.

## Acknowledgements

This project builds on [SubspaceAD](https://arxiv.org/), [AnomalyDINO](https://github.com/dammsi/AnomalyDINO), [PatchCore](https://github.com/amazon-science/patchcore-inspection), and [DINOv2](https://github.com/facebookresearch/dinov2). We thank the authors for releasing their code.
