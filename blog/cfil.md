# [Looking Back on Learned Experiences For Class/Task Incremental Learning](https://openreview.net/forum?id=RxplU3vmBx)

*Mozhgan PourKeshavarzi, Guoying Zhao, Mohammad Sabokrou.* *ICLR 2022*

This paper introduces a novel approach called "Cost-Free Incremental Learning (CF-IL)" to address the challenges of incremental learning in deep neural networks 
without requiring additional memory or parallel architectures. In incremental learning, the goal is to continually learn and adapt to new tasks without forgetting 
what has been learned previously.

Existing methods have used strategies like storing old data samples or updating only a subset of network parameters to manage incremental learning. 
However, these methods either demand a large memory budget or limit the model's ability to adapt to new task distributions. 
CF-IL proposes a different approach by introducing an "on-call transfer set" that provides past experiences whenever a new task is encountered in a data stream.

The key contribution of CF-IL is the introduction of a "memory recovery paradigm" which leverages the network itself to recall past experiences and 
generate a "transfer set" to mitigate catastrophic forgetting of previously learned tasks. 
This approach eliminates the need for external memory buffers or growing the network. 
Unlike other methods, CF-IL doesn't require a parallel architecture; it relies solely on the learner network.

When a new task emerges, the memory recovery paradigm is invoked to generate a transfer set, which includes synthesized images for previously learned classes. 
This involves generating preliminary model outputs for each learned class and
optimizing a random noise as an input to create transfer set examples for each learned class. 
The learner network is then retrained on a combined dataset that includes the transfer set and new task data. 
The retraining uses a two-part cost function composed of classification and knowledge distillation terms.

In essence, CF-IL proposes a method where the neural network itself is tasked with recalling and utilizing its past experiences to adapt to new tasks, 
emulating how humans learn and remember without external help. This memory recovery paradigm helps maintain knowledge while accommodating new information, 
allowing the model to learn incrementally without forgetting. The results presented in the paper demonstrate that CF-IL outperforms existing techniques 
both in TIL and CIL setups.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/cfil.png?raw=true" width=800>
</p>
