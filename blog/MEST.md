# [MEST: Accurate and Fast Memory-Economic Sparse Training Framework on the Edge](https://proceedings.neurips.cc/paper/2021/hash/ae3f4c649fb55c2ee3ef4d1abdb79ce5-Abstract.html)
*Geng Yuan, Xiaolong Ma, Wei Niu, Zhengang Li, Zhenglun Kong, Ning Liu, Yifan Gong, Zheng Zhan, Chaoyang He, 
Qing Jin, Siyue Wang, Minghai Qin, Bin Ren, Yanzhi Wang, Sijia Liu, Xue Lin*. *NeurIPS 2021*.

**TL;DR:** This paper proposes a novel sparse training approach that is specifically designed for edge devices: 
Memory-Economic Sparse Training (MEST). The framework consists of a new weight importance score and relaxed sparsity ratio 
that ensure superior accuracy at high sparsity ratios. MEST framework consistently outperforms well-known SOTA works such as SET, 
DeepR, DSR, RigL, SNFS, SNIP, and GraSP.

The paper first introduces existing works and strategies for network pruning such as heuristics-based pruning, regularization-based pruning,
and network architecture search. And also, more promising pruning algorithms for training on the edge namely *pruning-at-initialization* and
*sparse training*. The first works that use the *pruning-at-initialization* approach such as SNIP and GraSP need to first obtain a fixed sparse 
model from a dense structure and then follow the traditional training process. However, the whole process is still expensive and not compatible 
with edge-devices. On the other hand, sparse training approaches such as SET, DeepR, RigL, and SNFS show great potential for end-to-end edge training. 
Because they start with a sparse model structure picked (but not trained) from a dense structure, and then explore various sparse topologies at the given
sparsity ratio.

Sparse Evolutionary Training (SET) is the first study that presents sparse training with magnitude-based pruning and random weight growth. DeepR adds a 
stochastic parameter update to the training process in addition to SET. RigL updates the topology with magnitude-based pruning and gradient-based weight growth. 
SNFS uses exponentially smoothed gradients aka. momentum to identify layers and weights that lower the error efficiently. The downside of last 2 strategies 
is the computation of all the gradients irrespective of zero or non-zero weights, and therefore their memory footprint is equivalent to dense training.

**MEST** periodically removes less important non-zero weights from the sparse model and grows zero weights back during the sparse training process to discover
the best sparse topologies with a certain sparsity scheme and ratio. Unlike other studies, **MEST** considers a different and novel *importance score*. 
Because authors advocate that determining weight importance only based on its magnitude is not ideal due to the significant weight magnitude fluctuation.
Therefore **MEST** also employs weight’s gradient as an indicator of its importance: $|w_τ|+|λ\frac{∂ℓ(W_{τ−1}, D)}{∂(W_{τ−1})}|$ where $D$ denotes the training data,
ℓ(Wτ−1, D) and $\frac{∂ℓ(W_{τ−1}, D)}{∂(W_{τ-1})}$ are the loss and gradient at epoch τ. λ is a hyperparameter that controls the strength of the gradient in 
weight importance. As a result, three types of weights are considered important: **(i)** large weight magnitude with a small gradient, **(ii)** 
small weight magnitude with a large gradient, and **(iii)** large weight magnitude with a large gradient. To balance the exploration and exploitation 
trade-off **MEST** starts with a larger update frequency and gradually reduces this rate along with the training process.

**MEST** also proposed a *relaxed sparsity ratio*: As an option, to further improve accuracy, newly grown weights are added to the existing weights, 
skipping the pruning step, and the network training starts again. Then, the less important weights will be selected from all weights including 
the newly grown weights. This relaxation avoids forcing the existing weights in the model to be removed if they are more important than newly grown weights.
Finally, sparse training can continue to remain sparse throughout while still achieving the intended sparsity ratio.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim.github.io/blob/master/paper_figs/mest.png?raw=true" width=800>
</p>


