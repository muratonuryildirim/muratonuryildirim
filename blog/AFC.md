# [Adaptive Feature Consolidation](https://openaccess.thecvf.com/content/CVPR2022/html/Kang_Class-Incremental_Learning_by_Knowledge_Distillation_With_Adaptive_Feature_Consolidation_CVPR_2022_paper.html)
*Minsoo Kang, Jaeyoo Park, Bohyung Han*. *CVPR 2021*.

Existing continual learners based on knowledge distillation minimize the distances between the representations of the old and new models 
without considering which feature maps are important to maintain the previously acquired knowledge.

This paper adopts feature map level knowledge distillation strategy and observes how changes in the feature map representations affect the loss to calculate feature map importances.
Hence, Adaptive Feature Consolidation (AFC) maintains important features for robustness, while making less critical features flexible for adaptivity by using feature map level knowledge distillation.

To this end, it proposes a simple but effective feature map weighting or importance: approximating the change in the loss via the first order Taylor approximation. 
Feature maps that affect the loss function more will have more importance than the others.
As a result, these importance scores can be used in the loss function to guide the training of the continual learner to preserve the important feature maps by imposing a regularization in the loss function:

$L = L_{cls} + \lambda L_{disc}$ where $\lambda$ is a coefficient for discrepancy loss, $L_{disc} = I^t \lVert Z^{t-1} - Z^{t}\rVert ^2$ where $Z^{t}$ is set of feature maps for task $t$ and 
$I^t$ is the importance scores of feature maps for task $t$.

Experimental results present that the AFC outperforms many existing methods in various scenarios.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/afc.png?raw=true" width=500>
</p>
