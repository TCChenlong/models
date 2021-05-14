# PaddlePaddle Models

[![Documentation Status](https://img.shields.io/badge/docs-latest-brightgreen.svg?style=flat)](https://github.com/PaddlePaddle/models) [![License](https://img.shields.io/badge/license-Apache%202-blue.svg)](LICENSE)

models 由270+个 start-of-the-art 模型组成。这些模型分场景实现在飞桨的各个开发套件中。你可以根据场景和对应的场景下模型的介绍，来快速选择合适的模型。

## PaddleCV

### 图像分类

[图像分类](https://github.com/PaddlePaddle/PaddleClas) 是根据图像的语义信息对不同类别图像进行区分，是计算机视觉中重要的基础问题，是物体检测、图像分割、物体跟踪、行为分析、人脸识别等其他高层视觉任务的基础，在许多领域都有着广泛的应用。如：安防领域的人脸识别和智能视频分析等，交通领域的交通场景识别，互联网领域基于内容的图像检索和相册自动归类，医学领域的图像识别等。


### 目标检测

目标检测任务的目标是给定一张图像或是一个视频帧，让计算机找出其中所有目标的位置，并给出每个目标的具体类别。对于计算机而言，能够“看到”的是图像被编码之后的数字，但很难解图像或是视频帧中出现了人或是物体这样的高层语义概念，也就更加难以定位目标出现在图像中哪个区域。目标检测模型请参考 [PaddleDetection](https://github.com/PaddlePaddle/PaddleDetection)。

### 图像分割

图像语义分割顾名思义是将图像像素按照表达的语义含义的不同进行分组/分割，图像语义是指对图像内容的理解，例如，能够描绘出什么物体在哪里做了什么事情等，分割是指对图片中的每个像素点进行标注，标注属于哪一类别。近年来用在无人车驾驶技术中分割街景来避让行人和车辆、医疗影像分析中辅助诊断等。
图像语义分割模型请参考语义分割库[PaddleSeg](https://github.com/PaddlePaddle/PaddleSeg)


### 图像生成

图像生成是指根据输入向量，生成目标图像。这里的输入向量可以是随机的噪声或用户指定的条件向量。具体的应用场景有：手写体生成、人脸合成、风格迁移、图像修复等。[PaddleGAN](https://github.com/PaddlePaddle/PaddleGAN) 包含和图像生成相关的多个模型。

### 文字识别

文字识别是在图像背景复杂、分辨率低下、字体多样、分布随意等情况下，将图像信息转化为文字序列的过程，可认为是一种特别的翻译过程：将图像输入翻译为自然语言输出。[PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) 旨在打造一套丰富、领先、且实用的OCR工具库，助力使用者训练出更好的模型，并应用落地。


### 视频

[PaddleVideo](https://github.com/PaddlePaddle/PaddleVideo)面开源了视频分类、动作定位 和 目标跟踪等视频任务的领先实用算法。视频数据包含语音、图像等多种信息，因此理解视频任务不仅需要处理语音和图像，还需要提取视频帧时间序列中的上下文信息。


## PaddleNLP

[**PaddleNLP**](https://github.com/PaddlePaddle/PaddleNLP) 是基于 PaddlePaddle 深度学习框架开发的自然语言处理 (NLP) 工具，算法，模型和数据的开源项目。百度在 NLP 领域十几年的深厚积淀为 PaddleNLP 提供了强大的核心动力。使用 PaddleNLP，您可以得到：


## PaddleRec

个性化推荐，在当前的互联网服务中正在发挥越来越大的作用，目前大部分电子商务系统、社交网络，广告推荐，搜索引擎，都不同程度的使用了各种形式的个性化推荐技术，帮助用户快速找到他们想要的信息。[PaddleRec](https://github.com/PaddlePaddle/models/tree/develop/PaddleRec) 包含的模型如下。


## License
This tutorial is contributed by [PaddlePaddle](https://github.com/PaddlePaddle/Paddle) and licensed under the [Apache-2.0 license](LICENSE).


## 许可证书
此向导由[PaddlePaddle](https://github.com/PaddlePaddle/Paddle)贡献，受[Apache-2.0 license](LICENSE)许可认证。
