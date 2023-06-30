# [Chasing Sparsity in Vision Transformers: An End-to-End Exploration](https://arxiv.org/abs/2106.04533)
*Tianlong Chen, Yu Cheng, Zhe Gan, Lu Yuan, Lei Zhang, Zhangyang Wang*. *NeurIPS 2021*.

**TL;DR:** Although the popularity of vision transformers (ViTs) has lately skyrocketed, 
their vast model sizes and high training costs continue to be prohibitive, and traditional 
post-training pruning frequently results in greater training costs. This work conducted 
a comprehensive exploration that attempts to reduce the inference complexity and training memory 
overhead without compromising the attainable accuracy. The suggested method trains sparse subnetworks
while keeping parameter budget fixed, simultaneously optimizing model parameters, and investigating
various connections during the course of training.

The paper initially discusses that deep learning models get deeper and larger which causes enormous computation and memory costs. 
Parameter counts are frequently measured in billions rather than millions now, and this trend also continues with the transformers 
which established many new state-of-the-art records in image classification, object detection, image enhancement, and image generation by leveraging self-attention. 
However, this impressive performance suffers from heavy run-time, memory usage, and tedious training. That is why research on efficiency without compromising the performance of transformers conducted by the authors.

They have considered both *unstructured* and *structured pruning* in the experiments. 
State-of-the-art sparse training approaches for CNNs are implemented for vision transformers (ViTs).

**Sparse Vision Transformer Exploration** $SViTE$, an unstructured pruning approach, 
adopts $Erdos-Renyi$ for sparse initialization and applies *magnitude-based pruning* with *gradient-based growing*. 
They also apply a *cosine annealing* which is basically used to control exploration vs. exploitation trade-off for the pruning rate. 
In, **Structured Sparse Vision Transformer Exploration $S^2 ViTE$**, they inherit the design of sparsity distribution and update schedule from the unstructured $SViTE$. 
The key differences lie in the pruning and growth strategies: In pruning, *taylor pruning* which utilizes the first-order approximation of the training loss to 
estimate units’ significance for model sparsification is preferred. In growing, new nodes are activated based on the highest magnitude gradient. 
Lastly, in $SViTE+$, authors improved the $SViTE$ by selecting the most vital patches in the images by scoring the input token embeddings and selecting the *top-k* informative tokens.

The results showed that accuracy is not significantly compromised and even improved in some cases. 
For example, sparsified DeiT-Small at (5%, 50%) sparsity for (data, architecture), improves 0.28% top-1 accuracy and meanwhile benefits 49.32% FLOPs and 4.40% running time savings.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim.github.io/blob/master/paper_figs/svite.png?raw=true" width=800>
</p>
