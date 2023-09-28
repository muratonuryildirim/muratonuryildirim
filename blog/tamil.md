# [Task-Aware Information Routing from Common Representation Space in Lifelong Learning](https://openreview.net/forum?id=-M0TNnyWFT5)

*Prashant Shivaram Bhat, Bahram Zonooz, Elahe Arani.* *ICLR 2023*

TAMiL employs task-attention modules (TAMs) to capture task-specific information from a common representation space. 
It emphasizes that the choice of attention modules should offer flexibility to capture task-specific information effectively. 
These modules should also be diverse enough to differentiate between tasks during inference while ensuring that the continual learning model remains scalable for longer task sequences. 
To this end, the proposed approach uses 'simple undercomplete autoencoders' as TAMs.

**TAM Components:** Each TAM consists of two parts: τie θ (feature extractor) and τis θ (feature selector). 

$τ^{ie}$  (Feature Extractor): This is the first part of the TAM, and its primary role is to act as a feature extractor. 
In other words, it's responsible for capturing relevant information from the input data and transforming it into a lower-dimensional representation. 
The process typically involves the following steps:

- Linear Layer: The feature extractor starts with a linear layer. 
This layer applies linear transformations to the input data, which essentially means it performs a weighted sum of the input features. 
This initial linear transformation helps in learning a more compact and informative representation of the data.

- ReLU Activation: Following the linear layer, a Rectified Linear Unit (ReLU) activation function is applied. 
The ReLU activation function introduces non-linearity to the model. It effectively replaces negative values with zero and passes positive values unchanged. 
This non-linearity helps in capturing complex patterns and features in the data.

So, $τ^{ie}$ essentially reduces the dimensionality of the input data and extracts important features that are relevant to the task at hand.

$τ^{is}$ (Feature Selector): This is the second part of the TAM, and its primary role is to select task-specific information from the features extracted by the feature extractor. 
Here's how it works:

- Linear Layer: Similar to the feature extractor, the feature selector employs a linear layer. 
However, in this case, the linear layer is used to learn task-specific attention weights. 
These weights determine which features extracted by the feature extractor are relevant to the current task and should be emphasized.

- Sigmoid Activation: After the linear layer, a sigmoid activation function is applied. 
The sigmoid function takes the learned weights and maps them to values between 0 and 1. 
These values act as attention weights, with higher values indicating that a feature is more relevant to the current task, and lower values indicating less relevance.

So, $τ^{is}$  essentially selects and weights the features extracted by τie θ based on the current task, allowing the model to focus on the most relevant information for that task.
Overall, $τ^{ie}$ and $τ^{is}$  work together in a TAM to extract and emphasize task-specific information from the input data. 
The feature extractor reduces the dimensionality and extracts features, while the feature selector determines the importance of these features for the current task. 
This two-step process helps in adaptively learning and utilizing task-specific information during continual learning in the TAMiL method.

Authors placed the TAM modules in the upper levels of the layer hierarchy, as in the Figure, since in deep neural networks (DNNs), 
the initial layers are designed to capture general or generic information, whereas the later layers more have redundancy.

Finally, during inference, they used ignition event to trigger a particular TAM as a matching criterion while doing Class Incremental learning where task identities are not provided.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim/blob/master/blog/img/tamil.png?raw=true" width=700>
</p>
