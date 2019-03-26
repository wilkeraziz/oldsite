---
layout: default
title: VI Tutorial at Yandex NLP Week
menu: no
---

[Philip Schulz](//philipschulz.org) and [I](//wilkeraziz.github.io) have designed a *tutorial on variational inference and deep generative models for NLP audiences*. All of our tutorial's material is publicly available on [github](https://github.com/philschulz/VITutorial).


# <a name="general"> Variational Inference and Deep Generative Models

Neural networks are taking NLP by storm. Yet they are mostly applied to fully supervised tasks. 
Many real-world NLP problems require unsupervised or semi-supervised models, however, because annotated data is hard to obtain. 
This is where generative models shine. 
Through the use of latent variables they can be applied in missing data settings. Furthermore they can complete missing entries in partially annotated data sets.

This tutorial is about how to use neural networks inside generative models, thus giving us Deep Generative Models (DGMs). 
The training method of choice for these models is variational inference (VI). 
We start out by introducing VI on a basic level. From there we turn to DGMs. 
We justify them theoretically and give concrete advise on how to implement them. For continuous latent variables, we review the variational autoencoder and use Gaussian reparametrisation to show how to sample latent values from it. 
We then turn to discrete latent variables for which no reparametrisation exists. 
Instead, we explain how to use the score-function or REINFORCE gradient estimator in those cases. 
We finish by explaining how to combine continuous and discrete variables in semi-supervised modelling problems.

# Schedule

Check the branch `yandex2019` for all [modules](https://github.com/philschulz/VITutorial/tree/yandex2019/modules)

**Day 1**
* [Deep generative models](https://github.com/philschulz/VITutorial/blob/yandex2019/modules/M0_Intro/M0_Intro.pdf)
* [Variational inference](https://github.com/philschulz/VITutorial/blob/yandex2019/modules/M1_Basics/M1_Basics.pdf)
* [Discrete latent variables](https://github.com/philschulz/VITutorial/blob/yandex2019/modules/M3a_WS_NVIL/M3a_WS_NVIL.pdf)

**Day 2**
* [Continuous latent variables](https://github.com/philschulz/VITutorial/blob/yandex2019/modules/M3a_DGMs_ContinuousLatentVariables/M3a_DGMs_ContinuousLatentVariables.pdf)
* Practice: [jupyter notebook on discrete latent variables](https://github.com/probabll/dgm4nlp/blob/master/notebooks/sst/SST.ipynb)

**Day 3**
* Advanced topics
* Practice: jupyter notebook on continuous latent variables

# Further reading

This is a [list of papers](pages/landscape) you can use to kickstart your path to being an expert on DGMs.

Some people also asked me to list the techniques available to dealing with intermediate discrete representations (this is not an exhaustive list):
* the probabilistic way to do it, is to make the discrete representation stochastic and circumvent non-differentiability via marginalisation, this however leads to intractabilities that need to be addressed via approximate inference and sophisticated gradient estimation: [NVIL](https://www.cs.toronto.edu/~amnih/papers/nvil.pdf) and [in NLP](https://arxiv.org/pdf/1511.06038.pdf);
* you can use pseudo-gradients: gradient-like quantities that you can use when gradients are not defined, though note that this is typically done heuristically and leads to biased estimators
    * straight-through estimator (STE) including [Concrete](https://arxiv.org/pdf/1611.01144.pdf) and [GumbelSoftmax-ST](https://arxiv.org/pdf/1611.00712.pdf)
    * [SPIGOT](https://aclweb.org/anthology/P18-1173) is similar to STE, but uses a more sophisticated pseudo-gradient motivated from an NLP perspective
* you can define activations that are themselves solutions to an optimisation problem: this can be used to derive unbiased estimators (though sometimes it requires a change of objective):
    * [sparsemax](https://arxiv.org/pdf/1602.02068.pdf)
    * [sparsemap](http://proceedings.mlr.press/v80/niculae18a/niculae18a.pdf)

