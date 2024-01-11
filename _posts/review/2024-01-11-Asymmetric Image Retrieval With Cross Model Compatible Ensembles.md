---
layout: post
title: Asymmetric Image Retrieval With Cross Model Compatible Ensembles
tags: [WACV2024, Review, image, retrieval, cross model, ensemble]
published: true
author: Junuk Cha
category: review
math: true
---

WACV2024

<img src="https://github.com/JunukCha/junukcha.github.io/assets/92254092/dc3b000e-79ed-4839-95f6-c1cad771a23b" alt="image" 
     style="width:80%; display: block; margin-left: auto; margin-right: auto;">

## Introduction

In the realm of computer vision, especially in applications like face recognition and large-scale image retrieval, the challenge of efficiently and accurately retrieving images is important. Existing symmetric retrieval methods, where a single model is used for both gallery and query images, face a crucial trade-off between computational resources and retrieval accuracy.

- **Symmetric Retrieval Limitations:** In symmetric retrieval, larger models yield higher accuracy but are not feasible for user-side devices due to their computational and memory demands. Conversely, lightweight models, while more practical, suffer from lower accuracy due to their inferior representation capabilities.

- **Asymmetric Retrieval Approach:** To address these limitations, an asymmetric retrieval setting is proposed. It involves using a high-capacity model for indexing the gallery offline and a lightweight model for processing query images. However, this raises the cross model compatibility (CMC) problem, where independently trained models result in incompatible embedding spaces.

- **Previous Solutions and Their Limitations:** Prior solutions relied on knowlege distillation methods to align the query model's embedding space with that of the gallery model. While this showed accuracy improvements, it was inherently limited by the gallery model's performance and presented challenges in creating model ensembles.

- **Novel Approach:** They introduce a new method that uses embedding space transformations, allowing multiple gallery model embeddings to be transformed into the query model’s space. This approach is not constrained by the gallery model's accuracy and facilitates the use of diverse, independently trained models in an ensemble, overcoming the limitations of knowledge distillation.

- **Additional Contributions:** Beyond improving asymmetric retrieval accuracy, the approach includes an uncertainty-based method for gallery image rejection. By exploiting the diversity in transformed embeddings, they estimate the embedding's uncertainty, enhancing overall accuracy. For instance, rejecting 10% of the gallery embeddings can result in a 17.4% reduction in face recognition error​​.

---

## Method

1. **Cross Model Compatibility (CMC):**
  - The core idea is to create compatibility between the embedding spaces of the gallery and the query models.
  - A gallery model $$\phi_g$$ maps each image to the gallery embedding space.
  - This compatibility ensures that the embedding spaces of the gallery and query models can effectively interact with each other​​.

2. **Embedding Transformation:**
  - The method does not rely on knowledge distillation but uses embedding transformation models ($$T_g$$ and $$T_q$$) to align the embedding spaces.
  - The training scheme involves transforming corresponding embeddings from the gallery and query models to a unified embedding space.
  - Three types of loss terms (**similarity, KL-divergence, and dual-classification loss**) are applied during training to enforce compatibility and discriminative power of the embedding spaces​​.
  - A novel model-to-model transformation approach is introduced, where only the gallery's embedding space is transformed to the query’s. This allows multiple transformations from different gallery model spaces to the same query embedding space, while preserving computational efficiency on the user side​​.

3. **Cross Model Compatible Ensembles:**
  - The method leverages multiple gallery models and their corresponding transformation models.
  - During indexing, each gallery image is processed by all gallery models to produce a set of embeddings. These embeddings are then transformed to the embedding space of the query model.
  - A single gallery embedding is produced by averaging the transformed embeddings. This does not increase the test-time latency or the complexity of the querying process​​.

4. **Similarity Loss:**
  - The primary objective of the similarity loss is to ensure that the transformed embedding vectors from the gallery and query models are closely aligned in the unified embedding space.
  - This loss function measures the similarity between corresponding embeddings from the gallery ($$F_g$$) and query ($$F_q$$) models after they have been transformed by their respective transformation models ($$T_g$$ and $$T_q$$).
  - By minimizing this loss, the model ensures that similar images (regardless of whether they come from the gallery or query set) are close to each other in the unified embedding space.

5. **KL-Divergence Loss:**
  - KL-Divergence, or Kullback-Leibler Divergence, is a measure of how one probability distribution diverges from a second, expected probability distribution.
  - In the context of this method, the KL-Divergence loss is used to align the probability distributions of the transformed embeddings from the gallery and query models in the unified space.
  - This loss encourages the model to produce embeddings that not only are similar but also have similar distributions in the unified space, further enhancing the compatibility between the gallery and query models.

6. **Dual-Classification Loss:** 
  - The dual-classification loss is employed to ensure that the embedding spaces are not only similar and aligned but also discriminative.
  - This loss term enforces that the embeddings are discriminative by identity, meaning that embeddings from different classes (or identities) are well separated in the unified space.
  - A shared classification head is used in the training process to ensure that the embedding spaces from both models are aligned and discriminative. This shared classification head contributes to the dual-classification loss.

---

## Experimental Results and Analysis

### Performance Metrics
  - **1:1 Verification:** This is a standard testing protocol in face recognition. In this process, the algorithm determines whether a pair of templates belongs to the same person. A template may contain one or multiple images of a single individual. This metric is essential for verifying the identity of a person based on the images provided.

  - **1:N Open-Set Search:** Another standard protocol used in the study is the 1:N open-set search. Here, each query template is compared against a gallery of templates. The algorithm then decides if, and which, gallery template matches the query template. This metric is vital for searching and identifying a specific image from a large set of images (gallery).

  - **True Acceptance Rate (TAR) at a Specific False Acceptance Rate (FAR):** For both 1:1 verification and 1:N open-set search, the evaluation metric is the True Acceptance Rate (TAR) at a specific False Acceptance Rate (FAR). TAR@FAR measures the rate at which genuine matches are correctly identified (true acceptances) at a given rate of false acceptances. This metric balances the need for accuracy (correct matches) against the risk of false matches, providing a comprehensive view of the system's performance.


### Accuracy Gains by Ensemble Size
The experiments demonstrated significant accuracy gains with the ensemble approach. The increase in ensemble size showed a corresponding improvement in accuracy, indicating the effectiveness of the approach over traditional symmetric retrieval methods​​.

<img src="https://github.com/JunukCha/junukcha.github.io/assets/92254092/aabe551e-0728-42a4-97d8-ed8e7e68fc67" alt="image" 
    style="width:80%; display: block; margin-left: auto; margin-right: auto;">

### Diversity of Ensemble Components
The diversity of the ensemble components significantly impacts accuracy. The research categorizes this diversity into three types: D-T (Diversity of Transformation Models), D-TG (Diversity of Transformation and Gallery Models), and D-TGA (Diversity of Transformation, Gallery Models, and Gallery Model Architectures). **D-T:** This level involves using different transformation models with a single gallery model. The variety in transformation models aids in mapping gallery embeddings to the query space in unique ways, enhancing ensemble adaptability. **D-TG:** This approach adds diversity in the gallery models along with varied transformation models. Each gallery model with its unique transformation model contributes to a richer and more comprehensive ensemble, improving the overall robustness and accuracy. **D-TGA:** The most diverse approach, D-TGA, incorporates different architectures for the gallery models. This structural diversity ensures a broader range of data representations and feature extractions, significantly enhancing the ensemble's performance. Ensembles with diverse transformation models, gallery models, and model architectures achieved higher accuracy. This implies that a higher diversity in the ensemble leads to better performance​​.

<img src="https://github.com/JunukCha/junukcha.github.io/assets/92254092/232f9051-9f97-471b-b513-bd05ac14edfd" alt="image" 
    style="width:80%; display: block; margin-left: auto; margin-right: auto;">

### Comparison to Other Ensemble Alternatives
In the study comparing different ensemble approaches for image retrieval, the **proposed method** – which independently trains transformation models for each gallery model and then averages these transformed embeddings – was set against several alternatives. The **end-to-end averaging method**, one of these alternatives, simultaneously trains all transformation models. It integrates the transformation and averaging processes in an attempt to directly learn an averaged embedding representation during training. However, this approach might overlook the unique characteristics that individual models contribute to the ensemble.

Building on this concept, the **weighted end-to-end averaging method** introduces weights to the averaging process. In this method, each transformation model contributes a scalar value, influencing the final embedding's composition. This approach aims to recognize and incorporate the varying levels of importance of different models based on their individual contributions, potentially leading to a more nuanced combination of embeddings.

Another alternative, the **concatenation approach**, starts by combining all gallery embeddings into one comprehensive representation. This combined representation is then dimensionally reduced and transformed to align with the query model's embedding space, striving to create a unified representation from all gallery models before transformation.

In comparison, the results favored the proposed method. Its approach of treating each transformation model as an independent contributor and then combining their outputs proved more effective in optimizing ensemble performance. This superiority is attributed to its ability to better capture and amalgamate diverse representations from each model, enhancing accuracy and reliability in image retrieval tasks.

<img src="https://github.com/JunukCha/junukcha.github.io/assets/92254092/123190fb-0426-40b4-a075-ebccaa7b4a23" alt="image" 
    style="width:80%; display: block; margin-left: auto; margin-right: auto;">

### Uncertainty Analysis
The paper highlights the role of ensembles in evaluating uncertainty. Since ensembles involve multiple models making predictions, the variance in these predictions is used as a measure of uncertainty. A high variance among the predictions from different models in the ensemble suggests a higher degree of uncertainty, indicating a lack of consensus among the models.

In the context of their proposed ensemble method for asymmetric image retrieval, the authors use this principle to measure the uncertainty in gallery embeddings. Specifically, they compute the variance of the transformed embeddings of gallery models in the query embedding space. This variance is essentially the mean distance between every pair of transformed embeddings for a given gallery image. High variance indicates that the transformed embeddings from different models are inconsistent, reflecting high uncertainty about that image's representation in the query space.

The practical implications of this uncertainty analysis are significant. If a gallery image exhibits high variance (and thus high uncertainty), it might indicate that the image is less reliable or more challenging to retrieve accurately. The system could potentially use a variance threshold to reject gallery images that exceed this threshold, thereby maintaining higher reliability in the retrieval process.

<img src="https://github.com/JunukCha/junukcha.github.io/assets/92254092/7f06f239-f7b9-40cb-8709-2e1220f2ba7e" alt="image" 
    style="width:80%; display: block; margin-left: auto; margin-right: auto;">

To evaluate the effectiveness of this uncertainty estimation, the paper uses a risk-coverage curve. This curve illustrates the system's accuracy (risk) as a function of the percentage of gallery images registered (coverage). Adjusting the uncertainty threshold allows the system to balance risk and coverage, with a more stringent threshold leading to higher accuracy but lower coverage.

<img src="https://github.com/JunukCha/junukcha.github.io/assets/92254092/ccc47123-4d0b-4c64-8e66-a8ce776e4d59" alt="image" 
    style="width:80%; display: block; margin-left: auto; margin-right: auto;">

Overall, this uncertainty analysis in the proposed ensemble method provides a way to assess the reliability of the model's predictions and, by extension, enhance the overall performance of the image retrieval system.

### Compatible Query Model Update
The author addresses a scenario where an improved query model replaces an older one, and backfilling (recomputing all the gallery embeddings with the new model) is not feasible. This situation is particularly relevant in systems that don't retain data, except for training data.

The authors simulate this scenario as follows: Initially, the system comprises multiple gallery models and a single query model, all trained on 50% of the VggFace2 dataset. The gallery set is then mapped to the embedding spaces of all gallery models, and the gallery images are subsequently discarded. When a new query model becomes available (trained on 100% of the VggFace2 dataset), it replaces the older model. The corresponding embedding spaces of the gallery models are transformed to align with the embedding space of this updated query model using new transformation models.

This scenario represents a significant challenge as it deals with a substantial performance gap between the old and new models (trained on 50% and 100% of the data, respectively). The results demonstrate a considerable performance gain upon updating the query model. For example, the 1:N search TAR@FAR=1% increases from 73.98% to 78.96% with an ensemble size of four, despite using only lower-accuracy models for gallery indexing. Additionally, the results indicate that a larger ensemble size correlates with improved performance, even when the query model is substantially more accurate than the gallery models used for indexing.

<img src="https://github.com/JunukCha/junukcha.github.io/assets/92254092/fa340c7a-03e1-4d85-952c-9d3ec77461ce" alt="image" 
    style="width:80%; display: block; margin-left: auto; margin-right: auto;">

In essence, this section highlights the robustness and adaptability of the proposed approach in a scenario where updating the query model is necessary but backfilling is not an option. The findings suggest that the method can handle significant updates in the query model while still maintaining or even improving performance, showcasing its practical utility in dynamic, real-world applications.

---

For more detailed information and in-depth insights, I recommend referring to the original paper: "Asymmetric Image Retrieval with Cross Model Compatible Ensembles".

[Paper](https://openaccess.thecvf.com/content/WACV2024/papers/Shoshan_Asymmetric_Image_Retrieval_With_Cross_Model_Compatible_Ensembles_WACV_2024_paper.pdf)
<br>
[Supplementary](https://openaccess.thecvf.com/content/WACV2024/supplemental/Shoshan_Asymmetric_Image_Retrieval_WACV_2024_supplemental.pdf)