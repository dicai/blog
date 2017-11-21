---
layout: post
title: References on Bayesian nonparametrics
author: Diana Cai
tags:
- statistics
- references
- nonparametricbayes
- bayesian
summary: This post is a collection of references for Bayesian nonparametrics that I've found helpful or wish that I had known about earlier.
---

*Last updated: 11/15/17*

This post is a collection of references for Bayesian nonparametrics that I've found helpful or wish that I had known about earlier.
For many of these topics, some of the best references are lecture notes, tutorials, and lecture videos.
For general references, I've prioritized listing newer references with a more updated or comprehensive treatment of the topics.
Many references are missing, and so I'll continue to update this over time.


# Nonparametric Bayes: an introduction

These are references for people who have little to no exposure to the area, and
want to learn more. Tutorials and lecture videos offer a great way to get up to
speed on some of the more-established models, methods, and results.

0. Teh (and others). [Nonparametric Bayes tutorials.](https://www.stats.ox.ac.uk/~teh/npbayes.html)

    _This webpage lists a number of review articles and lecture videos that as an
introduction to the topic. The main focus is on Dirichlet processes, but a few
tutorials cover other topics: e.g., Indian buffet processes, fragmentation-coagulation processes._

1. Broderick. [Nonparametric Bayesian Methods: Models, Algorithms, and
   Applications](http://www.tamarabroderick.com/tutorial_2017_uc.html). 2017.
   See also [joint tutorial](http://www.tamarabroderick.com/tutorial_2017_simons.html) with Michael Jordan at the Simon's Institute.

   _An introduction to Dirichlet processes and the Chinese restaurant process,
   and nonparametric mixture models. Also comes with R code for generating from and
   sampling (inference) in these models._

2. Wasserman and Lafferty. [Nonparametric Bayesian Methods](http://www.stat.cmu.edu/~larry/=sml/NPBayes.pdf). 2010.

   _This gives an overview of Dirichlet processes and Gaussian processes and places
   these methods in the context of popular frequentist nonparametric estimation methods for, e.g., CDF and
   density estimation, regression function estimation._


# Theory and foundations

It turns out there's a lot of theory and foundational topics.

0. Orbanz. [Lecture notes on Bayesian nonparametrics](http://stat.columbia.edu/~porbanz/papers/porbanz_BNP_draft.pdf).
   2014.

   _A great introduction to foundations of Bayesian nonparametrics, and provides
   many references for those who want a more in-depth understanding of topics.
   E.g.: random measures, clustering and feature modeling, Gaussian processes,
   exchangeability, posterior distributions._


2. Ghosal and van der Vaart. _Fundamentals of Bayesian Nonparametric Inference._
    Cambridge Series in Statistical and Probabilistic Mathematics, 2017.
    [contents](www.cambridge.org/core_title/gb/299509)

    _The most recent textbook on Bayesian nonparametrics, focusing on topics
    such as random measures, consistency, contraction rates, and also covers
    topics such as Gaussian processes, Dirichlet processes, beta processes._

1. Kleijn, van der Vaart, van Zanten. [Lectures on Nonparametric Bayesian
   Statistics](https://staff.fnwi.uva.nl/b.j.k.kleijn/NPBayes-LecNotes-2015.pdf).
   2012.

   _Lecture notes with some similar topics as (and partly based on) the Ghosal and van der Vaart textbook, including a comprehensive treatment of posterior consistency._


## Specific topics

3. Kingman. _Poisson processes._ Oxford Studies in Probability, 1993.

    _Everything you wanted to know about Poisson processes. (See Orbanz lecture
     notes above for more references on even more topics on general point process theory.)_

4. Pitman. [Combinatorial stochastic processes](https://www.stat.berkeley.edu/~pitman/621.pdf). 2002.

5. Aldous. [Exchangeability and related topics](https://www.stat.berkeley.edu/~aldous/Papers/me22.pdf). 1985.

6. Orbanz and Roy. [Bayesian Models of Graphs, Arrays and
Other Exchangeable Random Structures](http://danroy.org/papers/OR-exchangeable.pdf). _IEEE TPAMI_, 2015.

7. Jordan. [Hierarchical models, nested models, and completely random
   measures](https://pdfs.semanticscholar.org/8c1e/16b374a82e01e55ff0cb0f0724374d6787b6.pdf). 2013.

8. Broderick, Jordan, Pitman. [Cluster and feature modeling from combinatorial
   stochastic processes](https://projecteuclid.org/euclid.ss/1377696938). 2013.

## Background: probability

Having basic familiarity with measure-theoretic probability is fairly important for understanding many of the ideas in this section. Many of the introductory references aim to avoid measure
theory (especially for the discrete models), but even this is not always the case, so it is helpful to have as much exposure as possible.

0. Hoff. _Measure and probability._ Lecture notes. 2013. [pdf](http://www.stat.washington.edu/people/pdhoff/courses/581/LectureNotes/mtheory.pdf)

    _Gives an overview of the basics of measure-theoretic probability, which are often assumed in many of the above/below references._

1. Williams. _Probability with martingales._ Cambridge Mathematical Textbooks, 1991.

2. Cinlar. _Probability and stochastics._ Springer Graduate Texts in Mathematics. 2011.


# Models and inference algorithms

There are too many papers on nonparametric Bayesian models and inference methods. Below, I'll list a few "classic" ones, and continue to add more over time.
The above tutorials contain many more references.

## Dirichlet processes: mixture models and admixtures

### Dirichlet process mixture model
1. Neal. Markov Chain sampling methods for Dirichlet process mixture models.
    _Journal of Computational and Graphical Statistics_, 2000.
    [pdf](https://www.cs.princeton.edu/courses/archive/fall11/cos597C/reading/Neal2000a.pdf)


1. Blei and Jordan. Variational inference for Dirichlet process mixtures.
    _Bayesian Analysis_, 2006.
    [pdf](http://www.cs.columbia.edu/~blei/papers/BleiJordan2004.pdf)

### Hierarchical Dirichlet process
2. Teh, Jordan, Beal, Blei. Hierarchical Dirichlet processes.
    _Journal of the American Statistical Association_, 2006.
    [pdf](https://people.eecs.berkeley.edu/~jordan/papers/hdp.pdf)

3. Hoffman, Blei, Wang, Paisley. Stochastic variational inference.
    _Journal of Machine Learning Research_, 2013.
    [pdf](http://www.jmlr.org/papers/volume14/hoffman13a/hoffman13a.pdf)

### Nested Dirichlet process & Chinese restaurant process

1. Rodriguez, Dunson, Gelfand. The Nested Dirichlet process.
_Journal of the American Statistical Association_, 2008.
[pdf](https://people.eecs.berkeley.edu/~jordan/sail/readings/rodriguez-dunson-gelfand.pdf)

2. Blei, Griffiths, Jordan. The nested Chinese restaurant process and Bayesian
   nonparametric inference of topic hierarchies.
    _Journal of the ACM_, 2010.
   [pdf](https://cocosci.berkeley.edu/tom/papers/ncrp.pdf)

3. Paisley, Wang, Blei, Jordan. Nested hierarchical Dirichlet processes.
_IEEE TPAMI_, 2015.
[pdf](http://www.columbia.edu/~jwp2128/Papers/PaisleyWangetal2015.pdf)

### Mixtures of Dirichlet processes
1. Antoniak. Mixture of Dirichlet processes with applications to Bayesian nonparametrics.
    _Annals of Statistics_, 1974.
    [pdf](https://projecteuclid.org/download/pdf_1/euclid.aos/1176342871)

### Additional inference methods
1. Ishwaran and James. Gibbs sampling methods for stick-breaking priors.
    _Journal of the American Statistical Association_, 2001.
    [pdf](http://www.tandfonline.com/doi/abs/10.1198/016214501750332758)

2. MacEachern. Estimating normal means with a conjugate style dirichlet process prior.
    _Communications in Statistics - Simulation and Computation_, 1994.
    [pdf](https://www2.stat.duke.edu/courses/Spring06/sta376/Support/Mixtures/Maceachern.Mueller.1998.pdf)

3. Escobar and West. Bayesian density estimation and inference using mixtures.
    _Journal of the American Statististical Association_, 1995.
    [pdf](https://people.eecs.berkeley.edu/~jordan/courses/281B-spring04/readings/escobar-west.pdf)


## Indian buffet processes and latent feature models

0. Griffiths and Ghahramani. The Indian buffet process: an introduction and review.
    _Journal of Machine Learning Research_, 2011.
[pdf](http://www.jmlr.org/papers/volume12/griffiths11a/griffiths11a.pdf)

1. Thibaux and Jordan. Hierarchical beta processes and the Indian Buffet
   process. _AISTATS_, 2007.
   [pdf](http://proceedings.mlr.press/v2/thibaux07a/thibaux07a.pdf)
   |
   [longer](https://www.cs.princeton.edu/courses/archive/fall07/cos597C/readings/ThibauxJordan2007.pdf)


