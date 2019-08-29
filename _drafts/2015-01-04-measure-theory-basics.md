---
layout: post
title: Measure theory basics
summary: Those interested in machine learning may be wondering why they should be familiar with measure theory. One of the main reasons has to do with why we need measure theory for probability in general.
tags:
- probability
---
### Why Measure Theory?

Those interested in machine learning may be wondering why they should be familiar with measure theory.

One of the main reasons has to do with why we need measure theory for probability in general. Without measure theory, we are limited in the kinds of random variables we can have: for instance, we may wish to deal with random variables which are neither discrete nor continuous. In addition, there are restrictions on what types of sets for which we can define probabilities. For instance, for the uniform distribution on [0,1], it is not possible to define a probability on every single subset. For more discussion, see Rosenthal (2006, Ch. 1).

Though it may be true that machine learning researchers need not have extensive knowledge and practice of measure theory, it is important to be familiar with the language and terminology used, as research on Bayesian nonparametrics has grown in recent years.

In this post, we provide the basic definitions along with intuitive explanations for terms that will arise in future posts.

### Intro: Probability Spaces

Areas measure theory is most prevalent in machine learning research include probability and stochastic processes. We work with respect to some probability space, which is a triple $$(\Omega, \mathcal{A}, P)$$, where $$\Omega$$ is the sample space (set of elementary outcomes), $$\mathcal{A}$$ is the $$\sigma$$-algebra (set of measurable subsets, or "events"), and $$P$$ is the probability measure (measure where the total mass is 1).

We now define and describe these terms more generally.

### Measure Theory Basics

For most spaces we're interested in, e.g. the real line, we cannot define a measure over all subsets of the space, so we have to restrict ourselves to a family of subsets that is termed measurable.

A $$\sigma$$-algebra $$\mathcal{A}$$ (also called $$\sigma$$-field) is a family of subsets of a set $$\Omega$$ such that:

The $$\sigma$$-algebra $$\mathcal{A}$$ is not empty.
if $$A \in \mathcal{A}$$, then $$\Omega \setminus A \in \mathcal{A}$$, i.e., if a subset is in the $$\sigma$$-algebra, then its complement must be in the $$\sigma$$-algebra too.
if $$A_1, A_2, \ldots \in \mathcal{A}$$ then $$\cup_{i=1}^{\infty} A_i \in \mathcal{A}$$, i.e. any countable union of measurable sets is also measurable.
A measurable space is a pair $$(\Omega, \mathcal{A})$$ where $$\Omega$$ is some space and $$\mathcal{A}$$ is a $$\sigma$$-algebra in $$\Omega$$.

A measure $$\mu$$ over $$(\Omega, \mathcal{A})$$ is a function $$\mu: \mathcal{A} \rightarrow [0, \infty]$$ such that:

$$\mu(\emptyset) = 0$$, i.e., the measure of the empty set is 0.
$$if A_1, A_2, \ldots \in \mathcal{A}$$ are disjoint, then $$\mu(\cup_{i=1}^{\infty}) = \sum_{i=1}^{\infty} \mu(A_i)$$.
Recall that a probability measure is one in which $$\mu(\Omega) = 1$$, i.e. the measure of the whole space is 1. The measure gives the probability of the events, which are subsets of the space.

A measure space is a triple $$(\Omega, \mathcal{A}, \mu)$$, where the elements of the triple are some space $$\Omega$$, a $$\sigma$$-algebra $$\mathcal{A}$$, and the measure $$\mu$$.

Given two measurable spaces $$(S, \mathcal{S})$$ and $$(T, \mathcal{T})$$, a function $$f:S \rightarrow T$$ is called a measurable function if $$f^{-1}(\mathcal{T}) \subset \mathcal{S}$$, i.e., if $$f^{-1}(B) \in \mathcal{S}$$ for every $$B \in \mathcal{T}$$. In other words, a function $$f$$ is measurable if its pre-image $$f^{-1}$$ is measurable (for every measurable subset $$B \in \mathcal{T}$$, $$f^{-1}(B)$$ is also measurable).

For any measure $$\mu$$, the support $$\text{supp }\mu$$ is defined to be the smallest closed set $$F$$, where $$F$$ is a subset of a topological space $$S$$, with $$\mu(F^c) = 0$$. When the cardinality of the support is less than or equal to 1, we say that $$\mu$$ is degenerate.

A measure $$\mu$$ is said to be have an atom $$s\in S$$ if the set $$\{s\} \in\mathcal{S}$$ is measurable and $$\mu(\{s\}) > 0$$.

### Probability Measures

As before, we have a probability space $$(\Omega, \mathcal{A}, P)$$, where $$P$$ is a probability measure on $$(\Omega, \mathcal{A})$$ with probability mass 1, and the elements $$A \in \mathcal{A}$$ called are the events. A random element $$X$$ taking values in $$S$$ is a measurable function $$X:\Omega\rightarrow S$$. (Here $$S$$ could be $$\mathbb{R}, \mathbb{R}^d, \mathbb{R}^{\infty}$$, or a function space, leading to random variables, random vectors, random sequences, and random processes, respectively). The probability of an event $$A$$ is given by $$P(X \in A) = P(X^{-1}(A))$$.

A stochastic process (or random process) is a collection of random variables $$\{X_i\}_{i\in I},$$ where $$I$$ in an index set, which can be infinite (and uncountable). The Kolmogorov consistency theorem guarantees the existence of such a set of uncountably many random variables (under certain conditions).

Stochastic processes are important for many Bayesian nonparametric models. Some examples include Gaussian processes, Poisson processes, gamma processes, Dirichlet processes, and beta processes. In future posts, we will discuss these in more detail.

#### Sources and Additional Resources:

Billingsley, Patrick. Probability and measure. John Wiley & Sons, 2008.

Çinlar, Erhan. Probability and stochastics. Vol. 261. Springer, 2011.

Kallenberg, Olav. Foundations of modern probability. Springer, 2002.

Rosenthal, Jeffrey. A first look at rigorous probability theory. Vol. 2. Singapore: World Scientific, 2006.

Tao, Terence. An introduction to measure theory. Vol. 126. American Mathematical Soc., 2011.
