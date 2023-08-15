# [Learning to Learn without Forgetting by Maximizing Transfer and Minimizing Interference](https://openreview.net/forum?id=B1gTShAct7)

*Matthew Riemer, Ignacio Cases, Robert Ajemian, Miao Liu, Irina Rish, Yuhai Tu, and Gerald Tesauro.* *ICLR 2019*

**TL;DR:** This work introduces a perspective on the continual learning problem, focusing on a trade-off between transfer and interference over time. 
It proposes the Meta-Experience Replay (MER) algorithm to address challenges related to non-stationary data and computational complexity. 
MER involves modifying the Reptile algorithm and utilizing an experience replay module to enhance continual learning by minimizing interference.

Authors argue that traditional approaches to the stability-plasticity dilemma in continual learning such as EWC divide learning into distinct phases, 
treating past experiences as old memories and current data as new learning which overlooks the uncertainty of future tasks.

Then, to address these issues, the authors propose a solution that promotes gradient alignment at each point in time. 
They propose a novel way to conceptualize the problem of continual learning, focusing on a balance between transfer and interference over time. 
They introduce the idea of enforcing gradient alignment across examples to optimize this balance. 
They advocate that the dot product of different observations' gradients should be greater than 0 to transfer the knowledge. 
In other words, their gradients should be in the similar direction.

To implement this concept, they present a new algorithm called Meta-Experience Replay (MER), which combines experience replay with optimization-based meta-learning. 
This algorithm aims to reduce interference and enhance transfer of knowledge to future tasks by adjusting the model's parameters accordingly.

In their approach, they modify the Reptile algorithm to integrate it with an experience replay module. 
The MER algorithm maintains a memory, $M$, using reservoir sampling. At each time step, it draws batches that include $k-1$ random samples from the memory, along with the current example (so in total $k$ samples). 
Each example within a batch is treated as its own Reptile batch of size 1 with an inner loop Reptile meta-update. This update is repeated in an outer loop across the batches.


<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/mer.png?raw=true" width=700>
</p>
