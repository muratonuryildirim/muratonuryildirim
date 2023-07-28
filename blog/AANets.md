# [AANets - Adaptive Aggregation Networks for Class-Incremental Learning](https://openaccess.thecvf.com/content/CVPR2021/html/Liu_Adaptive_Aggregation_Networks_for_Class-Incremental_Learning_CVPR_2021_paper.html)

*Yaoyao Liu, Bernt Schiele, Qianru Sun.* *CVPR 2021*

**TL;DR:** "Adaptive Aggregation Networks" (AANets) incorporate two types of residual blocks, namely "stable blocks" and "plastic blocks," at each residual level, using ResNet as the base architecture. 
The feature maps from two parallel blocks are aggregated and passed on to the subsequent level blocks. 
Aggregation weights dynamically balance the two types of blocks - stability and plasticity - during the network's operation.

**Stable and Plastic Blocks.** At each residual level, AANets incorporates a pair of stable and plastic blocks with the objective of achieving a balance between plasticity (for learning new classes)
and stability (to retain knowledge of old classes). The two types of blocks are designed to have different levels of learnability. 
The plastic block contains more learnable parameters, including all the convolutional weights denoted as η.
In contrast, the stable block has fewer learnable parameters, mainly consisting of neuron-level scaling weights, denoted as φ
The scaling weights φ are applied to the base model obtained in the 0-th task.
This significantly reduces the number of learnable parameters φ compared to the number of learnable parameters η, which are present in the plastic block 
leading to an adaptive model that can learn new information while preserving knowledge from previous tasks.

**Training and  Optimization.** The Adaptive Aggregation Networks (AANets) optimization is a two-level process, often referred to as bilevel optimization, where Level-1 and Level-2 are the two stages.

*Level-1 Optimization:* At Level-1, the focus is on learning the network parameters for the two types of residual blocks: stable blocks and plastic blocks. 
These residual blocks are the building blocks of the AANets architecture. 
This is a standard optimization process, and it utilizes all available data during the training phase.
The goal at Level-1 is to find the optimal set of parameters that minimize a predefined loss function on the training data. 
This involves performing forward and backward passes through the network to calculate the gradients and then updating 
the network parameters using gradient-based optimization methods (e.g., stochastic gradient descent, Adam, etc.).

*Level-2 Optimization:* At Level-2, the main objective is to adapt the aggregation weights of the two types of blocks, i.e., the stable and plastic blocks. 
These aggregation weights determine the balance between stability and plasticity in the network. 
The idea is to dynamically adjust the importance of each type of block based on the specific requirements of the task.
To optimize the aggregation weights, a balanced subset of data is used. 
This balancing is achieved by downsampling the data of new classes. 
This approach helps in ensuring that the network pays equal attention to both types of blocks and prevents any bias towards a specific type.

*Bilevel Optimization:* The two levels, Level-1 and Level-2, are formulated as a bilevel optimization program (BOP). 
In bilevel optimization, two optimization problems are solved in an alternating manner. 
The objective is to find the optimal values for both the network parameters and the aggregation weights.
At each iteration of the optimization process, the Level-1 problem is solved to update the network parameters while keeping the aggregation weights fixed. 
Then, the Level-2 problem is solved to find the optimal aggregation weights while keeping the network parameters fixed. 
This alternating process continues until convergence or a predefined stopping criterion is met.
By incorporating this bilevel optimization approach, 
AANets can effectively balance the stability and plasticity of the network, leading to better adaptation to the task at hand and improved overall performance.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/aanets.png?raw=true" width=900>
</p>
