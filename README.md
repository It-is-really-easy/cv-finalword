

# Enhanced Frequency-Aware Feature Fusion for Semantic Segmentation

[![GitHub](https://img.shields.io/badge/GitHub-It--is--really--easy.svg)](https://github.com/It-is-really-easy/cv-finalword/blob/main/FreqFusion.py) 


[![Google Drive](https://img.shields.io/badge/Google%20Drive-Download%20Checkpoints-blue.svg)](https://drive.google.com/file/d/1yS2Nu-v0FeLse2ed3PF2aO6pAprYFXfZ/view?usp=drive_link)

## 介绍

语义分割是一项具有挑战性的计算机视觉任务，需要精确的类别级别特征表示和准确的空间边界细节。传统的层次模型利用特征融合技术，将深层的粗糙语义特征与浅层的高分辨率空间特征相结合。然而，这些方法通常未能考虑不同层次特征的独特频率特性，导致性能次优。

为了解决这一问题，我们提出了两种新的特征融合方法：**DWT-FF** 和 **DSConv-FF**，分别利用离散小波变换和深度可分离卷积。**DWT-FF** 将特征分解为频率域信息，产生一个富含频率特征的初始融合结果，从而增强 FreqFusion 中三个模块的输入，使这些模块更好地感知频率域信息。

## 主要贡献

1. **提出 DSConv-FF：** 显著减少了计算复杂度，同时不牺牲特征融合能力，使其适用于实时部署。
2. **提出 DWT-FF：** 加强了频率信息的感知，提供了有效解决类内不一致性和边界偏移问题的方案，提高了分割性能。
3. **展示了 DWT 与注意力机制的协同效应：** 突出了它们在增强边界精度和全局特征表示方面的互补作用。

## 方法论

### 动机与概述

传统的卷积方法在平衡全局上下文信息和边界一致性方面存在困难，尤其是在语义分割任务中。低频的全局结构经常与高频的细节不一致，导致边缘细节保留不佳和预测结果不一致。为了解决这些问题，我们将基于小波的频率分解与 FreqFusion [24] 中的自适应频率感知滤波相结合，提供了一个鲁棒的边缘感知分割框架。

## 实验结果

表 2 显示了 FreqFusion 在不同配置下的实验结果，验证了我们提出的方法在效率和准确性方面的优越性。

| 模型               | mIoU (%) | Params (M) | FLOPs (G) |
|--------------------|----------|------------|-----------|
| SegNeXt + FreqFusion | 43.52     | 4.44        | 7.03       |
| + DWT              | 44.03     | +0.06       | +0.09      |
| + Attention        | 43.75     | +0.00       | +0.01      |
| + DWT + Attention  | 44.12     | +0.06       | +0.10      |

### 分析

DWT 模块通过提供频率感知的分解，显著提升了性能，特别是捕捉边界相关信息，这对于准确的分割至关重要。然而，DWT 单独并不总是能有效捕捉全局上下文，这对于语义分割任务是至关重要的。注意力机制通过选择性地细化空间关系，帮助模型集中于最重要的特征。当两者结合时，DWT 和注意力机制提供了互补的好处：DWT 增强了边界细节的捕捉，而注意力机制则细化了模型对重要区域的关注。

## 代码与模型

- **改进的 FreqFusion 代码：** [FreqFusion.py](https://github.com/It-is-really-easy/cv-finalword/blob/main/FreqFusion.py)
- **模型检查点下载：** [Google Drive](https://drive.google.com/file/d/1yS2Nu-v0FeLse2ed3PF2aO6pAprYFXfZ/view?usp=drive_link)

## 致谢

特别感谢 **Professor Ying Fu** 的深刻指导和 **Linwei Chen** 在项目开发过程中的技术支持。

### 日志
11.27
目前实现了只实现了mmsegementation
目标：
1、首先跑通segnext
2、加上freqfusion这个方法
3、改进，比如多个核或者将多个频率直接连续化处理等等
