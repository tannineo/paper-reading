# A Slightly-modified GI-based Author-verifier with Lots of Features (ASGALF)

## Abstract

- a modified way combining the min-max similarity measure
- a relatively large set of diverse features
  - letter level
  - word level
  - function word level
  - word shape level
  - word tag level

## Introduction

- a maths definition to the author identification task PAN at CLEF 2014.
- [Receiver Operating Characteristic (ROC)](https://en.wikipedia.org/wiki/Receiver_operating_characteristic)
  - `AUC`: the area under the ROC curve
  - `c@1`: the measure like `accuracy` but takes `the not answered` into account

$$
\argmax\limits_{h \in H} AUC(\{h(P_i):\forall P_i \in \mathcal{P}\}) \times C@1(\{h(P_i):\forall P_i \in \mathcal{P}\})
$$

- $N_c$: the number of correct answers
- $N_u$: the number of `not answered` problems
- $\mathcal{P}$: the total number of problems

$$
C@1 = \frac{N_c \frac{N_c N_u}{\left| \mathcal{P} \right|}}{\left| \mathcal{P} \right|}
$$

other latex fonts:

$$
n \in \mathbb{N} \\
$$

## Method description
