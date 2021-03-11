# Sequence to Sequence(Seq2Seq)

   * [Sequence to Sequence(Seq2Seq)](#sequence-to-sequenceseq2seq)
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
      * [模型信息](#模型信息)

## 简介

Sequence to Sequence (Seq2Seq)，使用编码器-解码器（Encoder-Decoder）结构，用编码器将源序列编码成vector，再用解码器将该vector解码为目标序列。Seq2Seq 广泛应用于机器翻译，自动对话机器人，文档摘要自动生成，图片描述自动生成等任务中。具体可以参考论文：[Sequence to Sequence Learning with Neural Networks](https://arxiv.org/abs/1409.3215)

## 数据集
使用的数据集为：[IWSLT'15 English-Vietnamese data ](https://nlp.stanford.edu/projects/nmt/),数据集中的英语到越南语的数据作为训练语料，tst2012的数据作为开发集，tst2013的数据作为测试集

- 数据集大小：17个类别，1360个32*32大小的图像
  - 训练集：1553条英文与越南语([tst2012.en](https://nlp.stanford.edu/projects/nmt/data/iwslt15.en-vi/tst2012.en)、[tst2012.vi](https://nlp.stanford.edu/projects/nmt/data/iwslt15.en-vi/tst2012.vi))
  - 测试集：1268条英文与越南语([tst2013.en]()、[tst2013.vi](https://nlp.stanford.edu/projects/nmt/data/iwslt15.en-vi/tst2013.vi))
- 数据格式：

## 环境依赖

- 硬件：XPU、GPU、CPU

- 系统：Linux、Windows、MacOS

- 框架：
  - PaddlePaddle >= 2.0.0

## 快速开始
``` bash
# clone this repo
git clone https://github.com/PaddlePaddle/models
cd models/dygraph/seq2seq

# 获取数据
python download.py

# 训练
sh run.sh

# 预测
sh infer.sh
```

## 代码结构与详细说明

### 代码结构

以下是本范例模型的简要目录结构及说明：

```
.
├── README.md              
├── args.py                # 训练、预测以及模型参数配置程序
├── reader.py              # 数据读取程序
├── download.py            # 数据下载程序
├── train.py               # 训练主程序
├── infer.py               # 预测主程序
├── run.sh                 # 训练脚本
├── infer.sh               # 预测脚本
├── attention_model.py     # 带注意力机制的翻译模型程序
└── base_model.py          # 无注意力机制的翻译模型程序
```

### 参数说明

可以在 `run.sh` 中设置训练相关参数，具体如下：

``` text
src_lang: en,                           # 源语言
tar_lang: vi,                           # 目标语言
attention: True,                        # 是否使用注意力机制
num_layers: 2,                          # 网络层数
hidden_size: 512,                       # 隐藏状态大小
src_vocab_size: 17191,                  # 源语言词表大小
tar_vocab_size: 7709,                   # 目标语言词表大小
batch_size: 128,                        # 批大小
dropout: 0.2,                           # 随机失活概率              
use_gpu: True,                          # 是否使用GPU进行训练
model_path: ./attention_models          # 模型存储路径
```

可以在 `infer.sh` 中设置预测相关参数，具体如下：

``` text
src_lang: en,                           # 源语言
tar_lang: vi,                           # 目标语言
attention: True,                        # 是否使用注意力机制
num_layers: 2,                          # 网络层数
hidden_size: 512,                       # 隐藏状态大小
src_vocab_size: 17191,                  # 源语言词表大小
tar_vocab_size: 7709,                   # 目标语言词表大小
batch_size: 128,                        # 批大小
dropout: 0.2,                           # 随机失活概率              
use_gpu: True,                          # 是否使用GPU进行训练
beam_size: 10                           # beam 大小               
```

### 训练流程

#### 使用XPU/GPU/CPU 进行训练
```bash
# step1: 获取数据
python download.py

# step2: 训练, 默认使用带有注意力机制的RNN模型，可以通过修改 --attention 来改变
bash run.sh

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
bash run.sh --mode eval
```

### 测试流程
#### 使用XPU/GPU/CPU 进行测试

```bash
# 预测，默认使用beam search的方法进行预测，加载第10个epoch的模型进行预测
bash infer.sh 
```


## 模型信息

关于模型的其他信息，可以参考下表：

| 信息 | 说明 |
| --- | --- |
| 发布者 | PaddlePaddle |
| 时间 | 2021.03 |
| 框架版本 | Paddle 2.0.1 |
| 支持硬件 | XPU、GPU、CPU |
| BLEU |  10.94  |
| BLEU(with Attention) |  25.24   |
| 下载链接 | [预训练模型]() \| [训练日志]() \| [vdl]() |
| benchmark | [benchmark](https://github.com/PaddlePaddle/benchmark/tree/master/dynamic_graph/seq2seq) |
