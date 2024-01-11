---
layout: post
title: Review WACV2024 Asymmetric Image Retrieval With Cross Model Compatible Ensembles
tags: [WACV2024, Review, image, retrieval, cross moel, ensemble]
published: true
author: Junuk Cha
category: code
math: true
---

![image](https://github.com/JunukCha/junukcha.github.io/assets/92254092/dc3b000e-79ed-4839-95f6-c1cad771a23b)


## Introduction

In the realm of computer vision, especially in applications like face recognition and large-scale image retrieval, the challenge of efficiently and accurately retrieving images is important. Existing symmetric retrieval methods, where a single model is used for both gallery and query images, face a crucial trade-off between computational resources and retrieval accuracy.

- **Symmetric Retrieval Limitations:** In symmetric retrieval, larger models yield higher accuracy but are not feasible for user-side devices due to their computational and memory demands. Conversely, lightweight models, while more practical, suffer from lower accuracy due to their inferior representation capabilities.

- **Asymmetric Retrieval Approach:** To address these limitations, an asymmetric retrieval setting is proposed. It involves using a high-capacity model for indexing the gallery offline and a lightweight model for processing query images. However, this raises the cross model compatibility (CMC) problem, where independently trained models result in incompatible embedding spaces.

- **Previous Solutions and Their Limitations:** Prior solutions relied on knowlege distillation methods to align the query model's embedding space with that of the gallery model. While this showed accuracy improvements, it was inherently limited by the gallery model's performance and presented challenges in creating model ensembles.

- **Our Novel Approach:** We introduce a new method that uses embedding space transformations, allowing multiple gallery model embeddings to be transformed into the query model’s space. This approach is not constrained by the gallery model's accuracy and facilitates the use of diverse, independently trained models in an ensemble, overcoming the limitations of knowledge distillation.

- **Additional Contributions:** Beyond improving asymmetric retrieval accuracy, our approach includes an uncertainty-based method for gallery image rejection. By exploiting the diversity in transformed embeddings, we estimate the embedding's uncertainty, enhancing overall accuracy. For instance, rejecting 10% of the gallery embeddings can result in a 17.4% reduction in face recognition error​​.

## Method

1. **Cross Model Compatibility (CMC):**

- The core idea is to create compatibility between the embedding spaces of the gallery and the query models.
- A gallery model (\(phi_g\)) maps each image to the gallery embedding space.
- This compatibility ensures that the embedding spaces of the gallery and query models can effectively interact with each other​​.
