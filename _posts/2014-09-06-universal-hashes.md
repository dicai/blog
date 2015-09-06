---
layout: post
title: Universal hash functions
tags:
- computer science
summary: Hashing is a general method of reducing the size of a set by reindexing the elements into \\(n\\) bins. This is done using a hash function, which maps some set \\( U \\) into a range \\([0, n-1]\\). When designing a hash function, we are interested in something that maps elements into a bin in a way that appears random.
---

Hashing is a general method of reducing the size of a set by reindexing the elements into \\(n\\) bins. This is done using a hash function, which maps some set \\( U \\) into a range \\([0, n-1]\\). When designing a hash function, we are interested in something that maps elements into a bin in a way that appears random.

Hashing is used frequently in various randomized algorithms. We now introduce \\(k\\)-wise independence, which gives a limited notion of independence and discuss it in the context of hashing to construct universal families of hash functions, which give space- and time-efficient data structures.

In future posts, we will discuss various randomized algorithms which use hashing and universal hash families to design efficient and practical approximation algorithms.

### Pairwise Independence

\\(k\\)-wise independence is a useful notion of independence and is more limited than mutual independence, which means that given a set of a random variables or events, any subset of them are independent. In contrast, \\(k\\)-wise independence says that any subset of random variables that is smaller than
\\(k\\) is independent, i.e., a set of random variables
\\( X_1, X_2, \ldots, X_N \\)
is \\(k\\)-wise independent if, for any subset \\(I \subset \\{1,\ldots,N\\}\\) with \\(|I| \leq k\\) and for any values \\(x_i, i\in I \\), we have

$$\Pr(\cap_{i\in I} X_i = x_i) = \prod_{i\in I} \Pr(X_i=x_i).$$

In this post, we focus on the case of \\(k=2\\), or pairwise independence: the random variables \\(X_1,X_2,\ldots,X_n\\) are pairwise independent if for any pair
\\(i,j\\) and any values \\(a,b\\)

\\[\Pr(X_i=a, X_j=b) = \Pr(X_i = a) \Pr(X_j=b).\\]

### Universal Hash Families

When designing hash functions, we want something completely random. However, this model is usually too expensive to compute and store. In practice, we use universal hash families, which have some nice provable properties.

Suppose we have some universe \\(U\\), which has a cardinality of at least
\\(n\\), and the set \\(V = \\{0,1,\ldots,n-1\\}\\). The family of hash functions
\\(\mathcal{H}:U\rightarrow V\\) is called \\(k\\)-universal if for any \\(k\\)
elements \\(x_1,\ldots,x_k\\) and hash function \\(h\\) chosen uniformly
from \\(\mathcal{H}\\), we have

$$\Pr(h(x_1)=\ldots=h(x_k)) \leq (n^{k-1})^{-1}.$$

That is, the probability of all \\(k\\) elements hashing to the same bin is at
most \\(\frac{1}{n^{k-1}}\\).

A family of hash functions \\(\mathcal{H}:U\rightarrow V\\) is called strongly
\\(k\\)-universal if for any \\(k\\) elements \\(x_1,\ldots,x_k\\) and values
\\(y_1,\ldots,y_k\\), and a randomly chosen hash function \\(h\\) from
\\(\mathcal{H}\\), we have

$$\Pr(h(x_1)=y_1,\ldots,h(x_k)=y_k) \leq (n^{k})^{-1}.$$

Strongly \\(k\\)-universal families are also called \\(k\\)-wise independent
hash families since \\(h(x_1), \ldots, h(x_k)\\) are \\(k\\)-wise independent. Strongly \\(k\\)-universal families are also \\(k\\)-universal.

For the rest of this post, we will only consider 2-universal families. When
\\(n\\) elements are hashed into \\(n\\) bins using a hash function from a
2-universal hash family, the maximum number of items in a bin is at most
\\(\sqrt{2n}\\) with probability \\(\frac{1}{2}\\).

### Constructing 2-Universal Families

We now discuss how to generate hash functions from a 2-universal family. Let the
universe \\(U = \\{0,\ldots,m-1\\}\\) and let the range be
\\(V=\\{0,\ldots,n-1\\}\\), where \\(m \geq n\\). Choose a prime \\(p \geq m\\). Consider the hash function

$$h_{ab}(x) = ((ax + b) \mod p)\mod n.$$

The 2-universal hash family is
$$\mathcal{H} = \{h_{a,b} | 1 \leq a \leq p-1, 0\leq b \leq p-1\}.$$

Thus, to get a 2-universal hash function from this family, we only need to generate \\(a\\) and \\(b\\) within the appropriate ranges (note \\(a\\) cannot be 0).

To generate hash functions from a strongly 2-universal family, we have the family

$$\mathcal{H} = \{h_{a,b} | 0 \leq a, b \leq p-1\},$$

 where the hash function is given by

$$h_{ab}(x) = (ax + b) \mod p.$$

In future posts, we will describe applications of universal hash families.

Resources

Mitzenmacher, Michael, and Eli Upfal. Probability and computing: Randomized algorithms and probabilistic analysis. Cambridge University Press, 2005.

Motwani, Rajeev, and Prabhakar Raghavan. Randomized algorithms. Chapman & Hall/CRC, 2010.
