---
layout: post
title: Binary Tree
date: 2018-06-29 15:23:24.000000000 -05:00
tags: algorithm
---

`this is just a algorithm learning blog for my own purpose of use.`

## Tree Traverse

- preorder traverse
- inorder traverse
- postorder traverse

`todo: recursive and iterative way`

## Reconstruct Bianry Tree from preorder/postorder and inorder

关键是通过post/pre list找到root的位置，比较好的办法是建立一个对inorder list：<value, index>的pair，查询效率可以变成O(1);

接下来只需要用recursive办法确定左子树与右子树的左右边界。

需要注意的是在preorder/postorder list里面，边界条件需要通过从inorder list中数有多少个元素来判断。