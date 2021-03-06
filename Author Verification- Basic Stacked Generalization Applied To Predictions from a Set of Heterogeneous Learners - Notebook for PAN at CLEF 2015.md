# Author Verification- Basic Stacked Generalization Applied To Predictions from a Set of Heterogeneous Learners - Notebook for PAN at CLEF 2015

## Introduction

- problem description
  - `c@1`: `A simple measure to assess non-response`
- problem-level unsupervised / dataset-level supervised
- two stages:
   1. to learn an optimal combination of parameters for each of the five approaches from which the individual learners are obtained
   2. to learn the optimal way to combine the learners together
- avoid overfitting
- chapter structures

## Motivations

- previous work based on manually observation and selection
- improvement plans:
  - combine the previous works
  - former competition suggested a meta-learning system with the output of heterogeneous learners
  - the General Impostor approaches:
    - `Automatically identifying pseudepigraphic texts`
    - `Determining if two documents are written by the same author`
  - reuse components from the previous work

## General Architecture

Our approach consists in training a set of 5 x N individual learners, with N learners obtained from each of the five distinct methods (we call them strategies) that we have implemented (see §4). Every model obtained at the end of this stage is a full “authorship verification system”, in the sense that, given a set of problems as input, it provides a set of scores in [0, 1] as answers. Then the training of the meta-learner takes place, which consists in selecting the optimal subset of individual learners and the optimal way to combine their outputs together. Both training stages are carried out with a generic ge- netic algorithm, which evaluates models according to their performance obtained with cross-validation.

### Genetic Algorithm

Configuration key-value pairs:

$$
C = \{ p_1 \mapsto v_1, ..., p_n \mapsto v_n \}
$$

And a set of instances (problem input data) `S`, `C` and `S` together define a model `M` through training:

$$
f_{train}(C, S) = M
$$

In testing mode, configuration `C`, model `M` and an instance `s` define a unique prediction `p`:

$$
f_{test}(C, M, s) = p
$$

In the genetic algorithm, A multi-configuration associates multiple values to one parameter:

$$
MC = \{p_1 \mapsto \{v_1^1, ..., v_{m_1}^1\}, ..., p_n \mapsto \{v_1^n, ..., v_{m_n}^n\}\}
$$

- The first generation of configurations is initialized randomly: N configurations are selected among the possibilities described by the union of multi-configurations
- Then every generation is obtained based on the individual performance of the configurations from the previous generation:
  - the "breeders" are selected in a way such that the probability of a configuration being selected is proportional to its rank by performance.
  - For every new configuration, two parents are selected randomly among the breeders and every parameter is assigned the value of either one of the parents value, with the possibility of mutation.

Additionally, the algorithm allows for a proportion of the new generation to be selected fully randomly, and for a proportion of the best previous configurations to be cloned to the next one (elitism).

We had observed in: that the meta-parameters of the genetic algorithm do not have a major impact on its success or its speed. Thus we used the following fixed values:

- Proportion of selected breeders: 10%.
- Probability of mutation (by gene/parameter): 0.02.
- Proportion of cloned “elite” configurations: 10%.
- Proportion of new fully random configurations: 5%.

The convergence of the algorithm is tested by looking at the n latest windows of m generations (length), starting from the (n ⇥ m)th generation: the mean of the perfor- mance is computed for every window, and the stop criterion is met if the first window obtains the maximum performance (that is, the performance didn’t improve on the last n   1 windows). This simple method offers some useful flexibility: depending on the characteristics of the process (e.g., size of the hypothesis space, time needed to compute a generation), the process can be set to favor speed or a more exhaustive exploration of the search space.
