---
title: "Sparse Table"
date: 2020-05-17T18:06:28+05:30
draft: false
toc: true
mathjax: true
author: "Ram Nad"
tags: ["competitive programming", "algorithms"]
---

# Sparse Table

Sparse Table is a data structure that lets you answer, most range queries in $\mathcal{O}(\log{n})$, in an immutable array. But for some queries like (minimum, maximum, gcd) it can answer queries in $\mathcal{O}(1)$. It also requires $\mathcal{O}(n\log{n})$ preprocessing time and extra space of similar order. One thing to note is that you cannot change the elements of the array, therefore this algorithm might be useful only when values of array remain unchanged. And also as in the case of [Square Root Decomposition]({{< ref "posts/sqrt-decomposition.md" >}}), the operation that we do on the range must be associative.

## Idea

First notice that binary representation of a number $n$ has exactly $\lfloor\log{n}\rfloor + 1$ bits, which is $\mathcal{O}(\log{n})$. Now suppose that we are given a range $[L, R]$ which is divided into segments of size $2^{0}$, $2^{1}$, $2^{2}$, $2^{3}$ $...$ and so on. It is clear that if we have $n$ elements in the array, then the number of segments cannot be more than the number of bits in the binary representation of $n$. Therefore if we have our values of queries over these segments, then we can combine them in $\mathcal{O}(\log{n})$ to get an answer to our query.

So, that is what we will do here. Assume we have an array of size $n$. We will precalculate the query for segments

$[I, I]$, $[I, I + 1]$ $[I, I + 3]$, $[I, I + 7]$ ... $[I, I + N - 1]$

for all possible values of $I$ (Not all the segments will be valid for all $I$).

**Note: $N$ is maximum possible power of $2$ less than or equal to $n$.**

Once, we have precalculated the above values we can answer as many range queries as required.

## Example

Let us look at an example to understand things better.

We have array, \$[2, 4, -1, 0, 6, 8, 9, 4, 3]\$ and for any possible range, we want to find the sum of elements in that range. So, we have $n = 9$. Therefore, $N = 8$ (maximum power of $2$ less than $n$). So, we will have the following segments (assuming $1$ based indexing) with values of their query,

$[1, 1] = 4$, $[1, 2] = 6$, $[1, 4] = 5$, $[1, 8] = 32$

$[2, 2] = 4$, $[2, 3] = 3$, $[2, 5] = 9$, $[2, 9] = 33$

$[3, 3] = -1$, $[3, 4] = -1$, $[3, 6] = 13$

$[4, 4] = 0$, $[4, 5] = 6$, $[4, 7] = 23$

$[5, 5] = 6$, $[5, 6] = 14$, $[5, 8] = 27$

$[6, 6] = 8$, $[6, 7] = 17$, $[6, 9] = 24$

$[7, 7] = 9$, $[7, 8] = 13$

$[8, 8] = 4$, $[8, 9] = 7$

$[9, 9] = 3$

Now suppose we want to calculate the value for the range $[3, 7]$, We have

$7 - 3 + 1 = 5 = 2^{2} + 2^{0}$

So we will use the segments

$[3, 3 + 2^{2} - 1]$ ($[3, 6]$)

$and$

$[3 + 2^{2}, 3 + 2^{2} + 2^{0} - 1]$ ($[7, 7]$)

Note that, for any given range we will have their difference less than equal to $n$ and we can always calculate the final query like this and it will take in the worst case $\mathcal{O}(\log{n})$ steps.

## Implementation

Here we will look at how to precalculate the values and how to do range queries. For complete implementation, check out the [code here](/code/sparse-table/code1.cpp).

```cpp
// Here `a` is the original array
int N = log(n) + 1;

int queries[n][N];

for(int i = 0; i < n; i++) {
    queries[i][0] = a[i];
}

for(int i = 1; i < N; i++) {
    for(int j = 0; j + (1 << i) <= n; j++) {
        queries[j][i] = queries[j][i - 1] + queries[j + (1 << (i-1))][i - 1];
    }
}
```

Now, let us understand the above code. First loop which runs a total of $n$ times assign the values for ranges of type, $[0, 0]$, $[1, 1]$, $...$.

Second loop runs for $N \times n$ times which is $\mathcal{O}(n\log{n})$. To understand the code let us take alook at one example.

`queries[1][3]` basically means the segment $[1, 8]$ ($2^{3}$ elements).

`1 << x` is equal to $2^{x}$, so `j + (1 << (i-1))` equals `j + $2^{i-1}$`. Therefore,

`queries[1 + (1 << (2))][2]` denotes the segment $[5, 8]$ and ofcourse `queries[1][3]` denotes the segment $[1, 4]$. Therefore,

`queries[1][2] + queries[1 + (1 << (2))][2]`

translates to somewhat $[1, 4] + [5, 8]$.

Try to look at some other examples by yourself (just assign `i` and `j` some suitable value) and convince yourself that this code actually, computes the value for all possible segments correctly.

Following is the code to calculate query for range, $[L, R]$

```cpp
int sum = 0;
int size = R - L + 1;
int pos = L;
for(int i = N - 1; i >= 0; i--) {
    if(size - (1 << i) >= 0) {
        sum += queries[pos][i];
        pos += 1 << i;
        size -= 1 << i;
    }
}
```

`pos` denotes the position from where we need to process queries and `size` denotes the number of elements left for processing. So, `pos` starts from $L$ and `size` starts from $(R - L + 1)$.

We basically start from biggest power of $2$ and whenever, we get to a value $2^{i}$ such that it is less than or equal to current `size`, we process range $[pos, pos + 2^{i} - 1]$, now because elements upto $pos + 2^{i} - 1$ is processed, we set $pos = pos + 2^{i}$ and also since total $2^{i}$ elements are processed, we now decrease size by the $2^{i}$.

Now notice that the new value of size will be less than $2^{i}$ (Thinks in terms of binary representation). So, it is guaranteed that size will eventually reach $0$.

## Minimum Range queries in $\mathcal{O}(1)$

Now, suppose that we need to find the minimum of numbers in the range. Preprocessing steps remain the same (except instead of adding the segments we find minimum between them). But the query part changes a bit.

Suppose we need to answer query for $[L, R]$ and $size = R - L + 1$. Find the largest power of $2$, less than equal to the size. Let this be $2^{j}$. Now if we find minimum between range $[L, L + 2^{j} - 1]$ and $[R - 2^{j} + 1, R]$, we will be done.

Why? because these two ranges cover all the elements between $[L, R]$. As, both the ranges, lie between $L$ and between $R$. ($L + 2^{j} - 1 <= R$ and $R - 2^{j} + 1 >= L$). Also, since the total number of elements combining both the ranges is greater than `size` (Again, think in terms of binary). So, it is guaranteed that all the elements are covered.

Now, if we need to calculate $2^{j}$ value for each query then it will again reduce to $\mathcal{O}(\log{n})$. So, instead, we precalculate these values as well. This can be done in $\mathcal{O}(n)$. Therefore, our overall complexity for precalculation remains the same. The complete implementation can be found [here](/code/sparse-table/code2.cpp).

## References

- [https://cp-algorithms.com/data_structures/sparse-table.html](https://cp-algorithms.com/data_structures/sparse-table.html)
- [https://www.hackerearth.com/practice/notes/sparse-table/](https://www.hackerearth.com/practice/notes/sparse-table/)
