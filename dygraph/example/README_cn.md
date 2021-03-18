# ResNet

[English](./README.md) | 简体中文

   * [ResNet](#resnet)
      * [一、简介](#一简介)
      * [二、数据集](#二数据集)
      * [三、环境依赖](#三环境依赖)
      * [四、快速开始](#四快速开始)
      * [五、模型信息](#五模型信息)
      * [六、二次开发](#六二次开发)

## 一、简介

![Image text](./images/resnet.png)

Resnet(Residual Neural Network) 由微软研究院的Kaiming He等四名华人提出，通过使用ResNet Unit成功训练出了152层的神经网络，并在ILSVRC2015比赛中取得冠军，在top5上的错误率为3.57%，同时参数量比VGGNet低，效果非常突出。

**论文:** [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385)

## 二、数据集

使用的数据集为：[Flowers](https://www.robots.ox.ac.uk/~vgg/data/flowers/)。

- 数据集大小：102个类别，8189张32*32大小的图像
  - 训练集：1020个图像
  - 验证集：1020个图像
  - 测试集：6149个图像
- 数据格式：使用飞桨框架内置Flowers数据集，默认格式为numpy.array，更多信息请参考[paddle.vision.datasets.Flowers](https://www.paddlepaddle.org.cn/documentation/docs/zh/api/paddle/vision/datasets/flowers/Flowers_cn.html)

## 三、环境依赖

- 硬件：XPU、GPU、CPU

- 框架：
  - PaddlePaddle >= 2.0.0

## 四、快速开始

本模型的实现存放于 [PaddleDetection](https://github.com/PaddlePaddle/PaddleDetection)中，快速开始请参考[快速开始](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.0-rc/docs/tutorials/QUICK_STARTED_cn.md),模型源文件地址为 [resnet.py](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.0-rc/ppdet/modeling/backbones/resnet.py#L39)。

## 五、模型信息

关于模型的其他信息，可以参考下表：

| 信息 | 说明 |
| --- | --- |
| 发布者 | PaddlePaddle |
| 时间 | 2021.03 |
| 框架版本 | Paddle 2.0.1 |
| 应用场景 | 图像分类 | 
| 支持硬件 | XPU、GPU、CPU |
| TOP-1 Error |  22.44  |
| TOP-5 Error |  6.21   |
| 下载链接 | [预训练模型]() \| [训练日志]() \| [vdl]() |
| benchmark | [benchmark](https://github.com/PaddlePaddle/benchmark/tree/master/dynamic_graph/resnet/paddle) |
| 混合精度训练 | [resnet(amp)]() |
| 模型源代码 | [ResNet](https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.0-rc/ppdet/modeling/backbones/resnet.py#L39) |
| 在线运行 | [使用ResNet50实现图像分类]() | 

## 六、二次开发

如果想要基于此模型进行二次开发，可以参考这篇文档: [如何进行二次开发]() .
