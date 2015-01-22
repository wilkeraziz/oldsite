---
layout: post
title:  Randomised Sampling
date:   2014-11-12
categories: review
---

This week, here at the [SLPLL], we discussed the paper [Randomized Pruning: Efficiently Calculating Expectations in Large Dynamic Programs][RP] by Bouchard-Côté et al. (2009).
If anything in this post is inaccurate, this my responsibility alone, I'm entirely to blame ;)

# Motivation

In NLP, we typically deal with discrete distributions (e.g. distributions over derivation trees) whose support are highly combinatorial objects that typically grow intractable pretty quickly. 
These distributions are often parameterised as log-linear models and encoded using formal tools (e.g. finite-state automata or context-free grammars). 
We can also view these objects as graphs or hypergraphs. 
Computing expectations under these distributions require a cubic-time algorithm (cubic with the size of the graphical representation), the Inside-Outside algorithm.
Expectations are necessary in task such as maximum likelihood estimation, empirical risk minimisation, MBR and consensus decoding.
Approximate search (e.g. local search or beam search) has proven adequate for tasks in which approximate MAP (often, rather Viterbi) inference suffices.
If reliable estimates of *expectations* are necessary, approximate search can in general only provide an *arbitrarily* biased view of the true distribution.


# Core idea

    This is the way I would present the idea, not what you will find in the paper


In this work, pruned decisions are modelled through auxiliary random variables.
The authors design a Markov chain that has as stationary distribution the true intractable posterior, and simulate this chain using Gibbs sampling by conditioning on the auxiliary random variables (which control degree of pruning).

Intuitively, the method "samples approximate distributions" encoded as truncated hypergraphs (aka *charts* in the case of parsing).
These are small enough for a complete Inside-Outside run which summarises (biased) feature expectations. 
Such approximate (or truncated) distributions are averaged and the expectations are guaranteed to converge to the true expectations in the limit of infinite samples.

# Method

The paper focuses on parsing. 
In parsing, the distribution over derivation trees is organised in a hypergraph (or chart). 
A hypernode (or chart cell) represents an input span. 
This organisation is common to several exact and approximate dynamic programs for parsing. 
The authors design two random vectors, one that selects spans for pruning considerations and one that controls assignments (whether or not that span is a constituent in a parse tree).
Together these two vectors make a "pruning mask", a mapping from spans to the set {prune, keep}.
Having a pruning mask, one can run this truncated DP and then inside-outside.
Instead of paying the complexity O(|G|^3) wher |G| is large, they pay N\*O(|G'|^3) where |G'| is small and N is a parameter (number of samples).
Sampling a configuration of the auxiliary random variables is equivalent to sampling a random mask. 
The authors use a simpler model can be used to determine the support of the vector of spans (here one can inject long known heuristics).
They show that sampling a new configuration of the vector of assignments, conditioned on the selected spans, is equivalent to i) sampling a derivation tree from the truncated distribution, and ii) assigning unselected spans if they happen to be constituents in that tree.
Applying a mask (or constructing a trucanted chart wrt the pruning mask) is equivalent to sampling an approximate distribution.

# Results

The authors show that their method works in practice and that sampling bias remain roughly constant as a function of input length in bitext parsing, while approximate search leads to increasingly biased estimates.

# My opinions

I think this paper goes a long way in motivating the need for alternatives to beam search.
Don't get me wrong, beam-search-style search is great! It is fast, easy to implement, with the right 
heuristic view of outside weights and with less naive beam filling algorithms it can lead to very few search errors, trading speed and quality 
is very simple, and it does nail most of the models we see around.
The problem is that in the end of the day our models can only be this complex.
If parameterised in a non DP-friendly way, everything falls apart.
So I wonder, should we be looking for alternative inference? Not to get faster inference 
for the models we have, but to enable inference for the models we would like to have.
These guys propose something along this direction :) still highly DP-based though.

Sometimes we have to simplify the model to make drawing independent samples tractable (in times, we even have to overestimate the support).
Other times, we start from an arbitrary derivation and simulate the distribution by means of MCMC, that is, we create a chain of autocorrelated derivations.
These guys, make a chain of autocorrelated distributions. In order to make it tractable, they prune directly the space of derivations (the support), but they do so in a simulation that converges to the true distribution.

I'm mostly insterested in inference algorithms that allow for an arbitrary parameterisation of the model.
This does not go all that way, but it goes in a nice direction.
It still focusses on the models we have (which decompose in terms of context-free productions and at most some low-order HMM features), however, it aims at a type of inference largely neglected, the pursue for unbiased expectations.

Even though I like the work, it is not very easy to read, it's presented in a hard-to-follow order and it leaves a lot of heavy lifting  to the reader. Hold on a sec, for a moment I thought I was talking about a NIPS paper ;).

[SLPLL]: {{ site.slpll_url }}
[RP]: http://papers.nips.cc/paper/3710-randomized-pruning-efficiently-calculating-expectations-in-large-dynamic-programs.pdf
