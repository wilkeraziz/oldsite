---
layout: photolist
title: VI Tutorial
menu: no
---

[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/philschulz/VITutorial/master)


[Philip Schulz](//philipschulz.org) and [I](//wilkeraziz.github.io) have designed a *tutorial on variational inference and deep generative models for NLP audiences*. All of our tutorial's material is publicly available on [github](https://github.com/philschulz/VITutorial).

Want to host our tutorial at your location? [Contact](#contact) one of us!


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

# <a name="news"> News

* The [tutorial code](//github.com/philschulz/VITutorial/tree/master/code/vae_notebook.ipynb) is now available! The user still needs to complete the TODOs in order for the code to run.
Make sure to follow the instructions and read the comments carefully. Also check out the links to the MXNet documention.

# <a name="tour"> Tour

**Upcoming**

Below are confirmed venues and dates (if available) for future presentations of the tutorial. Please contact us
if you interested in hosting the tutorial.

* ACL 2018, Melbourne: July 15th, 2018

**Past**
* Naver Labs, Grenoble, France: April 3 and April 6, 2018
  1. Deep Generative Models
* Uva-ILLC, Amsterdam: March 22, 2018 (room TBA)
* Macquarie University Sydney: March 19-20, 2018 (time and location TBA)
* Monash University
  1. Basics of Variational Inference: Thu, 16-11-217, 10am-11:30am
  2. Deep Generative Models: Thu, 16-11-2017, 2:30pm-4pm
* Melbourne University
  1. Basics of Variational Inference: Tue, 31-10-2017, Doug McDonell Building, room 8.03, 2:00pm-3:15pm
  2. Deep Generative Models: Thu, 02-11-2017, Doug McDonell Building, room 8.03, 2:15pm-3:30pm
  3. Coding Tutorial: Tue, 07-11-2017, Doug McDonell Building, room 8.03, 2:00pm-3:15pm
* Berlin, July 26-27 2017


# <a name="contact"> Contact

Want to host our tutorial? Have a suggestion? Contact one of us!

* [Philip](//philipschulz.org)
* [Wilker](//wilkeraziz.github.io)
