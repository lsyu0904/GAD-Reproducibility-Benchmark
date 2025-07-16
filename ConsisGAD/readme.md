# ConsisGAD 模型复现

本项目是 ICLR 2024 论文 [Consistency Training with Learnable Data Augmentation for Graph Anomaly Detection with Limited Supervision](https://openreview.net/forum?id=elMKXvhhQ9) 在本仓库中的复现实现。

ConsisGAD 专为有限监督场景下的图异常检测设计。它通过一致性训练和一种新颖的可学习数据增强机制，有效利用大量未标记数据来提升检测性能。

### 环境配置

本项目需要在独立的虚拟环境中运行。请注意，该模型使用的是 **DGL** 框架。

*   **核心依赖**: `Python 3.7`, `PyTorch 1.13.1`, `DGL 1.1.0`

```bash
# 1. 创建独立的 Conda 环境
conda create -n consis_gad python=3.7 -y
conda activate consis_gad

# 2. 安装相关依赖
pip install -r requirements.txt
```

### 运行方法

激活 `consis_gad` 环境后，使用以下命令运行实验。该模型的超参数通过 `config/` 目录下的 `.yml` 文件进行管理。

```bash
# --config 指定配置文件
# --runs   指定重复实验的次数
python main.py --config 'config/amazon.yml' --runs 5
```

### 复现实验结果

以下是在本代码库中运行 `ConsisGAD` 得到的性能指标。

| 数据集 | AUROC | AUPRC |
|:---|:---:|:---:|
| Amazon | 0.9495 | 0.8387 |
| Reddit | 0.6258 | 0.0569 |
| Weibo | 0.9472 | 0.8295 |
| T-Finance | 0.9502 | 0.8078 |
| DGraph-Fin| 0.6710 | 0.0065 |
| Elliptic | 0.8348 | 0.1561 |
| Questions | 0.7038 | 0.1538 |
| Tolokers | 0.7332 | 0.3779 |
| T-Social | 0.9496 | 0.4648 |
| Yelp | 0.7616 | 0.3666 |

*注：结果为特定运行下的快照，可能会因随机种子和环境而波动。*

### 原论文引用

```bibtex
@inproceedings{
chen2024consistency,
title={Consistency Training with Learnable Data Augmentation for Graph Anomaly Detection with Limited Supervision},
author={Nan Chen and Zemin Liu and Bryan Hooi and Bingsheng He and Rizal Fathony and Jun Hu and Jia Chen},
booktitle={The Twelfth International Conference on Learning Representations},
year={2024},
url={https://openreview.net/forum?id=elMKXvhhQ9}
}
```

---

> 想要查看本项目中所有模型的横向对比分析吗？请返回 **[项目主 README](../../README.md)**.
