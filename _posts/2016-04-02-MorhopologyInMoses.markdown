---
layout: post
title:  "Morphology features in Moses"
date:   2016-04-02
categories: toolkits
tag: Tools
---

# General arguments

Sparse features related to morphology. In general the features are made of string features extracted from input/output factors.
SparseMorphology does not produce actual useable features, it cannot even be instantiated by the decoder.
However, other FFs inherit from SparseMorphology. They all support at least the following set of arguments.

Arguments:

* input-factor=*int*  (default: 0)
    - which factor to extract from source phrases
    - Typical use: morphology tag factor
* output-factor=*int*  (default: 0)
    - which factor to extract from target phrases
    - Typical use: surface factor
* input-max-chars=*int*  (default: 0)
   - how long can the feature be in chars
       - 0 means no limit
       - n>0 means a prefix up to n chars
       - n<0 means a suffix up to n chars
   - Typical use: 0 (whole tag), or small positive n when tags contain attributes from general to specific (discards rare attributes)
* output-max-chars=*int*  (default: 0)
   - same as input-max-chars but applies to output factor
   - Typical use: -2 (or -n with small positive n) to consider just a suffix (for languages that mark with suffixes)
       - 2 (or small positive n) to consider just a prefix (for languages that mark with prefixes)
* feature-vocab=*path*
   - constrain the vocabulary of features
   - Format: the file must contain one feature per line (possibly paired with a weight which will be ignored)
   - Typical use: control the number of sparse features
* oov-feature=*str*  (default: None)
   - used in combination with feature-vocab to rewrite an OOV feature; if this is an empty string, the feature is simply not fired
   - Format: a non-empty string without empty spaces
   - Typical use: debugging perhaps?
* ignore-prefix-in-feature-vocab=*true\|false*  (default: false)
   - if true, assumes features in feature-vocab are prefixed by a component\'s name which should be ignored when reading entries from feature-vocab
   - Typical use: one wants to reuse a weight file to constrain the vocabulary, however, in weight files features are prefixed as in MyFF\_FeatureName
* input-vocab=*path*
   - constrain the vocabulary of input symbols, when a symbol is not in vocab it gets replaced by input-oov (see below)
   - Format: one symbol per line, no prefix, no weights
   - Typical use: reduce the number of combinations
* input-oov=*str*  (default: \*)
   - used in combination with input-vocab to rewrite OOV symbols.
   - Format: a string without empty spaces
* output-vocab=*path*
   - constrain the vocabulary of output symbols, when a symbol is not in vocab it gets replaced by output-oov (see below)
   - Format: one symbol per line, no prefix, no weights
   - Typical use: select strings likely to relate to useful morphemes
* input-oov=*str*  (default \*)
   - used in combination with output-vocab to rewrite OOV symbols.
   - Format: a string without empty spaces
* language-separator=*str*  (default: =>)
   - which symbol to use when concatenating input and output symbols
   - Format: non-empty string whitout white spaces

# SparsePhrasePairMorphology


For each phrase pair, this FF creates one sparse feature of the kind
        
        src_symbols => tgt_symbols

where `src_symbols` is a sequence of input symbols constructed by SparseMorphology, 
and `tgt_symbols` is a sequence of output symbols constructed by SparseMorphology.

Note that word-alignment does not directly affect this feature.
  
Arguments:

* word-separator=*str*  (default: colon)
   - which symbol to use when concatenating words
   - Format: non-empty string whitout white spaces

# SparseWordPairMorphology


For each word within a phrase pair, this FF creates one or more sparse feature of the kind

        src_symbol => tgt_symbol 

where `src_symbol` is an input symbol constructed by SparseMorpholog, 
and `tgt_symbol` is an output symbol constructed by SparseMorphology.

There is one such feature for each target word that aligns to the given source word special treatment applies if the source word is unaligned (see below).
 
Arguments:

* fire-unaligned=*true\|false*  (default: false)
   - fires src_symbol => unaligned-repr
   - Typical use: trying to learn which morphological features should not disappear 
* unaligned-repr=*str*  (default: \<null\>)
   - changes the representation of a null alignment
   - Typical use: beautifying things?


# Examples
 
Make phrase features by concatenating the input POS tag of source words and the last two chars of target words


    SparsePhrasePairMorphology name=PM input-factor=1 output-factor=0 output-max-chars=-2


Make word features by pairing source POS tag and target suffix for aligned words


    SparseWordPairMorphology name=WM input-factor=1 output-factor=0 output-max-chars=-2 


Make word features by pairing source POS tag and target suffix for aligned words. If a word is unaligned we pair it with a dummy token.


    SparseWordPairMorphology name=WM input-factor=1 output-factor=0 output-max-chars=-2 fire-unaligned=true


We can also constrain the output vocabulary


    SparseWordPairMorphology name=WM input-factor=1 output-factor=0 output-max-chars=-2 fire-unaligned=true output-vocab=SparseMorphology.ovocab


And the vocabulary of features


    SparseWordPairMorphology name=WM input-factor=1 output-factor=0 output-max-chars=-2 fire-unaligned=true output-vocab=SparseMorphology.ovocab feature-vocab=SparseWordPairMorphology.weights ignore-prefix-in-feature-vocab=true


Now we also fire missing features using a generic symbol 


    SparseWordPairMorphology name=WM input-factor=1 output-factor=0 output-max-chars=-2 fire-unaligned=true output-vocab=SparseMorphology.ovocab feature-vocab=SparseWordPairMorphology.weights ignore-prefix-in-feature-vocab=true missing-feature=*=>*



