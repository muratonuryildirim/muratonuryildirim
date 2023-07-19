# [Task Difficulty Aware Parameter Allocation & Regularization for Lifelong Learning](https://openaccess.thecvf.com/content/CVPR2023/html/Wang_Task_Difficulty_Aware_Parameter_Allocation__Regularization_for_Lifelong_Learning_CVPR_2023_paper.html)

*Wenjin Wang, Yunqing Hu, Qianglong Chen, Yin Zhang*. *CVPR 2023*.

**TL;DR:** Parameter Allocation & Regularization selects an appropriate strategy from parameter allocation and regularization for each task based on the learning difficulty.
which depends on whether the model has learned related tasks before.

Parameter regularization and allocation techniques have proven to be successful in addressing the issue of catastrophic forgetting during lifelong learning.
However, these methods treat all tasks equally, disregarding the varying levels of difficulty associated with each task.
Consequently, parameter regularization methods encounter notable forgetting when faced with a new task that differs significantly from the previously learned ones,
while parameter allocation methods incur unnecessary parameter overhead when dealing with simple tasks.

To tackle this challenge, Parameter Allocation & Regularization (PAR) dynamically selects an optimal strategy, either parameter allocation or regularization, for each task based on its learning difficulty.
By doing so, PAR effectively addresses both the issue of forgetting when encountering dissimilar tasks and the problem of parameter overhead during the learning of simpler tasks.

**Measuring Task Similarity:**

In order to determine the distance between two tasks, KL divergence of the data features is used to measure the difference between their distributions.
To ensure reliable estimation, a separate pre-trained feature extractor, namely ImageNet pre-trained ResNet18, is employed to  generate robust features $X^t_i$ for each image $x^t_i$ in task $T_t$.
But keeping the previous tasks data violates the incremental learning assumption. 
Instead, PAR only holds the mean of distributions for each class that are observed in previous tasks. (e.g. mean distribution of Class 1, mean distribution of Class 2 etc.)
When a new task comes, PAR calculates the distance between data feature distribution $X_i$ of sample $x_i$ and mean distribution of all images in the same task $T_i$. PAR calls this $p(l)$.
Then, it calculates the distance between the $X_i$ and mean distribution of previously seen classes. PAR calls this q(l).
In the last step, the KL divergence between p(l) and q(l) is calculated to decide whether new task is similar to any of the previous tasks. 
Authors make this decision by defining threshold values α and β to compare it with KL divergence and measure the similarity so that model can choose between Parameter Regularization and Allocation. 

**Parameter Regularization or Allocation:**
To choose between regularization or allocation, PAR considers the distance $s_{i,g}$ between the task $T_i$ and a task group $G_g$ by the average of distances of tasks in the group.
Then, to reflect the relatedness, which is usually measured by a value between 0 and 1, PAR maps the $s_{i,g}$  by a monotone increasing function: $s_{i,g}* = min(s_{i,g}, 1-e^{-2(s_{i,g})})$

If $s_{i,g}*$ ≤ α which is another hyperparameter set to 0.5, the new task is added to related group $G_g$ and learned by parameter regularization.
Otherwise, the new task assigns to a new group and learned by parameter allocation while considering hyperparameter β (set to 1) to decide the NAS procedure.

**Parameter Regularization:**

If a new task $T_t$ is easy for the expert model $E_g$ then it is related to the group $G_g$. PAR reuses the expert $E_g$ to learn this task by parameter regularization.
PAR simply applies LwF which utilizes distillation loss to regularize the existing parameters in an expert. Check [this paper](https://arxiv.org/abs/1606.09282) for more detail.

**Parameter Allocation:**

If existing groups are not related to the new task $T_t$, PAR assigns a new task group $G_{M+1}$ with a new expert $E_{M+1}$, where $M$ is the number of existing groups.
As the number of tasks increases, Neural Architecture Search (NAS) becomes excessively long and impractical.
To address this issue, PAR introduces a relatedness-aware architecture search strategy that aims to improve efficiency by considering the relationships between tasks during the NAS process,
thereby reducing the time overhead associated with searching for optimal architectures.

To search a cell for the new task, PAR considers a hyperparameter β. If $s_{t,g}$ ≤ β, PAR reuses the previously found cell structure for expert $E_g$ for the new task $T_t$.
Because a task distance greater than α but less than β indicates that the new task is not related enough to share the same expert with tasks in the group $G_g$ but can use the same architecture.
However, if $s_{t,g}$ > β, then PAR needs to find a new cell by proceeding with a Neural Architecture Search (NAS) to construct a new expert.
PAR adopts a sampling-based NAS method named [MDL](https://arxiv.org/abs/1905.07529) to determine the architecture of this new expert.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/par.png?raw=true" width=500>
</p>
