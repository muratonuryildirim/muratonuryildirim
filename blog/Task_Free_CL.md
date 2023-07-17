# [Task-Free Continual Learning](https://arxiv.org/abs/1812.03596)
*Rahaf Aljundi, Klaas Kelchtermans, Tinne Tuytelaars*. *CVPR 2019*.

**TL;DR:** Current continual learners require a discrete set of tasks to be trained.
This paper aims to provide an online continual learning setting where data flows as a stream and tasks are not clearly defined.
Therefore, it proposes a new protocol for parameter consolidation, considering the surface of a loss function.

Traditional methods for continual deep learning focus on sequential learning of tasks, where each task is learned one at a time with access to only current task data.
However, this setup is rarely practical. To address this, authors have proposed an online learning system that continuously adapts to changing data distributions without distinct task boundaries.
For this, they adopted [Memory Aware Synapses](https://arxiv.org/abs/1711.09601) which they believe is suitable for online CL scenarios, and proposed a new protocol.

**When to update weights importance:**

In the case of a task-based sequential learning setting where tasks have predefined boundaries, weights' importance is updated after each task, when learning has converged.
In the online case, the data is streaming without knowledge of a task’s start or end (i.e. when distribution shifts occur). Hence, the authors suggest looking at the surface of the loss function.
It is reasonable to say that plateaus in the loss function indicate stable learning regimes, where the model is confidently predicting the current labels, see Figure.

Whenever the model is in such a stable area, it’s a good time to consolidate the knowledge by updating the weights' importance.
This way, one can identify the parameters that are important for the currently acquired knowledge without any need for a task id or number.
When learning new and “different” samples, the model will then be encouraged to preserve this knowledge by regularizing the weights that are important with the given loss function:

$\min_\theta L(F(X;\theta, Y) + L(F(X_{replay};\theta, Y_{replay}) + \frac{\lambda}{2} \sum \Omega_i(\theta_i-\theta_i^*)^2$ where $\Omega_i$ is the weight importance of parameter $\theta_i$.

**Detecting plateaus in the loss surface:**

A sliding window over consecutive losses during training is observed to detect plateaus in the loss surface.
Simply monitoring the mean and the variance of the losses in this window will trigger weights' importance update whenever
the mean and the variance of the sliding window are both lower than a given threshold.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/task_free_CL.png?raw=true" width=600>
</p>

