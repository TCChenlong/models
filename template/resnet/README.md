# ResNet

English | [简体中文](./README_cn.md)
   
  * [ResNet](#resnet)
      * [1 Introduction](#1-introduction)
      * [2 Dataset](#2-dataset)
      * [3 Environment](#3-environment)
      * [4 Quick Start](#4-quick-start)
         * [Step1: Clone](#step1-clone)
         * [Step2: Training](#step2-training)
         * [Step3: Test](#step3-test)
         * [Use Pre-trained Models to Infer](#use-pre-trained-models-to-infer)
      * [5 Code Structure and Explanation](#5-code-structure-and-explanation)
         * [5.1 Code Structure](#51-code-structure)
         * [5.2 Parameter Explanation](#52-parameter-explanation)
         * [5.3 Training Process](#53-training-process)
            * [One GPU Training](#one-gpu-training)
            * [Multiple GPUs Training](#multiple-gpus-training)
            * [Outputs](#outputs)
         * [5.4 Evaluation Process](#54-evaluation-process)
         * [5.5 Test Process](#55-test-process)
         * [5.6 Use Pre-trained Models to Infer](#56-use-pre-trained-models-to-infer)
      * [6 Model Information](#6-model-information)
      * [7 Customization](#7-customization)

## 1 Introduction

![Image text](./images/resnet.png)

ResNet (Residual Neural Network) was come up with by four Chinese people from Microsoft Research, including Kaiming He. They evaluated residual nets with a depth of up to 152 layers through ResNet Unit, and carried out the first prize in ILSVRC2015. On the ImageNet test set, their ensemble had 3.57% top-5 error, and had lower complexity than VGGNet. This model is highly efficient. 

**Paper:** [Deep Residual Learning for Image Recognition](https://arxiv.org/abs/1512.03385).

## 2 Dataset

The dataset is [Flowers](https://www.robots.ox.ac.uk/~vgg/data/flowers/).

- The size of dataset: There are 102 categories, and 8189 images are of 32*32 pixels in width and height
  - Training set: 1020 images
  - Validation set: 1020 images
  - Test set: 6149 images
- The format of data: When you apply the PaddlePaddle’s API [Flowers](https://www.robots.ox.ac.uk/~vgg/data/flowers/), the default format is ``numpy.array``. For more details, please refer to [paddle.vision.datasets.Flowers](https://www.paddlepaddle.org.cn/documentation/docs/zh/api/paddle/vision/datasets/flowers/Flowers_cn.html).

## 3 Environment

- Hardwares: XPU, GPU, CPU
- Framework: 
  - PaddlePaddle >= 2.0.0

## 4 Quick Start

### Step1: Clone 

``` bash
# Clone this repo
git clone https://github.com/PaddlePaddle/models
cd models/dygraph/resnet
```

### Step2: Training
``` bash
# Training
python train.py
```

The output is: 
```
epoch 0 | batch step 0, loss 4.801 acc1 0.000 acc5 0.031, batch cost: 0.20029
epoch 0 | batch step 10, loss 12.695 acc1 0.017 acc5 0.102, batch cost: 0.07268
epoch 0 | batch step 20, loss 9.905 acc1 0.015 acc5 0.089, batch cost: 0.07277
```
This is the classification task. You need to notice that `` loss``  value will gradually decreases, and ``acc1`` (top-1 accuracy) and `` acc5``  (top-5 accuracy) will increase.

### Step3: Test
```bash
# Test
python train.py --mode test --test_image test_image.jpg
```
The output is: 
```
the image is buttercup！
```

### Use Pre-trained Models to Infer
```bash
# Use Pre-trained Models to Infer
python train.py --pretrained_model ./pretrained_model/resnet_model --test_image test_image.jpg
```

The output is:
```
the image is buttercup！
```

## 5 Code Structure and Explanation

### 5.1 Code Structure

```
|—— README.md
|—— README_en.md
|—— reader.py    # Data loading
|── run.sh       # Training and test scripts
|── train.py     # Training and test nets
```

### 5.2 Parameter Explanation

You can set training and evaluation parameters in `train.py`. And relative information is as following:

|  Parameter Name  | Default Value | Description | Others |
|  ----  |  ----  |  ----  |  ----  |
| use_data_parallel  | False, optional | Whether data is used to train models in a parallel manner or not ||
| epoch  | 120, optional | The number of epoch ||
| batch_size  | 32, optional | The value of `batch_size` ||
| max_iter | 0, optional | The maximum number of iteration | `max_iter` is only applied when benchmark is used |
| class_dim | 102, optional | The number of [Flowers](https://www.robots.ox.ac.uk/~vgg/data/flowers/)’ categories ||
| use_imagenet_data | False(the action set to store_true will store the argument as True, if present), optional | Whether IMAGENET is used or not ||
| data_dir | "./data/ILSVRC2012", optional | The address of IMAGENET ||
| lower_scale | 0.08, optional | The value of `lower_scale` in `ramdow_crop` ||
| lower_ratio | 3. / 4., optional | The value of `lower_ratio` in `ramdom_crop` ||
| upper_ratio | 4. / 3., optional | The value of `upper_ratio` in `ramdom_crop` ||
| resize_short_size | 256, optional | The shorter side’s length of a resized photo ||
| crop_size | 224, optional | The value of `crop_size` ||
| use_mixup | False, optional | Whether mixup is used or not ||
| mixup_alpha | 0.2, optional | The value of `mixup_alpha` ||
| reader_thread | 8, optional | The data size read by threading ||
| reader_buf_size | 16, optional | The buffer size read by threading ||
| interpolation | None, optional | Interpolation mode ||
| use_aa | False, optional | Whether auto argument is used or not ||
| image_mean | [0.485, 0.456, 0.406], optional | Image mean ||
| image_std | [0.229, 0.224, 0.225], optional | Image standard deviation ||
| use_gpu | True, optional | Whether GPU is used or not ||

### 5.3 Training Process

#### One GPU Training
```bash
python train.py
```

#### Multiple GPUs Training
```bash
python -m paddle.distributed.launch --selected_gpus=0,1,2,3  --log_dir ./mylog train.py   --use_data_parallel 1
```

Now, the program will import output logs of each procedure into `./mylog`.

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

#### Outputs
When the training starts, the output will be as following. Each `batch` of training will print values of current epoch, step and loss. The default execution is `epoch=10`, `batch_size=8`. Of course, you can tune parameters to reach better training results. But this also means more memories and time.

```text
epoch id: 0, batch step: 0, loss: 4.951202
epoch id: 0, batch step: 1, loss: 5.268410
epoch id: 0, batch step: 2, loss: 5.123999
```
Note: Please refer to [log]() in the following list to check all training logs.

### 5.4 Evaluation Process

```bash
python train.py --mode eval
```

The output is:
```
batch step 0, loss 4.801 acc1 0.000 acc5 0.031, batch cost: 0.20029
batch step 10, loss 12.695 acc1 0.017 acc5 0.102, batch cost: 0.07268
batch step 20, loss 9.905 acc1 0.015 acc5 0.089, batch cost: 0.07277
```

### 5.5 Test Process

```bash
python train.py --mode test --test_image test_image.jpg
```

The output is: 
```
the image is buttercup！
```

### 5.6 Use Pre-trained Models to Infer

The procedure of using pre-trained models to infer is as following: 

**Step1:** Download the pre-trained models

```bash
mkdir pretrained_model
cd pretrained_model
wget https://bj.bcebos.com/paddleseg/dygraph/cityscapes/bisenet_cityscapes_1024x1024_160k/model.pdparams
```

**Step2:** Use pre-trained models to infer

```bash
python train.py --pretrained_model ./pretrained_model/resnet_model --test_image test_image.jpg
```
The output is:
```
the image is buttercup！
```
## 6 Model Information

Please refer to the following list to check other models’ information:

| Information Name | Description |
| :-- | --- |
| Announcer | PaddlePaddle |
| Time | 2021.03 |
| Framework Version | Paddle 2.0.1 |
| Application Scenario | Image Classification |
| Supported Hardwares | XPU, GPU, CPU |
| TOP-1 Error |  22.44  |
| TOP-5 Error |  6.21   |
| Download Links | [Pre-trained Models]() \| [Training Log]() \| [vdl]() |
| Benchmark | [benchmark](https://github.com/PaddlePaddle/benchmark/tree/master/dynamic_graph/resnet/paddle) |
| Mixed-precision Training | [resnet(amp)]() |
| Source Code of ResNet | [ResNet](https://github.com/TCChenlong/models/blob/update_readme/dygraph/resnet/train.py#L270) |
| Online Running | [Use ResNet50 to Realize Image Classification]() |

## 7 Customization

Please refer to [the passage](#) to customize the models.