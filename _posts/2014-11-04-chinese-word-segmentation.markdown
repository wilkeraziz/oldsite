---
layout: post
title:  "Chinese word segmentation"
date:   2014-11-04
categories: work
tag: Benchmark
---

Benchmarking the effect of different Chinese word segmentation strategies on SMT performance (in terms of BLEU).

## Data


* training: TED talks (from IWSLT14) amounting 182,385 sentence pairs
* tuning: dev2010 + tst2010
* test: tst2011-2014

## Model

* standard hiero 
* 4-gram LM (target side of training data only)


## Segmenters

* [Stanford word segmenter](http://nlp.stanford.edu/software/segmenter.shtml)
	* ``ctb`` trained using Chinese Treebank
	* ``pku`` trained using data from Beijing University
* [jieba](https://github.com/fxsjy/jieba)
	* ``default`` based on some prefix dictionary matching
	* ``all`` forces more segmentation to happen (reducing vocabulary size)



## Comparison

In terms of BLEU, you should probably stick to Stanford using ``ctb`` models.

Segmenter | tst2011  | tst2012  | tst2013  | tst2014  |mean     
:---------|---------:|---------:|---------:|---------:|----------:
ctb       | *0.1545* | *0.1419* | *0.1458* | 0.1212   | **0.1408**
jieba     | 0.1532   | 0.1389   | 0.1451   |*0.1227*  | 0.1400 
pku       | 0.1535   | 0.1373   | 0.1438   | 0.1207   | 0.1388 
jieba-all | 0.1359   | 0.1223   | 0.1312   | 0.1082   | 0.1244 



That being said, ``jieba`` is very, *very*, **very** fast!
I haven't done a systematic comparison though. 

This is the time it took to segment the source side of the training set.

Segmenter | training2014 | tokens/sec
:---------|-------------:|----------:
ctb       | 4m           | 1,777
jieba     | 30s          | 14,220
jieba-all | 15s          | 28,441


Besides, parallelising ``jieba`` with ``multiprocessing.Pool`` in ``python`` is stupid simple and it will get *TED training2014* segmented in less than 5 seconds using the more accurate model.

{% highlight python %}
import jieba
import sys
import re
# number of jobs
jobs = 20
# read from stdin
content = sys.stdin.read()
# segment in parallel
jieba.enable_parallel(jobs)
output = ' '.join(jieba.cut(content, cut_all=False, HMM=True))
# cleanup blanks
output = re.sub(' +', ' ', output).strip()
# write to stdout
sys.stdout.write(output.encode('utf-8'))
print     

{% endhighlight %}


