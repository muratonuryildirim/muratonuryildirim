# [Rainbow Memory: Continual Learning With a Memory of Diverse Samples](https://openaccess.thecvf.com/content/CVPR2021/html/Bang_Rainbow_Memory_Continual_Learning_With_a_Memory_of_Diverse_Samples_CVPR_2021_paper.html)

*Jihwan Bang, Heesu Kim, YoungJoon Yoo, Jung-Woo Ha, Jonghyun Choi*. *CVPR 2021*.

**TL;DR:** Rainbow Memory (RM) focuses on blurry continual learning where tasks shares classes and is more realistic and practical. To enhance the sample diversity in the memory, RM fills the memory slots with the
samples drawn from the distribution corresponding to the robustness since diversity-induced memory by sampling both perturbation-robust and fragile data helps the models to preserve discriminative boundary for each class.
Hence, RM proposes a new diversity-aware sampling method for effectively managing the memory with limited capacity by leveraging classification uncertainty.

Rainbow Memory (RM) focuses on Online Continual Learning where the incoming samples are presented to a model only once except the ones that are selected as exemplars.
Moreover, it suggests that the disjoint Class Incremental Learning (CIL) setup exaggerates the catastrophic forgetting since it never exposes seen classes in successive tasks, 
but it not really representing the real-world where new classes do not show up exclusively. 
On the other hand, the blurry-CIL setup faints the task boundaries in a manner where each task comprises only a small number of classes that are also shared with the other tasks.
Hence, it proposed the blurry-CIL setup.

RM argues that the exemplars chosen to be stored in the memory should possess two crucial characteristics. 
Firstly, they must be representative of their corresponding class, and secondly, they should be discriminative in relation to the other classes. 
To identify such samples, it proposes that the ones located near the classification boundary are the most discriminative, while the ones closer to the center of the distribution are the most representative. 
In order to satisfy both of these characteristics, we suggest sampling exemplars that exhibit diversity in the feature space.

To ensure diversity, estimating the relative locations of each sample in the class-discriminative feature space can be computationally demanding. 
Therefore, RM proposes an alternative approach, which involves estimating the relative location using sample uncertainty, determined by the classification model. 
In simpler terms, it assumes that samples with higher model certainty will be positioned closer to the center of the class distribution, whereas samples with lower certainty will be positioned farther away. 

RM achieves diversity in the examplar set without the need for computationally intensive calculations: Specifically, it computes the uncertainty of a sample by
measuring the variance of model outputs of perturbed samples by various transformation methods for data augmentation: including color jitter, shear, and cutout.

It outperforms well-known replay-based methods in various online settings.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/rainbow_memory.png?raw=true" width=800>
</p>
