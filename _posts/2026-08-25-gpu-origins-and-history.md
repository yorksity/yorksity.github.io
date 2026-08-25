---
layout: post
title: "GPU的起源与历史演进"
date: 2026-08-25 00:00:00 +0800
tags: [GPU, 计算机历史, 硬件]
---

GPU（图形处理器）早已不只是用来打游戏的硬件。从1990年代诞生至今，它经历了从固定功能管线到通用并行计算引擎的深刻转变，深刻影响了深度学习、科学计算等领域。

## 前GPU时代：2D加速与早期3D

1980年代，PC的图形输出完全依赖CPU。IBM PC的CGA、EGA、VGA只是简单的帧缓冲控制器，没有任何图形加速能力。

1990年代初，真正的2D加速卡出现，如S3 Graphics的86C911。它能处理BitBlt、画线、填充等操作，将部分绘制工作从CPU中解放出来。但真正的转折点在于3D游戏的兴起。

## 第一代GPU：3D加速卡（1994–1999）

1994年，3dfx推出了 **Voodoo Graphics**，这是第一款真正意义上的3D加速芯片。它只处理3D渲染，需要配合一块2D显卡使用。Voodoo的出现让《雷神之锤》（Quake）等游戏焕然一新，消费级3D图形的大门就此打开。

1999年，NVIDIA发布了 **GeForce 256**，并将其定义为"世界上第一个GPU"。它首次在单芯片上集成了硬件T&L（Transform & Lighting，即变换与光照），将顶点计算从CPU转移到了GPU，是图形管线硬件化的关键一步。

## 可编程着色器时代（2000–2006）

2001年，NVIDIA GeForce 3和ATI Radeon 8500引入了可编程的顶点着色器和像素着色器。开发者不再受限于固定的光照模型，可以编写自定义着色程序，实现更丰富的视觉效果。

2002年，Cg/HLSL、GLSL等高级着色语言相继出现，使得GPU编程变得更加友好。DirectX 9（2002年）和Shader Model 3.0（2004年）进一步推动了可编程管线的普及，统一的浮点精度和动态分支能力让GPU开始具备类CPU的计算特征。

## GPGPU的诞生：GPU不再只是图形卡（2006–2012）

2006年，NVIDIA发布了 **CUDA**（Compute Unified Device Architecture），使得GPU可以用于通用计算。CUDA摒弃了图形API的束缚，以C语言扩展的形式直接暴露GPU的并行计算能力。流体模拟、金融建模、分子动力学等领域的计算密集型任务开始向GPU迁移。

2008年，Apple提出OpenCL规范，由Khronos Group维护，成为跨平台、跨厂商的异构计算标准。AMD、Intel、ARM等厂商纷纷加入支持。

2010年，NVIDIA Fermi架构大幅强化了双精度浮点和ECC内存，标志着GPU正式进入高性能计算（HPC）领域。同年，吴恩达团队首次使用GPU训练大规模深度神经网络，开启了深度学习时代的序幕。

## 深度学习专用GPU（2012–2020）

2012年，AlexNet在ImageNet竞赛中夺冠，使用两块GTX 580 GPU进行训练。这一事件被视为深度学习革命的起点之一。此后，GPU成为训练神经网络的标准硬件。

NVIDIA迅速响应，在后续架构中引入了专用的Tensor Core（Volta，2017年），支持混合精度矩阵乘法，极大提升了深度学习训练和推理的性能。A100（Ampere，2020年）进一步引入了结构化稀疏和MIG（多实例GPU）技术，面向数据中心和云原生场景。

## 现代GPU架构与未来趋势

当前GPU已高度分化：

- **消费级GPU**（NVIDIA GeForce RTX、AMD Radeon RX）：支持实时光线追踪、DLSS超分辨率等
- **数据中心GPU**（NVIDIA H100/B200、AMD Instinct MI300X）：面向训练和推理，强调高带宽内存（HBM）、多GPU互联（NVLink/Infinity Fabric）
- **移动端GPU**（Apple Silicon GPU、Qualcomm Adreno、ARM Mali）：在功耗限制下追求能效比，支持Metal、Vulkan等现代API

未来趋势包括：芯粒（Chiplet）设计、光互连、近存计算、以及AI与图形的深度融合。

## 结语

从3dfx Voodoo到NVIDIA H100，GPU的演进史是一部算力持续爆炸的历史。理解它的过去，有助于我们把握计算架构的发展方向。如今，GPU已经超越图形，成为现代计算的基石。