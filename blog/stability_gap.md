# [Continual evaluation for lifelong learning: Identifying the stability gap](https://openreview.net/forum?id=Zy350cRstc6)

*Matthias De Lange, Gido M van de Ven, Tinne Tuytelaars.* *ICLR 2023*

This paper discusses an intriguing phenomenon called the "stability gap" in the context of continual learning with neural networks. 
The stability gap refers to a situation where neural networks experience temporary forgetting of previously learned knowledge when adapting to new tasks, followed by a phase of performance recovery. 
The authors argue that this phenomenon has not received much attention due to standard evaluation practices in continual learning models.

The paper proposes a new framework for evaluating continual learning models, which includes per-iteration evaluation. 
Using this framework, the authors empirically demonstrate that common techniques in continual learning, such as experience replay, knowledge distillation, 
and parameter regularization, are prone to the stability gap. They observe the stability gap in various incremental learning benchmarks, including class, task, and domain-incremental scenarios. 
Furthermore, they find that the stability gap tends to increase when tasks are more dissimilar.

To explain the stability gap conceptually, the paper disentangles the gradients into two components: plasticity gradients $∇L_{plasticity}$ and stability gradients $∇L_{stability}$. 
They found that the plasticity gradient $∇L_{plasticity}$ dominates during the early phase of learning a new task 
since the network has already converged for the previous task which return near zero gradients $∇L_{stability}$ for replay buffer .
This results in significant parameter changes with little gradient signal $∇L_{stability}$ from the replay buffer of previous tasks. 
However, after some training steps, gradient signals $∇L_{stability}$ from the replay buffer become stronger and leads to an increasing gradient norm of the stability component $∇L_{stability}$, 
allowing the network to re-learn and recover some of the prior knowledge.

Hence, in contrast to the prior belief of $∇L_{stability}$ maintaining prior knowledge, authors find that stability is at least partially preserved by means of re-learning, leading to the recovery of prior knowledge.

In summary, the paper introduces and explores the stability gap phenomenon in continual learning with neural networks. 
It provides empirical evidence, proposes a new evaluation framework, and disentangles gradients to explain how networks experience temporary forgetting but recover prior knowledge when adapting to new tasks. 
This research has implications for improving the robustness of continual learning algorithms and addressing the challenges of catastrophic forgetting.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/stability_gap.png?raw=true" width=800>
</p>
