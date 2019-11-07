# A Dynamic Programming Model for Text Segmentation Based on Min-Max Similarity

## Abstract

- maximizing the lexical similarity within a segment or minimizing the similarity between adjacent segments

## Introduction

- dynamic programming can achieve a truely global optimization result.

a global optimization model - MMS for text segmentation.

## Related Work

Existing text segmentation algorithms can be classified into 2 categories(respect to the segmentation criteria being employed):

1. use high lexical similarity within a segment.
2. set boundaries where the two segments have lowest lexical similarity.

The MMS combines the two factors, using dynamic programming to avoid the NP problem(the high computational complexity)

## The Segmentation Algorithm

a mathematical definition of the problem.

### Segmentation Criterion Function

$$
J = F(Sim_{Within}, Sim_{Between}) = \alpha \cdot Sim_{Within} - (1 - \alpha) Sim_{Between}
$$

- $Sim_{Within}$ refers to the within-segment similarity
- $Sim_{Between}$ refers to the between-segment similarity
- F is a funciton whose value
  - increases as $Sim_{Within}$ increases
  - decreases as $Sim_{Between}$ increases
- $\alpha$ and $1 - \alpha$ are the relative weight of within-segment lexical similarity and between-segment lexical similarity

$$
Sim_{Within} = \sum_{i=1}^{N} \frac{\Sigma_{m = p_{i-1} + 1}^{p_i}\Sigma_{n = p_{i-1} + 1}^{p_i}D_{m,n}}{(p_i - p_{i-1})^2}
$$

## Evaluation

## Conclusion and Future Work
