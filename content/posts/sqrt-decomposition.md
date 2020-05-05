---
title: "Square Root Decomposition"
date: 2020-05-05T20:56:37+05:30
draft: false
toc: true
mathjax: true
author: "Ram Nad"
tags: ["competitive-programming", "algorithms"]
---

# Square Root Decomposition

Square Root Decomposition is an algorithm for answering range queries, in $\mathcal{O}(Q\sqrt{N})$, where $Q$ is the number of queries and $N$ is the number of elements in the range. It is very useful in a lot of CP questions. The basic technique of Square Root Decomposition can be used for doing certain queries on Trees as well.

## Motivation

Let us look at a problem, to motivate the need for this algorithm. Suppose we are given an array of $N$ integers.
$$a_{1}, a_{2}, a_{3} ...$$
and $Q$ queries. For each query, we are given to indexes $L$ and $R$. We need to give the sum of all the integers, in the range $a_{L}, a_{L+1}, ..., a_{R-1}, a_{R}$. Now this is easily solvable using [prefix-sums](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/) in $\mathcal{O}(1)$ time complexity and $\mathcal{O}(N)$ extra space complexity. But suppose along with this we are given queries of the second type, an index $i$ and an integer $A$. In queries of the second type, we need to update the value of $a_{i}$ to $A$.

This new problem is certainly more difficult than the first version. If we use the prefix-sums method, then update queries will take $\mathcal{O}(N)$ while, we can still answer queries of the first type (range query) in $\mathcal{O}(1)$. If we don't use prefix-sums then we can do update operations in $\mathcal{O}(1)$ but then we will need $\mathcal{O}(N)$ operations for answering range queries.

## Method

Square Root Decomposition allows us to efficiently answer both the queries (in $\mathcal{O}(\sqrt{N})$). The basic idea is to divide $N$ integers into $\sqrt{N}$ blocks each containing $\sqrt{N}$ elements (maybe except for the last block). And for each block, we pre-compute the range queries.

For example,

$a = [1, 3, 4, 5, 6, 3, -2, 1, 7]$

$N = 9$

$\sqrt{N} = 3$

$Block-1: [1, 3, 4], sum(Block-1): 8$

$Block-2: [5, 6, 3], sum(Block-2): 14$

$Block-3: [-2, 1, 7], sum(Block-3): 6$

Now, let us use the information given above to calculate, range query for $L=2$ and $R=6$.

$sum([3, 4, 5, 6, 3]) = sum(max([3, 4]), max([5, 6, 3]))$

Now, we already know the value of the second subexpression, and we can calculate the value of the first subexpression in $\mathcal{O}(\sqrt{N})$ (in the worst case). So, we have solved the query in $\mathcal{O}(\sqrt{N})$.

Now, these example can be generalized as follows, suppose taht blocks are as follows:

$$(X_{1} ... Y_{1}), (X_{2} ... Y_{2}), ......, (X_{\sqrt{N}} ... Y_{\sqrt{N}})$$

Now, suppose that $L$ lies in block ($X_{i} ... Y_{i}$) and $R$ lies in block ($X_{j} ... Y_{j}$).

Then we need to calculate, sum of the elements between $(a_{L} ... a_{Y_{i}})$ and sum of the elements between $(a_{L} ... a_{Y_{i}})$ each of which will take at most $\mathcal{O}(\sqrt{N})$ time. And in worst case we will have $\sqrt{N}$ blocks in between. Therefore, combining the solution will take $\mathcal{O}(\sqrt{N})$ time. Overall we do, $\mathcal{O}(\sqrt{N})$ operations 3 times which is still $\mathcal{O}(\sqrt{N})$.

Therefore, now we have proved that using square root decomposition we can perform range queries in $\mathcal{O}(\sqrt{N})$. Now, for update queries, we need to update the value of the element and also the value of the block in which the number lies. (clearly, this can be done in $\mathcal{O}(\sqrt{N})$).

## Conclusion

For, the sake of discussion we assumed that the operation is `sum`, but this need not be the case. We can apply this technique for any associative operation. (`min`, `max`, `multiplication` etc.)

For some operations like `sum` and `multiplication`, we can do update queries in $\mathcal{O}(1)$. Now, there exists a different algorithm ([Segment Tree](https://www.hackerearth.com/practice/data-structures/advanced-data-structures/segment-trees/tutorial/)) which will allow us to answer both the queries in $\mathcal{O}(\log{N})$ time complexity. But it is a bit more complicated to implement than the square root decomposition method.

For a complete implementation check this [code](/code/sqrt-decomposition/code.cpp).

_Thanks for Reading._

## References

- [https://cp-algorithms.com/data_structures/sqrt_decomposition.html](https://cp-algorithms.com/data_structures/sqrt_decomposition.html)
- [https://www.geeksforgeeks.org/sqrt-square-root-decomposition-technique-set-1-introduction/](https://www.geeksforgeeks.org/sqrt-square-root-decomposition-technique-set-1-introduction/)
- [https://www.youtube.com/watch?v=b6QhQSnKNSc](https://www.youtube.com/watch?v=b6QhQSnKNSc)
