---
layout: post
title: Learning String Source code 
date: 2018-05-03 15:23:24.000000000 -05:00
tags: java, source-code
---

## new String()

``` java
public String(char[] value, int offset, int count) {
    // check not null
    this.value = Arrays.copyOfRange(value, offset, offset + count);
}
// Example
char[] arr = {'a', 'b', 'c'};
new String(arr, 0, 3);
// output is abc
```
也就是说是指从offset开始数count个元素建立一个新String.

## String.indexOf(fromIndex, String s)
refer to 
``` java
int indexOf(char[] source, int fromIndex, char[] target) {
    for (int i = fromIndex; i < source.length; i++) {
        // Find first index match first
        if (source[i] != target[0]) {
            while (++i < souce.length && souce[i] != target[0]);
        }
        // Find the rest
        if (i < source.length) {
            int j = i + 1;
            int end = j + target.length - 1;
            for (int k = 0; j < end && souce[j] != target[k]; j++, k++);
        }
        if (j == end) {
            return i;
        }
    }
    return -1;
}
```

## StringBuilder

StringBuilder.append(CharSequence s, int start, int end);
注意这个`end`和String Constructor中不同，这个end是不包含在append的元素中的. 所以当我们需要在StringBuilder中添加元素时，需要用stringBuilder.append(input, fromIndex, input.length())来添加从fromIndex开始一直到input.length()-1的元素.