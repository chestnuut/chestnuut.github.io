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

### n queen problem

Try to put n queens into a chess board, which there is no conflict between these queens. (上下左右与对角线)

**Method 1** 

Time: $O(n*n!)$ Space: $O(n)$

Similar with DFS, we have n levels, each level has n possible solutions. The difference is we need to check if the current solution is valid. If **valid**, add to solution, check next.

Check valid in this method can cost $O(n)$ time. 

``` java
for (every row in rows) {
    if (column in current row == column) or (column - column in current row) == rows.size - row) {
        return false;
    }
}
return true;
``` 

**Method 2** 

Time: $O(n!)$ Space: $O(n)$

Check valid in this method can reduce to $O(1)$

Build three boolean arrays: usedColumns, usedDiagonals and usedRevDiagonals

The trick is usedDiagonals is from 0 to 2n-1; usedRevDiagonals is from -(n-1) to (n-1). we can add (n-1) to prevent negative value.

``` java
// DFS process
for (int i = 0; i < n; i++) {
    if (valid) {
        mark(usedColumns, usedDiagonals, usedRevDiagonals);
        // record result
        // DFS to next level
        unmark(usedColumns, usedDiagonals, usedRevDiagonals);
    }
}
```

### Print 2D array in Spiral Order

**Recursive way** record an offset. in each call stack, offset+1, size-2; (Only valid in n*n matrix)
**Iterative way** Both n*n and n*m matrix. Notice: 

``` java
// in n*n matrix. After while(i < j)
if (i == j) {
    // left the middle point 
    result.add(mat[i][j]);
}
// in n*m matrix
// There are 3 cases
if (left > right || up > down) {
    return result
}
if (left == right) {
    // there is one column left
    for (every ele: col) {result.add(ele);}
} else {
    // there is one row left
    for (every ele: row) {result.add(ele);}
}
```

### Spiral Generate 

Similar Logic with spiral print, the only difference is record a int num=0. Each time when iterate into the loop, num++.

## Recursion 与 LinkedList 的结合

### Reverse a LinkedList

Recursion and Iterative way.

### Reverse a LinkedList in pairs

input:

1 -> 2 -> 3 -> 4 -> 5 -> null

output:

2 -> 1 -> 4 -> 3 -> 5 -> null

``` java
if 1 is cur;
cur.next = [the return value of recursion calls];
cur.next.next = cur;
return cur.next;
```

## Recursion 与 String 的结合

### Reverse a String using recursion

### Abbreviation matching

A word "book" can be abbreviated by "4, b3, 1o1k, b2k, etc". Given a string and an abbreviation, return if the string match this abbreviation. Assume original string contains only alphabetic characters. e.g: sophisticated -> s11d

The key is to calculate the count from character. 

## Recursion 与 Binary Tree 相结合

**重点、常考**

`从下往上传值`

Way of thinking:
1. What do you expect from your lchild/rchild? (usually it is the return type of the recursion function)
    - Total number of nodes in my left subtree.
    - Total number of nodes in my right subtree.
2. What do you want to do in the current layer?
    - store in currentNode -> left # of nodes.
3. What do you want to report to your parent?
    - return left + right + 1

### getHeight

``` java
int getHeight(Node root) {
    if (root == null) return 0;
    //1
    int left = getHeight(root.left);
    int right = getHeight(root.right);
    //2
    int larger = Math.max(left, right);
    // 3
    return larger + 1;
}
```

### store number of nodes in each nodes' left sub-tree

``` java
int getNumber(Node root) {
    if (root == null) return 0;
    // 1
    int left = getNumber(root.left);
    int right = getNumber(root.right);
    // 2
    root.leftNodes = left;
    // 3
    return left + right + 1;
}

```

### Find the node with max difference in the total number of descendents in its left subtree and right subtree

1. left = number of nodes in left subtree

   right = number of nodes in right subtree

2. if abs(right - left) > global_max, update result
3. return left + right + 1

### Lowest Common Ancestor

1. left = a,b 是否在我的左边，如果在return a/b
   right = a,b 是否在我的右边, 如果在return a/b

2. 判断left != null and right != null,当前root就是LCA
3. return 不是空的那一边

``` java
if (root == null || root == a || root == b) {return root;}
left = lca(root.left, a, b);
right = lca(root.right, a, b);
if left != null && right != null {return root;}
return left== null ? right : left;
```

`LCA for k nodes in binary tree`
Maintain a set contains all nodes. Check if set.contains(root) in base case, if contains, return root.

`LCA for k nodes in m-nary tree`
record a count. For every node in root.children, do lca(), if find a match, count++, res = curNode. return the res node.

`LCA for big data processing`
Given a big tree with trillions of nodes, each node can have at most m branches, and given k nodes in the tree, how to return the **lowest common ancestor** for k nodes in m-nary tree. You are given 1000 machine to solve this problem.

Run BFS1 on first 10 levels, to find a and b
- both a and b is in first 10 levels. LCA(root, a, b, 10)
- only 1 node in first 10 levels, using map-reduce to find the 2nd node in the rest of the tree.
    - Assume calling find(M9_1, b), find(M9_2, b), ... , find(M9_512, b), assume b is returned in machine Mi. 
    - call LCA(root, a, Mi)
- neither a nor b
    - Run LCA(M9_1, a, b), LCA(M9_2, a, b), LCA(M9_3, a, b), ...
        - if only one machine return c, then c is the final result
        - if one machine return a, the other return b, call LCA(root, M9_i, M9_j, 10)
        - if only one machine return one node, a or b, call BFS to find b in this machine. If we can find b, then a is the result.