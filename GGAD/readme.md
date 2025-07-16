# GGAD 模型复现

本项目是 NeurIPS 2024 论文 [Generative Semi-supervised Graph Anomaly Detection](https://arxiv.org/abs/2402.11887) 在本仓库中的复现实现。

GGAD 考虑了一种半监督的图异常检测场景。其核心思想是通过利用已知的正常节点信息，生成结构和特征都与真实异常相似的伪异常节点（outlier nodes），从而为训练一个有效的单类分类器提供负样本。

### 环境配置

本项目需要在独立的虚拟环境中运行，以确保与原论文环境的兼容性。

*   **核心依赖**: `Python 3.7`, `PyTorch 1.11.0`, `PyG 2.1.0`

```bash
# 1. 创建独立的 Conda 环境
conda create -n ggad python=3.7 -y
conda activate ggad

# 2. 安装相关依赖
pip install -r requirements.txt
```

### 运行方法

激活 `ggad` 环境后，使用以下命令运行实验。

```bash
# --dataset 参数用于指定数据集名称
python run.py --dataset amazon
```

### 复现实验结果

以下是在本代码库中运行 `GGAD` 得到的性能指标。

| 数据集 | AUROC | AUPRC |
|:---|:---:|:---:|
| Amazon | 0.8801 | 0.6227 |
| Reddit | 0.6229 | 0.0506 |
| T-Finance| 0.5925 | 0.0860 |
| Questions| 0.4892 | 0.0309 |
| Tolokers | 0.5025 | 0.2293 |

*注：结果为特定运行下的快照，可能会因随机种子和环境而波动。*

### 原论文引用

```bibtex
@inproceedings{qiao2024generative,
  title={Generative Semi-supervised Graph Anomaly Detection},
  author={Qiao, Hezhe and Wen, Qingsong and Li, Xiaoli and Lim, Ee-Peng and Pang, Guansong},
  booktitle={Advances in Neural Information Processing Systems},
  year={2024}
}
```

---

> 想要查看本项目中所有模型的横向对比分析吗？请返回 **[项目主 README](../../README.md)**.
