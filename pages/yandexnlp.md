---
layout: default
title: VI Tutorial at Yandex NLP Week
menu: no
---


[Philip Schulz](//philipschulz.org) and [I](//wilkeraziz.github.io) have designed a *tutorial on variational inference and deep generative models for NLP audiences*. All of our tutorial's material is publicly available on [github](https://github.com/philschulz/VITutorial).

This is an extended edition I am presenting at [Yandex NLP Week in Moscow](https://academy.yandex.ru/events/data_analysis/NLP_week/).


# Schedule

Check the branch `yandex2019` for all [modules](https://github.com/philschulz/VITutorial/tree/yandex2019/modules)

**Day 1**
* [Deep generative models](https://github.com/philschulz/VITutorial/blob/yandex2019/modules/M0_Intro/M0_Intro.pdf)
* [Variational inference](https://github.com/philschulz/VITutorial/blob/yandex2019/modules/M1_Basics/M1_Basics.pdf)
* [Discrete latent variables](https://github.com/philschulz/VITutorial/blob/yandex2019/modules/M3a_WS_NVIL/M3a_WS_NVIL.pdf)

**Day 2**
* [Continuous latent variables](https://github.com/philschulz/VITutorial/blob/yandex2019/modules/M3b_VAE/M3b_VAE.pdf)
* Practice: [jupyter notebook on discrete latent variables](https://github.com/probabll/dgm4nlp/blob/master/notebooks/sst/SST.ipynb)

**Day 3**
* Advanced topics
* Practice: jupyter notebook on continuous latent variables

# Further reading

This is a [list of papers](landscape) you can use to kickstart your path to being an expert on DGMs.

Some people also asked me to list the techniques available to dealing with intermediate discrete representations (this is not an exhaustive list):
* the probabilistic way to do it is to make the discrete representation stochastic and circumvent non-differentiability via marginalisation, this however leads to intractabilities that need to be addressed via approximate inference and sophisticated gradient estimation: [NVIL](https://www.cs.toronto.edu/~amnih/papers/nvil.pdf) and [in NLP](https://arxiv.org/pdf/1511.06038.pdf);
* you can use pseudo-gradients (i.e. gradient-like quantities) that you can use when gradients are not defined, though note that this is typically done heuristically and leads to biased estimators
    * straight-through estimator (STE) including [Concrete](https://arxiv.org/pdf/1611.01144.pdf) and [GumbelSoftmax-ST](https://arxiv.org/pdf/1611.00712.pdf)
    * [SPIGOT](https://aclweb.org/anthology/P18-1173) is similar to STE, but uses a more sophisticated pseudo-gradient motivated from an NLP perspective
* you can define activations that are themselves solutions to an optimisation problem: this can be used to derive unbiased estimators (though sometimes it requires a change of objective):
    * [sparsemax](https://arxiv.org/pdf/1602.02068.pdf)
    * [sparsemap](http://proceedings.mlr.press/v80/niculae18a/niculae18a.pdf)



# DGMs in NLP

Non-exhaustive list (let me know if you would like me to add a paper to this list):

* Word representation: [Rios et al (2018)](https://doi.org/10.18653/v1/N18-1092), [Brazinskas et al (2018)](https://aclweb.org/anthology/C18-1151)
* Morphological analysis and inflection: [Zhou et al (2017)](http://aclweb.org/anthology/P17-1029), [Wolf-Sonkin et al (2018)](https://www.aclweb.org/anthology/P18-1245)
* Syntactic parsing: [Cheng et al (2017)](http://aclweb.org/anthology/P17-2019), [Corro and Titov (2019)](https://arxiv.org/pdf/1807.09875.pdf)
* Semantic parsing: [(Lyu and Titov (2019)](http://www.aclweb.org/anthology/P18-1037)
* Relation extraction: [Marcheggiani and Titov (2016)](http://ivan-titov.org/papers/tacl16diego.pdf)
* Document modelling: [Miao et al (2016)](https://arxiv.org/pdf/1511.06038.pdf), [Srivastava and Sutton (2017)](https://arxiv.org/pdf/1703.01488.pdf)
* Summarisation: [Miao and Blunsom (2016)](http://aclweb.org/anthology/D16-1031)
* Question answering: [Miao et al (2016)](https://arxiv.org/pdf/1511.06038.pdf)
* Alignment and attention: [Deng et al (2018)](https://arxiv.org/pdf/1807.03756.pdf)
* Machine translation: [Zhang et al (2016)](https://aclweb.org/anthology/D16-1050), [Schulz et al (2018)](https://aclweb.org/anthology/P18-1115), [Eikema and Aziz (2018)](https://arxiv.org/pdf/1807.10564.pdf)
* Vision and language: [Pu et al (2016)](http://papers.nips.cc/paper/6528-variational-autoencoder-for-deep-learning-of-images-labels-and-captions.pdf), [Wang et al (2017)](http://papers.nips.cc/paper/7158-diverse-and-accurate-image-description-using-a-variational-auto-encoder-with-an-additive-gaussian-encoding-space.pdf), [Calixto et al (2018)](https://arxiv.org/pdf/1811.00357.pdf)
* Dialogue modelling: [Wen et al (2017)](http://proceedings.mlr.press/v70/wen17a/wen17a.pdf), [Serban et al (2016)](https://arxiv.org/pdf/1605.06069.pdf)
* Speech modelling: [Fraccaro et al (2016)](https://arxiv.org/pdf/1605.07571.pdf)
* Language modelling: [Bowman et al (2016)](https://aclweb.org/anthology/K16-1002), [Goyal et al (2017)](https://papers.nips.cc/paper/7248-z-forcing-training-stochastic-recurrent-networks.pdf), [Xu and Durret (2018)](https://aclweb.org/anthology/D18-1480), [Ziegler and Rush (2019)](https://arxiv.org/pdf/1901.10548.pdf)
