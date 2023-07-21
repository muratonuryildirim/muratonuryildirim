# [Meta-DR: Continual Adaptation of Visual Representations via Domain Randomization and Meta-learning](https://openaccess.thecvf.com/content/CVPR2021/html/Volpi_Continual_Adaptation_of_Visual_Representations_via_Domain_Randomization_and_Meta-Learning_CVPR_2021_paper.html)

*Riccardo Volpi, Diane Larlus, Gregory Rogez.* *CVPR 2021*

**TL;DR:** Meta-DR addresses the issue of forgetting in continual learning models by involving domain randomization, 
which utilizes heavy image manipulations to randomize the distribution of the current domain in vision tasks. Building on this idea, 
Meta-DR introduces a meta-learning strategy that regularizes loss during model transfer to different "auxiliary" meta-domains. 

To address catastrophic forgetting, most studies store a few samples from all encountered domains during the model's lifespan. 
However, this may not be feasible in scenarios with privacy constraints or limited memory, like mobile applications. 
Therefore, Meta-DR aims to develop methods that enhance visual representations' inherent robustness against catastrophic forgetting without relying on data storage or model expansion.

The authors begin with a simple insight to tackle this: the severity of forgetting when adapting a model from one domain ($D_1$) to another ($D_2$) depends on the similarity between the two domains. 
Therefore, they devise a meta-learning approach and introduce a regularization strategy.
Typically, meta-learning requires access to multiple metatasks or meta-domains.
However, the similarity between sequential domains cannot be controlled since it violates continual learning principles. 
To overcome this limitation, inspired by domain randomization, Meta-DR creates "auxiliary" meta-domains by randomizing the original distribution, using standard image transformations.
Authors propose heavily perturbing the current domain's distribution to increase the likelihood that future domain samples will be closer to the current distribution, requiring lighter adaptation.

Meta-DR first trains the metamodel(s) with one batch of perturbed inputs $(\hat{x}, \hat{y})$ which provides the domain randomization and updates its parameters to $\hat{\theta}^t$ during task $t$.
To obtain cross-entropy loss, Meta-DR passes one batch of true inputs ($x, y$) from the continual learner with parameter $\theta^t$.
To regularize the continual learner, Meta-DR uses metamodel with parameters $\hat{\theta}^t$ and infers true inputs to get recall or regularization loss that helps backward transfer.
To adapt the continual learner to possible new domains, Meta-DR uses metamodel with parameters $\hat{\theta}^t$ again and infers perturbed inputs to get adapt loss that helps forward transfer.
Finally, continual learner's parameters are updated based on those three losses to obtain new parameters $\theta^{t+1}$: 

$$
Loss = L_T(x, y; \theta^t) + L_T(x, y; \hat{\theta}^t) + L_T(\hat{x}, \hat{y}; \hat{\theta}^t)
$$

Authors show that models trained using Meta-DR exhibit significantly enhanced robustness against catastrophic forgetting in the context of continual, supervised domain adaptation. 

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/meta_dr.png?raw=true" width=900>
</p>
