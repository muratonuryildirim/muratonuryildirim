# [Learning Efficient Convolutional Networks through Network Slimming](https://openaccess.thecvf.com/content_iccv_2017/html/Liu_Learning_Efficient_Convolutional_ICCV_2017_paper.html)
*Zhuang Liu,  Jianguo Li, Zhiqiang Shen, Gao Huang, Shoumeng Yan, Changshui Zhang*. *ICCV 2017*.

**TL;DR:** This work enforces channel-level sparsity in a simple but effective way. Authors calls this approach as network slimming
since it takes wide and large networks as input models and yields thin and compact models with comparable accuracy by identifying and pruning 
insignificant channels automatically. It demonstrated that effectiveness of this valid for several state-of-the-art CNN models, including VGGNet, 
ResNet and DenseNet. For VGGNet, a multi-pass version of network slimming gives a 20×reduction in model size and a 5× reduction in computing operations.


Authors initiate their paper with CNNs’ success and drawbacks in the fields of image classification, object detection, semantic segmentation: 
Although large CNNs have remarkable representation power, they are resource-hungry. For instance, a 152-layer ResNet which has more than 60 million parameters requires more than 20 Giga FLOPs when inferencing an image with resolution 224 × 224. Unfortunately, this is not reasonable on platforms such as mobile devices, wearables or IoT devices.  

Various approaches have been proposed to make CNNs more efficient such as network quantization, binarization, dynamic inference and unstructured weight pruning. Unfortunately, these techniques usually require specially designed softwares/hardwares for the speedup. That is why **network slimming** imposes *L1 regularization* on the scaling factors of batch normalization (BN) layers which is easy to implement without changing the existing CNN architectures. This enables to identify unimportant channels or neurons since each scaling factor corresponds to a specific convolutional channel or neuron. Hence, networks can become slimmer by removing insignificant channels or neurons. Pruning unimportant channels may sometimes temporarily degrade the performance, but this effect can be compensated by the fine-tuning of the pruned network and, if the process repeated for several times, **network slimming** yields even more compact network. 

More formally, the loss of the **network slimming has two** components: $L = \sum l(f(x,W),y) + \lambda \sum g(\gamma)$. First term is training loss of a CNN,and second term g(·) is a sparsity-induced penalty on the scaling factors γ of the BNs, and λ is a hyperparameter that balances the two terms. Higher λ values yields slimmer networks since it increases strength of the regularization. And, BNs has a mathematical representation of $\hat z = \frac {z_{in}-\mu}{\sqrt{\sigma^{2}+\epsilon}}$ and $z_{out}=\gamma \hat{z} + \beta$ where µ and σ are the mean and standard deviation values of 
input activations, γ and β are trainable affine transformation parameters (scale and shift). Therefore, one can easily leverage the γ parameters in BN layers for network slimming. which introduces no overhead to the network.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim.github.io/blob/master/paper_figs/network_slimming.png?raw=true" width=700>
</p>
