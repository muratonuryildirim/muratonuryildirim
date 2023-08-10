# [Heterogeneous Continual Learning](https://openaccess.thecvf.com/content/CVPR2023/html/Madaan_Heterogeneous_Continual_Learning_CVPR_2023_paper.html)

*Divyam Madaan, Hongxu Yin, Wonmin Byeon, Jan Kautz, Pavlo Molchanov.* *CVPR 2023*

HCL argues that assumption of maintaining the same network structure in CL is unrealistic for practical applications like autonomous driving, clinical applications, and recommendation systems.
Instead it suggests that the goal should be retaining knowledge from past learned representations while updating deep learning architectures continuously.
This is achieved by treating the continual learner as a series of learners, each trained with the same or different backbone architectures. 
Various architectures including LeNet, ResNet, RegNet, and vision transformers are considered.

To learn diverse representations continuously, HCL revisits knowledge distillation and transfers old model's knowledge to a new backbone. 
Considering lack of access to prior data, inspired by Deep Inversion (DI), HCL introduces Quick Deep Inversion (QDI) by utilizing current task examples to generate synthetic examples and optimizing them to minimize prediction error on previous tasks. 
This results in an interpolation between current and previous task instances, promoting adaptation to the current task while reducing catastrophic forgetting.
Motivated from a recent [work](https://arxiv.org/abs/2206.14532), HCL also utilizes  data augmentation, soft labeling, and low temperature in knowledge distillation to improve the transfer.

To sum up, HCL builds different models for each task while transfering the previously learned knowledge to a current model.
