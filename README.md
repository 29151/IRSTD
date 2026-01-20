# 红外小目标检测方法

本仓库旨在收集、整理并维护与红外小目标检测（IRST）相关的方法、论文与代码实现。后续会将相关文章逐篇添加到下面的列表中，便于学习与对比。

## 已收录文章
### 1、**One Shot is Enough for Sequential Infrared Small Target Segmentation -2025**  
  代码：[https://github.com/D-IceIce/one-shot-IRSTS](https://github.com/D-IceIce/one-shot-IRSTS)  

  网络图：
  <img width="1652" height="373" alt="image" src="https://github.com/user-attachments/assets/06c812a4-f559-4ed2-bd2f-c8681853ddc1" />

  测试数据集：sequential IRSTS（分割）

  个人总结：使用提示图片（已知mask）提取红外小目标在经过SAM Encoder的特征，使用该特征匹配目标图片的特征，找到目标所在位置的中心点。将该中心点作为提示投入SAM输出分割结果。

  特点：
   - 不需要单独训练，使用SAM的训练模型。
   - 输入是带有已知mask的提示图片和目标图片

### 2、**OSFormer: One-Step Transformer for Infrared Video Small Object Detection -2025**  
  论文：https://ieeexplore.ieee.org/document/11130659

  网络图：
  <img width="1261" height="802" alt="image" src="https://github.com/user-attachments/assets/fdfb528e-d242-4b03-a533-2b521ebae739" />

  测试数据集：AntiUAV, InfraredUAV, and UAVSwarm（boundingbox）

  特点：
   - 利用立方体式编码对序列数据进行一步式检测，避免了大部分方法两步检测序列数据的限制。
   - 使用可变size的patch-embeding解决了标准Vision Transformer的 "固定尺寸块划分" 与小目标检测的矛盾。
   - 在频域（cube经过2+1维傅里叶变换）使用多普勒自适应滤波器，利用 "运动频率差异" 而非 "幅度差异" 来区分目标与噪声。
   - 同时预测多帧的目标。

### 3、**Semi-Supervised Multiview Prototype Learning With Motion Reconstruction for Moving Infrared Small Target Detection**（S2MVP）  
  论文：IEEE Trans. on Geoscience and Remote Sensing (TGRS 2025)  
  代码：https://github.com/UESTC-nnLab/S2MVP

  网络图：  
  <img width="909" height="431" alt="image" src="https://github.com/user-attachments/assets/a07069a9-73fa-446a-a079-7239b82d877b" />  
  蓝色是推理路线，整个架构是训练路线。

  测试数据集：DAUB， ITSDT-15K, IRDST（boundingbox）.

  个人总结：为了解决有标注数据少和标注耗费大量人力的问题，创建了一种半监督的训练方式，教师网络（少量有标注数据训练过的）和学生网络相互学习。

  特点：
  - Extractor利用了ResNet50的预训练模型。
  - BMP改良了ConvGRU利用时序信息提取运动特征。
  - APF自适应过滤教师网络预测的伪标签，提高标签质量。
  - Pm存储目标特征模板作为“知识库”，通过未标注数据持续更新进化。

### 4、**SeqCSIST: Sequential Closely-Spaced Infrared Small Target Unmixing -2025**  
  论文：https://xplorestaging.ieee.org/document/11080063  
  代码：https://github.com/GrokCV/SeqCSIST
  
  网络图：
  <img width="1158" height="609" alt="image" src="https://github.com/user-attachments/assets/93c5c8a3-0141-45d1-a51f-0fbed518face" />
  
  创新：  
  - 提出了新的检测任务名为sequential CSIST unmixing，目的是解决多目标近距离时发生重叠在成像系统上呈现模糊斑块难以区分的问题，拓展了SIRST任务的定义。  
  - 创建了适配新任务的数据集：SeqCSIST，https://pan.baidu.com/s/1_sxGh5oFQ8-3RpUUeMN2Mg?pwd=kxe9  
  - 提出了适配新任务的检测方法：DeRefNet  

### 5、 **Toward Dense Moving Infrared Small Target Detection: New Datasets and Baseline -2024**  
  论文：[https://xplorestaging.ieee.org/document/11080063](https://ieeexplore.ieee.org/document/10636251)  
  代码：[https://github.com/GrokCV/SeqCSIST](https://github.com/UESTC-nnLab/DMIST)
  
  网络图：
  <img width="1274" height="481" alt="image" src="https://github.com/user-attachments/assets/30d266de-1caf-4cf0-b9d9-d1cef7091bc8" />
  
  创新：  
  - 为了解决密集目标检测的任务，合成了两个密集目标的数据集。  
  - 提出了LASNet来评估两个新数据集。（SST网络改良版）  

### 6、 **A New Motion Feature-Enhanced Multiframe Spatial–Temporal Infrared Target Detection Network -2025**  
  论文：https://ieeexplore.ieee.org/document/11145128  
  代码：https://github.com/lifenghong/MFE-Net  

  MFE-Net网络图：
  <img width="1054" height="552" alt="image" src="https://github.com/user-attachments/assets/1bd517d8-1e31-4115-a6af-b23d46d0c5b6" />

  创新：  
  - 旨在解决卫星图象和移动背景下的红外小目标检测，为此合成了新的数据集：MIRSat-QL
  - 在低分辨率特征图中计算光流对齐所有分辨率的特征，抑制背景移动的干扰。
  - 新的深浅特征融合模块AGFF

### 7、 **Enhancing Infrared Small Target Detection: A Saliency-Guided Multi-Task Learning Approach -2025**  
  论文：https://ieeexplore.ieee.org/abstract/document/10844059

  Light-SGMTLM网络图：  
  <img width="1423" height="551" alt="image" src="https://github.com/user-attachments/assets/347f3c92-7a38-43a4-8741-10ce7ebcd4be" />  

  特点：  
  - 多任务同时学习：目标检测和分割。
  - 注重与深层特征和浅层特征的融合。
  - backbone中的SIWD模块使用1x3和3x1的卷积替代3x3的卷积，保证感受野的同时降低了参数量。
  
