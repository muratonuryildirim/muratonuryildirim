# [Overcoming Catastrophic Forgetting in Incremental Few-Shot Learning by Finding Flat Minima](https://proceedings.neurips.cc/paper_files/paper/2021/hash/357cfba15668cc2e1e73111e09d54383-Abstract.html)

*Guangyuan Shi, Jiaxin Chen, Wenlong Zhang, Li-Ming Zhan, Xiao-Ming Wu.* *NeurIPS 2021*

This paper addresses the challenge of incremental few-shot learning, where a model must continually recognize new categories with only a few examples provided. 
The study finds that training with the base classes at the initial task only is superior to exeisting few-shot incremental learning approaches. 
This analysis suggests that preventing catastrophic forgetting requires actions in the primitive stage of training base classes rather than in later few-shot learning sessions. 
The proposed approach involves searching for flat local minima of the base training objective function and then fine-tuning model parameters within the flat region on new tasks. 
This enables the model to efficiently learn new classes while preserving knowledge of old ones. 
The experimental results demonstrate that the proposed approach outperforms all prior state-of-the-art methods and is very close to the approximate upper bound.

The key idea is to search for flat local minima of the base training objective function. 
In the flat region around these minima, the loss is small, and the base classes are expected to be well-separated. 
This can be achieved by introducing random noise to the model parameters multiple times and jointly optimizing multiple losses:

$$
L = {1 \over M} {\sum_{j=1}^M L_{base}(z; \phi+ \epsilon, \psi)}
$$

$$
L_{base} = L_{ce} + \lambda {1 \over C} {\sum_{c=1}^C |p_c - p_c^*|_2^2}
$$

where $\phi$ is feature extractor, $\psi$ is classifier, $\epsilon$ is a noise vector, $M$ is the sampling times, $L_{ce}$ refers to the cross-entropy loss of a training sample $z$, and, $p_c$ and $p_c^*$ are the class prototypes before and
after injecting noise respectively. The first term of $L_{base}$ is designed to find the flat region where the parameters $\phi$ of the embedding network can well separate the base classes.
The second term enforces the class prototypes fixed with in such region, which is designed to solve the prototype drift problem.

In the subsequent incremental few-shot learning stage, the model parameters are fine-tuned within the flat region.
This fine-tuning is accomplished by clamping the parameters after updating them on few-shot tasks. 
As a result, the model can efficiently learn new classes while preserving knowledge of the old ones. 

Detailed flow of F2M and its logic is given below:
<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/f2m.png?raw=true" width=575>
</p>
