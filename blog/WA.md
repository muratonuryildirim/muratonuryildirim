# [WA - Maintaining Discrimination and Fairness in Class Incremental Learning](https://arxiv.org/abs/1911.07053)

*Bowen Zhao, Xi Xiao, Guojun Gan, Bin Zhang, Shutao Xia. *CVPR 2020*

**TL;DR:** WA corrects the bias towards the new classes in the classifier while learning the data sequentially 
by aligning the weights of the classifier without any additional model or data cost. 
It basically makes the classifier weights as similar as possible to overcome the bias.


WA discovers that although knowledge distillation is useful in continual learning it is only beneficial to discriminate within old classes. 
However, the model tends to classify old classes as new ones since this minimizes the **Knowledge Distillation Loss** (KD) which 
highly influences the overall loss when the number of increments and classes is large and this creates a bias towards new classes:

$$
Loss = (1-\lambda)L_{ce} + \lambda L_{kd}
$$

Here, **Cross-Entropy Loss** (CE) is to learn the current task and **Knowledge Distillation Loss** (KD) to not forget the old tasks 
with a scalar $\lambda$ which is used to balance between the two terms. 

Therefore, the authors proposed a new method named Weight Aligning (WA) to eliminate the bias in the classifier layer 
whose norms of the weight vectors of new classes are much larger than old classes. WA adjusts weights that are belonged to the classes 
by simply multiplying them with a $\gamma = {\mu(Norm_{old})\over \mu(Norm_{new})}$ term: 

$$
W_{old} = W_{old}
$$

$$
W_{new}=\gamma \cdot W_{new}
$$

In this way, the average norm of the weight vectors for new classes becomes the same as that for old classes. 
Note that this only makes the average norms become equal, in other words, within new classes (or old classes), 
the relative magnitude of the norms of the weight vectors does not change. 
Such a design is mainly used to ensure the data within new classes (or old classes) can be separated well.

Experiments showed that WA improves the most methods by almost 12% overall in CIFAR100 and overpowers its biggest opponent -BiC- with 3% in ImageNet dataset.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/wa.png?raw=true" width=900>
</p>
