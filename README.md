# GAD-Reproducibility-Benchmark

本项目旨在对2024年图异常检测（Graph Anomaly Detection, GAD）领域的代表性论文进行标准化的代码复现和性能分析。作为[此处可以填写项目背景，如：一个课程项目或夏令营任务]的一部分，我们希望通过此仓库为后续研究者提供一个可靠的基准和统一的实验平台。

**项目目标：**
1.  **复现前沿算法**：深入理解并复现三篇顶级会议论文（NeurIPS'24, ICLR'24, AAAI'24）中的图异常检测模型。
2.  **标准化实验**：在统一的代码框架和多个公开基准数据集上对这些模型进行公平的性能评估和比较。
3.  **开放与共享**：提供一个结构清晰、易于使用的开源代码仓库，方便社区进行复现、比较和扩展。

## 1. 复现模型概览

本项目选择了以下三篇具有代表性的论文进行复现：

| 模型 | 论文标题 | 会议 | 核心思想 |
| :--- | :--- | :--- | :--- |
| **GGAD** | Generative Semi-supervised Graph Anomaly Detection | NeurIPS 2024 | 通过生成伪异常节点来辅助半监督图异常检测。 |
| **ConsisGAD** | Consistency Training with Learnable Data Augmentation for GAD | ICLR 2024 | 利用一致性训练和可学习的数据增强来处理有限监督场景。 |
| **ADA-GAD** | Anomaly-Denoised Autoencoders for Graph Anomaly Detection | AAAI 2024 | 设计一个两阶段框架，先在去噪的图上预训练，再在原图上检测。 |

## 2. 环境配置与安装

为了保证实验的可复现性，我们强烈建议使用 `conda` 创建并管理虚拟环境。

```bash
# 1. 克隆本仓库
git clone https://github.com/lsyu0904/GAD-Reproducibility-Benchmark.git
cd GAD-Reproducibility-Benchmark

# 2. 创建并激活 Conda 环境
conda create -n gad_benchmark python=3.8
conda activate gad_benchmark

# 3. 安装所有依赖项
# requirements.txt 文件整合了运行所有三个模型所需的依赖库
pip install -r requirements.txt
```

## 3. 数据集

本项目在多个公开的图异常检测基准数据集上进行了实验，包括 **Amazon, Reddit, T-Finance, Weibo, Yelp, Elliptic, DGraph-Fin, Questions, Tolokers, T-Social** 等。

请下载所需的数据集，并根据每个模型子目录中的说明，将它们放置在指定的位置（例如 `data/` 或各模型的 `dataset/` 目录）。

## 4. 如何运行实验

每个模型的复现代码都存放于独立的子目录中，以保持模块化和代码清晰性。

### 运行 GGAD
```bash
# 进入GGAD目录
cd GGAD/

# 运行指令 (以 amazon 数据集为例)
python run.py --dataset amazon
```

### 运行 ConsisGAD
```bash
# 进入ConsisGAD目录
cd ConsisGAD/

# 运行指令 (以 amazon 数据集为例, 运行5次)
python main.py --config 'config/amazon.yml' --runs 5
```

### 运行 ADA-GAD
```bash
# 进入ADA-GAD目录
cd ADA-GAD/

# 运行指令 (以 reddit 数据集为例)
python main.py --use_cfg --seeds 0 --dataset reddit
```
**注意：** 每个模型更详细的运行参数和配置，请参考其对应子目录下的文档。

## 5. 实验结果汇总与分析

我们在多个数据集上对三个模型进行了复现，并将关键性能指标（AUROC 和 AUPRC）汇总如下。所有结果均为本仓库代码运行得出。

#### AUROC (Area Under ROC Curve) 性能对比

| 数据集 | GGAD (复现) | ConsisGAD (复现) | ADA-GAD (复现) |
|:---|:---:|:---:|:---:|
| Amazon | 0.8801 | **0.9495** | 0.2092 |
| Reddit | 0.6229 | **0.6258** | 0.5625 |
| Weibo | - | **0.9472** | 0.9239 |
| T-Finance| 0.5925 | **0.9502** | 0.3232 |
| DGraph-Fin | - | **0.6710** | 0.4438 |
| Elliptic | - | **0.8348** | 0.3673 |
| Questions | 0.4892 | **0.7038** | 0.5335 |
| Tolokers | 0.5025 | **0.7332** | 0.4748 |
| T-Social | - | **0.9496** | 0.4222 |
| Yelp | - | **0.7616** | 0.5894 |

#### AUPRC (Area Under PR Curve) 性能对比

| 数据集 | GGAD (复现) | ConsisGAD (复现) | ADA-GAD (复现) |
|:---|:---:|:---:|:---:|
| Amazon | 0.6227 | **0.8387** | 0.0400 |
| Reddit | 0.0506 | **0.0569** | 0.0386 |
| Weibo | - | **0.8295** | 0.6631 |
| T-Finance| 0.0860 | **0.8078** | 0.0307 |
| DGraph-Fin | - | **0.0065** | 0.0035 |
| Elliptic | - | **0.1561** | 0.0162 |
| Questions | 0.0308 | **0.1538** | 0.0420 |
| Tolokers | 0.2293 | **0.3779** | 0.2246 |
| T-Social | - | **0.4648** | 0.0243 |
| Yelp | - | **0.3666** | 0.1946 |

*注："-" 表示该模型未在该数据集上进行复现实验。表格中的数值已四舍五入至4位小数。*

### 性能差异初步分析

在复现过程中，我们观察到实验结果与原论文报告的数值存在一定差异，同时各模型在不同数据集上表现各异。这在学术复现中是常见现象，主要可能归因于：
*   **环境因素**：依赖库（PyTorch, DGL等）的版本、硬件（CPU/GPU）和操作系统的细微差别。
*   **数据预处理**：官方代码中可能存在未在论文中详述的数据清洗或预处理步骤。
*   **随机性**：模型参数初始化、数据划分和训练过程中的随机操作（如dropout）都会引入波动。
*   **超参数敏感性**：部分模型可能对学习率、批大小等超参数非常敏感，我们的配置未必是全局最优。

更详细的针对每个模型的分析，请见其子目录下的文档。

## 6. 致谢

本项目的代码实现和复现工作基于以下优秀的开源项目，在此向原作者们表示诚挚的感谢：

*   **GGAD**: [https://github.com/mala-lab/GGAD](https://github.com/mala-lab/GGAD)
*   **ConsisGAD**: [https://github.com/Xtra-Computing/ConsisGAD](https://github.com/Xtra-Computing/ConsisGAD)
*   **ADA-GAD**: [https://github.com/jweihe/ADA-GAD](https://github.com/jweihe/ADA-GAD)

欢迎通过 Issue 或 Pull Request 对本项目进行提问和贡献！
