---
layout: post
title: Recursion
date: 2018-05-13 15:23:24.000000000 -05:00
---

`this is just a algorithm learning blog for my own purpose of use.`

### Fibonacci sequence

DP 解题方式就是如何定义表格里每个element的意义,以及把表格里的value填满

核心思想：
- 把一个大问题(size == n)的解决方案用比他小的问题（们）解决，思考从size=n-1增加到size=n的时候，如何用小问题solution构建大问题solution.
- 与recursion关系：
    - Recursion从大到小来解决问题，不记录任何sub-solution
    - DP从小到大解决问题，记录sub-solution
        - base case
        - induction rule

DP 常用方法:
- 一维的original data. (such as a rope, a word, a piece of wood),求max or min(cut, merge, etc..)
    - If the **weight** of each smallest element in the original data is identical/similar
        - Identical: 1 meter of rope
        - similar: a letter, a number
    - This kind of problem is usually simple:
    - linear scan 回头看
    - Examples:
        - Longest Ascending sub-array {when at i, look back i-1}
        - Longest Ascending sub-sequence {when at i, look back at 1...i-1}
        - cut rope
        - cut palindrome
    - If the weight are not the same
        - 使用中心开花的思想，index = [0,1,2,3...n-1],for each M[i,j], we usually need to try out all possible k that i < k < j,M[i,j] = max(M[i,k] +/-/* M[k,j])
        - Examples:
            - 沙子归并
            - 切木头

## Linear scan and Look back to the previous element

### Longest ascending subarray

Given an unsorted array, find the length of the longest subarray in which the numbers are in ascending order. eg: input array:{7,2,3,1,5,8,9,6},the longest ascending subarray is {1,5,8,9}, output is 4.

Base case: one element M[0] = 1

Induction rule: M[i] represents the max length of the ascending subarray,including ith element
`M[i] = M[i-1] + 1 if (input[i-1] < input[i]>)`

Time = O(n), Space = O(n) can be optimized O(1)

### Maximal product when cutting rope

Given a rope with integer length n, how to cut the rope into m integer-length parts with length p[0], p[1],...,p[m-1], in order to get the maximal product of p[0] * p[1] *...*p[m-1]? m is determined by you and must be greater than 0. (at least one cut must be made)

_ _ | _ _ _ product = 2 * 3 = 6

_ | _ | _ | _ | _ product = 1 * 1 * 1 * 1 * 1 = 1

 maintain a int array, length = length + 1. Because arr[0] is not exists.
 
 M[i + 1] = max((i - 1) * max(1, M[1]), (i - 2) * max(2, M[2]), ..., 1 * max(i - 1, M[i - 1]))

From the code, we only need to compare half of the cuttings
``` java
for (int j = 1; j <= i / 2; j++) {
    arr[i] = max(array[i], j * max(i - j, array[i - j]));
}
```

### Dictionary Problem

Given a dictionary with some words, determine if the given input can be concatenated with these words.

Similar idea: 左大段右小段. 左大段含义是存在temp result中的数据,右小段含义是需要manually check每个result是否在dict里面。

M[i] = (M[0] && dict.contains(substr(0, i))) || (M[1] && dict.contains(substr(1, i))) || ... || (M[i - 1] && dict.contains(substr(i - 1, i)))

