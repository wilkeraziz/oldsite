---
layout: post
title:  "Decoding via importance sampling"
date:   2014-11-12
categories: work
---

These are preliminary findings of my importance sampling SMT decoder.

## Data

BTEC corpus

* training: 44k sentences from the BTEC corpus
* tuning: dev1 + dev2
* test: dev3

## Model

Target model (P):

* standard hiero 
* 4-gram LM (target side of training data only)

Proxy model (Q):

* standard hiero
* stateless 4-gram LM (target side of training data only)

## Tuning

For now P and Q are independetly trained via Empirical risk minimisation using IBM-BLEU.

* tuned on n-best lists using `cdec`'s `minrisk` implementation

### Ongoing work

* joint tuning using weighted samples 

## Comparison

Decoder  | Minrisk impl  | Scaling   | Rule     | BLEU
:--------|:-------------:|:---------:|:--------:|---------:
baseline | cdec          | 1.0       | viterbi  | 0.5800   
:--------|:-------------:|:---------:|:--------:|---------:
chisel   | cdec          | 0.005     | map      | 0.5490
chisel   | cdec          | 0.005     | mbr-bleu | 0.5470
chisel   | cdec          | 0.005     | con-bleu | 0.5478
:--------|:-------------:|:---------:|:--------:|---------:
chisel   | cdec          | 0.01      | map      | 0.5225
chisel   | cdec          | 0.01      | mbr-bleu | 0.5226
chisel   | cdec          | 0.01      | con-bleu | 0.5226
:--------|:-------------:|:---------:|:--------:|---------:
chisel   | cdec          | 0.05      | map      | 0.4704
chisel   | cdec          | 0.05      | mbr-bleu | 0.4704
chisel   | cdec          | 0.05      | con-bleu | 0.4704
:--------|:-------------:|:---------:|:--------:|---------:
chisel   | cdec          | 0.1       | map      | 0.4498
chisel   | cdec          | 0.1       | mbr-bleu | 0.4498
chisel   | cdec          | 0.1       | con-bleu | 0.4498
:--------|:-------------:|:---------:|:--------:|---------:
chisel   | cdec          | 0.5       | map      | 0.4375
chisel   | cdec          | 0.5       | mbr-bleu | 0.4375
chisel   | cdec          | 0.5       | con-bleu | 0.4375
:--------|:-------------:|:---------:|:--------:|---------:
chisel   | cdec          | 1.0       | map      | 0.4369
chisel   | cdec          | 1.0       | mbr-bleu | 0.4369
chisel   | cdec          | 1.0       | con-bleu | 0.4369



