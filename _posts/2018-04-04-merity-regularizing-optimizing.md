---
title: 'Regularizing and Optimizing LSTM Language Models'
date: 2018-04-04
permalink: /posts/2018/04/merity-regularizing-optimizing/
tags:
  - Paper notes
  - RNN
  - Hyperparameters
---

Merity, S., Keskar, N. S., & Socher, R. (2017). Regularizing and optimizing LSTM language models.

OpenReview discussion [link](https://openreview.net/forum?id=SyyGPP0TZ)

_"Given the over-parameterization of neural networks, generalization performance crucially relies on the ability to regularize the models sufficiently. Strategies such as dropout (Srivastava et al., 2014) and batch normalization (Ioffe & Szegedy, 2015) have found great success and are now ubiquitous in feed-forward and convolutional neural networks."_

Awesome overview of regularization in RNNs in introduction.

Regularization strategies:

- Weight-dropped LSTM: DropConnect mask on H2H weights
- Randomized length BPTT
- Embedding dropout
- Activation regularization
- Temporal activation regularization

Optimizer choice: Adam (generally), SGD (word-level LM), avSGD (Averaged SGD)

**AvSGD**: _"AvSGD carries out iterations similar to SGD, but instead of returning the last iterate as the solution, returns an average of the iterates past a certain, tuned, threshold T. This threshold T is typically tuned and has a direct impact on the performance of the method.  We propose a variant of AvSGD where T is determined on the fly through a non-monotonic criterion and show that it achieves better training outcomes compared to SGD."_ [@polyak1992acceleration]

**Classic SGD**:

$$
w_{k+1} = w_k - \gamma_k \hat{\nabla} f(w_k)
$$

where $\hat{\nabla}$ is a stochastic gradient computed over a minibatch, and $k$ the current iteration. References to various useful SGD analysis papers.

**Averaged SGD**:

params: learning rate, $\lambda$ - decay term, $alpha$ - power for $\eta$ (lr) update, $t_0$ - point (iteration) at which to start averaging (default pytorch: $1e6$) and weight decay - L2 reg strength.

Take standard SGD steps, after some time point T start remembering weights multiplied by $\mu$. The final weight configuration is not the last iterate but the (weighted) average of the last $T_{total} - T$ iterates.

**Regularizers**

- Variational dropout: (sample one dropout mask, use it everywhere) for inputs and outputs of LSTMs
- DropConnect: (sample dropout mask for every batch) for hidden to hidden transitions
- Embedding dropout: remove some words **completely** with $p_{\epsilon}$, scale others by $\frac{1}{1 - p_{\epsilon}}$ 
- Weight tying: input and output embedding spaces hare parameters
- Activation regularization: regularize activations that are significantly larger than 0
$$
AR = \alpha L_2 (m \odot h_t)
$$

Where $m$ is the dropout mask applied to the outputs, $h_t$ are the inputs to the nonlinearity and $\alpha$ is a scaling parameter. 

- Temporal activation regularization: penalize differences between subsequent hidden states (slowness regularizer)
$$
TAR = \beta L_2 (h_t - h_{t-1})
$$

**Take-home** (Table 5 \& Chapter 6.3)

Hidden-to-hidden weight dropping helps **a lot**, embeddinng dropout and Averaged SGD also help substantially. Remainder helps, but within a few perplexity points.
