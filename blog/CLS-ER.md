# [Learning Fast, Learning Slow: A General Continual Learning Method based on Complementary Learning System](https://openreview.net/forum?id=uxxFrDwrE7Y)

*Elahe Arani, Fahad Sarfraz, Bahram Zonooz.* *ICLR 2022*

**TL;DR:** The paper introduces a method called CLS-ER (Complementary Learning System with Experience Replay) that aims to enhance continual learning in deep neural networks (DNNs) 
by mimicking the Complementary Learning Systems theory, which suggests that both fast instance-based learning and slower structured learning are crucial for effective knowledge accumulation in the brain.

The Complementary Learning Systems (CLS) theory asserts that optimal learning involves two systems: the hippocampus for quick adaptation and episodic learning, and the neocortex for gradual structured learning. 
This paper builds on this theory and addresses the deficiencies in existing methods that do not fully capture the fast learning network's role in continual learning.

The proposed CLS-ER method takes inspiration from the CLS theory and mimics the interplay between fast and slow learning mechanisms to improve continual learning in DNNs. 
The approach involves 3 models: Working Model, Stable Model, and Plastics Model. 
During training, memory samples ($X_m)$ are passed trough Stable Model ($\theta_s$) and Plastics Model ($\theta_p$) to calculate logits ($Z_s$) and ($Z_p$) respectively. 
The best logit ($Z$) that confidently finds correct class is used. 
Then, both 'memory + current data' ($X$) are passed trough the Working Model.
Hence, to train the Working Model ($\theta_w$) CLS-ER uses the following loss and update it standard SGD:

$$
L = L_{CE}(f(X;\theta_w), Y) + \lambda L_{MSE}(f(X_m;\theta_w), Z)
$$

To update Stable Model ($\theta_s$) and Plastics Model ($\theta_p$) they used the following step:

$$
\theta_i = \alpha_i \theta_i + (1 - \alpha_i) \theta_w
$$

Note that, Plastics Model updates more frequently to mimic rapid information adaptation,  and the Stable Model updates less frequently to mimic slow structured knowledge acquisition.

During inference, the stable model is used because it retains long-term memory across tasks, consolidates structural knowledge, and learns effective representations for generalization.


<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/cls-er.png?raw=true" width=700>
</p>
