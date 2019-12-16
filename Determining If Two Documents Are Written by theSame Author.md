# Determining If Two Documents Are Written by the Same Author

## Abstract

a almost unsupervised method:

> The main idea is to use repeated feature subsampling methods to determine if one document of the pair allows us to select the other from among a background set of 'impostors' in a sufficiently robust manner.

## Introduction

Author Verification Problems can all be simplified to one question: Whether the two sets of given documents are written by the same author.

Imposter methods: ask if X is sufficiently more similar to Y than to any of the generated impostors

- select the imposters properly
- then measure the similarity between documents

## Related Work

- `unmasking`: not effective to short documents.
- intrinsic plagiarism detection (Meyer zu Eissen, Stein, & Kulig, 2007)

classification vs similarity

the Impostor method use similarity method.

## Experimental Setup

- prepare the corpus
- try the baseline method
  - 4-gram features most frequently found in the corpus as feature universe:
    1. space-free characters of length 4
    2. a string of 4 or fewer characters surrounded by spaces
  - SVM
  - strong feature selecting
    - bag-of-words (words appear independently without regarding to the relative positions of each other)
    - function words

## The Many-Candidates Problem

> Given a large set of candidate authors, determine which, if any, of them is the author of a given anonymous document.

- sometimes called the open-set identification problem

### Many-Candidates Method

- precision - recall curve

the trade off in this method:

- with many candidates (in which case there might be many false negatives)
- with few candidates (in which case there might be many false positives)

## The Impostors Method

Steps:

1. Generate a set of impostors $Y_1, ..., Y_m$
2. Compute $score_X(Y) =$ the number of choices of feature sets (out of 100) for which $sim(X, Y) > sim(X, Y_i)$
3. Repeat the above with imposters $X1, ..., X_m$ and compute $score_Y(X)$ in analogous manner.
4. If $average(score_X(Y), score_Y(X))$ is greater than a threshold $\sigma^*$, assign $\left<X, Y\right>$ to `same-author`.

How to generate the impostor set? We need to think:

- quality
- quantity
- threshold

3 ways used:

1. fixed random query from google
2. query from google using small word sets of Y
3. choose other authors' posts from the `blog` (since the cases are from the blog)

Steps to generate the impostors:

- compute the min-max similarity to Y of each documents in the universe. Select the m most similar documents as potential impostors.
- randomly select n actual impostors from among the potential impostors.

the result turns out not to be sesitive to m and n.

## Results

the five method (including baseline methods) and their parameters:

1. threshold on similarity using cosine
2. threshold on similarity using min-max
3. classifying according to an SVM classifier learned on the training setl signed distance from the boundary is the parameter
4. the impostors method using the On-the-fly universe; the score threshold is the parameter.
5. The impostors method using Blog universe; the score threshold is the parameter.

The result of On-The-Fly impostors generating is encouraging. The method allows us to do the impostor method without understanding to the test documents.

But the Blog impostors (impostors from the same genre) produce the better results.

The longer the sample text is, the more accurate the classification result will be for impostor methods.

For `students' essays` case, texts are divided into genres and the X and Y in $\left<X,Y\right>$ are from different genres. The accuracy drops but still higher than the baseline methods.

## Conclusions

- if topic and genre differs the accuracy drops.
- if there are texts from the questioned author in the collected impostors, the result will be affected. Means the impostors should be completely divided from the test authors.
