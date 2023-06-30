# [Deep Rewiring: Training Very Sparse Deep Networks](https://arxiv.org/abs/1711.05136)
*Guillaume Bellec, David Kappel, Wolfgang Maass & Robert Legenstein*. *ICLR 2018*.

**TL;DR:** Deep Rewiring (DEEP R) enables to train directly a sparsely connected neural network. It automatically rewires the network during training so that total number of connections are strictly bounded all the time. DEEP R can be used to train very sparse feedforward and recurrent neural networks on standard benchmark tasks with just a minor loss in performance.

Authors motivate their paper with two main points: First, they state that deep neural networks are overparameterized and this creates a bottleneck in terms of energy consumption and memory. Second, they support their approach with neuroscience perspective which reveals human brain dominated by white matter aka. connections between neurons and synaptic connectivity in the brain is highly dynamic in the sense that new synapses are constantly rewired, especially during learning (Holtmaat et al., 2005; Stettler et al., 2006; Attardo et al., 2015; Chambers & Rumpel, 2017). In other words, rewiring is not a distinct process but a crucial component of the brain's learning algorithms.

Its working principle as follows: A connection parameter $θ_k$ and a constant sign $s_k$ ∈ {−1,1} are assigned to each connection *k*. If $θ_k$ is negative, then this connection is become *dormant* which means the corresponding weight is $w_k=0$. Otherwise, the connection is considered active, and $w_k = s_k * θ_k$. Authors use here a connection centric approach where the connections are in the focus rather than the neurons. It is also known as *unstructured sparsity* or *unstructured pruning*.

For all active connections, $θ_k$ is updated with **cross entropy loss + L1 regularization + noise**. Noise term is controlled by the temperature parameter *T* and $v_k$ which is sampled from a standard normal distribution. This noise helps to implement a random walk in parameter space.

During training, if parameter $θ_k$ shrinks to less than 0, then this connection is set to *dormant* and a new connection is selected at randomly from the inactive connections. For each connection that was set to the *dormant* state, a new connection is activated, chosen randomly from the uniform distribution over *dormant* connections. This rewiring strategy ensures that exactly **K** connections are active at any time during training.

<p align="center">
  <img src="https://github.com/muratonuryildirim/muratonuryildirim.github.io/blob/master/paper_figs/DeepR.png?raw=true" width=500>
</p>
