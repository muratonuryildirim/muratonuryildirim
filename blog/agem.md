# [Efficient Lifelong Learning with A-GEM](https://openreview.net/forum?id=Hkf2_sC5FX)

*Yaoyao Liu, Bernt Schiele, Qianru Sun.* *ICLR 2019*


A-GEM maintains an episodic memory of gradients (i.e., how the model's parameters should be updated) from earlier tasks. 
Instead of directly updating the model's parameters with the gradients computed on the current task, 
it combines gradients of both the current task's gradient and the gradient stored in memory from previous tasks.
However, instead of storing each task's individual gradients (which is GEM), it only stores the average of them.
By averaging the gradients of current and previous tasks, A-GEM ensures that updates to the neural network's parameters do not significantly deviate from what was learned during previous tasks. 

A-GEM also introduces a new metric that observes the area under learning curves for measuring how quickly a learner acquires new skills. 
This metric helps in assessing the adaptability and learning speed of machine learning algorithms in continual learning settings.

Finally, A-GEM is one of the first papers that consider online continual learning (task-IL) where learners observe each example only once. 
To overcome the challenging online continual learning scenario, it also tunes some basic hyper-parameters on the initial few tasks (such as the first 3 tasks).
Then, the best hyperparameters found on that few tasks are employed for the rest of the increments. 
