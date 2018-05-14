---
layout: post
title: Recursion
date: 2018-05-13 15:23:24.000000000 -05:00
---

`this is just a algorithm learning blog for my own purpose of use.`

What is Recursion?
1. 表象上：function calls itself
2. 实际上: Boil down a big problem to smaller ones. (problem with size n depends on size n-1, n-2, ..., n/2)
3. Implementation上，
    - Basic case: smallest case of problem to solve
    - Recursive rule: How to make the problem smaller? (If we can solve the sub-problem, how to solve the larger one?)

## Recursion I

### Fibonacci sequence

a classical problem on recursion.

### Time and space complexity analysis of recursion
1. draw recursion tree. in this example, Fib() can be described as n-level recursion tree. 
2. total **Time** is the number of nodes in this tree. so total is 2^n. total **Space** is the level of recursion tree (aka. call stack) is O(n).

### Optimal solution on fibonacci
1.  using dynamic programming. 
    - use an array store all result. this will lead to O(n) space and O(n) time.
    - use a variable to store result. when we receive the temp result, set b to temp and a to b. do it n times and we get the result in b.
2.  using matrix multiplication
    - This will lead to O(logn) time complexity and O(1) space
    - this method uses a fibonacci attributes in matrix.

    $$
        \begin{bmatrix}
            1&1 \\
            1&0 
        \end{bmatrix} *
        \begin{bmatrix}
            1&1 \\
            1&0 
        \end{bmatrix} = 
        \begin{bmatrix}
            2&1 \\
            1&1 
        \end{bmatrix}
    $$
    $$
        \begin{bmatrix}
            2&1 \\
            1&1 
        \end{bmatrix} *
        \begin{bmatrix}
            1&1 \\
            1&0 
        \end{bmatrix} = 
        \begin{bmatrix}
            3&2 \\
            2&1 
        \end{bmatrix}
    $$
    $$
        \begin{bmatrix}
            3&2 \\
            2&1 
        \end{bmatrix} *
        \begin{bmatrix}
            1&1 \\
            1&0 
        \end{bmatrix} = 
        \begin{bmatrix}
            5&3 \\
            3&2 
        \end{bmatrix}
    $$
    $$\dots$$

    - we can infer that matrix[0][0] is the fib(n) we want to calculate. then we can use a^b trick to decrease the running time to O(logn).

### Calculate **$a^b$**

Time $O(logN)$ Space $O(logN)$
- think about we already know the result of $a^{b/2}$, then we just need to multiply $a^{b/2}*a^{b/2}$. If b is odd, just multiply another a.


## Recursion 与计算的结合 

### a to the power of b: a^b

boil down to n/2

base case: b==0 -> a^b == 1

recursive rule: if we know the answer of a^(b/2), we can use a^(b/2) * a^(b/2) to get a^b;

``` java
long power (int a, int b) {
    if (b == 0) return 1;
    long res = power(a, b/2);
    return b % 2 == 0? res * res: res * res * a;
}
// If we assume b can less than 0
if (b < 0) :
    return 1/(double)power(a, -b);
else :
    return power(a, b);
```

## Recursion 与1D Array 和 2D Array相结合

- 与1D Array:
    - 二分法比较常见：Merge sort && Quick Sort
- 与2D Array:
    - 逐层递归 8 queen -> n queen

### 8 queen problem



