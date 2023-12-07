# [Meta-attention for ViT-backed Continual Learning](https://openaccess.thecvf.com/content/CVPR2022/html/Xue_Meta-Attention_for_ViT-Backed_Continual_Learning_CVPR_2022_paper.html)
*Mengqi Xue, Haofei Zhang, Jie Song, Mingli Song.* *CVPR 2022*

**TL;DR:** MEAT finds task specific masks for ViTs to continually learn. It has inspired by mask-based continual learning methods in CNNs and improves former approaches by only masking a portion of models parameters.
It renders MEAT more efficient and effective with less overhead and higher accuracy.

The paper focuses on ViT-backed continual learning and introduces a method called MEAT (MEta-ATtention). 
The proposed method is based on mask methods for three main reasons: 
(1) they allocate different parameters to each task, addressing catastrophic forgetting; 
(2) they are not sensitive to task order, an advantage in continual learning; and 
(3) they are more efficient in handling multiple tasks compared to replay and regularization methods, as they avoid expensive data storage.

MEAT leverages the architectural characteristics of Vision Transformers (ViTs) and introduces a mechanism called attention to self-attention, 
tailored for transformer-based architectures, making MEAT more effective. Unlike prior methods such as Piggyback, 
MEAT employs the Gumbel-softmax trick to address the optimization difficulty of discrete mask values, eliminating the need for manually setting threshold hyper-parameters. 
Additionally, MEAT introduces masks to only a portion of its parameters, increasing efficiency compared to prior methods where all parameters are assigned to masks.

Optimization objective of MEAT consists of two loss functions:
The first one is the conventional cross-entropy loss. The second one is drop-control loss which prevents excessive patch dropping to avoid isolating too many image tokens at the early training stage, 
which tends to degrade performance.

$$L = L_{ce} + αL_{dc}(m)$$

$$L_{dc}(m)= {1 \over L} \sum^L_{l=1} (λ− {1 \over n} \sum^n_{i=1} m^i_l)^2 $$


To sum up, instead of retraining weights $W$ for new tasks, MEAT customizes activation maps of $W$ to prevent catastrophic forgetting.
The paper positions MEAT as the first ViT-backed continual learning method, highlighting its advantages in addressing catastrophic forgetting, insensitivity to task order, and efficiency in handling multiple tasks.
