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

  
  
