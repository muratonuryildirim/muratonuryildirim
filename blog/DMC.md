# [Class-incremental Learning via Deep Model Consolidation](https://openaccess.thecvf.com/content_WACV_2020/html/Zhang_Class-incremental_Learning_via_Deep_Model_Consolidation_WACV_2020_paper.html)

*Junting Zhang, Jie Zhang, Shalini Ghosh, Dawei Li, Serafettin Tasci, Larry Heck, Heming Zhang, C.-C. Jay Kuo.* *WACV 2020*

**TL;DR:** DMC proposes two distillation loss for the continual learning to overcome *asymmetric information* flow between old and new classes during the learning process.

Authors argue that the limited effectiveness of regularization-based approaches primarily stems from the *asymmetric information* between old and new classes during the finetuning process. 
When incorporating new classes, they benefit from explicit and robust supervision through available labeled data. 
In contrast, information for old classes is only implicitly conveyed through a noisy regularization term. 
Additionally, excessive regularization can lead to model intransigence, hindering its ability to adapt to the new task, which is commonly known as "intransigence" in the context of Incremental Learning (IL).
Consequently, these methods inherently exhibit a bias either towards the old or the new classes in the final model, making it exceedingly challenging to strike a perfect balance between the two.

As in Figure, authors introduce a novel approach to class-incremental learning termed "Deep Model Consolidation" (DMC). 
This method involves a two-step process: 
Firstly, DMC trains a separate model for the new classes using labeled data. 
Secondly, it distills the knowledge from both new model and old model to contsruct consolidated student model which learns all the classes.
using publicly available unlabeled auxiliary data. This creates a unique double distillation training objective to train the IL model.

In this way, DMC addresses and eliminates the inherent bias caused by information asymmetry or excessive regularization during training. 
This is achieved by allowing the final student model to learn simultaneously from two teacher models—the old and new models. 
Consequently, DMC overcomes the challenges posed by limited access to legacy data by leveraging unlabeled auxiliary data,
which contains plentiful transferable representations to facilitate Incremental Learning.

Formally, teacher models infer the auxiliary data and produce the logits. Then, logits of student model are forced to be similar to corresponding logits coming from teachers.
Since DMC utilizes the logits only, it does not require any labels in the auxiliary dataset.

Lets say, we have 2-class incremental learning and learning 3rd task:
Teacher-1 has 4 output nodes, Teacher-2 has 2 output nodes and student model has 6 output nodes.
Student learns the initial 4 nodes with the supervision of Teacher-1, and rest of the nodes from Teacher-2.
Hence, student model only are trained with double distillation loss without any cross-entropy loss.


<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/dmc.png?raw=true" width=600>
</p>
