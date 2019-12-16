# Termset weighting by adapting term weighting schemes to utilize cardinality statistics for binary text categorization

```bib
@Article{Badawi2017,
author= {Badawi, Dimaand and Alt{\i}n{\c{c}}ay, Hakan},
title= {Termset weighting by adapting term weighting schemes to utilize cardinality statistics for binary text categorization},
journal= {Applied Intelligence},
year={2017},
volume={47},
number={2},
pages={456--472},
doi= {10.1007/s10489-017-0911-6},
url={https://doi.org/10.1007/s10489-017-0911-6}
}
```

## Abstract

a novel scheme for termset weighting.

weight of a given termset is computed as the product of two factors:

- a function of the member term frequencies that exist in the given document
- the numbers of positive and negative training documents in which the same number of members appear

## Introduction

Goal: determine the category of a given document.

The paper addesses the single-label binary text categorization problem.

- bag-of-words
- $X^2$
- collection frequecy factor (CFF)
- grammatical relations

> a termset is assumed to appear when all members exist in a document

Simulations have shown that the most effective way
of using phrases and termsets is to concatenate them with
BOW-based features

Selection of a GOOD subset if co-occurrence-based features:

- information gain
- mutual information
- frequency
- the use of the co-occurrence-based

the authors of this study have shown that for a given 2-termset, the occurrence of only one of the members may also convey valuable information

Weighting features:

- use collection frequency factor

## Document representation using termsets

termset, itemset, word combination feature

is assumed to occur in a given document if all members are present, regardless of their order and position.

feature selection methods:

- $X^2$
- mutual Information
- odds ratio
- information gain
