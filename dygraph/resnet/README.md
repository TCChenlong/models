# ResNet

   * [ResNet](#resnet)
      * [简介](#简介)
      * [数据集](#数据集)
      * [环境依赖](#环境依赖)
      * [快速开始](#快速开始)
      * [代码结构与详细说明](#代码结构与详细说明)
         * [代码结构](#代码结构)
         * [参数说明](#参数说明)
         * [训练流程](#训练流程)
            * [使用XPU/GPU/CPU 进行训练](#使用xpugpucpu-进行训练)
            * [训练输出](#训练输出)
         * [评估流程](#评估流程)
            * [使用XPU/GPU/CPU 进行评估](#使用xpugpucpu-进行评估)
         * [测试流程](#测试流程)
            * [使用XPU/GPU/CPU 进行测试](#使用xpugpucpu-进行测试)
         * [使用预训练模型预测](#使用预训练模型预测)
      * [模型信息](#模型信息)

## 简介

![Image text](./images/resnet.png)

Resnet(Residual Neural Network) 由微软研究院的Kaiming He等四名华人提出，通过使用ResNet Unit成功训练出了152层的神经网络，并在ILSVRC2015比赛中取得冠军，在top5上的错误率为3.57%，同时参数量比VGGNet低，效果非常突出。具体内容可以参考原论文：[Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385)

## 数据集

使用的数据集为：[Flowers](https://www.robots.ox.ac.uk/~vgg/data/flowers/)。

- 数据集大小：17个类别，1360个32*32大小的图像
  - 训练集：1088个图像
  - 测试集：272个图像
- 数据格式：使用飞桨框架内置Flowers数据集，默认格式为numpy.array，更多信息请参考[paddle.vision.datasets.Flowers](https://www.paddlepaddle.org.cn/documentation/docs/zh/api/paddle/vision/datasets/flowers/Flowers_cn.html)

## 环境依赖

- 硬件：XPU、GPU、CPU

- 系统：Linux、Windows、MacOS

- 框架：
  - PaddlePaddle >= 2.0.0

## 快速开始
``` bash
# clone this repo
git clone https://github.com/PaddlePaddle/models
cd models/dygraph/resnet

# 训练
python train.py

# 测试
python train.py --mode test

# 使用预训练模型预测
python train.py --pretrained_model ./pretrained_model/resnet_model
```

## 代码结构与详细说明

### 代码结构

```
|—— README.md
|—— reader.py    # 数据加载
|── run.sh       # 训练、测试脚本
|── train.py     # 训练、测试网络
```

### 参数说明

可以在 `train.py` 中设置训练与评估相关参数，具体如下：

``` text
"use_data_parallel": False,          # 是否使用数据并行训练模型
"e": 120,                            #训练epoch次数
"b": 32,                             #训练 batch_size 大小
```

### 训练流程

#### 使用XPU/GPU/CPU 进行训练
```bash
# 单机训练
python train.py

# 多机训练
python -m paddle.distributed.launch --selected_gpus=0,1,2,3  --log_dir ./mylog train.py   --use_data_parallel 1
```
此时，程序会将每个进程的输出log导入到`./mylog`路径下：
```
.
├── mylog
│   ├── workerlog.0
│   ├── workerlog.1
│   ├── workerlog.2
│   └── workerlog.3
├── README.md
└── train.py
```

#### 训练输出
执行训练开始后，将得到类似如下的输出。每一轮`batch`训练将会打印当前epoch、step以及loss值。当前默认执行`epoch=10`, `batch_size=8`。你可以调整参数以得到更好的训练效果，同时也意味着消耗更多的内存（显存）以及需要花费更长的时间。
```text
epoch id: 0, batch step: 0, loss: 4.951202
epoch id: 0, batch step: 1, loss: 5.268410
epoch id: 0, batch step: 2, loss: 5.123999
```
**注意：** 全部的训练日志请参考下表中的日志。

### 评估流程

#### 使用XPU/GPU/CPU 进行评估

```bash
python train.py --mode eval
```

### 测试流程
#### 使用XPU/GPU/CPU 进行测试

```bash
python train.py --mode test
```

### 使用预训练模型预测

使用预训练模型预测的流程如下：

```bash

# step1: 下载预训练模型到指定文件夹
mkdir pretrained_model
cd pretrained_model
wget https://bj.bcebos.com/paddleseg/dygraph/cityscapes/bisenet_cityscapes_1024x1024_160k/model.pdparams

# step2: 使用预训练模型完成预测
python train.py --pretrained_model ./pretrained_model/resnet_model
```
## 模型信息

关于模型的其他信息，可以参考下表：

| 信息 | 说明 |
| --- | --- |
| 发布者 | PaddlePaddle |
| 时间 | 2021.03 |
| 框架版本 | Paddle 2.0.1 |
| 支持硬件 | XPU、GPU、CPU |
| TOP-1 Error |  22.44  |
| TOP-5 Error |  6.21   |
| 下载链接 | [预训练模型]() \| [训练日志]() \| [vdl]() |
