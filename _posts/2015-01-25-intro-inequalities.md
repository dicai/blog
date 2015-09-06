---
layout: post
title: Important inequalities for probabilistic methods
---
In statistics, machine learning, theoretical computer science, and anything that incorporates randomness, we are interested in studying its behavior
(e.g., asymptotic convergence rates, approximation error) using probabilistic tail bounds.

Bounding the tail distribution, the probability that a random variable assumes values that are far from its expectation.
These bounds are the major tool for estimating the failure probability of algorithms and for establishing high probability bounds on their run time.

In this post, we discuss a few important inequalities that are frequently used and fundamental tools for analyzing probabilistic methods.

### Markov's Inequality

Markov's inequality is often too weak to use directly, but it used extensively for developing more sophisticated bounds, such as Chebyshev and Chernoff bounds,
which we discuss later. Markov's inequality is tight, i.e., it provides the best possible bound when we only know (1) the expectation of a random variable and
(2) the random variable is non-negative.

Let \\(X\\) be a random variable that assumes only non-negative values, and
assume that \\(\mathbb{E}[X]\\) exists. Then, for all \\(a > 0\\),

$$\Pr(X \geq a) \leq \frac{\mathbb{E}[X]}{a}.$$

We can see that this is true by considering the indicator variable \\(I\\) that
is 1 when \\(X\geq a\\) and 0 otherwise. Because \\(X\geq 0, a\geq 0\\), when
\\(X\geq a\\),
\\(\frac{X}{a} \geq I\\), and when \\(X < a\\), \\(\frac{X}{a}\\) is also
greater since \\(I\\) is 0. Thus, Markov's inequality follows by basic rules of probability and expectation:

\\[\Pr(X\geq a)=\mathbb{E}[I]\leq\mathbb{E}[\frac{X}{a}]=\frac{\mathbb{E}[X]}{a}.\\]

For example: Suppose we flip a coin $$n$$ times, $$X_1, X_2, \ldots, X_n$$, where $$X_n=1$$ if we have heads and $$X_n=0$$ if tails. Let $$X$$ be the total number of heads. The expectation of all $$n$$ flips is given by $$np$$, where $$p$$ is the probability of heads. The probability of obtaining a fraction of $$k$$ heads in the sequence is given by Markov's inequality:

$$\Pr( X \geq kn) \leq \frac{np}{kn} = \frac{p}{k}.$$

### Chebyshev's Inequality

If we know the first two moments of a random variable, we can compute both its expectation and variance.
Chebyshev's inequality bounds the probability of the distance of $$X$$ from its expectation $$\mathbb{E}[X]$$. For any $$a > 0$$, we have
\\[\Pr(|X - \mathbb{E}[X]| \geq a) \leq \frac{\text{Var}[X]}{a^2}.\\]

This follows from the direct application of Markov's inequality to
\\[ \Pr(|X - \mathbb{E}[X]|^2 \geq a^2) . \\]

Alternatively, we can express Chebyshev's inequality in terms of a constant factor of the random variables expectation:
\\[ \Pr(|X - \mathbb{E}[X]| \geq t \mathbb{E}[X]) \leq \frac{\text{Var}[X]}{t^2 (\mathbb{E}[X])^2},\\]

or standard deviation:
\\[\Pr(|X - \mathbb{E}[X]| \geq t \sigma[X]) \leq \frac{1}{t}.\\]

Chebyshev's inequality is often used in the analysis of asymptotic convergence.

Example: The Weak Law of Large Numbers (WLLN) states that for a sequence of iid random variables
$$X_1, X_2, \ldots$$ with mean $$\mu$$ and standard deviation $$\sigma$$, we have
\\[\lim_{n\rightarrow\infty}\Pr\left(\left|\frac{\sum_n X_n}{n}-\mu\right|>\epsilon\right) = 0.\\]

This can be seen by applying Chebyshev's inequality to the left-hand probability expression and taking the limit.

### Chernoff Bounds

Chernoff bounds are a style of bounds that uses Markov's inequality on the moment generating function (MGF) of a random variable,
giving exponentially decreasing bounds on the tail probability. For random
variable $$X$$, we apply Markov's inequality to $$e^{tX}$$ for some value of $$t$$: for $$t> 0$$,
\\[\Pr(X \geq a) = \Pr(e^{tX} \geq e^{ta}) \leq \frac{\mathbb{E}[e^{tX}]}{e^{ta}}.\\]

In particular, $$\Pr(X \geq a)$$ is bounded by the value of the right-hand expression with the minimum $$t >0$$.
We can derive similar bounds for $$t < 0$$ for $$\Pr(X \leq a)$$.

Chernoff-style bounds are often applied for bounding the tail distribution of the sum of independent $$0-1$$ random variables, or
Poisson trials (or Bernoulli trials when the variables are iid). Let $$X_1, X_2, \ldots, X_n$$ be a sequence of independent Poisson trials,
where $$p_n = \Pr(X_n = 1)$$, and let $$X = \sum_n X_n$$, with $$\mu = \mathbb{E}[X] = \sum_n p_n$$.

The goal is to bound the probability that the distance between $$X$$ and its
expectation is greater some $$\delta\mu$$, i.e.,
we want bounds on $$\Pr(X \geq (1+\delta)\mu)$$ and $$\Pr(X \leq (1-\delta)\mu)$$.

The MGF of $X$ is bounded by $$\exp{(e^t-1)\mu}$$, which can be seen by
computing the product of the MGF for each $$X_n$$  and bounding the individual terms.

We have the following Chernoff bounds for deviations above the mean by applying
Markov's inequality using the MGF of $$X$$:

For any $$\delta > 0$$,
\\[ \Pr(X \geq (1+\delta)\mu) < \\\{\left( \frac{e^\delta}{(1+\delta)^{1+\delta}} \right)\\\}^{\mu}.\\]
For $$0 < \delta \leq 1$$,
\\[ \Pr(X \geq (1+\delta)\mu) \leq \exp\left\\{\frac{-\mu\delta^2}{3}\right\\}.\\]
For $$R \geq 6 \mu$$,
\\[\Pr(X \geq R) \leq 2^{-R}.\\]

Similarly, for deviations below the mean, we have, for $$0 < \delta < 1$$:
\\[ \Pr(X \leq (1-\delta)\mu) < {\left(\frac{e^{-\delta}}{(1-\delta)^{1-\delta}}\right)}^{\mu}.\\]
\\[ \Pr(X \leq (1-\delta)\mu) \leq \exp\left\\{\frac{-\mu\delta^2}{2}\right\\}.\\]

Some of the upper and lower bounds above can be used to derive the following form of the  Chernoff bound: for $$0 < \delta < 1$$,
\\[\Pr(|X-\mu| \geq \delta\mu) \leq 2 \exp\{\frac{-\mu\delta^2}{3}\}.\\]

When we don't have the exact expectation $$\mathbb{E}[X]$$ available, we can use the
inequalities $$\mu \geq \mathbb{E}[X]$$ and $$\mu \leq \mathbb{E}[X]$$ instead.

Chernoff bounds are extremely powerful and used to give exponentially decreasing bounds on the tail probabilities in a number of randomized algorithms.
From the simple example of independent coin flips, we get an exponentially smaller bound than using Chebyshev's inequality.

#### Sources:

Mitzenmacher and Upfal. Probability and computing: Randomized algorithms and probabilistic analysis. Cambridge University Press, 2005.

Motwani and Raghavan. Randomized algorithms. Chapman & Hall/CRC, 2010.

Wasserman, Larry. All of statistics: a concise course in statistical inference. Springer, 2004.
