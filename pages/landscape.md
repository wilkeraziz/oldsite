---
layout: default
title: DGM landscape
menu: no
---

# Gradient estimation for stochastic computation graphs

Deep generative models (DGMs) are powerful tools for learning a joint distribution over observed and unobserved data. Example of DGMs include variational auto-encoders (VAEs) and generative adversarial networks (GANs). 
DGMs are typically estimated as to maximise a lowerbound on log-likelihood of observations. The key technique here is variational inference (VI), in particular, amortised VI (which can be thought of as VI powered by NNs). 

A lot of the success of NNs in supervised learning is due to the flexibility of maximum likelihood estimation powered by stochastic optimisation. For as long as we can express the probability of observations through a tractable and differentiable computation graph, we can count on the back-propagation algorithm (or other automatic differentiation toolboxes) to obtain gradient estimates on mini-batches of data. 

The main research challenge in DMGs concerns leveraging the full power of automatic differentiation and stochastic optimisation to latent-variable models, where intractable marginals need to be approximate by Monte Carlo estimation. 

This list contains papers that in my view one should read to navigate more easily through literature on deep generative models and their applications. 

# The depths

Some of the developments are very theoretical and you need to dig deep, you may skip through this section and get back to it on demand and as you grow more comfortable with the landscape.


* [A Stochastic Approximation Method](https://www.jstor.org/stable/2236626)
* Control variates
* Exponential families

# Variational inference

Our first mandatory checkpoint is VI.

I would start with a historical read, it will help you understand what the ELBO (VI's objective) accomplishes.

* [The wake-sleep algorithm for unsupervised neural networks](http://www.cs.toronto.edu/~fritz/absps/ws.pdf)

Then VI from the point of view of what it was initially proposed for: approximate posterior inference in Bayesian modelling.

* [Variational Inference: A Review for Statisticians](https://arxiv.org/pdf/1601.00670.pdf)

If you just care about deep generative models, and you don't really plan to look into Variational Bayes and modelling with conditionally conjugate models, you can skip the next block in your first pass through the list:

* [Variational Bayesian Inference with Stochastic Search](https://arxiv.org/pdf/1206.6430.pdf)
* [Stochastic Variational Inference](https://arxiv.org/pdf/1206.7051.pdf)
* [Black Box Variational Inference](https://arxiv.org/pdf/1401.0118.pdf)

Here we get to variational inference in deep learning, but at this point we are going to be using the *score function estimator* rather than the famous *reparameterised gradient*. I think this makes for a better order.

* [Neural Variational Inference and Learning in Belief Networks](https://arxiv.org/pdf/1402.0030.pdf)

If you want to go the extra mile, read the *REINFORCE estimator* paper:

* [Simple Statistical Gradient-Flowing Algorithms for Connectionist Reinforcement Learning](https://link.springer.com/content/pdf/10.1007%2FBF00992696.pdf)

Now we get to the territory of reparameterised gradients. 

* [Doubly Stochastic Variational Bayes for non-Conjugate Inference](http://jmlr.org/proceedings/papers/v32/titsias14.pdf)
* [Auto-Encoding Variational Bayes](https://arxiv.org/pdf/1312.6114.pdf)
* [Stochastic Backpropagation and Approximate Inference in Deep Generative Models](https://arxiv.org/pdf/1401.4082.pdf)

And here is a good view on implementation using automatic differentiation toolkits:

* [Gradient Estimation Using Stochastic Computation Graphs](https://arxiv.org/pdf/1506.05254)

If you care about semi-supervised learning you will like to read about this one:

* [Semi-Supervised Learning with Deep Generative Models](https://arxiv.org/pdf/1406.5298.pdf)

The reparameterised gradient was initially developed for a Gaussian approximate posterior, but we can go beyond that in at least three ways. We can design more expressive approximations by extending the hierarchy of the inference model:

* [Auxiliary Deep Generative Models]( https://arxiv.org/pdf/1602.05473.pdf)
* [Hierarchical Variational Models](https://arxiv.org/pdf/1511.02386.pdf)

We can use *known* distributions that are not (directly) reparameterisable:

* [Automatic Differentiation Variational Inference](https://arxiv.org/pdf/1603.00788.pdf)
* [Rejection Sampling Variational Inference](https://arxiv.org/pdf/1610.05683.pdf)
* [The Generalized Reparameterization Gradient](https://arxiv.org/pdf/1610.02287.pdf)

Or we can focus on being able to sample and to assess the density at a point, but not really knowing the density function in closed-form, by using a *normalising flow*.

* [Variational Inference with Normalising Flows](https://arxiv.org/abs/1505.05770)
* [Improving Variational Inference with Inverse Autoregressive Flow](https://arxiv.org/abs/1606.04934)

If you are curious about undestanding more about the challenges behind optimising the evidence lowerbounder (ELBO), you will like the following:

* [Towards a Deeper Understanding of Variational Autoencoding Models](https://arxiv.org/pdf/1702.08658.pdf) and [InfoVAE: Information Maximizing Variational Autoencoders](https://arxiv.org/pdf/1706.02262.pdf)
* [Fixing a Broken ELBO](https://arxiv.org/pdf/1711.00464.pdf)


If you are really serious about VI, you start questioning the ELBO, and you wonder why should one use KL divergence. Then start here:

* [Operator Variational Inference](https://arxiv.org/pdf/1610.09033.pdf)

# Baselines and Control variates


* [Simple Statistical Gradient-Flowing Algorithms for Connectionist Reinforcement Learning](https://link.springer.com/content/pdf/10.1007%2FBF00992696.pdf)
* [Policy Gradient Methods for Reinforcement Learning with Function Approximation](https://papers.nips.cc/paper/1713-policy-gradient-methods-for-reinforcement-learning-with-function-approximation.pdf)
* [MuProp: Unbiased Backpropagation for Stochastic Neural Networks](https://arxiv.org/abs/1511.05176)
* [REBAR: Low-variance, unbiased gradient estimates for discrete latent variable models](https://arxiv.org/pdf/1703.07370.pdf)
* [Backpropagation through the Void: Optimizing control variates for black-box gradient estimation](https://arxiv.org/pdf/1711.00123.pdf)

# Discrete variables and relaxations

* [Categorical Reparameterization with Gumbel-Softmax](https://arxiv.org/pdf/1611.01144.pdf)
* [The Concrete Distribution: A Continuous Relaxation of Discrete Random Variables](https://arxiv.org/pdf/1611.00712.pdf)
* [Lost Relatives of the Gumbel Trick](https://arxiv.org/pdf/1706.04161.pdf)

## More on Normalising flows

* [Variational Inference with Normalising Flows](https://arxiv.org/abs/1505.05770)
* [Improving Variational Inference with Inverse Autoregressive Flow](https://arxiv.org/abs/1606.04934)
* [Multiplicative Normalizing Flows for Variational Bayesian Neural Networks](https://arxiv.org/abs/1703.01961)
* [Conditional Density Estimation with Bayesian Normalising Flows](https://arxiv.org/pdf/1802.04908.pdf)

## Implicit models 

* [Generative Adversarial Networks](https://arxiv.org/pdf/1406.2661.pdf)
* [Deep and Hierarchical Implicit Models](https://arxiv.org/pdf/1702.08896.pdf)

## Some NLP Applications

* [Generating Sentences from a Continuous Space](//arxiv.org/pdf/1511.06349.pdf)
* [Semantic Parsing with Semi-Supervised Sequential Autoencoders](https://arxiv.org/pdf/1609.09315.pdf)
* [Language as a Latent Variable: Discrete Generative Models for Sentence Compression](https://arxiv.org/pdf/1609.07317.pdf)
* [Discovering Discrete Latent Topics with Neural Variational Inference](//arxiv.org/pdf/1706.00359.pdf)
* [Multi-space Variational Encoder-Decoders for Semi-supervised Labeled Sequence Transduction](https://arxiv.org/pdf/1704.01691.pdf)
* [Deep Generative Model for Joint Alignment and Word Representation](https://arxiv.org/pdf/1802.05883.pdf)




