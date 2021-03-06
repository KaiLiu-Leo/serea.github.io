---
title: "生成对抗网络分解———GAN dissection: visualizing and understanding generative adversarial networks"
image: 
  path: /images/recipes/GAN/image1.jpeg
  thumbnail: images/recipes/GAN/image1.jpeg
  caption: "理解生成对抗网络"
categories:
  - GAN
  - Deep Learning
---

## 生成对抗网络分解：可视化和理解生成对抗网络

原文链接[GAN dissection: visualizing and understanding generative adversarial networks](https://arxiv.org/abs/1811.10597) Bau et al., *arXiv’18*

早些时候我们查看了使用可视化帮助理解和解释RNN网络，今天选择的这篇论文给我们个选择看看GAN中到底发生了什么。除了这篇论文，代码在[GitHub](https://github.com/CSAILVision/GANDissect)上可以查看，视频示范操作可以在项目主页[项目主页](https://gandissect.csail.mit.edu/)中找到。

我们感兴趣的是生成图片的GANs。

> “根据人们的观察，训练好的GAN看起来能够学习图片上的物品：例如，一个门出现在建筑上而不是树上。我们希望理解GAN是如何表示一个结构的。物体对于GAN看起来到底是单纯的像素模式没有具体的物体表征含义如门或者树，还是GAN包含了人类理解物体相关的内在变量？如果GAN包含了门和树的变量，是这些变量导致了这些物体的生成过程，还是他们不怎么相关？物体之间的表示如何关联在一起？”

研究的基础是在LSUN场景数据集上训练的三个Progressive GANs的变量。为了理解GANs中发生了什么，作者使用了结合分解（dissection）和干预（intervention）的方法。

给出一个训练的分割模型（segmentation model）（将图像中的像素映射到一个预定义的物品类别），我们可以分解GAN的中间层去识别独立单元与每个物品类别之间的一致程度。论文中的分解模型是在ADE20k场景数据集上训练并且能够将输入图像分解为336个物品类别，29个大类和25个材料。

分解可以揭示单元与特定物品类别的外貌相关，但这种关系是因果关系么？两个不同类别的干预可以帮助我们更好的理解。首先，我们消除这些单元，观察图像中相关联的物品是否消失。其次，我们可以强制打开单元看是相关联的图像是否出现在之前没有出现的图像中。

文中的第一张图片提供了很好的总结。从中我们可以看到（a）教堂的一组生成图片，（b）分解GAN匹配树的单元的结果。当我们去掉这些单元的时候（c）大部分树消失了，当我们精确的触发他们（d）这些树又出现了。

相同的洞察可以用来人类指导的模型提升。这些是我们人工生成的图片（f）。如果我们识别出GAN导致这些物品生成的单元（e），我们可以通过关闭这些单元去掉生成图片中我们不想要的物品。

