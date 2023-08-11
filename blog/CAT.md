# [Continual Learning of a Mixed Sequence of Similar and Dissimilar Tasks](https://proceedings.neurips.cc/paper_files/paper/2020/hash/d7488039246a405baf6a7cbc3613a56f-Abstract.html)

*Zixuan Ke,Bing Liu, and Xingchang Huang.* *NeurIPS 2020*


The paper introduces a technique called CAT (Continual Learning with forgetting Avoidance and knowledge Transfer) 
to address the challenge of learning a sequence of mixed similar and dissimilar tasks while managing forgetting and transferring knowledge effectively. 
The proposed CAT model aims to find different subnetworks for each task and subsequent tasks are learned based on the task similarity.

If the new task similar to the one of the previous task *t*, learning process of new one starts with the mask of task *t*.
Similarity is basically measured by forward transfer score compared to one simple neural network. 
If the subnetwork performs better than the simple network, then this is a promosing sign to call that tasks are similar.

By using task masks (TM):
-  It protects the important knowledge for dissimilar tasks, preventing forgetting.
-  It selectively transfers useful knowledge from similar tasks to improve learning of new tasks by employing knowledge transfer attention (KTA). 

This transfer of knowledge can happen in both forward and backward directions. 
Empirical evaluations demonstrate that CAT outperforms existing baseline models in scenarios involving these challenges.

