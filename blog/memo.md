# [A Model or 603 Exemplars: Towards Memory-Efficient Class-Incremental Learning](https://openreview.net/forum?id=S07feAlQHgM)

*Da-Wei Zhou, Qi-Wei Wang, Han-Jia Ye, De-Chuan Zhan.* *ICLR 2023*

This paper focuses on the problem of Continual Incremental Learning (CIL), which involves training models to learn new tasks while retaining knowledge from previously learned tasks without forgetting.
The authors explore various methods for achieving this while taking memory constraints into account and identify two primary sources of memory cost in CIL: exemplars and model buffers/expansions. 
However, they observe that the memory usage of expanded or stored models is not consistently considered in evaluations, leading to unfair comparisons with memory-based methods.


To address this, they align memory costs by switching the size of extra backbones into extra exemplars, enabling a fair comparison between methods. 
The authors present experimental results using benchmark datasets like CIFAR100 and ImageNet100 and, show that both approaches performs nearly identical.

Throughtout the experiments, they also analyze the impact of different layers within a neural network and find that shallow and deep layers behave differently in CIL. 
The authors highlight that shallow layers tend to learn generalized features, while deep layers specialize in task-specific features. 
By sharing shallow layers and creating new deep layers for new tasks, memory efficiency can be improved. 
The saved memory can then be used to store more exemplars, further enhancing performance.
Motivated by this observation, they introduce a baseline method called MEMO (Memory-efficient Expandable Model).

MEMO updates the shallow layers continually while freezing the deeper task-specific layers after learning them.
This is due to the findings indicating that in cases where the number of 'base classes' or classes learned at initial Task is restricted (e.g., 10 classes), 
the generalized blocks lack the ability to effectively capture and transfer feature representations and these representations require incremental updates. 
On the other hand, in scenarios with a larger number of base classes (e.g., 50 classes), the ability to create transferable generalized blocks becomes more pronounced. 
Then, freezing these blocks as well leads to improved performance in such scenarios.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/memo.png?raw=true" width=800>
</p>
