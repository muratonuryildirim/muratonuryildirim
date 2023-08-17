# [Learning curves for continual learning in neural networks: Self-knowledge transfer and forgetting](https://openreview.net/forum?id=tFgdrQbbaa)

*Ryo Karakida, Shotaro Akaho.* *ICLR 2022*

This study focuses on enhancing our understanding of sequential training in machine learning by conducting a theoretical analysis of its generalization error. 
The investigation delves into learning curves, which signify how the generalization error is influenced by factors such as sample size and the number of tasks. 
Note that experiments were done in Task Incremental Learning settings where the classsifier heads are different for each task while the feature extractor is shared.

The key contributions of this study can be summarized as follows:

1. **Transitions in Transfer Learning:** The study identifies distinct transitions between negative and positive transfer based on the similarity of target tasks.
   If the targets are sufficiently similar, positive knowledge transfer occurs, meaning that predictions for subsequent tasks improve when compared to training without considering the first task.
   Conversely, backward transfer (prediction on the previous task) is affected by a larger critical similarity value, and even subtle dissimilarities between targets can lead to negative transfer.
   This negative transfer causes a rapid increase in error, highlighting the severity of catastrophic forgetting.

2. **Learning of the Same Target Function:** The research investigates a form of continual learning where the same target function is learned across multiple tasks.
   Interestingly, even for the same target function, the model's performance improves or deteriorates in a non-monotonic manner.
   This behavior depends on the sample size of each task. For equal sample sizes, a monotonically decreasing trend in generalization error from task to task can be ensured.
   However, unbalanced sample sizes lead to generalization deterioration.

In essence, this study contributes to a deeper understanding of how sequential training impacts generalization error,
offering insights into the dynamics of knowledge transfer and forgetting in machine learning tasks.
It also sheds light on the behavior of various models during the training process, thereby enhancing our grasp of sequential learning's universal characteristics.
