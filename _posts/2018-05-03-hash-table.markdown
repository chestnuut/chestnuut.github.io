---
layout: post
title: hash-table
date: 2018-05-03 15:23:24.000000000 -05:00
tags: algorithm
---

- Hash set is a Set of key. eg: {1,3,5} only contains Key.

- Hash map is a `<key, value>` pair.

- Hash collison:
    - chaining. (linkedlist or self balanced bianry tree).
    - open addressing. (probe + rehash);
    
## Related Topic

### For a composition of different kinds of words, try to find the top k frequent words.

Step 1: calculate and record the frequency of each word. A count_map{words, count}

Step 2: maintain a k-size min heap, if the ongoing value > heap.top(), insert -> pop(). Otherwise, do nothing.

### If there is only one missing number from 1 to n in an unsorted array, how to find it in $O(n)$ time? Eg. {3,1,4} missing 2

*Intuitively:* Create a size n hash set, iterate through the array, use set.contains() reduce time to O(1).
Time: $O(n)$, Space: $O(n)$

*Method 2:* Mathematical way. Using `sum(n) - sum(array)`. Time: $O(n)$, Space:$O(1)$. Cons: overflow, need to use long type to handle overflow.

*Method 3:* Exclusive or. Recall 1^1 = 0, we can use (1^2^3^4)^(3^1^4) = 2. Time: $O(n)$, Space:$O(1).

*Method 4:* Swap to the target position. Swap the element in the array to its actual position. {3,1,4}->create a size n+1 array, swap -> {1,[],3}. Iterate elements in array[0]-array[n-1], if ele != index, then we found it. otherwise, return array[n].

### Find common numbers between two sorted array
**Assumption:**
1. length of n and m? -> n < m
2. duplicate elements in each array. -> yes

*Intuitively*, store n in hash set. Iterate m, if element in n is also in the set, store in result.
需要注意如果array中有duplicate,需要一个hashmap来存储元素出现的元素.
Time:O(m+n), Space: O(n).

*Method 2:* binary search elements in n in m. Time: O(nlogm), Space: O(1).

*Method 3:* 谁小移谁。
```java
if (i < j) i++;
else if (i > j) j++;
else {
    store result;
    i++,j++;
}
```
Time:O(m+n), Space: O(1)
