---
layout: post
title: Perfect Hashing with a 2-Universal Hash Family
tags:
- computer science
- algorithms
summary: Previously, we discussed universal hash families. In this post, we discuss a method of using a 2-universal hash family along with a Las Vegas algorithm to allow for perfect hashing, where the time required to find an item in a hash table is constant.
---

Previously, we discussed [universal hash families](http://www.dianacai.com/blog/2014/09/06/universal-hashes/). In this post, we discuss a method of using a 2-universal hash family along with a
[Las Vegas algorithm](https://en.wikipedia.org/wiki/Las_Vegas_algorithm) to allow for perfect hashing, where the time required to find an item in a hash table is constant.

A dictionary is a data structure used to maintain a set $$S$$ under insertion and deletion of elements, or keys, from some universe $$U$$. Dictionaries are typically implemented efficiently using hash tables.

Perfect Hashing

Perfect hashing is a method for storing a static dictionary, i.e. the items are permanently stored in the table, which only needs to support search queries. A hash function $$h: U \rightarrow V$$ is called perfect for a set $$S \subset U$$ if $$h$$ does not cause any collisions among the keys of the set $$S$$.

Let $$h$$ be chosen uniformly from a 2-universal family of hash functions. Let $$V$$ be the range $$[0,n-1]$$. Then for any set $$S \subset U$$ of size $$m$$, if the number of items in the universe $$n$$ is at least the size of the number of bins squared, $$m^2$$, the hash function is perfect with probability at least $$\frac{1}{2}$$.

In practice, when $$n \geq m^2$$, we can use a Las Vegas algorithm, where we randomly draw hash functions from the 2-universal family until we find one with no collisions, where on average, we only need to try two hash functions. However, this method requires on average $$m^2$$ bins.

We can improve the space requirement to having the worst case be $$O(m)$$ bins as follows. First, we pick a hash function $$h_1$$ uniformly at random from a 2-universal family and hash items in the set using it, resulting in some collisions. We choose the first hash function with a Las Vegas algorithm, trying hash functions until we have at most $$m$$ collisions. For each bin with $$k > 1$$ items in it (ones with collisions), we can, as before, use $$k^2$$ space to achieve no collisions with a second hash function $$h_2$$ from a 2-universal family. As before, we use a Las Vegas algorithm to choose the second hash function such that there are no collisions.

Sources:

Mitzenmacher and Upfal. Probability and computing: Randomized algorithms and probabilistic analysis. Cambridge University Press, 2005.

Motwani and Raghavan. Randomized algorithms. Chapman & Hall/CRC, 2010.
