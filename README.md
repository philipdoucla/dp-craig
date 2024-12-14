# CREPE: Coresets for Robust and Efficient Privacy-preserving Embeddings

## Overview

CREPE addresses two critical challenges in modern machine learning:

Efficient Training: Reducing the computational cost of training large-scale models by using subset selection techniques like CRAIG (Coresets for Accelerating Incremental Gradient descent).

User Privacy: Ensuring differential privacy (DP) by injecting noise into gradient computations, preventing the leakage of individual data points during training.

This project explores the integration of CRAIG and DP to create a differentially private coreset, enabling efficient and privacy-preserving training. The key challenge lies in selecting representative subsets using noisy gradients, which introduces randomness and potential inaccuracies.

## Objective

To evaluate the performance of CRAIG on noisy gradients under differential privacy constraints, analyzing its impact on training time, training/test accuracy, and privacy guarantees.

## Methodology

### 1. Dataset and Model Selection

**Dataset**: MNIST (handwritten digit recognition).

**Models**: A 2-layer Convolutional Neural Network (CNN) and a ResNet model, chosen to balance simplicity and complexity.

### 2. CRAIG Setup

**Data Selection Proportion**: 10% of the dataset is selected.

**Coreset Selection Frequency**: Every 20 epochs across 50 total training epochs.

**Optimization Strategy**: Per-class facility location problem solved with lazy greedy optimization to enhance efficiency.

### 3. Differential Privacy Setup

**Library**: Opacus for DP-SGD implementation.

**Gradient Clipping**: Maximum norm clipping (C = 1.0).

**Noise Addition**: Gaussian noise with standard deviations (σ) of 1.0, 3.0, and 5.0.

**Privacy Budget**: Maintained (ε, δ) parameters throughout training.

### 4. CRAIG + DP Integration

**Gradient Processing:**

- Last layer: Gradients processed with DP (clipping + noise) before CRAIG selects coresets.

- Intermediate layers: Gradients passed through DP-SGD pipeline.

**Parameter Updates**: Learnable parameters updated using noisy gradients computed from selected coresets.

## References
- Martin Abadi, Andy Chu, Ian Goodfellow, H. Brendan McMahan, Ilya Mironov, Kunal Talwar, and Li Zhang. Deep learning with differential privacy. In Proceedings of the 2016 ACM SIGSAC Conference on Computer and Communications Security, CCS ’16, page 308–318, New York, NY, USA, 2016. Association for Computing Machinery. ISBN 9781450341394. doi:10.1145/2976749.2978318. URL https://doi.org/10.1145/2976749.2978318.
- Dan Feldman, Chongyuan Xiang, Ruihao Zhu, and Daniela Rus. Coresets for differentially private k-means clustering and applications to privacy in mobile sensor networks. In Proceedings of the 16th ACM/IEEE International Conference on Information Processing in Sensor Networks, IPSN ’17, page 3–15, New York, NY, USA, 2017. Association for Computing Machinery. ISBN 9781450348904. doi: 10.1145/3055031.3055090. URL https://doi.org/10.1145/3055031.3055090.
- Baharan Mirzasoleiman, Jeff Bilmes, and Jure Leskovec. Coresets for data-efficient training of machine learning models. In Hal Daumé III and Aarti Singh, editors, Proceedings of the 37th International Conference on Machine Learning, volume 119 of Proceedings of Machine Learning Research, pages 6950–6960. PMLR, 13–18 Jul 2020. URL https://proceedings.mlr.press/v119/mirzasoleiman20a.html.
- Ashkan Yousefpour, Igor Shilov, Alexandre Sablayrolles, Davide Testuggine, Karthik Prasad, Mani Malek, John Nguyen, Sayan Ghosh, Akash Bharadwaj, Jessica Zhao, Graham Cormode, and Ilya Mironov. Opacus: User-friendly differential privacy library in PyTorch. arXiv preprint arXiv:2109.12298, 2021

