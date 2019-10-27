# Measuring Differentiability- Unmasking Pseudonymous Authors

## Abstract

- test the rate of degradation of the accuracy of learned models as the best features are iteratively dropped from the learning process.

## Introduction

problems of authorship verification on long texts.

- the negative examples is easy to fetch but the range of examples is wide and some cases cannot represent the `whole negative class`
- we can chop a large text into chunks so we have many small cases from the same author.

## Authorship Attribution with Two Candidates

features lists:

- frequencies of function words (Mosteller and Wallace 1964)
- syntactic structures (Baayen et al., 1996; Stamatatos et al., 2001)
- parts-of-speech n-grams (Koppel et al., 2002)
- complexity and richness measures (such as sentence length, word length, type/token ratio) (Yule 1938; Tweedie and Baayen 1998; De Vel et al., 2002)
- syntactic and orthographic idiosyncrasies (Koppel and Schler 2003)

using features to form vectors, use learning methods:

- multivariate analysis
- decision trees
- neural networks

linear separators work well for text categorization:

- Naïve Bayes (Mosteller and Wallace 1964; Peng et al., 2004)
- Winnow and Exponential Gradient (Lewis et al., 1996; Dagan et al., 1997; Koppel et al., 2002)
- linear support vector machines (SVM) (Joachims 1998; De Vel et al., 2002; Diederich et al., 2003)

## Authorship Verification: Naïve Approaches

- Lining up impostors: impostors imitating the style can affect the classification result.
- One class learning: apply a one-class learner, such as a one-class support vector machine (Chang and Lin 2001), that finds an optimal boundary that circumscribes all positive examples of A
- Comparing A directly to X: using cross-validation to classify A and X. If find one solution with high accuracy. Then we can say A did not write X.

the methods above need improvement.

## A New Approach: Unmasking

> if A and X are by the same author, then whatever differences there are between them will be reflected in only a relatively small number of features, despite possible differences in theme, genre and the like.

1. baseline using one-class SVM (Chang and Lin 2001)
   - using SVM kernel: [RBF](https://en.wikipedia.org/wiki/Radial_basis_function_kernel)
2. then `unmasking` applied:
   1. step 1: SVM classification
   2. step 2: drop kth most important positive/negative features (so 2k features dropped)
   3. it's a iteration, do the step 1 again.
   4. we can see when most important features dropped, the accuracy of the true author drops.
3. Meta-learning: Identifying Same-Author Curves:
   1. extract features of curves from SVM classification iterations
   2. features:
      1. accuracy after 6 elimination rounds is lower than 89% and
      2. the second highest accuracy drop in two iterations is greater than 16%.

Accuracy Results: Leave-one-book-out Tests

- TODO: the table in the paper need more cases to show the relation of accuracy to other parameters

## Extension: Using Negative Examples

- train on original author with his/her 'impostors'
- then judge the questioned text.

- the `same-author` result is about the same
- the `different-author` result accuracy drops.

> In short, the basic impostors method often wrongly concludes that a given author wrote a given book, but when it concludes that a given author did not write a given book (because some impostor looks more plausible), it is almost always correct.

combining the `unmasking` and `imporstor` involved training, the algorithm:

```
Given: anonymous book X, works of suspect author A, (optionally)impostors {A1,...,An}

Step 1 - Impostors method (optional)

if impostors {A1,...,An} are given then {
  Build model M for classifying A vs. all impostors
  Test each chunk of X with built model M
  for each impostor Ai {
    Build model Mi for classifying Ai vs. {A 'U' all other impostors}
    Test each chunk of X with built model Mi
  }
  If for some Ai number of chunks assigned to Ai > number of chunks assigned to Ai {
    return diffrent-author
  }
}

Step 2 - Unmasking

Build degradation curve <A,X>
Represent degradation curve as feature vector (see text)
Test degradation curve vector (see text)
  if test result positive
    reutrn same-author
  else
    return diffrent-author

Method Build Degradation Curve:

Use 10 fold cross validation for A against X
for each fold {
  Do m iterations {
    Build a model for A against X
    Evaluate accuracy results
    Add accuracy number to degradation curve <A, X>
    Remove k top contributing features (in each direction) from data
  }
}

```

## Effects of Topic Variability on Unmasking

- not applicable on `same author diffrent topic` problems.

## An Alternative Measure of Depth of Difference

- the infomation gain curve:
  - less key features but more inportance
