---
layout: post
title: The Extended Schwartz Theorem and strong posterior consistency
author: Diana Cai
tags:
- statistics
- probability
- nonparametricbayes
- Bayesian asymptotics
summary: Schwartz's theorem is a classical tool used to derive posterior consistency and is the foundation of many modern results for establishing frequentist consistency of Bayesian methods. An extension of Schwartz's original theorem makes it much more broadly applicable. In this post, we review the extended Schwartz theorem, show how it can be used to recover the classical Schwartz theorem, and how it can be used to establish "strong" posterior consistency.
---

[Schwartz's theorem](https://www.dianacai.com/blog/2021/02/14/schwartz-theorem-posterior-consistency/) is a classical tool used to derive posterior
consistency and is the foundation of many modern results for establishing
frequentist consistency of Bayesian methods.
As we discuss in [our post on the original Schwartz result](https://www.dianacai.com/blog/2021/02/14/schwartz-theorem-posterior-consistency/),
the theorem itself had somewhat limited applicability; it was straightforward to use to
establish weak consistency, provided the KL support condition on the prior
holds, but was generally not enough to guarantee posterior consistency with
respect to strong metrics, such as the L1 distance.
This is because the uniformly consistent tests do not always exist for other
metrics.

But an extension of Schwartz's original theorem makes it much more broadly
applicable. In this post, we review the extended Schwartz theorem, show how it
can be used to recover the classical Schwartz theorem, and how it can be used to
establish "strong" posterior consistency.
For an introduction to posterior consistency and basic definitions, see
[our post on the original Schwartz result](https://www.dianacai.com/blog/2021/02/14/schwartz-theorem-posterior-consistency/).


# Preliminaries and notation


We consider the same i.i.d. modeling setting as in our discussion on classical Schwartz.
Let \\(\mathcal{P}\\) denote our model class, which is a
space of densities
with respect to a \\(\sigma\\)-finite measure \\(\mu\\),
where \\(p: \mathbb{X} \rightarrow \mathbb{R}\\) is a measurable function that
is nonnegative and integrates to 1.
We denote the distribution
of a density \\(p \in \mathcal{P}\\) as \\(P\\), i.e., \\(p = \frac{dP}{d\mu}\\).
Denote the joint distribution of \\(n \in \mathbb{N} \cup \\{\infty\\} \\) samples by
\\(P^{(n)}\\).

Let \\(\Pi\\) be a prior distribution on our space of models \\(\mathcal{P}\\),
    consider the following Bayesian model:

$$
\begin{align}
p &\sim \Pi \\
X_1,\ldots,X_n \,|\, p &\stackrel{i.i.d.}{\sim} p,
\end{align}
$$

where each \\(X_i \in \mathbb{X}\\).
In this post, we assume the model is _well-specified_ and that there is some true
density \\(p_0 \in \mathcal{P}\\) from which the data are generated.

Under certain regularity conditions on \\(\mathcal{P}\\),
(a version of) the posterior distribution, \\(\Pi(\cdot \,|\, X_1,\ldots, X_n)\\),
can be expressed via the Bayes's formula:
for all measurable subsets \\(A \subseteq \mathcal{P} \\),

$$\begin{align}
\Pi(A \,|\, X_1,\ldots, X_n)
    = \frac{\int_{A} \prod_{i=1}^n p(X_i) \,d\Pi(p)}{\int_{\mathcal{P}} \prod_{i=1}^n p(X_i) \,d\Pi(p)}.
\end{align}$$


# The Extended Schwartz Theorem

The statement of the theorem in Ghosal and van der Vaart has two parts;
here we state the first part below as a theorem --
which provides tools for more general results --
and the second part as a corollary -- which leads to insights directly about posterior consistency.
Lastly, we'll discuss how to prove the classical Schwartz's theorem using the
extended version, and how to get results on strong posterior consistency.

**Theorem (Extended Schwartz).**
Suppose there exists a set
\\( \mathcal{P}\_0 \subseteq \mathcal{P} \\)
and a number \\(c\\) with
\\(\Pi(\mathcal{P}\_0) > 0 \\)
and
\\(K(p_0; \mathcal{P}\_0) \leq c. \\)
Let
\\(\mathcal{P}\_n \subseteq \mathcal{P}\\)
be a set that satisfies
either condition (a) or condition (b) for some constant \\(C > c\\):

(a) There exist tests \\(\phi_n\\) such that

$$
\begin{align}
\phi_n \stackrel{n\rightarrow\infty}{\longrightarrow} 0, ~~P_0^{(\infty)}\text{-a.s.},
    \quad
    \text{and}~~
\int_{\mathcal{P}_n} P^{(n)}(1-\phi_n) \, d\Pi(p) \leq e^{-Cn}.
\end{align}
$$


(b)
    The prior satisfies
$$
\begin{align}
\Pi(\mathcal{P}_n) \leq e^{-Cn}.
\end{align}
$$

Then

$$
\begin{align}
\Pi(\mathcal{P}_n \,|\, X_{1:n}) \stackrel{n\rightarrow\infty}{\longrightarrow} 0, \quad P_0^{(\infty)}\text{-a.s.}
\end{align}
$$


### Remarks on theorem statement


The theorem above provides some conditions under which the posterior
probability of the set \\(\mathcal{P}\_n \\) goes to 0 with probability 1.
At the expense of its greater generality, this version of the theorem may as a
result appear more mysterious in its application.

First recall that \\(\mathcal{P}\\) is the space of densities of our model
class. The statement describes behaviors for two general subsets of densities
\\(\mathcal{P}\_0\\) and \\(\mathcal{P}\_n\\):
- What are the sets \\(\mathcal{P}\_0\\)?
    These sets show up in conditions on the prior / KL divergence bound and
    serve as a prior support condition.
    E.g, it is applied to KL neighborhoods in the classical Schwartz theorem.

- What are the sets \\(\mathcal{P}\_n\\)?
    These sets are present in the conditions (a) and (b) as well as in the asymptotic result.
    The theorem allows us to establish when the posterior probability of a  _general subset_
    \\(\mathcal{P}\_n\ \subseteq \mathcal{P} \\) is going 0 a.s., rather than a
    _specific subset_ needed to show consistency (e.g., a neighborhood of \\(p_0\\)).
    As we'll see below, we'll apply this to show posterior consistency by
    decomposing the complement of a neighborhood \\(U^c\\) into a union of two
    other subsets, and apply this general theorem to each of the other subsets.



Regarding the conditions (a) and (b), note that either (a) _**or**_ (b) needs to
    hold to imply the result.
    First note that condition (b) a special case of condition (a) when \\(\phi_n = 0\\),
    but serves as a useful restatement of (a), as we'll see in the proof of the
    corollary.
    Thus, in order to prove
    \\(
        \Pi(\mathcal{P}\_n \,|\, X_{1:n}) \stackrel{n\rightarrow\infty}{\longrightarrow} 0 ~(P_0^{(\infty)}\text{-a.s.}),
    \\)
    we only need to assume condition (a) holds.

**Condition (a).** These two conditions should look familiar and close to the
classical Schwartz testing conditions.
One condition that is commonly used to verify the classical Schwartz theorem is
that the sequence of tests have **exponentially small
error probabilities** (Ghosh and Ramamoorthi [2], Proposition 4.4.1):
i.e., for some \\(C > 0\\),

$$\begin{align}
P_0^{(n)}(\phi_n) \leq e^{-Cn}, \qquad \sup_{p \in \mathcal{P}_n} P^{(n)}(1- \phi_n) \leq e^{-Cn},
\end{align}$$

where in the classical Schwartz theorem, \\(\mathcal{P}\_n = U^c\\).

Here \\(P_0^{(n)}(\phi_n) \leq e^{-Cn}\\) implies,
     via the Borel-Cantelli lemma, the first part of the condition in the extended
     Schwartz theorem, i.e., that  \\(\phi_n \rightarrow 0\\) a.s.
And in the extended Schwartz theorem, the second part of the condition replaces
\\(\sup_{p \in U^c} P^{(n)}(1- \phi_n) \leq e^{-Cn}\\)
    with an integral against the prior distribution \\(\Pi\\) over the set of
    densities in \\(\mathcal{P}\_n\\).




**Condition (b).** This condition essentially says that if \\(\mathcal{P}\_n\\)
    is a set that the prior assigns a small amount of mass to, then
    asymptotically, the
    posterior will also assign a small amount of mass to that set.



### Proof of theorem

The proof itself follows similar steps to that of the proof of the classical Schwartz theorem; see
our [post on the classical Schwartz for additional details](https://www.dianacai.com/blog/2021/02/14/schwartz-theorem-posterior-consistency/).
We include a sketch below for completeness.

<details>
   <summary style="color:maroon;font-size:14pt">_(Expand for proof sketch)_
   </summary>
Since the test functions \\(\phi_n \in [0,1]\\), we can upper bound the posterior from above as

$$\begin{align}
\Pi(\mathcal{P}_n \,|\, X_1,\ldots, X_n)
    &\leq
    \phi_n + \frac{(1- \phi_n) \int_{\mathcal{P}_n} \prod_{i=1}^n \frac{p(X_i)}{p_0(X_i)} \,d\Pi(p)}{\int_{\mathcal{P}} \prod_{i=1}^n \frac{p(X_i)}{p_0(X_i)} \,d\Pi(p)}.
\end{align}$$

The first term \\(\phi_n\rightarrow 0\\) in \\(P_0^{(\infty)}\\)-a.s. by the first
part of assumption (a).

Using very similar steps as the classical Schwartz proof,
the denominator is bounded below as follows: for any \\(c' > c\\), eventually \\(P_0^{(\infty)}\\)-a.s.,

$$\begin{align}
    \int_{\mathcal{P}} \prod_{i=1}^n \frac{p(X_i)}{p_0(X_i)} \,d\Pi(p)
    \geq \Pi(\mathcal{P}_0) e^{-c' n}.
\end{align}$$

Applying Fubini's theorem, we can bound the probability of the numerator as follows:

$$\begin{align}
P_0^{(n)}\left(
        (1- \phi_n) \int_{\mathcal{P}_n} \prod_{i=1}^n \frac{p(X_i)}{p_0(X_i)} \,d\Pi(p)
        \right)
   &=
   \int (1 - \phi_n) \int_{\mathcal{P}_n} \prod_{i=1}^n \frac{p(X_i)}{p_0(X_i)} \,d\Pi(p)  \, dP_0^{(n)}
     \\
    &=
     \int_{\mathcal{P}_n} \int (1 - \phi_n) \, dP^{(n)} \,d\Pi(p)
    \\
    &=
     \int_{\mathcal{P}_n} P^{(n)} (1 - \phi_n) \,d\Pi(p)
    \\
    &\leq  e^{-Cn},
\end{align}$$

where in the last line, we applied the second part of assumption (a).

Finally, applying Markov's inequality,
\\(\sum_{n \geq 1} e^{-n(C - c')} < \infty \\) for \\(C > c'\\),
and so by the Borel--Cantelli lemma, the numerator goes to 0 almost surely.

</details>

## Corollary: posterior consistency

The theorem above implies the following result on posterior consistency,
    which is more readily compared to the statement of the classical Schwartz theorem.


**Corollary (Extended Schwartz).**
Consider the model

$$
\begin{align}
p \sim \Pi, \qquad
X_{1:n} \,|\, p \stackrel{iid}{\sim} p \\
\end{align}.
$$

Suppose that
\\(p_0\\) is in the KL support of the prior, i.e.,
\\(p_0 \in \mathrm{KL}(\Pi)\\),
and that for every neighborhood \\(U\\) of  \\(p_0\\),
there exists a constant \\(C > 0\\),
measurable partitions
\\(\mathcal{P} = \mathcal{P_{n,1}} \sqcup \mathcal{P_{n,2}}\\)
<!--\\(\mathcal{P_n} = \mathcal{P_{n,1}} \cup \mathcal{P_{n,2}}\\)-->
and tests \\(\phi_n\\) such that the following conditions hold:

(i)
    The test functions satisfy

$$
\begin{align}
P_0^{(n)} \phi_n \leq e^{-Cn}
    \qquad
    \text{and}~~
    \sup_{p \, \in \, \mathcal{P}_{n,1} \cap U^c} P^{(n)}(1-\phi_n) \leq e^{-Cn}.
\end{align}
$$



(ii)
    The prior satisfies
$$
\begin{align}
\Pi(\mathcal{P}_{n,2}) \leq e^{-Cn}.
\end{align}
$$

Then the posterior is consistent at \\(p_0\\): i.e., for every neighborhood \\(U\\) of \\(p_0\\),

$$
\begin{align}
\Pi_n(U^c \,|\, X_{1:n})
\stackrel{n\rightarrow\infty}{\longrightarrow} 0, \quad \text{a.s.-}P_0^\infty.
\end{align}
$$


### Remarks on corollary statement

In particular, the conditions are essentially the same as the classical
Schwartz theorem, but now we split the space of densities \\(\mathcal{P}\\)
into (1) one part \\(\mathcal{P}\_{n,1}\\) that goes into the testing condition,
and (2) another part \\(\mathcal{P}\_{n,2}\\) that has small prior mass and therefore small posterior mass (and so does not need to be tested).
In the Bayesian asymptotics literature, the sequence of sets
\\(\\{\mathcal{P}\_{n,1}\\}\\) are often called _sieves_.


If we take \\(\mathcal{P}\_{n,1} = \mathcal{P}\\) and
\\(\mathcal{P}\_{n,2} = \emptyset\\), then the extended Schwartz conditions (i) and (ii) imply
that the same testing conditions as
classical Schwartz hold, i.e., that the test sequence is uniformly consistent.



### Proof of the corollary

The result follows from applying parts (a) and (b) separately from the theorem above.

<details>
   <summary style="color:maroon;font-size:14pt">_(Expand for proof)_
   </summary>

   Let \\(U\\) be a neighborhood with radius \\(\epsilon < C\\).
Note that the KL condition implies that if \\( \mathcal{P}\_0 = U \\),
     then \\(0 > \Pi(K_\epsilon(p_0)) \geq \Pi(U)\\)
    and that \\(K(p_0; \mathcal{P}_0) \leq \epsilon. \\)

Apply part (a) with
\\( \mathcal{P}\_0 = U \\)
    and
\\( \mathcal{P}\_n = U^c \cap \mathcal{P}\_{n,1} \\).
That is, suppose there there exist tests \\(\phi_n\\) such that

$$
\begin{align}
\phi_n \stackrel{n\rightarrow\infty}{\longrightarrow} 0, ~~P_0^{(\infty)}\text{-a.s.},
    \qquad
    \text{and}~~
\int_{U^c \cap \mathcal{P}_{n,1}} P^n(1-\phi_n) \, d\Pi(p) \leq e^{-Cn}.
\end{align}
$$

Then, we have that
\\(\Pi(U^c \cap \mathcal{P}\_{n,1} \,|\, X_{1:n}) \rightarrow 0 \\) a.s.


Now apply part (b) with
\\( \mathcal{P}\_0 = U \\)  and
\\( \mathcal{P}\_n = \mathcal{P}\_{n,2} \\).
Then, we have that
\\(\Pi(\mathcal{P}\_{n,2} \,|\, X_{1:n}) \rightarrow 0 \\) a.s.

Putting these together, we have
\\[
    \Pi(U^c \,|\, X_{1:n}) \leq
\Pi(U^c \cap \mathcal{P}\_{n,1} \,|\, X_{1:n}) +
\Pi(\mathcal{P}\_{n,2} \,|\, X_{1:n})
    \rightarrow 0, \quad P_0^{(\infty)}\text{-a.s.}
\\]
</details>


# Strong posterior consistency


In this section, we state a theorem that establishes _strong posterior consistency_, i.e.,
posterior consistency with the strong topology;
this result is  a consequence of applying the extended Schwartz theorem above.
_Note:_ the statement of this corollary in Ghosal and van der Vaart (2017) [1] uses the terminology
"strongly consistent" to refer to \\(P_0\\)-a.s. consistency, rather than
referring to convergence in the strong topology.

## Preliminaries: covering and metric entropy

In order to establish a more direct strong posterior consistency result,
   the (extended Schwartz)  testing condition is
replaced with a bound on the complexity of the space, which is measured by a
function of the _covering number_ \\(N(\epsilon, \mathcal{P}\_{n,1}, d)\\) with respect to the
set \\(\mathcal{P}\_{n,1} \subseteq \mathcal{P}\\). In order to define
the covering number, we need to first introduce another definition.

A set \\(S\\) is called an \\(\epsilon\\)-net for \\(T\\) if for every
\\(t \in T\\), there exists \\(s \in S\\) such that \\(d(s,t) < \epsilon\\).
This means that the set \\(T\\) is covered by a collection of balls of radius
\\(\epsilon\\) around the points in the set \\(S\\).
The **\\(\epsilon\\)-covering number**, denoted by
\\(N(\epsilon, T, d)\\), is the minimum cardinality of an
\\(\epsilon\\)-net.

The quantity \\(\log N(\epsilon, T, d)\\) is called _metric entropy_, and
a bound on this quantity is a condition that appears in many posterior concentration
results.



## Strong posterior consistency via extended Schwartz


Again we consider the model \\(X_{1:n} \,|\, p \stackrel{i.i.d.}{\sim} p\\) and \\(p \sim \Pi \\).
The following theorem leads to posterior consistnecy with respect to any distance
\\(d\\) that is bounded above by the Hellinger distance, e.g., the \\(\mathcal{L}\_1\\) distance.

**Theorem (strong consistency).**
Let \\(d\\) be a distance that generates convex balls and satisfies
\\(d(p_0, p) \leq d_H(p_0, p)\\) for every \\(p\\).
Suppose that for every \\(\epsilon > 0\\), there exist partitions
\\(\mathcal{P} = \mathcal{P}\_{n,1} \sqcup \mathcal{P}\_{n,2}\\)
and a constant \\(C > 0\\) such that, for sufficiently large \\(n\\),

1. \\( \log N(\epsilon, \mathcal{P}\_{n,1}, d) \leq n \epsilon^2, \\)

2. \\( \Pi(\mathcal{P}\_{n,2}) \leq e^{-Cn}. \\)

Suppose \\(p_0 \in \text{KL}\_\epsilon(\Pi)\\).
Then the posterior distribution is consistent at \\(p_0\\).


# References


1. Ghosal and van der Vaart (2017). _Fundamentals of Nonparametric Bayesian Inference_ (Cambridge Series in Statistical and Probabilistic Mathematics). Cambridge: Cambridge University Press.

2. Kleijn, van der Vaart, van Zanten. [_Lectures on Nonparametric Bayesian Statistics_](https://staff.fnwi.uva.nl/b.j.k.kleijn/NPBayes-LecNotes-2015.pdf)
