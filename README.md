# 红外小目标检测方法

本仓库旨在收集、整理并维护与红外小目标检测（IRST）相关的方法、论文与代码实现。后续会将相关文章逐篇添加到下面的列表中，便于学习与对比。

## 已收录文章
### 1、**One Shot is Enough for Sequential Infrared Small Target Segmentation -2025**  
  代码：[https://github.com/D-IceIce/one-shot-IRSTS](https://github.com/D-IceIce/one-shot-IRSTS)  

  网络图：
  <img width="1652" height="373" alt="image" src="https://github.com/user-attachments/assets/06c812a4-f559-4ed2-bd2f-c8681853ddc1" />

  实验数据集：sequential IRSTS（分割）

  个人总结：使用提示图片（已知mask）提取红外小目标在经过SAM Encoder的特征，使用该特征匹配目标图片的特征，找到目标所在位置的中心点。将该中心点作为提示投入SAM输出分割结果。

  特色：
   - 不需要单独训练，使用SAM的训练模型。
   - 输入是带有已知mask的提示图片和目标图片

### 2、**OSFormer: One-Step Transformer for Infrared Video Small Object Detection -2025**  
  论文：https://ieeexplore.ieee.org/document/11130659

  网络图：
  <img width="1261" height="802" alt="image" src="https://github.com/user-attachments/assets/fdfb528e-d242-4b03-a533-2b521ebae739" />

  实验数据集：AntiUAV, InfraredUAV, and UAVSwarm（boundingbox）

  特色：
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

  实验数据集：DAUB， ITSDT-15K, IRDST（boundingbox）.

  个人总结：为了解决有标注数据少和标注耗费大量人力的问题，创建了一种半监督的训练方式，教师网络（少量有标注数据训练过的）和学生网络相互学习。

  特色：
  - Extractor利用了ResNet50的预训练模型。
  - BMP改良了ConvGRU利用时序信息提取运动特征。
  - APF自适应过滤教师网络预测的伪标签，提高标签质量。
  - Pm存储目标特征模板作为“知识库”，通过未标注数据持续更新进化。

### 4、**SeqCSIST: Sequential Closely-Spaced Infrared Small Target Unmixing -2025**  
  论文：https://xplorestaging.ieee.org/document/11080063  
  代码：https://github.com/GrokCV/SeqCSIST
  
  网络图：
  <img width="1158" height="609" alt="image" src="https://github.com/user-attachments/assets/93c5c8a3-0141-45d1-a51f-0fbed518face" />

  实验数据集：SeqCSIST
  
  特色：  
  - 提出了新的检测任务名为sequential CSIST unmixing，目的是解决多目标近距离时发生重叠在成像系统上呈现模糊斑块难以区分的问题，拓展了SIRST任务的定义。  
  - 创建了适配新任务的数据集：SeqCSIST，https://pan.baidu.com/s/1_sxGh5oFQ8-3RpUUeMN2Mg?pwd=kxe9  
  - 提出了适配新任务的检测方法：DeRefNet  

### 5、 **Toward Dense Moving Infrared Small Target Detection: New Datasets and Baseline -2024**  
  论文：[https://xplorestaging.ieee.org/document/11080063](https://ieeexplore.ieee.org/document/10636251)  
  代码：[https://github.com/GrokCV/SeqCSIST](https://github.com/UESTC-nnLab/DMIST)
  
  网络图：
  <img width="1274" height="481" alt="image" src="https://github.com/user-attachments/assets/30d266de-1caf-4cf0-b9d9-d1cef7091bc8" />

  实验数据集：DMIST-60，DMIST-100
  
  特色：  
  - 为了解决密集目标检测的任务，合成了两个密集目标的数据集。  
  - 提出了LASNet来评估两个新数据集。（SST网络改良版）  

### 6、 **A New Motion Feature-Enhanced Multiframe Spatial–Temporal Infrared Target Detection Network -2025**  
  论文：https://ieeexplore.ieee.org/document/11145128  
  代码：https://github.com/lifenghong/MFE-Net  

  MFE-Net网络图：
  <img width="1054" height="552" alt="image" src="https://github.com/user-attachments/assets/1bd517d8-1e31-4115-a6af-b23d46d0c5b6" />

  实验数据集：MIRSat-QL  

  特色：  
  - 旨在解决卫星图象和移动背景下的红外小目标检测，为此合成了新的数据集：MIRSat-QL
  - 在低分辨率特征图中计算光流对齐所有分辨率的特征，抑制背景移动的干扰。
  - 新的深浅特征融合模块AGFF

### 7、 **Enhancing Infrared Small Target Detection: A Saliency-Guided Multi-Task Learning Approach -2025**  
  论文：https://ieeexplore.ieee.org/abstract/document/10844059

  Light-SGMTLM网络图：  
  <img width="1423" height="551" alt="image" src="https://github.com/user-attachments/assets/347f3c92-7a38-43a4-8741-10ce7ebcd4be" />  

  实验数据集： Small-ExtIRShip（来源于GL-Light-NLDF），Small-SSDD（来源于SSDD），IHAST ，IRDST， NUAA-SIRST，IRSTD-1k  

  特色：  
  - 多任务同时学习：目标检测和分割。
  - 注重与深层特征和浅层特征的融合。
  - backbone中的SIWD模块使用1x3和3x1的卷积替代3x3的卷积，保证感受野的同时降低了参数量。
  
### 8、 **Direction-Coded Temporal U-Shape Module for Multiframe Infrared Small Target Detection -2025**  
  论文：https://ieeexplore.ieee.org/document/10321723  
  代码：https://github.com/TinaLRJ/Multi-frame-infrared-small-target-detection-DTUM

  DTUM模块网络图：
  <img width="936" height="303" alt="image" src="https://github.com/user-attachments/assets/73067fc1-20c6-44e9-88b1-452dcef817b6" />

  实验数据集：NUDT-MIRSDT

  特色：  
  - 提出了时序模块DTUM，即插即用。
  - 合成了SNR较低的红外小目标运动数据集：NUDT-MIRSDT

### 9、 **LMAFormer: Local Motion Aware Transformer for Small Moving Infrared Target Detection -2025**  
  论文：https://ieeexplore.ieee.org/document/10758760  
  代码：https://github.com/lifier/LMAFormer  

  LMAFormer网络图：
  <img width="1619" height="787" alt="image" src="https://github.com/user-attachments/assets/eadf83d5-2d23-42d3-96f3-266e77d70d3d" />

  实验数据集：NUDT-MIRSDT, IRDST，TSIRMT  

  特色：  
  - 合成了背景运动的序列数据集：TSIRMT
  - 提出了运动感知特征提取模块（MAFEM）
  - 提出了MJQM 方法，提高对运动背景的建模能力

### 10、 **Infrared Small Target Detection in Satellite Videos:A New Dataset and A Novel Recurrent Feature Refinement Framework -2025**  
  论文：https://arxiv.org/abs/2409.12448  
  代码：https://github.com/XinyiYing/RFR

  RFR网络图：
  <img width="1285" height="449" alt="image" src="https://github.com/user-attachments/assets/d8b39318-8ad3-4505-825e-d9fc6e5b48c2" />

  实验数据集： IRSatVideo-LEO

  特色：
  - 合成了卫星背景的红外运动目标数据集： IRSatVideo-LEO
  - RFR充分利用长期时间依赖性，轻松与单帧方法结合

### 11、 **Infrared Small Target Detection via Multi-Path Deep Conduction -2025**  
  论文：https://ieeexplore.ieee.org/document/11210177

  MPDCNet网络图：
  <img width="1277" height="725" alt="image" src="https://github.com/user-attachments/assets/a5aeb5ff-7592-4b23-b107-c2bbd958d53b" />  

  实验数据集：DSAT，SIATD

  特色：  
  - 三路分支提取特征：空间特征、振幅、相位，之后再融合。
  - 融合和解码过程使用了大量SSM（SS2D），长距离捕捉信息，提取全局特征。

### 12、 **Infrared Small Target Detection Method Based on High–Low-Frequency Semantic Reconstruction -2024**  
  论文：https://ieeexplore.ieee.org/document/10599184  

  HLSR-net网络图：
  <img width="1299" height="537" alt="image" src="https://github.com/user-attachments/assets/885358d1-9015-4632-8053-d8a9295d2736" />

  特色：
  - 在频域分别对高频部分和低频部分通过u型网络进行重建，增强目标特征，抑制背景。

### 13、 **DCSDNet: A Dual-Stream Cooperative Sensing Detection Network for Infrared Small Targets -2026**    
  论文：https://ieeexplore.ieee.org/abstract/document/11224770  

  DCSDNet网络图：
  <img width="1291" height="557" alt="image" src="https://github.com/user-attachments/assets/26efe057-95dd-4c40-91ed-5ca8608cdcbf" />

  实验数据集：VEDAI-IR, NUAA-SIRST, IRSTD-1K

  特色：
  - 密集分组特征学习（DGFL）模块，用于从红外小目标中提取多层次特征。
  - 精炼特征融合瓶颈（RFFB）模块。该模块通过动态关注关键区域，实现了精细化的特征融合
  - 重新思考了现有模型中特征金字塔结构的必要性，并舍弃了这一范式。开发了协同感知主干网络（FHB），以增强特征提取能力，同时减轻特征稀释和错位风险。

### 14、 **DCCS-Det: Directional Context and Cross-Scale-Aware Detector for Infrared Small Target -2026**  
  论文：https://ieeexplore.ieee.org/document/11305185  
  代码：https://github.com/ML202010/DCCS-Det

  DCCS-Det网络图：
  <img width="1054" height="663" alt="image" src="https://github.com/user-attachments/assets/79b27981-cc6e-4a94-b712-e33a188b08c7" />

  实验数据集：
  IRSTD-1K, NUAA-SIRST, SIRST-Aug

  特色：  
  - 双分支提取特征，辅助分支使用DSE Block（内含ss2d）提取上下文信息。
  - LaSEA模块，采用跨尺度特征提取和随机池化采样策略，增强引导解码器信息融合。
  
### 15、 **MDAFNet: Multiscale Differential Edge and Adaptive Frequency Guided Network for Infrared Small Target Detection -2026**  
  论文：https://ieeexplore.ieee.org/document/11303211  
  
  MDAFNet网络图：
  <img width="1299" height="616" alt="image" src="https://github.com/user-attachments/assets/c74f91ad-a903-4235-a72a-832ed159c64a" />

  实验数据集：
  IRSTD-1K, NUAA-SIRST, and SIRST-Aug  

  特色：  
  - MSDE module作为独立的辅助分支，保证了边缘完整性。
  - DAFE module利用双分支减弱高频噪声。

### 16、 **GSFANet: Global Spatial–Frequency Attention Network for Infrared Small Target Detection -2025**  
  论文：https://ieeexplore.ieee.org/document/11133697  
  
  GSFANet网络图：
  <img width="1269" height="650" alt="image" src="https://github.com/user-attachments/assets/7a1ee608-460f-466c-b35d-79615ab1f6db" />

  实验数据集：  
  SIRST, NUDT-SIRST , and IRSTD-1k 

  特色：
  - 基于核函数和门控机制的全局空间–频率注意力机制（HGKA）
  - 参数化小波下采样（PWD）模块
  - 基于频率解耦的自适应特征融合模块（AdaPD）

### （遥感小目标）17、 **Multiscale Gaussian Attention Mechanism for Tiny-Object Detection in Remote Sensing Images -2025**
  论文：Multiscale Gaussian Attention Mechanism for Tiny-Object Detection in Remote Sensing Images  
  代码：https://github.com/cszzshi/MGAM  
  
  网络框架图(ResNet+MGAM)：
  <img width="1094" height="435" alt="image" src="https://github.com/user-attachments/assets/1384dd13-6d6f-4286-8321-0a9fbb402dd5" />

  特色：
  - 即插即用，可置于各个主流模型的stage之后。
  - 在特征提取和注意力机制过程中不使用卷积或线性层。尽管 引入了一些额外的计算，但由于其复杂度低，对 GFLOPs 和模型大小几乎没有影响，只会略微降低模型的训练速度。此外，骨干网络的预训练权重可以直接使用。
  - MFEM来捕捉不同感受野的特征。然后使用GAM计算这些特征的通道和空间注意力。最后根据来自基础模块的原始特征图与注意力特征图之间的差异，为来自不同尺度的注意力特征图分配不同的权重。

### 18、 **ADSUNet: Accumulation-difference-based Siamese U-Net for inter-frame infrared dim and small target detection -2025**
  论文：10.1016/j.patcog.2025.111942  
  代码：https://github.com/zhanglw882/ADSUNet  
  
  ADUSNet网络图：
  <img width="1113" height="885" alt="image" src="https://github.com/user-attachments/assets/1edaf579-0295-4406-b30f-e7e9bd4d314f" />

  特色：
  - 采用了共享权重的孪生网络提取邻近两帧图像的多尺度空域显著性特征。
  - 利用了时序信息：在U型网络的跳连接中设计了累积-差分注意力模块融合邻帧信息，通过帧间空域显著性特征与帧间的差异特征的融合，并对融合后的特征引入了注意力机制，进一步提高了红外小目标帧间时空特征的提取能力；

### 19、 **Infrared dim tiny-sized target detection based on feature fusion -2025**
  论文：https://www.nature.com/articles/s41598-025-88956-8  

  网络图：
  <img width="1246" height="508" alt="image" src="https://github.com/user-attachments/assets/6d6402d3-d0d7-4a09-aec8-1a779a7f6c66" />

  实验数据集：NUDT-SIRST , and IRSTD-1k

  特色：
  -  DODTE模块通过计算相邻各方向的像素差异生成位置信息特征图，以增强后续小目标位置信息。
  -  RBPL模块使用金字塔的形式提取形状信息，最后生成简略检测图（channel=1）.

### 20、 **Infrared Dim Small Target Detection Algorithm Based on Adaptive Attention Transformer Network -2025**
  论文：https://doi.org/10.1007/s12204-025-2823-7

  网络图：
  <img width="1113" height="684" alt="image" src="https://github.com/user-attachments/assets/7df1a560-4374-45da-bef6-6783f699c086" />

  实验数据集：IRSTD-1K, NUAA-SIRST

  特色：
  - 改进注意力机制：使用小型网络判断出哪些点更值得注意，计算注意力时Q和K不变，V会根据之前筛选的点做稀疏化，在保证前提的情况下，降低了计算量。
  - GCA融合模块，对低级特征使用空间非局部全局注意力，对高级特征图使用通道的非局部全局注意力，拼接融合。
