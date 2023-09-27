# [On the Soft-Subnetwork for Few-Shot Class Incremental Learning](https://openreview.net/forum?id=z57WK5lGeHd)

*Haeyong Kang, Jaehong Yoon, Sultan Rizky Hikmawan Madjid, Sung Ju Hwang, Chang D. Yoo.* *ICLR 2023*

**TL;DR:** Soft-SubNetworks (SoftNet) is for few-shot class-incremental learning. 
The main goal of SoftNet is to incrementally learn a sequence of sessions, where each session contains
only a few training examples per class while preserving the knowledge learned from previous sessions.


The objective of SoftNet is to perform class-incremental learning while mitigating catastrophic forgetting 
(forgetting previously learned knowledge) and avoiding overfitting to a few samples in each new training session.

SoftNet initally trains a randomly initialized dense model with base classes(e.g. 50 -60 classes) and 
freezes the weights with a largest magnitudes ($M_{major}$) for a given sparsity level. 
Then, in the following tasks, it replay some data from previous tasks with a few samples from current task to find 
optimal subnetwork that consist of new task specific connections ($M_{minor}$) + frozen connections ($M_{major}$).
Hence, only the minor part of the weights is updated to adapt to the new class knowledge in the current session.
That way, SoftNet does not store task-specific subnetworks but keeps a single subnetwork that is trained with both past and current tasks.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/softnet.png?raw=true" width=700>
</p>
