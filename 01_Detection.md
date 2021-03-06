# Detection
## NMS系列去重算法

2017----Soft-NMS----Improving Object Detection With One Line of Code

2018----Softer-NMS- Rethinking Bounding Box Regression for Accurate Object Detection

2018----IoUNet----Acquisition of Localization Confidence for Accurate Object Detection

2018----CVPR----Improving Object Localization with Fitness NMS and Bounded IoU Loss

2018----NIPS----Sequential Context Encoding for Duplicate Removal

M2Det: A Single-Shot Object Detector based on Multi-Level Feature Pyramid Network [PDF](https://arxiv.org/pdf/1811.04533.pdf) [Github](https://github.com/qijiezhao/M2Det)

Grid R-CNN [PDF](https://arxiv.org/pdf/1811.12030.pdf)

## 人脸检测

1、天津大学、武汉大学、腾讯AI实验室提出的人脸检测模型，主要针对移动端设计（backbone MobileNet v2）
在高通845上达到140fps的实时性。论文主要提出一个解决类别不均衡问题（侧脸、正脸、抬头、低头、表情、遮挡等各种类型）：
增加困难类别和样本的损失函数权重。

但是MobileNet v2的检测框架应该没有这么快，并且论文的预测特征点和3D旋转角时，使用全连接网络，计算量大，
应该更耗时才对。论文只给出特征点预测，但是一张图片N个人，如何区分特征点属于何人？论文没有告知如何计算检测框。
论文应该很多细节没有讲述清晰，应该是idea分拆，写成连续剧的节奏。

PFLD:A Practical Facial Landmark Detector.[pdf](https://arxiv.org/pdf/1902.10859.pdf)

## object Detection

1、国防科技大学和旷视科技联合提出，典型的RPN+FPN架构，backbone基于SNet,增加Context Enhancement
Module(FPN多尺度分辨率特征融合)和spatial attention module（RPN->1x1卷积实现空间注意力模型），
实验结果相对于MobileNetV2-SSDLite速度和精度均有提高。

ThunderNet: Towards Real-time Generic Object Detection.[PDF](https://arxiv.org/pdf/1903.11752.pdf)

2、CVPR2019论文、商汤，浙江大学等联合提出的Libra R-CNN。motivation来自于作者认为的三个不平衡：数据不平衡，特征不平衡，
损失函数不平衡。数据不平衡采用：N总样本根据IoU分成K个子样本,增加困难样本的采样概率。特征不平衡采用：ResNet Identity 和
non-local模块修正语义特征。损失函数不平衡：论文设计Balanced L1 Loss（**待验证和理解**）。

论文提出的三个不平衡，可以认为是3个trick，可以集成到其他模型，改进检测的精度。

Libra R-CNN: Towards Balanced Learning for Object Detection.[pdf](https://arxiv.org/pdf/1904.02701.pdf)

3.阿德莱德大学沈春华项目组提出的目标检测方向新论文FCOS,去除传统目标检测的FPN操作,添加Center-ness分支，直接anchor free预测
(l; t; r; b) 四维向量（节省anchor相关的超参数设定以及计算），依赖于NMS，直接生成目标检测框。论文提出的FCOS希望可以应用于
后续的语义分割，姿态估计等领域。论文的性能在one-stage领域state-of-art，节省大量FPN的计算，但是没有任何关于速度的指标，比较遗憾。

FCOS: Fully Convolutional One-Stage Object Detection.[pdf](https://arxiv.org/pdf/1904.01355.pdf)
## other

2、商汤和香港中文大学联合提出，ICLR2019论文，实在没看懂啥意思。

Feature Intertwiner for Object Detection. [PDF](https://arxiv.org/pdf/1903.11851.pdf)


# tricks

1.backbone与特征提取

目标检测的backbone一般基于ImageNet预训练的图像分类网络。图像分类问题只关注分类和感受视野，不用关注物体定位，
但是目标检测领域同时很关注空间信息。如果下采样过多，会导致最后的feature map很小，小目标很容易漏掉。很多基础架构网络，
比如ResNet、Xception、DenseNet、FPN、DetNet、R-CNN，PANet、等神经网络提取图像的上下文信息，不断在特征提取方向优化。

2.基于Anchor生成的算法

比如Sliding window、Region Proposal Network (RPN) 、CornerNet、meta-anchor等。

3.IoU计算

UnitBox，IoU-Net，GIoU

4.损失函数

包括L1和L2，Focal loss，增加困难类别和样本的损失函数权重

5.优化NMS

包括Soft-NMS,Softer-NMS,以及Relation Netwrok，ConvNMS，NMS Network，Yes-Net等。

6.通用tricks

类别不平衡（增加样本）,数据增强

# 待记录

Adaptive NMS: Refining Pedestrian Detection in a Crowd.[pdf](https://arxiv.org/pdf/1904.03629.pdf)


