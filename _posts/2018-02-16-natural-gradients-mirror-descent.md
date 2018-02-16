---
layout: post
title: Natural gradient descent and mirror descent
author: Diana Cai
tags:
- statistics
- information geometry
summary: In this post, we discuss the natural gradient and present the main result of Raskutti and Mukherjee (2014), which shows that the mirror descent algorithm is equivalent to natural gradient descent in the dual Riemannian manifold.
---

In this post, we discuss the natural gradient, which is the direction of
steepest descent in a Riemannian manifold [1], and present the main result of
Raskutti and Mukherjee (2014) [2], which shows that the mirror descent algorithm is equivalent to natural
gradient descent in the dual Riemannian manifold.

# Motivation

## Steepest descent line search

Suppose we want to minimize some convex differentiable function
 \\(f: \Theta \rightarrow {\mathbb{R}}\\) . A common approach is to do a line
search using the steepest descent algorithm
$$\begin{aligned}
    \theta_{t+1} = \theta_t - \alpha_t \nabla f(\theta),\end{aligned}$$
where  \\(\alpha_t\\)  is the step-size and the direction we step in is the
gradient of the function.

However, in applications where the parameters lie on a non-Euclidean
Riemannian manifold[^1] with metric tensor  \\(H = (h_{ij})\\)  (an inner
product on the tangent space of the manifold at a point), the direction
of steepest descent is actually the *natural gradient*:

$$\begin{aligned}
    \theta_{t+1} = \theta_t - \alpha_t \underbrace{H^{-1} \nabla
    f(\theta)}_{\text{natural gradient}},\end{aligned}$$

where  \\(H\\)  is the Fisher information matrix for a statistical manifold. This update equation is called
*natural gradient descent*.


Natural Gradients
================

Recall that in an Euclidean space (with a orthonormal coordinate system)
 \\(\Theta={\mathbb{R}}^n\\) , the squared length of a small incremental
vector  \\(d\theta\\)  that connects  \\(\theta\\)  and  \\(\theta + d\theta\\)  is given by

$$\begin{aligned}
   ||d\theta||^2  = \langle d\theta, d\theta \rangle
    = \sum_{i \in [n]} (d \theta_i)^2.
\end{aligned}$$

But for a Riemannian manifold, the squared length is given by the quadratic form

$$
\begin{aligned}
    ||d\theta||^2 = \langle H d\theta, d\theta \rangle = \sum_{i,j \in [n]} h_{ij}(\theta) d\theta_i d\theta_j,
\end{aligned}
$$

where \\(H = (h_{ij})\\) is an \\(n \times n\\) matrix called the Riemannian
metric tensor (which depends on \\(\theta\\).
In the Euclidean case, we just get that \\(H = I_n\\).

In this Riemannian manifold, the direction of steepest descent of a
function \\(f(\theta)\\) at \\(\theta \in \Theta\\) is defined by the vector
\\(d\theta\\) that minimizes \\(f(\theta + d\theta)\\), where \\(||d\theta||\\) has
a fixed length, i.e., under the constraint

$$\begin{aligned}
   ||d \theta||^2 = \epsilon^2.
   \end{aligned}
$$


#### Theorem (Amari, 1998) [1]:

The steepest descent direction of \\(f(\theta)\\) in a Riemannian space is
given by

$$\begin{aligned}
    -\tilde\nabla f(\theta) = -H^{-1} \nabla f(\theta),
\end{aligned}$$

where \\(H^{-1} = (h^{ij})\\) is the inverse of the metric \\(H = (h_{ij})\\),
and \\(\nabla f\\) is the conventional gradient:

$$\begin{aligned}
    \nabla f(\theta) :=
    \begin{bmatrix}
        \frac{\partial}{\partial\theta_1} f(\theta) \\
        \vdots \\
        \frac{\partial}{\partial\theta_n} f(\theta)
    \end{bmatrix}.
\end{aligned}
$$


*Proof*:
Write \\(d\theta = \epsilon v\\), i.e., we decompose the vector into its
magnitude \\(\epsilon\\) and direction \\(v\\), and search for the vector
\\(v\\) that decreases the value of the function the most.

Writing the linearized function, we have
$$\begin{aligned}
    f(\theta  + d\theta ) = f(\theta) + \epsilon v^\top \nabla     f(\theta)
\end{aligned}$$

subject to the constraint that \\(||v||^2 = v^\top H v =1\\), i.e., \\(v\\) is a
unit vector representating just the direction.

Setting the derivative with respect to \\(v\\) of the Lagrangian to 0, i.e.,
$$\begin{aligned}
    \mathcal{L}(\theta,v,\lambda)
    =     \nabla_v
    \{ v^\top \nabla f(\theta) - \lambda v^\top H v\} = \nabla f(\theta) - 2 \lambda Hv = 0,
\end{aligned}$$

so we have that

$$\begin{aligned}
    \nabla f(\theta) &= 2 \lambda H v \\
    \implies
   v &= \frac{1}{2\lambda} H^{-1}  \nabla f(\theta),
\end{aligned}$$

which is the direction that causes the function’s value to decrease the
most. Lastly, plugging \\(v\\) above into the constraint \\(v^\top H v = 1\\),
we can solve for \\(\lambda\\).

Thus, the direction of steepest descent is \\(H^{-1}  \nabla f(\theta)\\),
i.e., the natural gradient.

Lastly, note that in a Euclidean space, the metric tensor is just the
identity matrix, so we get back standard gradient descent.

Mirror descent and Bregman divergence
=====================================

Mirror descent is a generalization of gradient descent that takes into
account non-Euclidean geometry. The mirror descent update equation is

$$\begin{aligned}
    \theta_{t+1} =
    \arg\min_{\theta \in \Theta} \left\{  \langle \theta, \nabla f(\theta_t) \rangle
    + \frac{1}{\alpha_t}  \underbrace{\Psi(\theta, \theta_t)}_{\text{proximity
    fn}}
    \right\}.
\end{aligned}$$

Here \\(\Psi: {\mathbb{R}}^p \times {\mathbb{R}}^p \rightarrow {\mathbb{R}}_+\\),
and when

$$\begin{aligned}
    \Psi(\theta,\theta') = \frac{1}{2} ||\theta-\theta'||_2^2,
\end{aligned}$$

we get back the standard gradient descent update[^3].

The proximity function \\(\Psi\\) is commonly chosen to be the *Bregman divergence*. Let
\\(G: \Theta \rightarrow {\mathbb{R}}\\) be a strictly convex,
twice-differentiable function, then the Bregman divergence
\\(B_G: \Theta \times \Theta \rightarrow {\mathbb{R}}^+\\) is:

$$\begin{aligned}
    B_G(\theta,\theta') = G(\theta) - G(\theta') - \langle \nabla G(\theta'),
    \theta-\theta'\rangle.
\end{aligned}$$

Equivalence of natural gradient and mirror descent
==================================================

#### Bregman divergences and convex duality

The convex conjugate[^2] of a function \\(G\\) is defined to be

$$\begin{aligned}
    H(\mu) := \sup_{\theta \in \Theta} \{\langle \theta,\mu\rangle -
    G(\theta)\}.\end{aligned}$$

Now, if \\(G\\) is a lower semi-continuous
function, then we have that \\(G\\) is the convex conjugate of \\(H\\). This
implies that \\(G\\) and \\(H\\) have a dual relationship. If \\(G\\) is strictly
convex and twice differentiable, so is \\(H\\). Let \\(g = \nabla G\\) and
\\(h = \nabla H\\). Then \\(g = h^{-1}\\).

Now let \\(\mu = g(\theta) \in \Phi\\) be the point at which the supremum
for the dual function is attained be the *dual* coordinate system to
\\(\theta\\). The dual Bregman divergence
\\(B_H: \Phi  \times \Phi \rightarrow {\mathbb{R}}^+\\) induced by the
strictly convex differentiable function \\(H\\)

$$\begin{aligned}
    B_H(\mu,\mu') = H(\mu) - H(\mu') - \langle \nabla H(\mu'), \mu-\mu'\rangle.
\end{aligned}$$

The dual coordinate relationship gives us

-   \\(B_H(\mu,\mu') = B_G(h(\mu'), h(\mu))\\)

-   \\(B_G(\theta,\theta') = B_H(g(\theta'), g(\theta))\\)

For exponential families, the function \\(G\\) is the log partition
function[^4]. We’ll now work through some examples.

#### Example: \[Normal\]
Consider the family \\(N(\theta, I_p)\\). The log partition function is

$$\begin{aligned}
    G(\theta) = \frac{1}{2} ||\theta||_2^2,
\end{aligned}$$

and the conjugate function of \\(G\\) is

$$\begin{aligned}
    H(\mu) &= \sup_{\theta} \{ \mu^\top \theta - \frac{1}{2} \theta^\top \theta \}
    \\
    &= \mu^\top\mu - \frac{1}{2} \mu^\top \mu = \frac{1}{2} ||\mu||_2^2,
\end{aligned}$$

since the expression in the supremum is maximized when \\(\theta = \mu\\)
(so we plug this in for \\(\theta\\) to get the second line). Then we can
easily write the Bregman divergence induced by \\(G,H\\) as

$$\begin{aligned}
        B_G(\theta,\theta') &= \frac{1}{2}||\theta-\theta'||_2^2 \\
        B_H(\mu,\mu') &= \frac{1}{2}||\mu-\mu'||_2^2.
\end{aligned}$$

#### Example: \[Poisson\]
Now suppose we have the family \\(\text{Poisson}(\exp(\theta))\\). We have

$$\begin{aligned}
        G(\theta) &= \exp(\theta) \\
        H(\theta) &= \sup_\theta \{ \mu^\top \theta - \exp(\theta) \} = \mu^\top
        \log\mu - \mu,
    \end{aligned}$$

where we plugged in \\(\theta = \log \mu\\) above. So the Bregman divergence induced by \\(G,H\\) is

$$\begin{aligned}
        B_G(\theta,\theta') &= \exp(\theta) - \exp(\theta') -
        (\theta-\theta')^\top \exp(\theta') \\
        B_H(\mu,\mu') &= \mu \log(\mu / \mu').
\end{aligned}$$

#### Bregman divergences and Riemannian manifolds

Now that we have introduced what the Bregman divergence of an
exponential family looks like (with respect to the log partition
function \\(G\\) and its dual Bregman divergence with respect to \\(H\\), where
\\(H\\) is the conjugate of \\(G\\), we are ready to discuss the respective
primal and dual Riemannian manifolds induced by these divergences.

-   **Primal Riemannian manifold**: \\((\Theta, \nabla^2 G)\\), where
    \\(\nabla^2 G \succ 0\\) (since \\(G\\) is strictly convex and
    twice differentiable).

-   **Dual Riemmanian manifold**: \\(B_H(\theta,\theta')\\) induces the
    Riemannian manifold \\((\Phi, \nabla^2 H)\\), where
    \\(\Phi = \{\mu: g(\theta) = \mu, \theta \in \Theta\}\\), i.e., the
    image of \\(\Theta\\) under the continuous map \\(g = \nabla G\\).

#### Theorem (Raskutti and Mukherjee, 2014):

The mirror descent step with Bregman divergence defined by \\(G\\) applied
to the function \\(f\\) in the space \\(\Theta\\) is equivalent to the natural
gradient step along the dual Riemannian manifold \\((\Phi, \nabla^2 H)\\).

*(Proof Sketch)*:

**Step 1**: Rewrite the mirror descent update in terms of the dual
Riemannian manifold coordinates \\(\mu \in \Phi\\):

$$\begin{aligned}
    \theta_{t+1} & =
    \arg\min_{\theta \in \Theta} \left\{  \langle \theta, \nabla f(\theta_t) \rangle
    + \frac{1}{\alpha_t}  B_G(\theta,\theta_t) \right\}
    \\
    \mu_{t+1} &= \mu_t - \alpha_t \nabla_\theta f(h(\mu_t)),\end{aligned}$$

since minimizing by differentiation and the dual coordinates
relationship gives us

$$\begin{aligned}
    g(\theta_{t+1}) = g(\theta_t) + \alpha_t \nabla_\theta f(\theta) \\
    \mu = g(\theta), \quad
    \theta = h(\mu) = \nabla H(\mu).
\end{aligned}$$

**Step 2**:
Apply the chain rule:

$$\begin{aligned}
    \nabla_\mu f(h(\mu)) &= \nabla_\mu h(\mu) \nabla_\theta f(h(\mu))
    \\
    \implies
    (\nabla_\mu h(\mu))^{-1}    \nabla_\mu f(h(\mu)) &=
    \nabla_\theta f(h(\mu))\end{aligned}$$

and plugging this in to the update above, we get

$$\begin{aligned}
    \mu_{t+1} &= \mu_t - \alpha_t \nabla_\theta f(h(\mu_t)) \\
    \\
    &= \mu_t - \alpha_t
    (\underbrace{\nabla_\mu h(\mu)}_{\nabla^2 H(\mu)})^{-1}   \nabla_\mu f(h(\mu))
    \\
    &= \mu_t - \alpha_t
    (\nabla^2_\mu H(\mu))^{-1}    \nabla_\mu f(h(\mu)),
    \end{aligned}$$

which corresponds to the natural gradient step.


## High-level summary:

The main result of [2] is that the mirror descent update with Bregman
divergence is equivalent to the natural gradient step along the *dual*
Riemannian manifold.

What does this mean? For natural gradient descent we know that

-   the natural gradient is the direction of steepest descent along a
    Riemannian manifold, and

-   it is Fisher efficient for parameter estimation (achieves the CRLB,
    i.e., the variance of any unbiased estimator is at least as high as
    the inverse Fisher information),

but neither of these things are known for mirror descent.

The paper also outlines potential algorithmic benefits: natural gradient
descent is a second-order method, since it requires the computation of
an inverse Hessian, while the mirror descent algorithm is a first-order
method and only involves gradients.



### References

1.  Amari. Natural gradient works efficiently in learning. 1998

2.  Raskutti and Mukherjee. The information geometry of mirror
    descent. 2014.

### Footnotes
[^1]: a smooth manifold equipped with an inner product on the tangent
    space \\(T_p \Theta\\)

[^2]: aka Fenchel dual, Legendre transform. Also e.g. for a convex
    optimization function, we can essentially write the dual problem
    (i.e., the inf of the Lagrangian), as the negative conjugate
    function plus linear functions of the Langrange multipliers.

[^3]: this can be seen by writing down the projected gradient descent update and rearranging terms

[^4]: see the [table listing the log partition function for exponential family distributions](https://en.wikipedia.org/wiki/Exponential_family#Table_of_distributions)
