# [Error Sensitivity Modulation based Experience Replay: Mitigating Abrupt Representation Drift in Continual Learning](https://openreview.net/forum?id=zlbci7019Z3)

*Fahad Sarfraz, Elahe Arani, Bahram Zonooz.* *ICLR 2023*

This paper explores the dynamics of error-based learning in the brain and how they can be applied to deep neural networks (DNNs) in the context of Continual Learning (CL). 
The authors present evidence suggesting that different characteristics of errors, particularly their size, influence how learning occurs in the brain. 
In the brain, sensitivity to errors decreases as their magnitude increases, meaning that the brain tends to learn more from small errors compared to large ones. 
This sensitivity is modulated by a mechanism that takes into account the history of past errors, implying that the brain maintains a memory of errors.

However, DNNs lack a similar mechanism to modulate error sensitivity, and they typically scale learning linearly with error size. 
This becomes problematic in the context of CL, where sudden shifts in the data distribution can lead to a spike in errors, particularly larger ones. 
These larger errors can dominate gradient updates and disrupt previously learned representations, especially when there are not enough memory samples available.

To address this issue, the paper proposes a method called Error Sensitivity Modulation-based Experience Replay (ESMER). 
ESMER allows the model to prioritize learning from small consistent errors over large sudden errors, enabling it to gradually adapt to new tasks and mitigate abrupt representation drift at task boundaries.

Additionally, the paper suggests an Error-Sensitive Reservoir Sampling approach for maintaining the memory buffer. 
This approach pre-selects low-loss samples from the current batch based on error memory, ensuring that only well-learned incoming samples are added to the buffer. 
This helps retain information without causing representation drift when replaying samples.

The error memory is maintained using the momentum update of the mean cross-entropy loss ($\mu_l$) on the batch of samples from the current task. 
The stable model assesses how well new samples fit into the consolidated decision boundary and representation space, enabling it to adapt to new classes without disrupting previously learned representations.
Hence, ESMER first calculates the cross-entropy loss $L_{ce}$ using stable model $\theta_s$ for each sample $i$ in the current task batch: $l_s^i = L_{ce}(f(x^i, \theta_s), y^i)$.
Then, the weight assigned to each sample is determined by:

$$
\lambda^i = 
\begin{cases}
  1 & \text{if } l_s^i \le \beta \mu_l \\
  \mu_l \over l^i  & \text{otherwise}
\end{cases}
$$

where β controls the margin for a sample to be considered a low-loss. This weighting strategy essentially reduces weight $\lambda^i$ as sample loss moves away from the mean estimate, and consequently 
reducing learning from high-loss samples so that the model learns more from samples with low-loss.

Therefore, the loss of a current task become $L_w^T = \sum \lambda^i l_s^i$. Next, the loss of the memomry can be calculates as $L_w^M = L_{ce}(f(x^m, \theta_w), y^m) + L_{sc}(f(x^m, \theta_w), f(x^m, \theta_s))$ 
where the mean squared loss is used as the semantic consistency loss $L_{sc}$ and γ controls the strength of consistency loss. Finally, the overall loss of the working model is become: $L_w = L_w^T +L_w^M$.

In summary, ESMER reduces the impact of large errors on learning in DNNs, particularly in the context of CL. 
By prioritizing small consistent errors and maintaining an error memory buffer, this approach enables the model to adapt gradually to new tasks, reducing abrupt representation drift at task boundaries.



<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/esmer.png?raw=true" width=600>
</p>
