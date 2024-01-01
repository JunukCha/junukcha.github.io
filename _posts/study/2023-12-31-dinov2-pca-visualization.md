---
layout: post
title: DINOv2 PCA visualization code
tags: [DINOv2, PCA, visualization, code]
published: true
author: Junuk Cha
category: code
math: true
---

## DINOv2
Foundation models such as CLIP and DINO have garnered significant attention from researchers. To keep up with recent technological advances, I have studied DINOv2. Briefly, DINOv2 excels in extracting semantic features due to its training with a Self-Supervised Learning (SSL) method. This ability is evident in Figure 1 of the [DINOv2 paper](https://arxiv.org/pdf/2304.07193.pdf), which visualizes the first three components of PCA. In this figure, similar parts of objects are colored the same. For instance, the wings of an eagle and an airplane are green, while their heads are red. These results demonstrate DINOv2's proficiency in extracting semantic features from images. I have implemented code to reproduce this PCA visualization.

## PCA visualization
For my analysis, I used four images of different dog breeds (a Corgi, a Shiba Inu, and a Retriever), each in various poses and shapes.
<table>
  <tr>
    <td><img src="/media/blog/2023/12/31/DINOv2 PCA visualization code/1.jpg" alt="dog1"/></td>
    <td><img src="/media/blog/2023/12/31/DINOv2 PCA visualization code/2.jpg" alt="dog2"/></td>
    <td><img src="/media/blog/2023/12/31/DINOv2 PCA visualization code/3.jpg" alt="dog3"/></td>
    <td><img src="/media/blog/2023/12/31/DINOv2 PCA visualization code/4.jpg" alt="dog4"/></td>
  </tr>
</table>

However, the PCA values (RGB) indicated similar parts of the dogs. For example, feet are colored purple and heads are colored orange.

### Result
<img alt="results" src="/media/blog/2023/12/31/DINOv2 PCA visualization code/results.jpg" style="width: 50%">

These results confirm DINOv2's capability to extract useful and semantic features from an image.

----

### Code
For a more detailed view of the implementation, please visit my <a href="https://github.com/JunukCha/DINOv2_pca_visualization" target="_blank">GitHub repository</a>

![code1](/media/blog/2023/12/31/DINOv2 PCA visualization code/code1.png)
Firstly, various libraries such as 'sklearn' for PCA and 'torch' for DINOv2 are loaded.

<br>
![code2](/media/blog/2023/12/31/DINOv2 PCA visualization code/code2.png)
The input image size should be exactly divisible by 14.<br>
DINOv2 can be loaded with torch.hub.<br>
You can choose the DINOv2 version like 'dinov2_vits14'.

[DINOv2 version](https://github.com/facebookresearch/dinov2): 
```
import torch

# DINOv2
dinov2_vits14 = torch.hub.load('facebookresearch/dinov2', 'dinov2_vits14')
dinov2_vitb14 = torch.hub.load('facebookresearch/dinov2', 'dinov2_vitb14')
dinov2_vitl14 = torch.hub.load('facebookresearch/dinov2', 'dinov2_vitl14')
dinov2_vitg14 = torch.hub.load('facebookresearch/dinov2', 'dinov2_vitg14')

# DINOv2 with registers
dinov2_vits14_reg = torch.hub.load('facebookresearch/dinov2', 'dinov2_vits14_reg')
dinov2_vitb14_reg = torch.hub.load('facebookresearch/dinov2', 'dinov2_vitb14_reg')
dinov2_vitl14_reg = torch.hub.load('facebookresearch/dinov2', 'dinov2_vitl14_reg')
dinov2_vitg14_reg = torch.hub.load('facebookresearch/dinov2', 'dinov2_vitg14_reg')
```

<br>
![code3](/media/blog/2023/12/31/DINOv2 PCA visualization code/code3.png)
This PCA model is utilized for background removal.

<br>
![code4](/media/blog/2023/12/31/DINOv2 PCA visualization code/code4.png)
Masks for each image are created using the PCA model. The value 0.6 is determined empirically

<br>
![code5](/media/blog/2023/12/31/DINOv2 PCA visualization code/code5.png)
This PCA model is used for visualizing semantic features. The PCA model inputs foreground pixels `x_norm_patchtokens[i,masks[i],:]`.

<br>
![code6](/media/blog/2023/12/31/DINOv2 PCA visualization code/code6.png)
This PCA model is also used for feature visualization. However, unlike the previous model, this one processes all pixels, including the background, `x_norm_patchtokens`.

The results can be shown below.
<img alt="results" src="/media/blog/2023/12/31/DINOv2 PCA visualization code/results_raw.jpg" style="width: 50%">

----

For more detailed code, please click on <a href="https://github.com/JunukCha/DINOv2_pca_visualization" target="_blank">this link</a>. If you have any questions, feel free to contact me via email at <jucha@unist.ac.kr>.