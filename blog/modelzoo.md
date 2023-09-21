# [Model Zoo: A Growing Brain That Learns Continually](https://openreview.net/forum?id=WfvgGBcgbE7)

*Rahul Ramesh, Pratik Chaudhari.* *ICLR 2022*

The paper "Model Zoo" introduces a novel approach to continual learning, where a set of models, referred to as the "Model Zoo," is progressively expanded to tackle a growing set of tasks. 
In this setup, a new model is added to the zoo after each learning episode, and it is trained on the most recent task as well as a subset of past tasks (typically 2-4). 
After T episodes, the Model Zoo consists of an ensemble of T models, each trained on a subset of tasks.

The key idea behind Model Zoo is to compute the output for a particular task by averaging the outputs of all models that have been trained on that task. 
For instance, if there is a "green" task (see Figure below), the output for this task would be the average of the outputs produced by the green output heads of the first two models. 
This ensemble-based approach allows the zoo to collectively address a wide range of tasks.

Identifying related sets of tasks is crucial in this approach because it determines which tasks are trained together. 
To address this challenge, the paper draws inspiration from Adaboost and uses the training losses of tasks to identify which tasks should be trained together. 
A "learner" is introduced to the zoo, which is trained on tasks with high training losses, similar to how Adaboost focuses on samples with high training errors. 
This strategy enables the zoo to adapt and improve its performance over time, even if it initially performs poorly on some tasks.

Continual learning typically involves variations in terms of model storage, sample storage, and computational requirements. 
Some methods store no data from previous tasks, while others use a limited replay buffer to store a fraction of the data from past tasks (usually 5-10%). 
Catastrophic forgetting, where a model rapidly forgets solutions to past tasks, is a common challenge in these settings and a primary concern for existing methods.

Model Zoo distinguishes itself by outperforming the "Isolated" baseline, a method that basically trains a small model per task which is not a true continual learning. 
Despite not engaging the true continual learning, "Isolated" achieves better performance (more than a 10% margin) than existing continual learning methods. 
This suggests that existing methods may not effectively leverage data from multiple tasks.

However, in an online setting, if larger models are used in "Isolated" baseline, it perform poorly but achieve better accuracy than all existing methods when trained for multiple epochs. 
This suggests that existing methods may be under-trained in the single-epoch setting, indicating that this may not be the appropriate setting to develop continual learning methods.


In summary, the Model Zoo approach introduces a unique paradigm for continual learning by progressively expanding an ensemble of models to handle a growing set of tasks, 
using a task-relatedness metric inspired by Adaboost. 
This approach offers promising results in terms of both backward transfer (improving on previous tasks) and 
forward transfer (solving new tasks), with reduced training and inference times compared to existing methods.


<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/modelzoo.png?raw=true" width=500>
</p>
