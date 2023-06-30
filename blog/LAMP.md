# [Layer-Adaptive Sparsity for the Magnitude-Based Pruning](https://arxiv.org/abs/2010.07611)
*Jaeho Lee, Sejun Park, Sangwoo Mo, Sungsoo Ahn, Jinwoo Shin*. *ICLR 2021*.

**TL;DR:** Layer-adaptive magnitude-based pruning (LAMP) proposes a novel importance score for global pruning. 
The score is a rescaled version of weight magnitude that incorporates the model-level $l$<sub>2</sub> distortion 
which mimics the approximate distortion in the model incurred by pruning, and does not require any hyperparameter tuning or heavy computation.


Authors start their paper with a definition of pruning, its benefits, and what points are currently open to questions: 
Neural network pruning is basically removing “unimportant weights” from a model to meet practical constraints (Han et al., 2015), 
mitigate overfitting (Hanson & Pratt, 1988) and enhance interpretability and understanding (Mozer & Smolensky, 1988) (Frankle & Carbin, 2019). 
However, weight importance is still a vaguely defined notion.

Recent advancements in neural network pruning have shown that straightforward magnitude-based pruning can attain state-of-the-art with carefully 
selected layerwise sparsity. However, without a clear consensus on “how to choose” the layerwise sparsities are usually led to handcrafted heuristics 
or an extensive hyperparameter search. To fill this gap, authors present a novel importance score for global pruning, 
called the layer-adaptive magnitude-based pruning (LAMP) score. Results of the LAMP consistently outperform existing schemes for layerwise sparsity selection.

**LAMP score** is a squared weight magnitude, normalized by the sum of all “*surviving weights*” in the layer. 
In other words, The LAMP score is a rescaled weight magnitude, approximating the model-level distortion from pruning. 
Importantly, it is **designed to approximate the distortion** on the model being pruned. 
To compute the LAMP score, the score of weight *u* is calculated with a squared value of itself divided by the sum of 
squared values of weights that have larger values than weight *u* within each layer or weight matrix. 
After the LAMP score calculation, scores are sorted in ascending order. Then, connections with the smallest LAMP scores are globally 
pruned until the desired global sparsity constraint is met. The LAMP score has been tested with sparse-to-sparse training, 
one-shot pruning (a single training-pruning-retraining cycle), and pruning at initialization, and it has been demonstrated that it enhances all those methods.


<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim.github.io/blob/master/paper_figs/lamp.png?raw=true" width=900>
</p>
