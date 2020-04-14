---
layout: post
title: Reading list on probabilistic numerics
author: Diana Cai
tags:
- statistics
- machinelearning
- numerics
summary: Probabilistic numerical methods have seen a recent surge of interest. However, the methods date back to many key contributions made in the 60s-80s. The goal here is to collect a relevant, organized reading list here. I hope to update
---

*(Last updated: 04/10/2020)*

Probabilistic numerical methods have experienced a recent surge of interest. However,
the literature of many key contributions date back to 60s-80s, a period before
many modern developments in computing. The goal here is to collect a relevant, organized reading list here. I hope to update
this post with more references and possibly short descriptions of the papers as
I get to reading more of them.

The [Probabilistic Numerics Website](http://probabilistic-numerics.org/literature/index.html) has a more complete set of papers and serves as a great reference on this topic.

# Recent surveys

Here are recent surveys that collect a lot of the literature and developments in the field as well as open problems the authors believe are important to tackle.

1. Hennig, P., Osborne, M. A., & Girolami, M. (2015). [Probabilistic numerics and
   uncertainty in computations.](https://arxiv.org/pdf/1506.01326.pdf) Proceedings of the Royal Society of London A:
   Mathematical, Physical and Engineering Sciences, 471(2179).

2. Oates, C. J., & Sullivan, T. J. (2019). [A Modern Retrospective on
   Probabilistic Numerics.](https://arxiv.org/pdf/1901.04457.pdf) ArXiv e-Prints, 1901.04457.


# Selected historical papers

The first discussion of probabilistic numerics apparently dates back to
Poincar&eacute; in 1896. Here we collect some important papers building
foundations in probabilistic numerics, which mostly focused on the problem of integration.

0. Sul’din, A. V. (1959). Wiener measure and its applications to approximation
   methods. I. Izvestiya Vysshikh Uchebnykh Zavedenii. Matematika, (6), 145–158.

1. Sul’din, A. V. (1960). Wiener measure and its applications to approximation
   methods. II. Izvestiya Vysshikh Uchebnykh Zavedenii. Matematika, (5),
   165–179.

1. Kimeldorf, G. S., & Wahba, G. (1970). A correspondence between Bayesian
   estimation on stochastic processes and smoothing by splines. The Annals of
   Mathematical Statistics, 41(2), 495–502.

1. Larkin, F. M. (1972). Gaussian measure in Hilbert space and applications in
   numerical analysis. Rocky Mountain Journal of Mathematics, 2(3), 379–422.

1.  Micchelli C. A., & Rivlin T. J. A survey of optimal recovery. Optimal Estimation in
    Approximation Theory. Springer, 1977, 1–54.

1. Kadane, J. B., & Wasilkowski, G. W. (1985). Average case epsilon-complexity
   in computer science: A Bayesian view. In Bayesian Statistics 2, Proceedings
   of the Second Valencia International Meeting (pp. 361–374).

1. Wozniakowski, H. [A survey of information-based complexity](https://www.sciencedirect.com/science/article/pii/0885064X85900202). J. Complexity,
   1(1):11–44, 1985.

2. Diaconis, P. (1988). [Bayesian numerical analysis](http://probabilistic-numerics.org/assets/pdf/Diaconis_1988.pdf). Statistical Decision Theory
   and Related Topics IV, 1, 163–175.


# Recent papers on probabilistic numerics

For lack of a better title, here we collect more recent papers on probabilistic numerics, focusing on
general overviews, rather than specific numerical methods.

##  Decision-theoretic views on probabilistic numerics

1. Cockayne, J., Oates, C., Sullivan, T., & Girolami, M. (2017). [Bayesian
   Probabilistic Numerical Methods](https://arxiv.org/abs/1702.03673). ArXiv e-Prints, stat.ME 1702.03673.

2. Oates, C. J., Cockayne, J., Prangle, D., Sullivan, T. J., & Girolami, M.
   (2019). [Optimality Criteria for Probabilistic Numerical
   Methods](https://arxiv.org/pdf/1901.04326.pdf). ArXiv
   e-Prints, 1901.04326.

3. Owhadi, H., & Scovel, C. (2017). [Universal Scalable Robust Solvers from
   Computational Information Games and fast eigenspace adapted Multiresolution
   Analysis.](http://arxiv.org/abs/1703.10761)
   ArXiv:1703.10761 [Math, Stat].

4. Owhadi, H., Scovel, C., & Schafer, F (2019). [Statistical Numerical
   Approximation.](https://pdfs.semanticscholar.org/6fd4/f6c23c84e902572bd5b6ae1f652f4ac2598d.pdf).
   Notices of the American Mathematical Society, 66(10).

# Probabilistic linear solvers

These papers propose probabilistic methods for solving linear systems $$Ax=b$$, where generally a prior is placed on either the unknown quantity $$A^{-1}$$ or $$A^{-1}b$$, and posterior point estimates often have an explicit relationship with classical itereates obtained from iterative algorithms, such as the [conjugate gradient method](https://www.dianacai.com/blog/2018/08/31/conjugate-gradient-linear-systems/).

1. Hennig, P. (2015). [Probabilistic Interpretation of Linear Solvers.](https://epubs.siam.org/doi/abs/10.1137/140955501) SIAM J on Optimization, 25(1).

2. Cockayne, J., Oates, C., & Girolami, M. (2018). [A Bayesian Conjugate Gradient Method.](https://projecteuclid.org/euclid.ba/1558144846) Bayesian Analysis, 14(23), 937--1012.

3. Bartels, S., Cockayne, J., Ipsen, I., & Hennig, P. [Probabilistic linear solvers: a unifying view.](https://link.springer.com/article/10.1007/s11222-019-09897-7) Statistics and Computing, 29(6), 1249--1263.

# Probabilistic integration

In addition to the historical papers above, there are a lot of recent papers on probabilistic integration.

1. Xie, X., Briol, F., & Girolami, M (2018). [Bayesian Quadrature for Multiple Related Integrals](https://arxiv.org/abs/1801.04153).
    ICML, PMLR 80:5369-5378.

# Applications

1. Bartels, S., Hennig, P (2016). Probabilistic Approximate Least Squares. AISTATS, PMLR 51, 676-684.



