# 红外小目标检测方法

本仓库旨在收集、整理并维护与红外小目标检测（IRST）相关的方法、论文与代码实现。后续会将相关文章逐篇添加到下面的列表中，便于学习与对比。

## 已收录方法
- **One Shot is Enough for Sequential Infrared Small Target Segmentation -2025**  
  代码：[https://github.com/D-IceIce/one-shot-IRSTS](https://github.com/D-IceIce/one-shot-IRSTS)  

  整体网络图：
  <img width="1652" height="373" alt="image" src="https://github.com/user-attachments/assets/06c812a4-f559-4ed2-bd2f-c8681853ddc1" />

  测试数据集：sequential IRSTS  

  概述：使用提示图片（已知mask）提取红外小目标在经过SAM Encoder的特征，使用该特征匹配目标图片的特征，找到目标所在位置的中心点。将该中心点作为提示投入SAM输出分割结果。

  特点：
   - 不需要单独训练，使用SAM的训练模型。
   - 输入是带有已知mask的提示图片和目标图片

- 十大
