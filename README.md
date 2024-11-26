This work from these papers：
@article{weikun4770354generic,
  title={Generic Physics-Informed Machine Learning Framework for Battery Remaining Useful Life Prediction Using Small Early-Stage Lifecycle Data},
  author={WEIKUN, DENG and Le, Hung and Gogu, Christian and Nguyen, Khanh TP and Medjaher, Kamal and Morio, J{\'e}r{\^o}me and Wu, Dazhong},
  journal={Available at SSRN 4770354}
}

@inproceedings{deng2024novel,
  title={A Novel PIML Architecture with Innovative Learning Paradigm Applied in Battery Prognostics},
  author={Deng, Weikun and Nguyen, Khanh TP and Gogu, Christian and Mejaher, Kamal and Morio, J{\'e}r{\^o}me and Le, Hung and Wu, Dazhong},
  booktitle={2024 10th International Conference on Control, Decision and Information Technologies (CoDIT)},
  pages={248--253},
  year={2024},
  organization={IEEE}
}

@article{weikun2023physics,
  title={Physics-informed machine learning in prognostics and health management: State of the art and challenges},
  author={Weikun, DENG and Nguyen, Khanh TP and Medjaher, Kamal and Christian, GOGU and Morio, J{\'e}r{\^o}me},
  journal={Applied Mathematical Modelling},
  volume={124},
  pages={325--352},
  year={2023},
  publisher={Elsevier}
}
# PIML-benchmark-architecture
Benchmark training methodology and framework for PIML (to ensure that knowledge filtering and embedded knowledge is ML-friendly)

README
English Version
This project implements a Physics-Informed Machine Learning (PIML) framework for predicting the Remaining Useful Life (RUL) of fast-charging lithium-ion batteries. The model combines domain-specific knowledge of Solid Electrolyte Interface (SEI) layer growth with data-driven modeling via Dilated Convolutional Neural Networks (DCNN).

Major Contributions:

A hybrid dual-branch architecture integrating physics-based SEI growth models and data-driven DCNN features.
Enhanced prediction accuracy using a three-step learning strategy, significantly reducing mean absolute error (MAE) compared to baseline DCNN models.
Improved interpretability and insight into battery degradation mechanisms while retaining computational efficiency.
The framework was validated on the MIT-Stanford fast-charging battery datasets, showcasing superior performance over existing benchmarks in RUL prediction.

中文版本
本项目实现了一种用于预测快充锂电池剩余使用寿命（RUL）的物理信息驱动机器学习（PIML）框架。模型结合了固态电解质界面（SEI）层增长的领域知识与基于膨胀卷积神经网络（DCNN）的数据驱动建模。

主要贡献：

提出了结合物理驱动的SEI增长模型和数据驱动DCNN特征的混合双分支架构。
通过三步学习策略显著提高了预测精度，与基准DCNN模型相比，大幅降低了平均绝对误差（MAE）。
提供了对电池退化机制的深入洞见，同时保持了较高的计算效率。
该框架在MIT-Stanford快充锂电池数据集上验证，RUL预测性能优于现有基准模型。

Here is the reason why we need train the PI and ML separately：
Different parts of the program meet different objectives at different stages of study, progressively approaching higher points.Informed means that it should be and does not affect the original performance of the ML but also brings benefits, otherwise it means that the form and content of the physical knowledge does not match the embedding method and the data-driven model.
不同部分在不同学习阶段满足同一目标，逐步逼近更优点，Informed 含义应该是并且不影响ML原有的表现还能带来增益，否则就表示物理知识的形式、内容与嵌入方式和数据驱动模型不匹配。
Three-Step Learning Strategy
1. Data-Driven Branch Pretraining
Process:

Train the data-driven branch (DCNN) using raw time-series data such as current, voltage, temperature, and time.
The model extracts multi-scale features through dilated convolutions and predicts the Remaining Useful Life (RUL) based solely on data-driven methods.
The objective is to minimize the difference between predicted and actual RUL, ensuring that the branch learns high-quality temporal patterns.
Benefits:

Provides a solid baseline prediction.
Ensures the model can independently perform RUL prediction without physical constraints.
2. Physics-Driven Branch Training
Process:

Use physical models, such as SEI growth dynamics, to train the physics-driven branch. The model aligns its predictions with the pre-trained data-driven branch.
Custom neural network layers embed physical relationships, making predictions interpretable and consistent with known physical laws.
Parameters specific to the physical model are optimized while keeping the data-driven branch frozen.
Benefits:

Embeds domain-specific physical knowledge into the model.
Enhances interpretability by ensuring predictions align with real-world degradation mechanisms.
3. Joint Global Optimization
Process:

Combine the outputs of the data-driven and physics-driven branches using feature fusion.
Train the entire framework end-to-end, leveraging both the flexibility of the data-driven branch and the interpretability of the physics-driven branch.
Optimize all model parameters together to ensure global performance.
Benefits:

Maximizes the strengths of both branches for superior RUL prediction accuracy.
Enhances generalization across diverse conditions and datasets.
Provides a unified framework that is both efficient and interpretable.
