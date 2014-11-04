---
layout: post
title:  "Chinese word segmentation"
date:   2014-11-04
categories: jekyll update
---

Benchmarking the effect of different Chinese word segmentation strategies on SMT performance (in terms of BLEU).

## Data


* training: TED talks (from IWSLT14)
* tuning: dev2010 + tst2010
* test: tst2011-2014

## Segmenters

* [Stanford word segmenter](http://nlp.stanford.edu/software/segmenter.shtml)
	* ``ctb`` trained using Chinese Treebank
	* ``pku`` trained using data from Beijing University
* [jieba](https://github.com/fxsjy/jieba)
	* ``default`` based on some prefix dictionary matching
	* ``all`` forces more segmentation to happen (reducing vocabulary size)



## Comparison


Segmenter | tst2011  | tst2012  | tst2013  | tst2014  |mean     
:---------|---------:|---------:|---------:|---------:|----------:
ctb       | *0.1545* | *0.1419* | *0.1458* | 0.1212   | **0.1408**
jieba     | 0.1532   | 0.1389   | 0.1451   |*0.1227*  | 0.1400 
pku       | 0.1535   | 0.1373   | 0.1438   | 0.1207   | 0.1388 
jieba-all | 0.1359   | 0.1223   | 0.1312   | 0.1082   | 0.1244 