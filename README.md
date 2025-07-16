# GAD-Reproducibility-Benchmark
# 图异常检测算法复现基准 (A Reproducibility Benchmark for Graph Anomaly Detection)

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-blue.svg" alt="Python Version">
  <img src="https://img.shields.io/badge/PyTorch-1.11+-orange.svg" alt="PyTorch Version">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License">
</p>

## 1. 项目简介 (Introduction)

本项目旨在对图异常检测（Graph Anomaly Detection, GAD）领域的最新研究成果进行深度复现与基准测试。根据项目要求，我们选取了三篇近年发表于人工智能顶会的论文，在超过10个公开基准数据集上进行了严格的代码复现和性能评估。

本仓库的目标是：
* 为社区提供一个统一、可复现的 GAD 算法实验平台。
* 深入分析不同模型在多样化数据集上的性能表现与差异。
* 提供详细的配置、开箱即用的运行脚本与结果分析。

### 复现论文列表
* **ConsisGAD:** *Consistency Training with Learnable Data Augmentation for Graph Anomaly Detection with Limited Supervision* (ICLR 2024)
* **GGAD:** *Generative Semi-supervised Graph Anomaly Detection* (NeurIPS'24)
* **ADA-GAD:** *Anomaly-Denoised Autoencoders for Graph Anomaly Detection* (AAAI 2024)

## 2. 性能总览 (Overall Performance)

我们在多个数据集上对三个模型进行了测试，主要性能指标为 **AUROC**。下表汇总了我们复现的核心结果。更详细的 AUPRC、Rec@K 指标及逐模型的深入分析请参阅 `analysis/` 目录下的报告。

| Dataset     | **ConsisGAD**<br>(AUROC) | **GGAD**<br>(AUROC) | **ADA-GAD**<br>(AUROC) |
| :---------- | :----------------------: | :------------------: | :--------------------: |
| amazon      |      0.950 / 0.955* |        0.8801        |         0.2092         |
| reddit      |          0.626           |        0.6229        |         0.5625         |
| tfinance    |          0.950           |        0.5925        |           -            |
| tsocial     |          0.950           |          -           |           -            |
| dgraphfin   |          0.671           |          -           |           -            |
| elliptic    |          0.835           |          -           |           -            |
| yelp        |          0.762           |          -           |           -            |
| weibo       |          0.947           |          -           |         0.9239         |
| questions   |          0.704           |          -           |           -            |
| tolokers    |          0.733           |          -           |           -            |
| photo       |            -             |          -           |           -            |

*注：表格数据来源于各个模型的复现实验。"-" 代表该实验未进行或未在报告中提供。Amazon* 结果来自ConsisGAD复现中的两次不同运行。*

## 3. 环境设置 (Setup)

### 3.1. 克隆本仓库
```bash
git clone [https://github.com/your-username/GAD-Reproducibility-Benchmark.git](https://github.com/your-username/GAD-Reproducibility-Benchmark.git)
cd GAD-Reproducibility-Benchmark
