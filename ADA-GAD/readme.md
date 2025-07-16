# ADA-GAD 模型复现

本项目是 AAAI 2024 论文 [ADA-GAD: Anomaly-Denoised Autoencoders for Graph Anomaly Detection](https://arxiv.org/abs/2312.14535) 在本仓库中的复现实现。

ADA-GAD 提出了一种新颖的两阶段框架。第一阶段，它通过一种无需学习的去噪增强方法生成异常程度降低的图，并在此之上预训练图自动编码器以捕捉正常模式；第二阶段，它在原始图上重新训练解码器以进行最终的异常检测。

### 环境配置

本项目需要在独立的虚拟环境中运行，以确保依赖的兼容性。

*   **核心依赖**: `Python 3.8` (推荐), `PyTorch 1.10.1`, `PyG 2.2.0`

```bash
# 1. 创建独立的 Conda 环境
conda create -n ada_gad python=3.8 -y
conda activate ada_gad

# 2. 安装相关依赖
pip install -r requirements.txt
```

### 运行方法

激活 `ada_gad` 环境后，使用以下命令运行实验。

```bash
# --use_cfg 表示使用配置文件
# --seeds 指定随机种子
# --dataset 指定数据集名称
python main.py --use_cfg --seeds 0 --dataset reddit
```

### 复现实验结果

以下是在本代码库中运行 `ADA-GAD` 得到的性能指标。

| 数据集 | AUROC | AUPRC |
|:---|:---:|:---:|
| Amazon | 0.2092 | 0.0400 |
| Reddit | 0.5625 | 0.0386 |
| Weibo | 0.9239 | 0.6631 |
| T-Finance| 0.3232 | 0.0307 |
| DGraph-Fin| 0.4438 | 0.0035 |
| Elliptic | 0.3673 | 0.0162 |
| Questions| 0.5335 | 0.0420 |
| Tolokers | 0.4748 | 0.2246 |
| T-Social | 0.4222 | 0.0243 |
| Yelp | 0.5894 | 0.1946 |

*注：结果为特定运行下的快照，可能会因随机种子和环境而波动。*

### 原论文引用

```bibtex
@inproceedings{he2024ada,
  title={Ada-gad: Anomaly-denoised autoencoders for graph anomaly detection},
  author={He, Junwei and Xu, Qianqian and Jiang, Yangbangyan and Wang, Zitai and Huang, Qingming},
  booktitle={Proceedings of the AAAI Conference on Artificial Intelligence},
  volume={38},
  number={8},
  pages={8481--8489},
  year={2024}
}
```

---

> 想要查看本项目中所有模型的横向对比分析吗？请返回 **[项目主 README](../../README.md)**.
