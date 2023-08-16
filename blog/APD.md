# [Scalable and Order-robust Continual Learning with Additive Parameter Decomposition](https://openreview.net/forum?id=r1gdj2EKPB)

*Jaehong Yoon, Saehoon Kim, Eunho Yang, Sung Ju Hwang.* *ICLR 2020*

The proposed method addresses the challenges of catastrophic forgetting and order-sensitivity in continual learning. 
The key idea is to create a scalable and order-robust continual learning model that handles a large number of tasks. 
Instead of using a completely shared set of weights, the method represents task parameters as a sum of task-shared and sparse task-adaptive parameters. 
This is achieved through an approach called Additive Parameter Decomposition (APD). 
APD ensures that task-adaptive parameters for earlier tasks remain mostly unchanged and are only updated to reflect changes made to task-shared parameters.

To enhance scalability, hierarchical knowledge consolidation is used with APD. 
This involves clustering the task-adaptive parameters to obtain hierarchically shared parameters. 
When a new task arrives, referred to as an APD-Net, it utilizes the task-shared parameters to the maximum extent and 
learns the incremental differences that cannot be explained by shared parameters using sparse task-adaptive parameters. 
Clustering the task-adaptive parameters into hierarchically shared parameters is further done to effectively capture the varying degree of knowledge sharing among tasks.

This approach has several advantages:

*Catastrophic Forgetting Alleviation:* APD reduces catastrophic forgetting by keeping the task-adaptive parameters for previous tasks mostly unchanged. 
Learning on later tasks only updates the task-shared parameters with generic knowledge.

*Memory Efficiency:* Unlike expansion-based approaches, the network topology remains unchanged, making it memory-efficient. 
This effect is even more pronounced with hierarchically shared parameters.

*Fast Training:* The method trains quickly as it doesn't require multiple rounds of retraining.

*Order-Robustness:* The task-shared parameters remain relatively stable, ensuring robustness against the order in which tasks arrive.

In summary, the proposed method, through APD and hierarchical knowledge consolidation, effectively handles catastrophic forgetting and order-sensitivity in continual learning. 
It achieves scalability, memory efficiency, fast training, and order-robustness while maintaining task-specific knowledge and effectively utilizing shared parameters.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/apd.png?raw=true" width=800>
</p>
