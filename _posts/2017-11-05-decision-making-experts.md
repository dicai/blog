---
layout: post
title: Online decision making under total uncertainty
author: Diana Cai
tags:
- computer science
- algorithms
summary: In this post, we will discuss a few simple algorithms for online decision making with expert advice. In particular, this setting assumes no prior distribution on the set of outcomes, but we use hindsight to improve future decisions. The algorithms discussed include a simple deterministic and randomized majority weighted decision algorithm,
---

In this post, we will discuss a few simple algorithms for online decision making with expert
advice. In particular, this setting assumes no prior distribution on the set of
outcomes, but we use hindsight to improve future decisions. The algorithms discussed include a simple deterministic and randomized majority weighted decision algorithm.

Lastly, we discuss a randomized algorithm called the _multiplicative weights algorithm_. This
algorithm has been discovered in a number of fields, and is the basis of many
popular algorithms, such as the Ada Boost algorithm in machine learning and
game-playing algorithms in economics.

This post mostly follows [1] and [2], which contain much more detail on this subject.
In particular, we will omit proofs and refer to these references for the details.

# Overview

Consider a setting with $$T < \infty$$ rounds. During each round, you get a finite set of actions you can take, e.g.,
$$\mathcal{A} = \{0,1\}$$, and associated with each action is some cost
associated with it, that is revealed after taking the action. We would like to
design a policy that minimizes our cost (or maximizes the reward).

For example: consider the scenario of predicting whether or not a single stock's price
will go up or down. Thus, each round is a day, and the action we take is binary,
corresponding to up/down. At the end of the day, we observe the final price of
the stock: if we make a correct prediction, we lose nothing, but if we make an
incorrect prediction, we lose 1 dollar.

We will consider the setting of _total uncertainty_, where we a priori have
no knowledge of the distribution on the set of outcomes, e.g., due to lack of
computational resources or data.

We will consider a few algorithms based on knowledge of $$n$$ experts.

# Predictions with expert advice

Consider again the example of predicting a stock's price, whose movement can be _arbitrary_
or _adversarial_ (which comes up, in practice, in a variety of other settings).
But, we get to view the predictions of $$n$$ experts (who may or may not be good
at predicting and could even be correlated in some manner).

We would like to design an algorithm that limiting the total cost -- i.e., bad predictions -- by
limiting it to be about the same as the _best_ expert. Because we do not know who
the best expert is until the end, we need some way of maintaining and updating
our belief of the best expert so that we can make some prediction in each round.

## Predicting with the majority

### Deterministic algorithm
The simplest algorithm is to just predict according to the majority prediction
of the experts: if most experts predict the price will go up, we will also
predict the price will go up. But what happens if the majority is wrong every
single day? Then, we will lose money every day.

Instead, we can maintain a weight for each expert $$w_i$$, that is initially 1
for all experts, but that we decay every time the expert makes a mistake in the
prediction. Then, our action is to predict according to the _weighted majority_,
which will downweight the predictions of the bad experts. Thus, the algorithm
will predict, at each round, according to the decision with the highest total
weight of the experts.

Let $$\eta \in (0,1)$$ be a parameter such that if the expert makes a mistake,
we will decay their weight by $$(1-\eta)$$, i.e., for the $$i$$th expert, we have
for the $$t$$th round

$$w_i^{(t+1)} = (1-\eta) \, w_i^{(t)}.$$

Then, after $$T$$ steps, if $$m_i^{(T)}$$ is the number of mistakes from expert
$$i$$, we have following bound on the number of mistakes of our algorithm $$M^{(T)}$$:
for all $$i$$, we have

$$M^{(T)} \leq 2(1+\eta) \, m_i^{(T)} + 2 \frac{\log n}{\eta}.$$

Note that the _best_ expert will have the fewest number of mistakes $$m_i^{(T)}$$,
and that the bound holds for all experts. Thus, the number of mistakes the
algorithm makes is roughly a little less than twice the number of mistakes of
the best expert (only the first term depends on $$T$$).


### Randomized algorithm

It turns out we can do even better if we convert the above algorithm to a
randomized algorithm. Here, instead of predicting with the weighted majority,
we will predict with the weighted majority with probability proportional to the
weight. For instance, if the total weight of the experts predicting "up" is
$$\frac{3}{4}$$, then instead of predicting up, our algorithm will instead
predict up with probability proportional to $$\frac{3}{4}$$.

For this algorithm, we instead have the bound

$$M^{(T)} \leq (1+\eta) \, m_i^{(T)} + 2 \frac{\log n}{\eta},$$

which is a factor of 2 less (in the first term) than the above deterministic
algorithm. Thus, this algorithm will perform roughly on the same order as the
best expert.


# Multiplicative weights


Now, we consider a more general setting. Here we will choose one decision in
each round out of $$n$$ possible decisions, and each decision will incur a
_cost_, which is revealed after _making_ the decision. Above, we studied the
special case where each decision corresponds to a choice of an expert, and
the cost $$m_i^{(t)}$$ is 1 for a mistake, and 0 otherwise. Here we will instead
consister costs that can be in $$[-1,1]$$.


A naive strategy would be to pick a decision randomly; the expected penalty is
that of the average decision. But, if a few decisions are better, we can observe
this as the costs are revealed, and upweight those better decisions so that we
can pick them in the future. This motivates the multiplicative weight algorithm,
which has been discovered independently in many fields, e.g., machine learning, optimization, and game theory.
The goal is to design an algorithm that, in the long run, has total expected cost roughly on the
order of the best decision, i.e., $$\min_i \sum_{t=1}^T m_i^{(t)}$$.

Again, we will maintain a weighting of the decisions $$w_i^{(t)}$$, where all weights initially are set to 1.
At each round $$t=1,\ldots,T$$, we have a distribution $$p^{(t)}$$ over a
set of decisions
\\[
    p^{(t)} = \left\\{\frac{w_1^{(t)}}{\Phi^{(t)}}, \ldots, \frac{w_n^{(t)}}{\Phi^{(t)}} \right\\},
\\]
where $$\Phi^{(t)} = \sum_i w_i^{(t)}$$ is the normalization term.

For each round $$t=1,\ldots,T$$, we iterate the following:

1. Randomly select a decision $$i$$ from $$p^{(t)}$$ (thus, each decision
is chosen with probability proportional to its weight $$w_i^{(t)}$$).

2. The decision is made, and the cost vector $$m^{(t)}$$ is revealed, where
the $$i$$th component correponds to the cost of decision $$i$$ (with cost $$m_i^{(t)} \in [-1,1]$$). The costs could be chosen arbitrarily by nature.

3. Update the weights of the costly decisions: for each decision $$i$$, set
\\[
w_i^{(t+1)} = w_i^{(t)} (1 - \eta \, m_i^{(t)}),
\\]
where $$\eta \leq \frac{1}{2}$$ is fixed in advance.
Here, the multiplicative term $$(1-\eta m_i^{(t)})$$ is less than 1 (thus, a
decay) if there is a larger cost, but if the cost is negative, this will increase the weights. A cost of 0 would not change the weight at all.


The expected cost of the algorithm from sampling decision $$i \sim p^{(t)}$$ is
\\[
E_{i \in p^{(t)}}(m_i^{(t)}) = \langle m^{(t)}, p^{(t)} \rangle,
\\]
i.e., the sum of the costs weighted by the probability of sampling each respective decision.
The _total expected cost_ is the sum of the expected cost for each round:
\\[
\sum_{t=1}^T \langle m^{(t)}, p^{(t)}\rangle.
\\]
We can now consider a bound for this value.

## Bound for the expected total cost

Assuming all costs $$m_i^{(t)}$$ lie in $$[-1,1]$$, and that $$\eta \leq 1/2$$,
then we have the following bound after $$T$$ rounds: for any decision
$$i$$,

\\[
\sum_{t=1}^T \langle m^{(t)}, p^{(t)}\rangle
\leq
\sum_{t=1}^T m_i^{(t)} + \eta \sum_{t=1}^T |m_i^{(t)}| + \frac{\log n}{\eta}.
\\]


# References

0. Arora. [Advanced Algorithms notes](https://www.cs.princeton.edu/courses/archive/fall16/cos521/Lectures/lec8.pdf).
1. Arora, Hazan, Kale. [The multiplicative weights update method: a meta
   algorithm and its applications](http://theoryofcomputing.org/articles/v008a006/).
2. Borodin and El Yaniv. Online computation and competitive analysis.
