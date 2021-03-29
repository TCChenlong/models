# ResNet

[English](./README.md) | 简体中文
   
   * [ResNet](#resnet)
      * [一、简介](#一简介)
      * [二、数据集](#二数据集)
      * [三、环境依赖](#三环境依赖)
      * [四、快速开始](#四快速开始)
         * [step1: clone](#step1-clone)
         * [step2: 训练](#step2-训练)
         * [step3: 测试](#step3-测试)
         * [使用预训练模型预测](#使用预训练模型预测)
      * [五、代码结构与详细说明](#五代码结构与详细说明)
         * [5.1 代码结构](#51-代码结构)
         * [5.2 参数说明](#52-参数说明)
         * [5.3 训练流程](#53-训练流程)
            * [单机训练](#单机训练)
            * [多机训练](#多机训练)
            * [训练输出](#训练输出)
         * [5.4 评估流程](#54-评估流程)
         * [5.5 测试流程](#55-测试流程)
         * [5.6 使用预训练模型预测](#56-使用预训练模型预测)
      * [六、模型信息](#六模型信息)
      * [七、二次开发](#七二次开发)

## 一、简介

![Image text](./images/resnet.png)

Resnet(Residual Neural Network) 由微软研究院的Kaiming He等四名华人提出，通过使用ResNet Unit成功训练出了152层的神经网络，并在ILSVRC2015比赛中取得冠军，在top5上的错误率为3.57%，同时参数量比VGGNet低，效果非常突出。

**论文:**[Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385)

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

### step1: clone 

``` bash
# clone this repo
git clone https://github.com/PaddlePaddle/models
cd models/dygraph/resnet
```

### step2: 训练
``` bash
# 训练
python train.py
```

此时的输出为：
```
epoch 0 | batch step 0, loss 4.801 acc1 0.000 acc5 0.031, batch cost: 0.20029
epoch 0 | batch step 10, loss 12.695 acc1 0.017 acc5 0.102, batch cost: 0.07268
epoch 0 | batch step 20, loss 9.905 acc1 0.015 acc5 0.089, batch cost: 0.07277
```
由于是分类任务，需要关注 ``loss`` 逐渐降低，``acc1、acc5`` (TOP1准确率，TOP5准确率)逐渐升高。

### step3: 测试
```bash
# 测试
python train.py --mode test --test_image test_image.jpg
```
此时的输出为：
```
the image is buttercup！
```

### 使用预训练模型预测
```bash
# 使用预训练模型预测
python train.py --pretrained_model ./pretrained_model/resnet_model --test_image test_image.jpg
```

此时的输出为：
```
the image is buttercup！
```

## 五、代码结构与详细说明

### 5.1 代码结构

```
|—— README.md
|—— README_en.md
|—— reader.py    # 数据加载
|── run.sh       # 训练、测试脚本
|── train.py     # 训练、测试网络
```

### 5.2 参数说明

可以在 `train.py` 中设置训练与评估相关参数，具体如下：

|  参数   | 默认值  | 说明 | 其他 |
|  ----  |  ----  |  ----  |  ----  |
| use_data_parallel  | False, 可选 | 是否使用数据并行训练模型 ||
| epoch  | 120, 可选 | epoch次数 ||
| batch_size  | 32, 可选 | batch_size 大小 ||
| max_iter | 0, 可选 | 最大迭代次数 | 仅在benchmark时使用 |
| class_dim | 102, 可选 | 花朵数据集的类别数 ||
| use_imagenet_data | False(如果添加该参数即为True), 可选 | 是否使用 IMAGENET数据集 ||
| data_dir | "./data/ILSVRC2012", 可选 | IMAGENET数据集地址 ||
| lower_scale | 0.08, 可选 | ramdom_crop 中 lower_scale 的值 ||
| lower_ratio | 3. / 4., 可选 | ramdom_crop 中 lower_ratio 的值 ||
| upper_ratio | 4. / 3., 可选 | ramdom_crop 中 upper_ratio 的值 ||
| resize_short_size | 256, 可选 | 将图片重新设置大小后较短边的边长 ||
| crop_size | 224, 可选 | crop_size 的大小 ||
| use_mixup | False, 可选 | 是否使用mixup ||
| mixup_alpha | 0.2, 可选 | mixup_alpha 大小 ||
| reader_thread | 8, 可选 | 多线程读取数据的数量 ||
| reader_buf_size | 16, 可选 | 多线程读取数据的缓冲大小 ||
| interpolation | None, 可选 | 插值模式 ||
| use_aa | False, 可选 | 是否使用 auto argument ||
| image_mean | [0.485, 0.456, 0.406], 可选 | 图像均值 ||
| image_std | [0.229, 0.224, 0.225], 可选 | 图像标准差 ||
| use_gpu | True, 可选 | 是否使用GPU环境 ||

### 5.3 训练流程

#### 单机训练
```bash
python train.py
```

#### 多机训练
```bash
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
**注意：** 全部的训练日志请参考下表中的[日志]()。

### 5.4 评估流程

```bash
python train.py --mode eval
```

此时的输出为：
```
batch step 0, loss 4.801 acc1 0.000 acc5 0.031, batch cost: 0.20029
batch step 10, loss 12.695 acc1 0.017 acc5 0.102, batch cost: 0.07268
batch step 20, loss 9.905 acc1 0.015 acc5 0.089, batch cost: 0.07277
```

### 5.5 测试流程

```bash
python train.py --mode test --test_image test_image.jpg
```

此时的输出为：
```
the image is buttercup！
```

### 5.6 使用预训练模型预测

使用预训练模型预测的流程如下：

**step1:** 下载预训练模型

```bash
mkdir pretrained_model
cd pretrained_model
wget https://bj.bcebos.com/paddleseg/dygraph/cityscapes/bisenet_cityscapes_1024x1024_160k/model.pdparams
```

**step2:** 使用预训练模型完成预测
```bash
python train.py --pretrained_model ./pretrained_model/resnet_model --test_image test_image.jpg
```
此时的输出为：
```
the image is buttercup！
```
## 六、模型信息

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
| 模型源代码 | [ResNet](https://github.com/TCChenlong/models/blob/update_readme/dygraph/resnet/train.py#L270) |
| 在线运行 | [使用ResNet50实现图像分类]() |

## 七、二次开发

如果想要基于此模型进行二次开发，可以参考这篇文档: [使用模型库中的模型进行二次开发]()。
