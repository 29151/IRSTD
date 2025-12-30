# 红外小目标检测方法

本仓库旨在收集、整理并维护与红外小目标检测（IRST）相关的方法、论文与代码实现。后续会将相关文章逐篇添加到下面的列表中，便于学习与对比。

## 已收录方法
- **One Shot is Enough for Sequential Infrared Small Target Segmentation -2025**  
  代码：[https://github.com/D-IceIce/one-shot-IRSTS](https://github.com/D-IceIce/one-shot-IRSTS)  

  网络图：
  <img width="1652" height="373" alt="image" src="https://github.com/user-attachments/assets/06c812a4-f559-4ed2-bd2f-c8681853ddc1" />

  测试数据集：sequential IRSTS（分割）

  概述：使用提示图片（已知mask）提取红外小目标在经过SAM Encoder的特征，使用该特征匹配目标图片的特征，找到目标所在位置的中心点。将该中心点作为提示投入SAM输出分割结果。

  特点：
   - 不需要单独训练，使用SAM的训练模型。
   - 输入是带有已知mask的提示图片和目标图片

- **OSFormer: One-Step Transformer for Infrared Video Small Object Detection -2025**  
  论文：https://ieeexplore.ieee.org/document/11130659

  网络图：
  <img width="1261" height="802" alt="image" src="https://github.com/user-attachments/assets/fdfb528e-d242-4b03-a533-2b521ebae739" />

  测试数据集：AntiUAV, InfraredUAV, and UAVSwarm（boundingbox）

  特点：
   - 利用立方体式编码对序列数据进行一步式检测，避免了大部分方法两步检测序列数据的限制。
   - 使用可变size的patch-embeding解决了标准Vision Transformer的 "固定尺寸块划分" 与小目标检测的矛盾。
   - 在频域（cube经过2+1维傅里叶变换）使用多普勒自适应滤波器，利用 "运动频率差异" 而非 "幅度差异" 来区分目标与噪声。
   - 同时预测多帧的目标。

- **Semi-Supervised Multiview Prototype Learning With Motion Reconstruction for Moving Infrared Small Target Detection**（S2MVP）  
  论文：IEEE Trans. on Geoscience and Remote Sensing (TGRS 2025)  
  代码：https://github.com/UESTC-nnLab/S2MVP

  网络图：  
  <img width="909" height="431" alt="image" src="https://github.com/user-attachments/assets/a07069a9-73fa-446a-a079-7239b82d877b" />  
  蓝色是推理路线，整个架构是训练路线。

  测试数据集：DAUB， ITSDT-15K, IRDST（boundingbox）.

  概述：为了解决有标注数据少和标注耗费大量人力的问题，创建了一种半监督的训练方式，教师网络（少量有标注数据训练过的）和学生网络相互学习。

  特点：
  - Extractor利用了ResNet50的预训练模型。
  - BMP改良了ConvGRU利用时序信息提取运动特征。
  - APF自适应过滤教师网络预测的伪标签，提高标签质量。
  - Pm存储目标特征模板作为“知识库”，通过未标注数据持续更新进化。
