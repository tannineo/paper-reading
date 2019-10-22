# A Simple Measure to Assess Non-response

## Abstract

- some times `not responding` or `not to answer` is better than a wrong answer in a some scenarios like `classification` problems.
- a measure called `c@1` propoesed.

## Introduction

- in machine learning, choosing wrong answers should be punished, while not giving the answer is better than a wrong answer but worse than a right answer.

## Looking for the Value of Not Responding

### The example - Reading Comprehension Problem

- there are several questions
- each question has several options
- one option is correct
- additional rules:

  - reward to the `right answer`
  - punishment to the `wrong answer`
  - no action to `not responding`

- $n_{ac}$ for correct answer, get `1` score
- $n_{aw}$ for wrong answer, get `-1` score
- $n_{u}$ for the not answered, get `0` score

$n = n_{ac} + n_{aw} + n_{u}$, the measure:

$$
UF = \frac{1}{n} \sum\limits_{i=1}^n U(i) = \frac {n_{ac} - n_{aw}}{n}
$$

We use this measure to from a `ranking fomula` and add a constant(1) to it like this:

$$
Ranking = \frac{n_{ac} - n_{aw}}{n} + 1 \\
= \frac{n_{ac} - n_{aw} + n}{n} \\
= \frac{2n_{ac} + n_u}{n}
$$

We can see the unanswerd problems has the `half value` of the correct answer.

### A rationale for the Value of Unanswered Questions

> Unanswered questions have the same value
> as if a proportion of them would have been answered correctly

$$
P(C) = P(C \cap A) + P(C \cap \lnot A) \\
= P(C \cap A) + P(C / \lnot A) * P(\lnot A) \\
$$

inside we have:

- $P(C \cap A) = \frac{n_{ac}}{n}$
- $P(\lnot A) = \frac{n_u}{n}$
- $P(C / A) = \frac{n_{ac}}{n - n_u}$

### `c@1` - the propoesed measure

$$
c@1 = \frac{n_{ac}}{n} + \frac{n_{ac}}{n} \frac{n_u}{n} = \frac{n_{ac}}{n} (1 + \frac{n_u}{n})
$$

- when $n_u = 0$: the traditional accuracy
- $n_u$ has the value
- when $n_{ac} = 0$: the system will receive a `0` score

### Why not $P(C / \lnot A) = P(\lnot C / \lnot A) = 0.5$

so the equation will be:

$$
P(C) = P(C \cap A) + P(C \cap \lnot A) \\
= P(C \cap A) + P(C / \lnot A) * P(\lnot A) \\
= P(C \cap A) + 0.5 * P(\lnot A) \\
= \frac{n_{ac}}{n} + 0.5 * \frac{n_u}{n}
$$

- not fair
- we should encourage the `not given` answers on wrong answers

### Why not $P(C / \lnot A) = P(C / A)$

so the equation will be:

$$
P(C) = P(C \cap A) + P(C \cap \lnot A) \\
= P(C / A) * P(A) + P(C / \lnot A) * P(\lnot A) \\
= P(C / A) * P(A) + P(C / A) * P(\lnot A) \\
= P(C / A) = \frac{n_{ac}}{n_{ac} + n_{aw}}
$$

nothing related to `the not answered`, and the system will tend to give the answer when it's 100% sure.

## Evaluation of `c@1`

- similar stability & discrimination power with `accuracy`
- sensitivity is higher than the `accuracy`

## Related Work

- `Accuracy`
- Mean Reciprocal Rank (MRR)
- Confidence Weighted Score (CWS)
- a explict self score

## Conclusion

> Unanswered questions have the same value as if a proportion of them had been answered correctly, and the value they add is related to the performance (accuracy) observed over the answered questions.

Non-response must be assessed if we want to measure effective reading and not just the ability to rank options.
