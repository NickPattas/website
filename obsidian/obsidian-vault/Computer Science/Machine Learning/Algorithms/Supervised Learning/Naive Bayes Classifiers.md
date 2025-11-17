### Key Features of Naive Bayes Classifiers

The main idea behind the Naive Bayes classifier is to use **Bayes' Theorem**

- The Naive Bayes Classifier is a *simple probabilistic classifier* and it has very *few number* of **parameters** which are used to build the ML models that can predict at a *faster speed* than other classification algorithms.
- It is a probabilistic classifier because *it assumes that one feature in the model is independent of existence of another feature*. In other words, each feature contributes to the predictions with *no relation between each other*.
- Naïve Bayes Algorithm is used in spam filtration, Sentimental analysis, classifying articles and many more.
#### Baye's Theorem

Bayes' theorem (also known as the Bayes Rule or Bayes Law) is used to **determine the conditional probability of event A when event B has already occurred**.

The general statement of Bayes’ theorem is “The conditional probability of an event A, given the occurrence of another event B, is equal to the product of the event of B, given A, and the probability of A divided by the probability of event B.” i.e.

$P(y∣X)=P(X)P(X∣y)⋅P(y)$

Where:
- $P(y∣X)P(y∣X)$: Posterior probability, probability of class $y$ given features $X$
- $P(X∣y)P(X∣y)$: Likelihood, probability of features $X$ given class $y$
- $P(y)P(y)$: Prior probability of class $y$
- $P(X)P(X)$: Marginal likelihood or evidence



![[Naive_Bayes_Classifier.ipynb]]


## **Further Reading**

* [What are Naive Bayes classifiers? (IBM)](https://www.ibm.com/think/topics/naive-bayes)
* [Naive Bayes](https://scikit-learn.org/stable/modules/naive_bayes.html#naive-bayes)
* [Naive Bayes Classifier (Wiki)](https://en.wikipedia.org/wiki/Naive_Bayes_classifier)
