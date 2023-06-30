# [Three Scenarios for Continual Learning](https://arxiv.org/abs/1904.07734)
*Gido M. van de Ven, Andreas S. Tolias*. *NeurIPS 2018*.

**TL;DR:** While learning the tasks sequentially, artificial neural networks suffer from the catastrophic forgetting. 
To overcome this issue lots of methods have been proposed yet there are difficulties to directly compare those methods due to different
in evaluation protocols. To enable more structured comparisons, this paper describes three continual learning scenarios based on if task 
identity is provided at test time and, in case it is not, whether it must be inferred.

Modern, cutting-edge deep neural networks may be taught to perform impressively on a range of specific tasks. However, when number of tasks presented
sequentially to the networks a phenomenon called **catastrophic forgetting** arises. When models trained on a new task, a neural network forgets 
previously learnt tasks. This is a problem in machine learning since it is preferred for a model to be able to learn several tasks and maintain knowledge
about each one, rather than forgetting previous tasks while learning the new ones. 

In the literature, a great deal of methods have been proposed to alleviate catastrophic forgetting. However, many of those studies claimed 
“state-of-the-art” performance due to lack of structured comparison protocols even though some of them dramatically fails in some concepts. 
That is why, authors presents the three unique learning scenarios of varying complexity to allow for more organized comparisons of approaches 
in continual learning. The difference between both circumstances is whether task identification is known at test time, and if not, whether task identity 
has to be inferred.

The first scenario in continual learning is referred to as **task-incremental learning**, where models are always aware of the task at hand and can be 
trained with task-specific components. This is the easiest continual learning scenario and the standard network architecture features a *"multi-headed"* 
output layer, where each task has its own output units and the rest of the network is shared by several tasks. 

The second scenario is called **domain-incremental learning**, where task identity is not provided at test time but models only need to solve the task 
without identifying it. Typical example of this scenario is protocols whereby the structure of the tasks is always the same, but the input-distribution 
is changing. An example of this is an agent learning to survive in different environments. 

The third scenario is called **class-incremental learning**, models are not aware of the task at hand so that they should be able to first identify the task
and then do the inference for each task. It is actually a real-world problem of incrementally learning new classes of objects. Hence, this is the hardest 
continual learning scenario.

Finally, authors proved that current regularization methods *(e.g. elastic weight consolidation and synaptic intelligence)* were ineffective 
in **class-incremental learning** and it is necessary to incorporate the use of past experiences’ memory buffers in order to successfully solve 
the problem at hand.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim.github.io/blob/master/paper_figs/cl_scenarios.png?raw=true" width=600>
</p>
