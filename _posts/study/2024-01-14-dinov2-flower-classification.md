---
layout: post
title: DINOv2 flower classification code
tags: [DINOv2, classification, tsne, visualization, code]
published: true
author: Junuk Cha
category: code
math: true
---

## Introduction
As you may know, DINOv2 proccess a powerful ability to extract semantic features from input images. (Please refer to [this post](https://junukcha.github.io/code/2023/12/31/dinov2-pca-visualization/)). Based on extracted semantic features, I have addressed the flower classification problem.  
What I'm going to share can be summarized as follows:
1. The result comparisons of using the fully connected layer with DINOv2 and Resnet 50 as backbone for classification.
2. The visualization of TSNE.

---

## Dataset
Before starting to talk about the results, I briefly explain the dataset I used.

### 17 Catergory Flower Dataset
It has 17 categories of flowers, with 80 images for each class. I have implemented the code to processing this dataset. [dataset code](https://github.com/JunukCha/DINOv2_classification/blob/master/lib/datasets.py)

---

## The result comprisions
I used Resnet50 + Classifier (a simple FC layer) and DINOv2 + Classifier (a simple FC layer). I used the same classifier. 

### Resnet50 + Classifier
Epoch: 1 | train loss: 2.7797 | train acc: 2.4 | valid loss: 2.6566 | valid acc: 12.3  
Save best model at epoch 1.  
Epoch: 2 | train loss: 2.5889 | train acc: 15.0 | valid loss: 2.5042 | valid acc: 28.9  
Save best model at epoch 2.  
Epoch: 3 | train loss: 2.4263 | train acc: 42.3 | valid loss: 2.3996 | valid acc: 50.3  
Save best model at epoch 3.  
Epoch: 4 | train loss: 2.3427 | train acc: 57.7 | valid loss: 2.3335 | valid acc: 60.6  
Save best model at epoch 4.  
Epoch: 5 | train loss: 2.2982 | train acc: 66.2 | valid loss: 2.3178 | valid acc: 64.2  
Save best model at epoch 5.  
Test loss: 2.2783 | test acc: **67.6**

### DINOv2 + Classifier
Epoch: 1 | train loss: 2.5425 | train acc: 23.4 | valid loss: 2.1657 | valid acc: 72.8  
Save best model at epoch 1.  
Epoch: 2 | train loss: 2.0407 | train acc: 87.2 | valid loss: 1.9574 | valid acc: 97.9   
Save best model at epoch 2.  
Epoch: 3 | train loss: 1.9418 | train acc: 99.0 | valid loss: 1.9346 | valid acc: 100.0   
Save best model at epoch 3.  
Epoch: 4 | train loss: 1.9317 | train acc: 99.9 | valid loss: 1.9340 | valid acc: 99.7  
Epoch: 5 | train loss: 1.9307 | train acc: 100.0 | valid loss: 1.9339 | valid acc: 99.7  
Test loss: 1.9339 | test acc: **99.6**

The performace when using DINOv2 is better than that with Resnet50. DINOv2's accuracy on train set and validation set dramatically increased.

---

## The visualization of TSNE
### TSNE of Resnet50
![image](https://github.com/JunukCha/DINOv2_classification/raw/master/assets/tsne_resnet50.jpg)
### TSNE of DINOv2
![image](https://github.com/JunukCha/DINOv2_classification/raw/master/assets/tsne_dinov2.jpg)

The TSNE results for DINOv2 demonstrate that the features are more coherent within each class.

### Interactive
I implemented the interactive figure. You can interact with with your mouse, and check how similar they are in the same cluster.
![GIF](https://github.com/JunukCha/DINOv2_classification/raw/master/assets/interactive.gif)

---
For more detailed code, please click on [this link](https://github.com/JunukCha/DINOv2_classification). If you have any questions, feel free to leave a comment.