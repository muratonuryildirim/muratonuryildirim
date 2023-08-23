# [Learning Bayesian Sparse Networks with Full Experience Replay for Continual Learning](https://openaccess.thecvf.com/content/CVPR2022/html/Yan_Learning_Bayesian_Sparse_Networks_With_Full_Experience_Replay_for_Continual_CVPR_2022_paper.html)

*Qingsen Yan, Dong Gong, Yuhang Liu, Anton van den Hengel, Javen Qinfeng Shi*. *CVPR 2022*.

Sparse Neural Network for Continual Learning (SNCL) aims to selectively activate sparse neurons for learning both current and past tasks at any given stage. 
By doing so, one can allocate more parameter space and model capacity to be reserved for future tasks. 
This approach effectively reduces interference between parameters dedicated to different tasks. 

SNCL utilizes Variational Bayesian Sparsity (VBS) priors on the activations of neurons in all layers to regularize the learned weight from previous tasks intead of completely freezing them. 
Additionally, it employs Full Experience Replay (FER) to provide effective supervision in learning the sparse activation patterns of neurons across various layers and selects those exemplars by 
reservoir-sampling strategy to maintain the memory buffer efficiently.

It basically searches the best subnetwork for all the tasks until task $t$ while considering previous tasks with the replay buffer and regularizes the weights from previous tasks to alleviate catastrophic forgetting.
Therefore, it does not assign one subnetwork per task but it always returns one subnetwork regardless the number of tasks with the following loss:

$$
L = \sum_{i=1}^T L_{CE} +  L_{FER} + L_{VBS} 
$$

where $L_{CE}$ is the cross entropy loss, $L_{FER}$ is replay loss and $L_{VBS}$ is prior to regularize the parameters.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/sncl.png?raw=true" width=800>
</p>
