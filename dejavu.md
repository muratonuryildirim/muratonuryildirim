# [Deja Vu: Continual Model Generalization for Unseen Domains](https://openreview.net/forum?id=L8iZdgeKmI6)

*Chenxi Liu, Lixu Wang, Lingjuan Lyu, Chen Sun, Xiao Wang, Qi Zhu.* *ICLR 2023*

**TL;DR:** This paper introduces the RaTP, which aims to improve target domain generalization, target domain adaptation, and forgetting alleviation in the context of continual domain shift learning. 
The framework combines techniques like training-free data augmentation, a novel pseudo-labeling mechanism, and prototype contrastive alignment to achieve its goals,
and it outperforms existing methods in experimental evaluations."


This paper addresses the challenge of deep learning models operating in non-stationary environments where the distribution of target data continuously shifts over time. 
The authors introduce a framework called RaTP, which focuses on improving the model's ability for both target domain generalization (TDG) and target domain adaptation (TDA), 
while also alleviating catastrophic forgetting and maintaining good performance on previously trained domains.

The authors focus on the problem of Continual Domain Shift Learning (CDSL), 
where a model is initially trained on a labeled source domain and then faces a series of unlabeled target domains that appear over time. 
The goal is to enhance the model's performance during the training stage of each new, previously unseen target domain (referred to as the "Unfamiliar Period"), 
while maintaining good performance on domains encountered earlier.

RaTP utilizes a training-free data augmentation module based on Random Mixup, which generates data samples outside of the current training domain.
It also proposes a Top2 Pseudo Labeling mechanism that emphasizes samples with higher possibilities of correct classification, resulting in more accurate pseudo-labels.
Top2 Pseudo Labeling (T2PL) mechanism addresses the problem of providing accurate supervision for subsequent optimizations when target domains arrive with data but no labels. 
Unlike existing approaches that struggle with inter-class distinguishability, T2PL uses softmax confidence scores to measure the likelihood of correct classification for data samples 
and constructs class centroids using the top 50% of samples. This approach mitigates issues related to class boundary vagueness and the quality of centroids.

Moreover, the paper introduces the use of Prototype Learning (PL) to address challenges related to cross-domain sample variability and insufficient data quantity. 
PL has been effective in tackling these issues in various prior works. 
The challenges are translated into problems of random uncertainty in augmented data and limited data availability in the exemplar memory M. 
To address these challenges, the paper proposes a new algorithm called Prototype Contrastive Alignment (PCA) to align domains and enhance the model's generalization ability.

Therefore, it final objective is become: 
$L_{CE} + L_{PCA} + L_{DIS}$ where $L_{CE}$ is Cross-Entropy Loss, $L_{PCA}$ is Prototype Contrastive Alignment Loss and $L_{DIS}$ is Distillation Loss.
As for the source domain,there is no distillation $L_{DIS}$ because there is no stored old model in the stage of source training.

The authors validate the effectiveness of RaTP through comprehensive experiments and ablation studies on various datasets, including Digits, PACS, and DomainNet. 
The results demonstrate that RaTP significantly outperforms state-of-the-art methods in handling the challenges of Continual Domain Shift Learning.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/ratp.png?raw=true" width=800>
</p>
