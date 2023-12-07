# [DyTox: Transformers for Continual Learning With DYnamic TOken eXpansion](https://openaccess.thecvf.com/content/CVPR2022/html/Douillard_DyTox_Transformers_for_Continual_Learning_With_DYnamic_TOken_eXpansion_CVPR_2022_paper.html)

*Arthur Douillard, Alexandre Ramé, Guillaume Couairon, Matthieu Cord.* *CVPR 2022*

**TL;DR:** DyTox uses ViT to continually learn. It trains the backbone with current task and memory from the previous tasks. 
During training it also trains task tokens and assigns different classifiers for each task.
Hence, it is basically a well-studied CL approach with transformers and task tokens.


The paper introduces a DyTox transformer model for CL, which involves splitting an image into multiple patches and embedding them using linear projection. 
The embedded patch tokens undergo processing through five successive Self-Attention Blocks (SAB). For each task (indexed as t=1 to T), 
the processed patch tokens are then fed into a Task-Attention Block (TAB), with each forward pass through the TAB being modified by a task-specialized token θt specific to the given task. 
The final embeddings for all tasks are provided separately to independent classifiers for each task, predicting the respective task's classes. All logits are activated with a sigmoid function. 
As an example, for task t=3, one forward pass is conducted through the SABs, followed by three task-specific forward passes through the unique TAB.

The model is trained using three different losses:

1. Classification Loss ($L_{clf}$): This loss is a binary cross-entropy applied to the classification probabilities. It serves as a primary loss function for the model.

2. Knowledge Distillation Loss ($L_{kd}$): Inspired by acknowledged distillation techniques, this loss is applied to the probabilities. It helps in reducing forgetting during training. 

3. Divergence Loss ($L_{div}$): This loss is inspired by the "auxiliary classifier" of DER. It utilizes the current last task's embedding to predict both current classes and 
extra class representing all previous classes encountered via rehearsal. This additional classifier is discarded at test-time, and its purpose is to encourage better diversity among classes.

$$ L = (1-\alpha)L_{clf} + \alpha L_{kd} + \lambda L_{div}$$

To sum up, DyTox is a novel dynamic strategy for continual learning based on a transformer architecture. 
In this model, self-attention layers are shared across all tasks, and task-specific tokens are introduced to achieve task-specialized embeddings through a new task-attention layer. 
This architecture enables the dynamic processing of new tasks with minimal memory overhead and eliminates the need for complex hyperparameter tuning. 
Experimental results demonstrate that DyTox scales effectively to large datasets, achieving state-of-the-art performances. 
Additionally, when considering a large number of tasks (e.g., CIFAR100 with 50 steps), the number of parameters increases reasonably compared to previous dynamic strategies.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/dytox.png?raw=true" width=1000>
</p>
